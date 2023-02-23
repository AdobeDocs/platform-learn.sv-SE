---
title: Spåra händelser | Migrera mål från at.js 2.x till Web SDK
description: Lär dig spåra konverteringshändelser för Adobe Target med Experience Platform Web SDK.
source-git-commit: 287ebcb275c4fca574dbd6cdf7e07ba4268bddb5
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 0%

---


# Spåra målkonverteringshändelser med Platform Web SDK

Konverteringshändelser för Target kan spåras med Platform Web SDK som liknar at.js. Konverteringshändelser faller vanligtvis inom följande kategorier:

* Automatiskt spårade händelser som inte kräver någon konfiguration
* Inköpskonverteringshändelser som ska justeras för implementering av plattformens Web SDK
* Konverteringshändelser som inte är köpta och som kräver koduppdateringar

## Jämförelse av målspårning

I följande tabell jämförs hur at.js och Platform Web SDK spårar konverteringshändelser

| Aktivitetsmål | Mål at.js 2.x | Platform Web SDK |
|---|---|---|
| Konvertering > Visad sida | Spåras automatiskt. Baserat på värdet av `context.address.url` i på at.js-begäran nyttolast. | Spåras automatiskt. Baserat på värdet av `xdm.web.webPageDetails.URL` i `sendEvent` nyttolast |
| Konvertering > Visad mbox | Spårat med begäran om en visningsruta eller ett meddelande med `trackEvent()` eller `sendNotifications()` med `type` värde för `display`. | Spårat med en Platform Web SDK `sendEvent` ring med `eventType` av `decisioning.propositionDisplay`. |
| Konvertering > Klickade på ett element | Spåras automatiskt för VEC-baserade aktiviteter. Visas som ett at.js-nätverksanrop med en `notifications` -objektet i nyttolasten i begäran och `type` värde för `click`. | Spåras automatiskt för VEC-baserade aktiviteter. Visas som en SDK för plattformar `sendEvent` ring med `eventType` av `decisioning.propositionInteract`. |
| Engagemang > Sidvyer | Spåras automatiskt | Spåras automatiskt |
| Engagemang > Tid på plats | Spåras automatiskt | Spåras automatiskt |

<!--
| Revenue > RPV, AOV, or Total Sales | Tracked based on the `orderTotal` parameter values for the specified mbox(es) | Tracked based on the `xdm.commerce.order.priceTotal` values. Its best to use the "any mbox" option in the goal setup. |
| Revenue > Orders | Tracked based on the unique `orderId` parameter values for the specified mbox(es) | Tracked based on the unique values for `xdm.commerce.order.purchaseID`. Its best to use the "any mbox" option in the goal setup. |
| Engagement > Custom Scoring | Tracked with the `mboxPageValue` parameter. Refer to the [dedicated documentation](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/capture-score.html) for more details. | Tracked with `data.__adobe.target.mboxPageValue` in the `sendEvent` payload |
-->

## Automatiskt spårade händelser

Följande konverteringsmål kräver inga specifika justeringar av implementeringen:

* Konvertering > Visad sida
* Konvertering > Klickade på ett element
* Engagemang > Sidvyer
* Engagemang > Tid på plats

>[!NOTE]
>
>Platform Web SDK ger större kontroll över de värden som skickas i nyttolasten. Kontrollera att målfunktionerna som QA URL:er och Konverteringsmålen &quot;Viewed a Page&quot; fungerar som de ska `xdm.web.webPageDetails.URL` värdet innehåller den fullständiga sidans URL med rätt skiftläge för tecken.

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
| Spåra en klickkonverteringshändelse för en mbox-plats (scope) | Kör `trackEvent()` eller `sendNotifications()` med `type` värde för `click` för en viss mbox-plats | Kör en `sendEvent` kommando med en händelsetyp av `decisioning.propositionInteract` |
| Spåra en anpassad konverteringshändelse som även kan innehålla ytterligare data, till exempel parametrar för målprofilen | Kör `trackEvent()` eller `sendNotifications()` med `type` värde för `display` för en viss mbox-plats | Kör en `sendEvent` kommando med en händelsetyp av `decisioning.propositionDisplay` |

>[!NOTE]
>
>Fast `decisioning.propositionDisplay` används oftast för att öka intrycket av specifika omfattningar, men bör även användas som direkt ersättning för at.js `trackEvent()` vanligtvis. The `trackEvent()` som standard är en typ av `display` om inget anges. Kontrollera implementeringen för att säkerställa att du använder rätt händelsetyp för alla anpassade konverteringar som du har definierat.

Mer information om hur du använder finns i den dedikerade at.js-dokumentationen [`trackEvent()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/adobe-target-trackevent/) och [`sendNotifications()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/adobe-target-sendnotifications-atjs-21/) för att spåra Target-händelser.

at.js-exempel med `trackEvent()` för att spåra en klickning på en mbox-plats:

```JavaScript
adobe.target.trackEvent({
  "type": "click",
  "mbox": "homepage_hero"
});
```

Med en implementering av Platform Web SDK kan du spåra händelser och användaråtgärder genom att anropa `sendEvent` kommando, fylla i `_experience.decisioning.propositions` XDM-fältgrupp och inställning av `eventType` till ett av två värden:

* `decisioning.propositionDisplay`: Signalerar målaktivitetens återgivning.
* `decisioning.propositionInteract`: Signalerar en användarinteraktion med aktiviteten, som ett musklick.

The `_experience.decisioning.propositions` XDM-fältgruppen är en array med objekt. Egenskaperna för varje objekt hämtas från `result.propositions` som returneras i `sendEvent` kommando: `{ id, scope, scopeDetails }`

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

Lär dig sedan hur du [aktivera delning av domänöverskridande ID](cross-domain.md) för enhetliga besökarprofiler.

>[!NOTE]
>
>Vi vill hjälpa dig att lyckas med målmigreringen från at.js till Web SDK. Om du stöter på problem med din migrering eller känner att det saknas viktig information i den här guiden ber vi dig att meddela oss genom att publicera i [den här communitydiskussionen](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).