---
title: Skicka parametrar - Migrera från Adobe Target till Adobe Journey Optimizer - mobiltillägg för beslut
description: Lär dig hur du skickar parametrar för mbox, profile och entity till Adobe Target med Experience Platform Web SDK.
source-git-commit: afbc8248ad81a5d9080a4fdba1167e09bbf3b33d
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 0%

---

# Skicka parametrar till Target med tillägget Adobe Journey Optimizer - Decisioning Mobile

Målimplementeringarna skiljer sig åt på olika webbplatser på grund av webbplatsens arkitektur, affärskrav och vilka funktioner som används. De flesta Target-implementeringar omfattar att skicka olika parametrar för sammanhangsberoende information, målgrupper och innehållsrekommendationer.

Vi använder en enkel produktinformationssida och en orderbekräftelsesida för att visa skillnaderna mellan tilläggen när parametrar skickas till Target.


| Exempel på parametern at.js | Platform Web SDK, alternativ | Anteckningar |
| --- | --- | --- |
| `at_property` | N/A | Egenskapstoken har konfigurerats i [datastream](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html#target) och kan inte anges i anropet `sendEvent`. |
| `pageName` | `xdm.web.webPageDetails.name` | Alla Target-mbox-parametrar måste skickas som en del av `xdm`-objektet och överensstämma med ett schema med klassen XDM ExperienceEvent. Mbox-parametrar kan inte skickas som en del av `data`-objektet. |
| `profile.gender` | `data.__adobe.target.profile.gender` | Alla målprofilsparametrar måste skickas som en del av objektet `data` och prefixeras med `profile.` för att mappas korrekt. |
| `user.categoryId` | `data.__adobe.target.user.categoryId` | Reserverad parameter används för målets kategoritillhörighetsfunktion som måste skickas som en del av objektet `data`. |
| `entity.id` | `data.__adobe.target.entity.id` <br>OR<br> `xdm.productListItems[0].SKU` | Enhets-ID:n används för Recommendations-målräknare. Dessa enhets-ID:n kan antingen skickas som en del av `data`-objektet eller mappas automatiskt från det första objektet i `xdm.productListItems` -arrayen om implementeringen använder den fältgruppen. |
| `entity.categoryId` | `data.__adobe.target.entity.categoryId` | Enhetskategori-ID:n kan skickas som en del av objektet `data`. |
| `entity.customEntity` | `data.__adobe.target.entity.customEntity` | Anpassade enhetsparametrar används för att uppdatera Recommendations produktkatalog. Dessa anpassade parametrar måste skickas som en del av objektet `data`. |
| `cartIds` | `data.__adobe.target.cartIds` | Används för Target-s kundvagnsbaserade rekommendationsalgoritmer. |
| `excludedIds` | `data.__adobe.target.excludedIds` | Används för att förhindra att specifika enhets-ID returneras i en rekommendationsdesign. |
| `mbox3rdPartyId` | Ange i objektet `xdm.identityMap` | Används för synkronisering av målprofiler mellan enheter och kundattribut. Namnområdet som ska användas för kund-ID:t måste anges i [målkonfigurationen för datastream](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/using-mbox-3rdpartyid.html). |
| `orderId` | `xdm.commerce.order.purchaseID` | Används för att identifiera en unik order för målkonverteringsspårning. |
| `orderTotal` | `xdm.commerce.order.priceTotal` | Används för att spåra ordersummor för målkonverterings- och optimeringsmål. |
| `productPurchasedId` | `data.__adobe.target.productPurchasedId` <br>OR<br> `xdm.productListItems[0-n].SKU` | Används för spårning av målkonvertering och rekommendationer. Mer information finns i avsnittet [enhetsparametrar](#entity-parameters) nedan. |
| `mboxPageValue` | `data.__adobe.target.mboxPageValue` | Används för aktivitetsmålet [för anpassad poängsättning](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/capture-score.html). |

{style="table-layout:auto"}

## Egna parametrar

Egna mbox-parametrar måste skickas som XDM eller med dataobjektet med kommandot `sendEvent`. Det är viktigt att se till att XDM-schemat innehåller alla fält som krävs för målitimplementeringen.


## Profilparametrar

Målprofilsparametrar måste skickas..

## Enhetsparametrar

Enhetsparametrar används för att skicka beteendedata och kompletterande kataloginformation för Target Recommendations. Alla [enhetsparametrar](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html) som stöds av at.js stöds också av Platform Web SDK. På samma sätt som profilparametrar bör alla enhetsparametrar skickas under objektet `data.__adobe.target` i plattformens Web SDK `sendEvent` -kommandonyttolast.

Entitetsparametrar för ett specifikt objekt måste ha prefixet `entity.` för korrekt datainhämtning. De reserverade parametrarna `cartIds` och `excludedIds` för rekommendationsalgoritmer ska inte prefixas och värdet för var och en måste innehålla en kommaavgränsad lista med entitets-ID:n.



## Inköpsparametrar

Inköpsparametrar skickas till en orderbekräftelsesida efter en lyckad beställning och används för målkonverterings- och optimeringsmål. Med en plattformsbaserad SDK-implementering som använder beslutstillägget mappas dessa parametrar automatiskt från XDM-data som skickas som en del av fältgruppen `commerce`.


Inköpsinformation skickas till mål när fältgruppen `commerce` har `purchases.value` inställt på `1`. Orderns ID och ordersumman mappas automatiskt från objektet `order`. Om `productListItems`-arrayen finns används `SKU`-värdena för `productPurchasedId`.


## Kund-ID (mbox3rdPartyId)

Target tillåter profilsynkronisering mellan enheter och system med ett enda kund-ID.



Läs sedan om hur du [spårar målkonverteringshändelser](track-events.md) med Platform Web SDK.

>[!NOTE]
>
>Vi strävar efter att hjälpa dig att lyckas med din migrering av mobilmål från måltillägget till beslutstillägget. Om du stöter på problem med din migrering eller om du känner att det saknas viktig information i den här guiden kan du meddela oss genom att publicera [den här communitydiskussionen](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
