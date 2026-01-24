---
title: Migrera mål från at.js 2.x till Web SDK
description: Lär dig migrera en Adobe Target-implementering från at.js 2.x till Adobe Experience Platform Web SDK. Ämnen som omfattar biblioteksöversikt, implementeringsskillnader och andra viktiga hänvisningar.
exl-id: 43b9ae91-4524-4071-9eb4-12a0a8aec242
source-git-commit: 4690d41f92c83fe17eda588538d397ae1fa28af0
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# Återge målaktiviteter som använder den formulärbaserade dispositionen

I vissa målinriktade implementeringar kan regionala mrutor (som nu kallas omfång) användas för att leverera innehåll från aktiviteter som använder den formulärbaserade Experience Composer. Om implementeringen av at.js Target använder mboxes måste du göra följande:

* Uppdatera alla referenser från din at.js-implementering som använder `getOffer()` eller `getOffers()` till motsvarande Platform Web SDK-metoder.
* Lägg till kod för att utlösa en `propositionDisplay`-händelse så att ett intryck räknas.

## Begär och tillämpa innehåll på begäran

Aktiviteter som skapats med Target formulärbaserade disposition och som levereras till regionala mrutor kan inte återges automatiskt av Platform Web SDK. På liknande sätt som at.js måste erbjudanden som levereras till specifika målplatser återges på begäran.


+++at.js Exempel med `getOffer()` och `applyOffer()`:

1. Kör `getOffer()` för att begära ett erbjudande för en plats
1. Kör `applyOffer()` för att återge erbjudandet till en angiven väljare
1. Ett aktivitetsintryck ökar automatiskt vid tidpunkten för `getOffer()`-begäran

```JavaScript
// Retrieve an offer for the homepage-hero location
adobe.target.getOffer({
  "mbox": "homepage_hero",

  // Render offer to the #hero-banner selector
  "success": function(offers) {
    adobe.target.applyOffer({
      "mbox": "homepage_hero",
      "selector": "#hero-banner",
      "offer": offers
    });
  },
  "error": {
    console.log(error);
  },
  "timeout": 3000
});
```

+++

+++Plattformsmotsvarighet för Web SDK med kommandot `applyPropositions`:

1. Kör kommandot `sendEvent` för att begära erbjudanden (erbjudanden) för en eller flera platser (omfattningar)
1. Kör kommandot `applyPropositions` med metadataobjekt som innehåller instruktioner för hur du använder innehåll på sidan för varje omfång
1. Kör kommandot `sendEvent` med eventType för `decisioning.propositionDisplay` för att spåra ett intryck

```JavaScript
// Retrieve propositions for homepage_hero location (scope)
alloy("sendEvent", {
  "decisionScopes": ["homepage_hero"]
}).then(function(result) {
  var retrievedPropositions = result.propositions;
    
  // Render offer (proposition) to the #hero-banner selector by supplying extra metadata
  return alloy("applyPropositions", {
    "propositions": retrievedPropositions,
    "metadata": {
      // Specify each regional mbox or scope name along with a selector and actionType
      "homepage_hero": {
        "selector": "#hero-banner",
        "actionType": "setHtml"
      }
    }
  }).then(function(applyPropositionsResult) {
    var renderedPropositions = applyPropositionsResult.propositions;

    // Send the display notifications via sendEvent command
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
});
```

+++

Med Platform Web SDK får du större kontroll över hur du använder formulärbaserade aktiviteter på sidan med kommandot `applyPropositions` och `actionType`:

| `actionType` | Beskrivning | at.js `applyOffer()` | SDK för plattformswebben `applyPropositions` |
| --- | --- | --- | --- |
| `setHtml` | Rensa innehållet i behållaren och lägg sedan till erbjudandet i behållaren | Ja (används alltid) | Ja |
| `replaceHtml` | Ta bort behållaren och ersätt den med erbjudandet | Nej | Ja |
| `appendHtml` | Lägger till erbjudandet efter den angivna väljaren | Nej | Ja |

Mer information om ytterligare återgivningsalternativ och exempel finns i [dedikerad dokumentation](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=sv-SE) om hur du återger innehåll med hjälp av Platform Web SDK.

## Implementeringsexempel

Exemplsidan nedan bygger på implementeringen som beskrivs i föregående avsnitt, men lägger bara till ytterligare omfång till kommandot `sendEvent`.

+++Platform Web SDK-exempel med flera omfattningar

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

  <!--Prehiding snippet for Target with asynchronous deployment-->
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
    alloy("sendEvent", {
      // Request and render VEC-based activities
      "renderDecisions": true,
      // Request content for form-based activities using the "homepage_hero" scope
      "decisionScopes": ["homepage_hero"]
    }).then(function(result) {
      var retrievedPropositions = result.propositions;
        
      // Render offer (proposition) to the #hero-banner selector by supplying extra metadata
      return alloy("applyPropositions", {
        "propositions": retrievedPropositions,
        "metadata": {
          // Specify each regional mbox or scope name along with a selector and actionType
          "homepage_hero": {
            "selector": "#hero-banner",
            "actionType": "setHtml"
          }
        }
      }).then(function(applyPropositionsResult) {
        var renderedPropositions = applyPropositionsResult.propositions;

        // Send the display notifications via sendEvent command
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

Läs sedan om hur du [skickar målparametrar med hjälp av Platform Web SDK](send-parameters.md).

>[!NOTE]
>
>Vi vill hjälpa dig att lyckas med målmigreringen från at.js till Web SDK. Om du stöter på problem med din migrering eller om du känner att det saknas viktig information i den här guiden kan du meddela oss genom att publicera [den här communitydiskussionen](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587?profile.language=sv#M463).
