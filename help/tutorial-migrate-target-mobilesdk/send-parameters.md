---
title: Skicka parametrar - Migrera från Adobe Target till Adobe Journey Optimizer - mobiltillägg för beslut
description: Lär dig hur du skickar parametrar för mbox, profile och entity till Adobe Target med Experience Platform Web SDK.
exl-id: 927d83f9-c019-4a6b-abef-21054ce0991b
source-git-commit: 314f0279ae445f970d78511d3e2907afb9307d67
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 0%

---

# Skicka parametrar till Target med tillägget Adobe Journey Optimizer - Decisioning Mobile

Målimplementeringarna skiljer sig åt på olika webbplatser på grund av webbplatsens arkitektur, affärskrav och vilka funktioner som används. De flesta Target-implementeringar omfattar att skicka olika parametrar för sammanhangsberoende information, målgrupper och innehållsrekommendationer.

Med måltillägget skickades alla Target-parametrar med funktionen `TargetParameters`.

Med beslutets förlängning:

* Parametrar avsedda för flera Adobe-program kan skickas i XDM-objektet
* Parametrar som bara är avsedda för Target kan skickas i objektet `data.__adobe.target`


>[!IMPORTANT]
>
> Med tillägget Decsioning gäller parametrar som skickas i en begäran alla scope i begäran. Om du behöver ange olika parametrar för olika omfattningar måste du göra ytterligare förfrågningar.

## Egna parametrar

Anpassade mbox-parametrar är det mest grundläggande sättet att skicka data till Target och kan skickas i XDM- eller `data.__adobe.target`-objekten.

## Profilparametrar

Profilparametrar lagrar data för en längre tidsperiod i användarens målprofil och måste skickas i objektet `data.__adobe.target`.

## Enhetsparametrar

[Entitetsparametrar](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html) används för att skicka beteendedata och kompletterande kataloginformation för målrekommendationer. På samma sätt som profilparametrar ska alla enhetsparametrar skickas under objektet `data.__adobe.target`.

Entitetsparametrar för ett specifikt objekt måste ha prefixet `entity.` för korrekt datainhämtning. De reserverade parametrarna `cartIds` och `excludedIds` för rekommendationsalgoritmer ska inte prefixas och värdet för var och en måste innehålla en kommaavgränsad lista med entitets-ID:n.

## Inköpsparametrar

Inköpsparametrar skickas till en orderbekräftelsesida efter en lyckad beställning och används för målkonverterings- och optimeringsmål. Med en Platform Mobile SDK-implementering som använder beslutstillägget mappas dessa parametrar automatiskt från XDM-data som skickas som en del av fältgruppen `commerce`.

Inköpsinformation skickas till mål när fältgruppen `commerce` har `purchases.value` inställt på `1`. Orderns ID och ordersumman mappas automatiskt från objektet `order`. Om `productListItems`-arrayen finns används `SKU`-värdena för `productPurchasedId`.

Om du inte skickar `commerce` fält i XDM-objektet kan du skicka ordningsinformationen till målet med hjälp av fälten `data.__adobe.target.orderId`, `data.__adobe.target.orderTotal` och `data.__adobe.target.productPurchasedId`.

## Kund-ID (mbox3rdPartyId)

Target tillåter profilsynkronisering mellan enheter och system med ett enda kund-ID. Detta kund-ID ska skickas i fältet `identityMap` för XDM-objektet och mappas till fältet Mål-ID för tredje part i datastream.

## Tabell

| Exempel på parametern at.js | Platform Web SDK | Anteckningar |
| --- | --- | --- |
| `at_property` | N/A | Egenskapstoken har konfigurerats i [datastream](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html#target) och kan inte anges i anropet `sendEvent`. |
| `pageName` | `xdm.web.webPageDetails.name` | Alla Target-mbox-parametrar måste skickas som en del av `xdm`-objektet och överensstämma med ett schema med klassen XDM ExperienceEvent. Mbox-parametrar kan inte skickas som en del av `data`-objektet. |
| `profile.gender` | `data.__adobe.target.profile.gender` | Alla målprofilsparametrar måste skickas som en del av objektet `data` och prefixeras med `profile.` för att mappas korrekt. |
| `user.categoryId` | `data.__adobe.target.user.categoryId` | Reserverad parameter används för målets kategoritillhörighetsfunktion som måste skickas som en del av objektet `data`. |
| `entity.id` | `data.__adobe.target.entity.id` <br>OR<br> `xdm.productListItems[0].SKU` | Enhets-ID används för beteenderäknare för målrekommendationer. Dessa enhets-ID:n kan antingen skickas som en del av `data`-objektet eller mappas automatiskt från det första objektet i `xdm.productListItems` -arrayen om implementeringen använder den fältgruppen. |
| `entity.categoryId` | `data.__adobe.target.entity.categoryId` | Enhetskategori-ID:n kan skickas som en del av objektet `data`. |
| `entity.customEntity` | `data.__adobe.target.entity.customEntity` | Anpassade enhetsparametrar används för att uppdatera produktkatalogen Recommendations. Dessa anpassade parametrar måste skickas som en del av objektet `data`. |
| `cartIds` | `data.__adobe.target.cartIds` | Används för Target-s kundvagnsbaserade rekommendationsalgoritmer. |
| `excludedIds` | `data.__adobe.target.excludedIds` | Används för att förhindra att specifika enhets-ID returneras i en rekommendationsdesign. |
| `mbox3rdPartyId` | Ange i objektet `xdm.identityMap` | Används för synkronisering av målprofiler mellan enheter och kundattribut. Namnområdet som ska användas för kund-ID:t måste anges i [målkonfigurationen för datastream](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/using-mbox-3rdpartyid.html). |
| `orderId` | `xdm.commerce.order.purchaseID`<br> (när `commerce.purchases.value` är inställd på `1`) | Används för att identifiera en unik order för målkonverteringsspårning. |
| `orderTotal` | `xdm.commerce.order.priceTotal`<br> (när `commerce.purchases.value` är inställd på `1`) | Används för att spåra ordersummor för målkonverterings- och optimeringsmål. |
| `productPurchasedId` | `xdm.productListItems[0-n].SKU`<br> (när `commerce.purchases.value` är inställd på `1`) <br>OR<br> `data.__adobe.target.productPurchasedId` | Används för spårning av målkonvertering och rekommendationer. Mer information finns i avsnittet [enhetsparametrar](#entity-parameters) nedan. |
| `mboxPageValue` | `data.__adobe.target.mboxPageValue` | Används för aktivitetsmålet [för anpassad poängsättning](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/capture-score.html). |

{style="table-layout:auto"}


## Exempel på att skicka parametrar

Låt oss använda ett enkelt exempel för att demonstrera skillnaderna mellan tilläggen när parametrar skickas till Target.

### Android

>[!BEGINTABS]

>[!TAB SDK som mål]

```Java
Map<String, String> mboxParameters = new HashMap<String, String>();
mboxParameters1.put("status", "platinum");
 
Map<String, String> profileParameters = new HashMap<String, String>();
profileParameters1.put("gender", "male");
 
List<String> purchasedProductIds = new ArrayList<String>();
purchasedProductIds.add("ppId1");
TargetOrder targetOrder = new TargetOrder("id1", 1.0, purchasedProductIds);
 
TargetProduct targetProduct = new TargetProduct("pId1", "cId1");
 
TargetParameters targetParameters = new TargetParameters.Builder()
                                    .parameters(mboxParameters)
                                    .profileParameters(profileParameters)
                                    .product(targetProduct)
                                    .order(targetOrder)
                                    .build();
```

>[!ENDTABS]

### iOS

>[!BEGINTABS]

>[!TAB SDK som mål]

```Swift
let mboxParameters = [
                        "status": "platinum"
                     ]
 
let profileParameters = [
                            "gender": "male"
                        ]
 
let order = TargetOrder(id: "id1", total: 1.0, purchasedProductIds: ["ppId1"])
 
let product = TargetProduct(productId: "pId1", categoryId: "cId1")
 
let targetParameters = TargetParameters(parameters: mboxParameters, profileParameters: profileParameters, order: order, product: product))
```


>[!ENDTABS]






Läs sedan om hur du [spårar målkonverteringshändelser](track-events.md) med Platform Web SDK.

>[!NOTE]
>
>Vi strävar efter att hjälpa dig att lyckas med din migrering av mobilmål från måltillägget till beslutstillägget. Om du stöter på problem med din migrering eller om du känner att det saknas viktig information i den här guiden kan du meddela oss genom att publicera [den här communitydiskussionen](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
