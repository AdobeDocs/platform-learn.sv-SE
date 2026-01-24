---
title: Spåra händelser - Migrera mål från at.js 2.x till Web SDK
description: Lär dig spåra konverteringshändelser för Adobe Target med Experience Platform Web SDK.
exl-id: 5da772bc-de05-4ea9-afbd-3ef58bc7f025
source-git-commit: d4308b68d6974fe47eca668dd16555d15a8247c9
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---

# Spåra målkonverteringshändelser med Platform Web SDK

Konverteringshändelser för Target kan spåras med Platform Web SDK som liknar at.js. Konverteringshändelser faller vanligtvis inom följande kategorier:

* Automatiskt spårade händelser som inte kräver någon konfiguration
* Inköpskonverteringshändelser som ska justeras för implementering av plattformens Web SDK
* Konverteringshändelser som inte är köpta och som kräver koduppdateringar

## Målspårningsjämförelse

I följande tabell jämförs hur at.js och Platform Web SDK spårar konverteringshändelser

| Aktivitetsmål | Mål at.js 2.x | Platform Web SDK |
|---|---|---|
| Konvertering > Visad sida | Spåras automatiskt. Baserat på värdet `context.address.url` i nyttolasten för at.js-begäran. | Spåras automatiskt. Baserat på värdet för `xdm.web.webPageDetails.URL` i nyttolasten `sendEvent` |
| Konvertering > Visad mbox | Spårat med begäran om en visningsruteplats eller ett meddelande med `trackEvent()` eller `sendNotifications()` med värdet `type`. `display` | Spårat med ett Platform Web SDK `sendEvent`-anrop med `eventType` av `decisioning.propositionDisplay`. |
| Konvertering > Klickade på ett element | Spåras automatiskt för VEC-baserade aktiviteter. Visas som ett at.js-nätverksanrop med ett `notifications`-objekt i nyttolasten i begäran och ett `type`-värde på `click`. | Spåras automatiskt för VEC-baserade aktiviteter. Visas som ett Platform Web SDK `sendEvent`-anrop med `eventType` av `decisioning.propositionInteract`. |
| Engagemang > Sidvyer | Spåras automatiskt | Spåras automatiskt |
| Engagemang > Tid på plats | Spåras automatiskt | Spåras automatiskt |

<!--
| Revenue > RPV, AOV, or Total Sales | Tracked based on the `orderTotal` parameter values for the specified mbox(es) | Tracked based on the `xdm.commerce.order.priceTotal` values. Its best to use the "any mbox" option in the goal setup. |
| Revenue > Orders | Tracked based on the unique `orderId` parameter values for the specified mbox(es) | Tracked based on the unique values for `xdm.commerce.order.purchaseID`. Its best to use the "any mbox" option in the goal setup. |
| Engagement > Custom Scoring | Tracked with the `mboxPageValue` parameter. Refer to the [dedicated documentation](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/capture-score.html?lang=sv-SE) for more details. | Tracked with `data.__adobe.target.mboxPageValue` in the `sendEvent` payload |
-->

## Automatiskt spårade händelser

Följande konverteringsmål kräver inga specifika justeringar av implementeringen:

* Konvertering > Visad sida
* Konvertering > Klickade på ett element
* Engagemang > Sidvyer
* Engagemang > Tid på plats

>[!NOTE]
>
>Platform Web SDK ger större kontroll över de värden som skickas i nyttolasten. För att garantera att målfunktioner som QA-URL:er och konverteringsmålen &quot;Viewed a Page&quot; fungerar som de ska, kontrollerar du att värdet `xdm.web.webPageDetails.URL` innehåller den fullständiga URL:en med rätt skiftläge.

<!--
## Purchase conversion events

The following conversion goals are based on the order details information passed in the Platform Web SDK `sendEvent` payload:

* Revenue > Revenue per Visit (RPV)
* Revenue > Average Order Value (AOV)
* Revenue > Total Sales
* Revenue > Orders

Target at.js implementations typically use an order confirmation mbox with the `trackEvent()` or `sendNotifications()` functions to pass the order ID, order total, and a list of product IDs purchased. These methods are specific to Target.

The Platform Web SDK is a shared library for all Adobe applications and you may have other applications such as Adobe Analytics to consider. Because of this shared nature, its best send a single order confirmation call using the appropriate commerce XDM field group.

For more information and an example, refer to the tutorial section about [sending purchase parameters to Target](send-parameters.md#purchase-parameters). 
-->

## Anpassade spårade händelser

Vid målinriktade implementeringar används ofta anpassade konverteringshändelser för att spåra klick för formulärbaserade aktiviteter, för att ange en konvertering i ett flöde eller för att skicka parametrar utan att begära nytt innehåll.

Tabellen nedan visar metoden at.js och motsvarigheten till Platform Web SDK för några vanliga användningsfall för konverteringsspårning.

| Användningsfall | Mål at.js 2.x | Platform Web SDK |
|---|---|---|
| Spåra en klickkonverteringshändelse för en mbox-plats (scope) | Kör `trackEvent()` eller `sendNotifications()` med värdet `type` för `click` för en specifik mbox-plats | Kör ett `sendEvent`-kommando med händelsetypen `decisioning.propositionInteract` |
| Spåra en anpassad konverteringshändelse som även kan innehålla ytterligare data, till exempel parametrar för målprofilen | Kör `trackEvent()` eller `sendNotifications()` med värdet `type` för `display` för en specifik mbox-plats | Kör ett `sendEvent`-kommando med händelsetypen `decisioning.propositionDisplay` |

>[!NOTE]
>
>Även om `decisioning.propositionDisplay` oftast används för att öka antalet visningar för specifika omfattningar, bör den även användas som direkt ersättning för at.js `trackEvent()` vanligtvis. Funktionen `trackEvent()` är som standard av typen `display` om den inte anges. Kontrollera implementeringen för att säkerställa att du använder rätt händelsetyp för alla anpassade konverteringar som du har definierat.

Mer information om hur du använder [`trackEvent()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/adobe-target-trackevent/) och [`sendNotifications()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/adobe-target-sendnotifications-atjs-21/) för att spåra Target-händelser finns i den dedikerade at.js-dokumentationen.

Exempel på at.js som använder `trackEvent()` för att spåra en klickning på en mbox-plats:

```JavaScript
adobe.target.trackEvent({
  "type": "click",
  "mbox": "homepage_hero"
});
```

Med en implementering av Platform Web SDK kan du spåra händelser och användaråtgärder genom att anropa kommandot `sendEvent`, fylla i `_experience.decisioning.propositions` XDM-fältgruppen och ställa in `eventType` på ett av två värden:

* `decisioning.propositionDisplay`: Signalerar återgivningen av målaktiviteten.
* `decisioning.propositionInteract`: Signalerar en användarinteraktion med aktiviteten, som ett musklick.

`_experience.decisioning.propositions` XDM-fältgruppen är en objektmatris. Egenskaperna för varje objekt härleds från `result.propositions` som returneras i kommandot `sendEvent`: `{ id, scope, scopeDetails }`

```JavaScript
alloy("sendEvent", {
  xdm: { ...},
  decisionScopes: ["hero-banner"]
}).then(function (result) {
  var propositions = result.propositions;

  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      for (var j = 0; j < proposition.items; j++) {
        var item = proposition.items[j];

        if (item.schema === "https://ns.adobe.com/personalization/measurement") {
          // add metric to the DOM element
          const button = document.getElementById("form-based-click-metric");

          button.addEventListener("click", event => {
            const executedPropositions = [
              {
                id: proposition.id,
                scope: proposition.scope,
                scopeDetails: proposition.scopeDetails
              }
            ];
            // send the click track event
            alloy("sendEvent", {
              "xdm": {
                "eventType": "decisioning.propositionInteract",
                "_experience": {
                  "decisioning": {
                    "propositions": executedPropositions
                  }
                }
              }
            });
          });
        }
      }
    }
  }
});
```

Läs sedan om hur du [aktiverar delning av korsdomän-ID](cross-domain.md) för konsekventa besökarprofiler.

>[!NOTE]
>
>Vi vill hjälpa dig att lyckas med målmigreringen från at.js till Web SDK. Om du stöter på problem med din migrering eller om du känner att det saknas viktig information i den här guiden kan du meddela oss genom att publicera [den här communitydiskussionen](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587?profile.language=sv#M463).
