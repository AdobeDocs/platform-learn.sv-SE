---
title: Återge VEC-aktiviteter | Migrera mål från at.js 2.x till Web SDK
description: Lär dig hur du hämtar och använder funktioner för visuell upplevelsedisposition med en Web SDK-implementering av Adobe Target.
feature: Visual Experience Composer (VEC),Implement Client-side,APIs/SDKs,at.js,AEP Web SDK, Web SDK,Implementation
source-git-commit: dad7a1b01c4313d6409ce07d01a6520ed83f5e89
workflow-type: tm+mt
source-wordcount: '1130'
ht-degree: 0%

---

# Återge VEC-aktiviteter (Adobe Target Visual Experience Composer)

Målaktiviteter ställs in med Visual Experience Composer (VEC) eller den formulärbaserade dispositionen. Platform Web SDK kan hämta och använda VEC-baserade aktiviteter på sidan precis som at.js. För den här delen av migreringen kommer du att:

* Installera webbläsartillägget Visual Editing Helper, om det behövs
* Kör en `sendEvent` ringa till Platform Web SDK för att begära aktiviteter.
* Uppdatera alla referenser från implementeringen av at.js som använder `getOffers()` köra ett mål `pageLoad` begäran.

## Webbläsartillägg för hjälp för visuell redigering

Med webbläsartillägget Adobe Experience Cloud Visual Editing Helper för Google Chrome kan du läsa in webbplatser tillförlitligt i Adobe Target Visual Experience Composer (VEC) för att snabbt skapa och skapa QA-webbupplevelser.

Webbläsartillägget Visuell redigeringshjälp fungerar med webbplatser som använder at.js eller Platform Web SDK.

>[!IMPORTANT]
>
>Det nya tillägget Hjälp för visuell redigering ersätter det tidigare [Webbläsartillägg för målets VEC-hjälp](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html). Om det äldre VEC Helper-tillägget är installerat bör det tas bort eller inaktiveras innan tillägget Visuell redigeringshjälp används.

### Hämta och installera hjälpen för visuell redigering

1. Navigera till [Webbläsartillägget Adobe Experience Cloud Visual Editing Helper i Chrome Web Store](https://chrome.google.com/webstore/detail/adobe-experience-cloud-vi/kgmjjkfjacffaebgpkpcllakjifppnca).
1. Klicka på Lägg till i **Krom** > **Lägg till tillägg**.
1. Öppna VEC i Target.
1. Om du vill använda tillägget klickar du på ikonen för tillägget Visuell redigeringshjälp ![Ikon för tillägg för visuell redigering](assets/VEC-Helper.png) i webbläsarens verktygsfält när du är i VEC- eller QA-läge.

Hjälpprogrammet för visuell redigering aktiveras automatiskt när en webbplats öppnas i Target VEC för att underlätta redigeringen. Tillägget har inga villkorsinställningar. Tillägget hanterar alla inställningar automatiskt, inklusive inställningarna för cookies för samma plats.

Mer information om [Hjälptillägg för visuell redigering](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension.html) och [felsöka Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/troubleshoot-composer.html).

## Begär och tillämpa innehåll automatiskt

När Platform Web SDK har konfigurerats på sidan kan du begära innehåll från Target. Till skillnad från at.js, som kan konfigureras att automatiskt begära innehåll när biblioteket läses in, kräver Platform Web SDK att du kör ett kommando explicit.

Om din at.js-implementering har `pageLoadEnabled` inställning inställd på `true` som möjliggör automatisk återgivning av VEC-baserade aktiviteter, så skulle du utföra följande `sendEvent` med Platform Web SDK:

```Javascript
alloy("sendEvent", {
  "renderDecisions": true
});
```

>[!TIP]
>
> När du använder taggfunktionen (tidigare Launch) för att implementera Web SDK kan sendEvent-kommandon för VEC-aktiviteter implementeras i en regel med [!UICONTROL Skicka händelse] åtgärdstyp med [!UICONTROL Återge beslut om visuell personalisering] markerat alternativ.

När Platform Web SDK återger en aktivitet på sidan med `renderDecisions` ange till `true`, utlöses ett extra varningsanrop automatiskt för att öka ett intryck och tilldela besökaren till aktiviteten. Det här anropet använder en händelsetyp med värdet `decisioning.propositionDisplay`.

![Anrop till Platform Web SDK som ökar ett målintryck](assets/target-impression-call.png)

## Begär och tillämpa innehåll på begäran

Vissa Target at.js-implementeringar kan ha `pageLoadEnabled` ange till `false` och i stället använder du `getOffers()` funktion för att köra en `pageLoad` begäran. Den här typen av konfiguration används om implementeringen kräver ytterligare bearbetning av `getOffers()` innan du lägger till innehåll på sidan eller begär innehåll för flera platser i ett enda samtal.

Följande kod använder `getOffers()` och `applyOffers()` att tillämpa VEC-baserade aktiviteter på begäran i stället för automatiskt vid biblioteksladdning.

```JavaScript
adobe.target.getOffers({
  request: {
    execute: {
      pageLoad: {}
    }
  }
}).
then(response => adobe.target.applyOffers({ response: response }));
```

Platform Web SDK har ingen specifik `pageLoad` -händelse. Alla förfrågningar om Target-innehåll styrs med `decisionScopes` med `sendEvent` -kommando. The `__view__` syftet med `pageLoad` begäran. motsvarande Platform Web SDK `sendEvent` metoden skulle vara:

1. Kör en `sendEvent` som innehåller `__view__` beslutsområde
1. Använd det returnerade innehållet på sidan med `applyPropositions` kommando
1. Kör en `sendEvent` med `decisioning.propositionDisplay` händelsetyp och förslagsinformation för att öka ett intryck

```Javascript
alloy("sendEvent", {
  // Request the special "__view__" scope for target-global-mbox / pageLoad
  decisionScopes: ["__view__"]
}).then(function(result) {
  // Check if content (propositions) were returned
  if (result.propositions) {
    var retrievedPropositions = result.propositions;
    // Apply propositions to the page
    return alloy("applyPropositions", {
      propositions: retrievedPropositions
    }).then(function(applyPropositionsResult) {
      var renderedPropositions = applyPropositionsResult.propositions;
      // Send a display notification with the sendEvent command
      alloy("sendEvent", {
        "xdm": {
          "eventType": "decisioning.propositionDisplay",
          "_experience": {
            "decisioning": {
              "propositions": renderedPropositions
            }
          }
        }
      });
    });
  }
});
```

>[!NOTE]
>
>Det går att [återge ändringar manuellt](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#manually-rendering-content) i Visual Experience Composer. Manuell återgivning av VEC-baserade ändringar är inte vanligt. Kontrollera om din at.js-implementering använder `getOffers()` funktion för att manuellt köra ett mål `pageLoad` begära utan att använda `applyOffers()` för att använda innehållet på sidan.

Med Platform Web SDK får utvecklarna stor flexibilitet när det gäller att begära och återge innehåll. Se [dedikerad dokumentation om återgivning av personaliserat innehåll](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html) för ytterligare alternativ och information.

## Implementeringsexempel

Implementeringen av grundplattformen Web SDK är nu klar. Vår grundläggande exempelsida med automatisk återgivning av Target-innehåll aktiverad bör se ut så här:

```HTML
<!doctype html>
<html>
<head>
  <title>Example page</title>
  <!--Data Layer to enable rich data collection and targeting-->
  <script>
    var digitalData = { 
      // Data layer information goes here
    };
  </script>

  <!--Third party libraries that may be used by Target offers and modifications-->
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.1/jquery.min.js"></script>

  <!--Prehiding snippet for Target with asynchronous Web SDK deployment-->
  <script>
    !function(e,a,n,t){var i=e.head;if(i){
    if (a) return;
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("mboxEdit") !== -1, ".body { opacity: 0 !important }", 3000);
  </script>

  <!--Platform Web SDK base code-->
  <script>
    !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
    []).push(o),n[o]=function(){var u=arguments;return new Promise(
    function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
    (window,["alloy"]);
  </script>

  <!--Platform Web SDK loaded asynchonously. Change the src to use the latest supported version.-->
  <script src="https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js" async></script>
  
  <!--Configure Platform Web SDK then send event-->
  <script>
    alloy("configure", {
      "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
      "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
    });
    
    // Send an event to the Adobe edge network and render Target content automatically 
    alloy("sendEvent", {
      "renderDecisions": true
    });
  </script>
</head>
<body>
  <h1 id="title">Home Page</h1><br><br>
  <p id="bodyText">Navigation</p><br><br>
  <a id="home" class="navigationLink" href="#">Home</a><br>
  <a id="pageA" class="navigationLink" href="#">Page A</a><br>
  <a id="pageB" class="navigationLink" href="#">Page B</a><br>
  <a id="pageC" class="navigationLink" href="#">Page C</a><br>
  <div id="homepage-hero">Homepage Hero Banner Content</div>
</body>
</html>
```

>[!TIP]
>
> När du använder taggfunktionen (tidigare Launch) för att implementera Web SDK ersätter taggarna embed-koden grundkoden för Platform Web SDK, Platform Web SDK inläst asynkront och Configure Platform Web SDK ovan. Kommandot sendEvent görs i en regel med [!UICONTROL Skicka händelse] åtgärdstyp med [!UICONTROL Återge beslut om visuell personalisering] markerat alternativ.

## Bygga aktiviteter med webbläsartillägget Visual Editing Helper

Med webbläsartillägget Adobe Experience Cloud Visual Editing Helper för Google Chrome kan du läsa in webbplatser tillförlitligt i Adobe Target Visual Experience Composer (VEC) för att snabbt skapa och skapa QA-webbupplevelser.

Webbläsartillägget Visuell redigeringshjälp fungerar med webbplatser som använder at.js eller Platform Web SDK.

>[!IMPORTANT]
>
>Det nya tillägget Hjälp för visuell redigering ersätter det tidigare [Webbläsartillägg för målets VEC-hjälp](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html). Om det äldre VEC Helper-tillägget är installerat bör det tas bort eller inaktiveras innan tillägget Visuell redigeringshjälp används.

### Hämta och installera hjälpen för visuell redigering

1. Navigera till [Webbläsartillägget Adobe Experience Cloud Visual Editing Helper i Chrome Web Store](https://chrome.google.com/webstore/detail/adobe-experience-cloud-vi/kgmjjkfjacffaebgpkpcllakjifppnca).
1. Klicka på Lägg till i **Krom** > **Lägg till tillägg**.
1. Öppna VEC i Target.
1. Om du vill använda tillägget klickar du på ikonen för tillägget Visuell redigeringshjälp för webbläsare ( ikonen för tillägget Visual Editing ) i webbläsarens verktygsfält när du är i VEC- eller QA-läge.

Hjälp för visuell redigering aktiveras automatiskt när en webbplats öppnas i Target VEC som stöder redigering. Tillägget har inga villkorsinställningar. Tillägget hanterar alla inställningar automatiskt, inklusive inställningarna för cookies för samma plats.

Mer information om [Hjälptillägg för visuell redigering](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension.html) och [felsöka Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/troubleshoot-composer.html).

Lär dig hur du begär och [återge formulärbaserade målaktiviteter](render-form-based-activities.md).

>[!NOTE]
>
>Vi vill hjälpa dig att lyckas med målmigreringen från at.js till Web SDK. Om du stöter på problem med din migrering eller känner att det saknas viktig information i den här guiden ber vi dig att meddela oss genom att publicera i [den här communitydiskussionen](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).
