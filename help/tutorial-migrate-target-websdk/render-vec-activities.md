---
title: Återge VEC-aktiviteter - migrera mål från at.js 2.x till Web SDK
description: Lär dig hur du hämtar och använder funktioner för visuell upplevelsedisposition med en Web SDK-implementering av Adobe Target.
exl-id: bbbbfada-e236-44de-a7bf-5c63ff840db4
source-git-commit: d4308b68d6974fe47eca668dd16555d15a8247c9
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 0%

---

# Återge VEC-aktiviteter (Adobe Target Visual Experience Composer)

Målaktiviteter ställs in med Visual Experience Composer (VEC) eller den formulärbaserade dispositionen. Platform Web SDK kan hämta och använda VEC-baserade aktiviteter på sidan precis som at.js. För den här delen av migreringen:

* Installera webbläsartillägget Visual Editing Helper
* Kör ett `sendEvent`-anrop med Platform Web SDK för att begära aktiviteter.
* Uppdatera alla referenser från din at.js-implementering som använder `getOffers()` för att köra en Target `pageLoad`-begäran.

## Webbläsartillägg för hjälp för visuell redigering

Med webbläsartillägget Adobe Experience Cloud Visual Editing Helper för Google Chrome kan du läsa in webbplatser tillförlitligt i Adobe Target Visual Experience Composer (VEC) för att snabbt skapa och skapa QA-webbupplevelser.

Webbläsartillägget Visuell redigeringshjälp fungerar med webbplatser som använder at.js eller Platform Web SDK.

### Hämta och installera hjälpen för visuell redigering

1. Navigera till webbläsartillägget [Adobe Experience Cloud Visual Editing Helper i Chrome Web Store](https://chrome.google.com/webstore/detail/adobe-experience-cloud-vi/kgmjjkfjacffaebgpkpcllakjifppnca).
1. Klicka på Lägg till i **Chrome** > **Lägg till tillägg**.
1. Öppna VEC i Target.
1. Om du vill använda tillägget klickar du på ikonen för tillägget för visuell redigeringshjälp i webbläsaren ![Visual Editing Extension &#x200B;](assets/VEC-Helper.png){zoomable="yes"} i Chrome webbläsares verktygsfält när du är i VEC- eller QA-läge.

Hjälpprogrammet för visuell redigering aktiveras automatiskt när en webbplats öppnas i Target VEC för att underlätta redigeringen. Tillägget har inga villkorsinställningar. Tillägget hanterar alla inställningar automatiskt, inklusive inställningarna för cookies för samma plats.

Mer information om tillägget [Hjälp för visuell redigering](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension.html?lang=sv-SE) och [felsökning av Visual Experience Composer](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/troubleshoot-composer.html?lang=sv-SE) finns i den dedikerade dokumentationen.

>[!IMPORTANT]
>
>Det nya [hjälptillägget &#x200B;](https://chrome.google.com/webstore/detail/adobe-experience-cloud-vi/kgmjjkfjacffaebgpkpcllakjifppnca) för visuell redigering ersätter det tidigare [målwebbläsartillägget för VEC-hjälp](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html?lang=sv-SE). Om det äldre VEC Helper-tillägget är installerat bör det tas bort eller inaktiveras innan tillägget Visuell redigeringshjälp används.

## Begär och tillämpa innehåll automatiskt

När Platform Web SDK har konfigurerats på sidan kan du begära innehåll från Target. Till skillnad från at.js, som kan konfigureras att automatiskt begära innehåll när biblioteket läses in, kräver Platform Web SDK att du kör ett kommando explicit.

Om din at.js-implementering har inställningen `pageLoadEnabled` inställd på `true` som aktiverar automatisk återgivning av VEC-baserade aktiviteter kör du följande `sendEvent`-kommando med Platform Web SDK:

>[!BEGINTABS]

>[!TAB JavaScript]

```Javascript
alloy("sendEvent", {
  "renderDecisions": true
});
```

>[!TAB Taggar]

Använd åtgärdstypen [!UICONTROL Send event] med alternativet [!UICONTROL Render visual personalization decisions] markerat i taggar:

![Skicka en händelse med valda beslut om visuell återgivning för återgivning i taggar](assets/vec-sendEvent-renderTrue.png){zoomable="yes"}

>[!ENDTABS]

<!--
When the Platform Web SDK renders an activity to the page with `renderDecisions` set to `true`, an additional notification call fires automatically to increment an impression and attribute the visitor to the activity. This call uses an event type with the value `decisioning.propositionDisplay`.

![Platform Web SDK call incrementing a Target impression](assets/target-impression-call.png){zoomable="yes"}
-->

## Begär och tillämpa innehåll på begäran

Vissa Target-implementeringar kräver viss anpassad bearbetning av VEC-erbjudanden innan de kan användas på sidan. Eller så begär de flera platser i ett enda samtal. I en at.js-implementering kan detta göras genom att ställa in `pageLoadEnabled` på `false` och använda funktionen `getOffers()` för att köra en `pageLoad`-begäran.

+++ Exempel på at.js som använder `getOffers()` och `applyOffers()` för att manuellt återge VEC-baserade aktiviteter

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

+++

Plattformens Web SDK har ingen specifik `pageLoad`-händelse. Alla förfrågningar om Target-innehåll styrs med alternativet `decisionScopes` med kommandot `sendEvent`. Omfånget `__view__` tjänar syftet med begäran `pageLoad`.

+++ En motsvarande Platform Web SDK `sendEvent`-metod:

1. Kör ett `sendEvent`-kommando som innehåller beslutsområdet `__view__`
1. Använd det returnerade innehållet på sidan med kommandot `applyPropositions`
1. Kör ett `sendEvent`-kommando med händelsetypen `decisioning.propositionDisplay` och förslagsinformationen för att öka ett intryck

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

+++

>[!NOTE]
>
>Det går att [manuellt återge ändringar som gjorts &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=sv-SE#manually-rendering-content) i Visual Experience Composer. Manuell återgivning av VEC-baserade ändringar är inte vanligt. Kontrollera om din at.js-implementering använder funktionen `getOffers()` för att manuellt köra en `pageLoad` Target-begäran utan att använda `applyOffers()` för att tillämpa innehållet på sidan.

Med Platform Web SDK får utvecklarna stor flexibilitet när det gäller att begära och återge innehåll. Mer information och mer information finns i [dedikerad dokumentation om återgivning av anpassat innehåll](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=sv-SE).

## Implementeringsexempel

Implementeringen av grundplattformen Web SDK är nu klar.

>[!BEGINTABS]

>[!TAB JavaScript]

JavaScript-exempel med automatisk innehållsrendering i Target:

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


>[!TAB Taggar]

Exempelsida för taggar med automatisk återgivning av målinnehåll:


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

    <!--Tags Header Embed Code: REPLACE WITH THE INSTALL CODE FROM YOUR OWN ENVIRONMENT-->
    <script src="//assets.adobedtm.com/launch-EN93497c30fdf0424eb678d5f4ffac66dc.min.js" async></script>
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

Lägg till Adobe Experience Platform Web SDK-tillägget i taggar:

![Lägg till Adobe Experience Platform Web SDK-tillägget](assets/library-tags-addExtension.png){zoomable="yes"}

Lägg till önskade konfigurationer:
![konfigurerar migreringsalternativen för Web SDK-taggtillägg](assets/tags-config-migration.png){zoomable="yes"}

Skapa en regel med en [!UICONTROL Send event]-åtgärd och [!UICONTROL Render visual personalization decisions] vald:
![Skicka en händelse med återgivningsanpassningar markerade i taggar &#x200B;](assets/vec-sendEvent-renderTrue.png){zoomable="yes"}

>[!ENDTABS]

Läs sedan om hur du begär och [återger formulärbaserade målaktiviteter](render-form-based-activities.md).

>[!NOTE]
>
>Vi vill hjälpa dig att lyckas med målmigreringen från at.js till Web SDK. Om du stöter på problem med din migrering eller om du känner att det saknas viktig information i den här guiden kan du meddela oss genom att publicera [den här communitydiskussionen](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
