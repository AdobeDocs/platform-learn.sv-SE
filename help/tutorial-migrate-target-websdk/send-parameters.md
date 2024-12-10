---
title: Skicka parametrar - Migrera mål från at.js 2.x till Web SDK
description: Lär dig hur du skickar parametrar för mbox, profile och entity till Adobe Target med Experience Platform Web SDK.
exl-id: 7916497b-0078-4651-91b1-f53c86dd2100
source-git-commit: 0697c6d13272182432e11fdb9d84a752d39527b6
workflow-type: tm+mt
source-wordcount: '1547'
ht-degree: 0%

---

# Skicka parametrar till Target med Platform Web SDK

Målimplementeringarna skiljer sig åt på olika webbplatser på grund av webbplatsens arkitektur, affärskrav och vilka funktioner som används. De flesta Target-implementeringar omfattar att skicka olika parametrar för sammanhangsberoende information, målgrupper och innehållsrekommendationer.

Vi använder en enkel produktinformationssida och en orderbekräftelsesida för att visa skillnaderna mellan biblioteken när parametrar skickas till Target.

Anta följande två exempelsidor med at.js:

+++at.js på en produktinformationssida:

```HTML
<!doctype html>
<html>
<head>
  <title>Product Details - Men's Shirt</title>
  <!--Target parameters -->
  <script>
    targetPageParams = function() {
      return {
        // Property token
        "at_property": "5a0fd9bb-67de-4b5a-0fd7-9cc09f50a58d",
        // Mbox parameters
        "pageName": "product detail",
        // Profile parameters
        "profile.gender": "male",
        "user.categoryId": "clothing",
        // Entity parameters for Target Recomendations
        "entity.id": "SKU-00001-LARGE",
        "entity.categoryId": "clothing,shirts",
        "entity.customEntity": "some value",
        "cartIds": "SKU-00002,SKU-00003",
        "excludedIds": "SKU-00001-SMALL",
        // Customer ID for cross-device profile synching and Customer Attributes
        "mbox3rdPartyId": "TT8675309",
      };
    };
  </script>
  <!--Target at.js library loaded asynchonously-->
  <script src="/libraries/at.js" async></script>
</head>
<body>
  <h1 id="title">Men's Large Shirt</h1>
  <p>SKU: SKU-00001-LARGE</p>
</body>
</html>
```

+++


+++at.js på en orderbekräftelsesida:

```HTML
<!doctype html>
<html>
<head>
  <title>Order Confirmation</title>-->
  <!--Target parameters -->
  <script>
    targetPageParams = function() {
      return {
        // Property token
        "at_property": "5a0fd9bb-67de-4b5a-0fd7-9cc09f50a58d",
        // Order confirmation parameters
        "orderId": "ABC123",
        "productPurchasedId": "SKU-00002,SKU-00003",
        "orderTotal": 1337.89,
        // Customer ID for cross-device profile synching and Customer Attributes
        "mbox3rdPartyId": "TT8675309",
      };
    };
  </script>
  <!--Target at.js library loaded asynchonously-->
  <script src="/libraries/at.js" async></script>
</head>
<body>
  <h1 id="title">Order Confirmation</h1>
  <p>Thank you for your order</p>
</body>
</html>
```

+++


## Sammanfattning av parametermappning

Målparametrarna för de här sidorna skickas annorlunda med Platform Web SDK. Det finns flera sätt att skicka parametrar till Target med at.js:

- Ange med funktionen `targetPageParams()` för sidans load-händelse (används i exemplen på den här sidan)
- Ange med funktionen `targetPageParamsAll()` för alla Target-begäranden på sidan
- Skicka parametrar direkt med funktionen `getOffer()` för en enda plats
- Skicka parametrar direkt med funktionen `getOffers()` för en eller flera platser


Platform Web SDK är ett enda konsekvent sätt att skicka data utan behov av extra funktioner. Alla parametrar måste skickas i nyttolasten med kommandot `sendEvent` och faller under två kategorier:

- Mappas automatiskt från objektet `xdm`
- Manuellt skickad med objektet `data.__adobe.target`

Tabellen nedan visar hur exempelparametrarna skulle ommappas med Platform Web SDK:

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

Egna mbox-parametrar måste skickas som XDM-data med kommandot `sendEvent`. Det är viktigt att se till att XDM-schemat innehåller alla fält som krävs för målitimplementeringen.

at.js-exempel med `targetPageParams()`:

```JavaScript
targetPageParams = function() {
  return {
    "pageName": "product detail"
  };
};
```

Exempel på JavaScript för Platform Web SDK med kommandot `sendEvent`:

>[!BEGINTABS]

>[!TAB JavaScript]

```JavaScript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webPageDetails": {
        // Other attributes included according to xdm schema
        "name": "product detail"
      }
    }
  }
});
```

>[!TAB Taggar]

I taggar använder du först ett [!UICONTROL XDM object]-dataelement för att mappa till XDM-fältet:

![Mappning till ett XDM-fält i ett XDM-objektdataelement](assets/params-tags-pageName.png){zoomable="yes"}

Ta sedan med din [!UICONTROL XDM object] i din [!UICONTROL Send event] [!UICONTROL action] (flera [!UICONTROL XDM objects] kan [sammanfogas](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/core/overview.html?lang=en#merged-objects)):

![Inkludera ett XDM-objektdataelement i en Send-händelse](assets/params-tags-sendEvent.png){zoomable="yes"}

>[!ENDTABS]


>[!NOTE]
>
>Eftersom anpassade mbox-parametrar är en del av `xdm`-objektet måste du uppdatera alla målgrupper, aktiviteter eller profilskript som refererar till de här mbox-parametrarna med deras nya namn. Mer information finns på sidan [Uppdatera målgrupper och profilskript för kompatibilitet med plattformswebbsäkra DK](update-audiences.md) i den här självstudiekursen.


## Profilparametrar

Målprofilsparametrar måste skickas under objektet `data.__adobe.target` i kommandotolken för Platform Web SDK `sendEvent`.

Precis som at.js måste alla profilparametrar också ha prefixet `profile.` för att värdet ska lagras korrekt som ett beständigt Target-profilattribut. Den reserverade parametern `user.categoryId` för målets kategoritillhörighetsfunktion har prefixet `user.`.

at.js-exempel med `targetPageParams()`:

```JavaScript
targetPageParams = function() {
  return {
    "profile.gender": "male",
    "user.categoryId": "clothing"
  };
};
```

Exempel på SDK för plattformswebben med kommandot `sendEvent`:

>[!BEGINTABS]

>[!TAB JavaScript]

```JavaScript
alloy("sendEvent", {
  "data": {
    "__adobe": {
      "target": {
        "profile.gender": "male",
        "user.categoryId": "clothing"
      }
    }
  }
});
```

>[!TAB Taggar]

Skapa först ett dataelement i taggar för att definiera objektet `data.__adobe.target`:

![Definiera ditt dataobjekt i ett dataelement](assets/params-tags-dataObject.png){zoomable="yes"}

Inkludera sedan dataobjektet i [!UICONTROL Send event] [!UICONTROL action] (flera [!UICONTROL objects] kan vara [sammanfogade](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/core/overview.html?lang=en#merged-objects)):

![Inkludera ett dataobjekt i en Send-händelse](assets/params-tags-sendEvent-withData.png){zoomable="yes"}

>[!ENDTABS]

## Enhetsparametrar

Enhetsparametrar används för att skicka beteendedata och kompletterande kataloginformation för Target Recommendations. Alla [enhetsparametrar](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html) som stöds av at.js stöds också av Platform Web SDK. På samma sätt som profilparametrar bör alla enhetsparametrar skickas under objektet `data.__adobe.target` i plattformens Web SDK `sendEvent` -kommandonyttolast.

Entitetsparametrar för ett specifikt objekt måste ha prefixet `entity.` för korrekt datainhämtning. De reserverade parametrarna `cartIds` och `excludedIds` för rekommendationsalgoritmer ska inte prefixas och värdet för var och en måste innehålla en kommaavgränsad lista med entitets-ID:n.

at.js-exempel med `targetPageParams()`:

```JavaScript
targetPageParams = function() {
  return {
    "entity.id": "SKU-00001-LARGE",
    "entity.categoryId": "clothing,shirts",
    "entity.customEntity": "some value",
    "cartIds": "SKU-00002,SKU-00003",
    "excludedIds": "SKU-00001-SMALL"
  };
};
```

Exempel på SDK för plattformswebben med kommandot `sendEvent`:

>[!BEGINTABS]

>[!TAB JavaScript]

```JavaScript
alloy("sendEvent", {
  "data": {
    "__adobe": {
      "target": {
        "entity.id": "SKU-00001-LARGE",
        "entity.categoryId": "clothing,shirts",
        "entity.customEntity": "some value",
        "cartIds": "SKU-00002,SKU-00003",
        "excludedIds": "SKU-00001-SMALL"
      }
    }
  }
});
```

>[!TAB Taggar]

Skapa först ett dataelement i taggar för att definiera objektet `data.__adobe.target`:

![Definiera ditt dataobjekt i ett dataelement](assets/params-tags-dataObject-entities.png){zoomable="yes"}

Inkludera sedan dataobjektet i [!UICONTROL Send event] [!UICONTROL action] (flera [!UICONTROL objects] kan vara [sammanfogade](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/core/overview.html?lang=en#merged-objects)):

![Inkludera ett dataobjekt i en Send-händelse](assets/params-tags-sendEvent-withData.png){zoomable="yes"}

>[!ENDTABS]

>[!NOTE]
>
>Om fältgruppen `commerce` används och arrayen `productListItems` ingår i XDM-nyttolasten mappas det första `SKU`-värdet i den här arrayen till `entity.id` för att öka en produktvy.


## Inköpsparametrar

Inköpsparametrar skickas till en orderbekräftelsesida efter en lyckad beställning och används för målkonverterings- och optimeringsmål. Med en plattformsbaserad Web SDK-implementering mappas de här parametrarna automatiskt från XDM-data som skickas som en del av fältgruppen `commerce`.

at.js-exempel med `targetPageParams()`:

```JavaScript
targetPageParams = function() {
  return {
    "orderId": "ABC123",
    "productPurchasedId": "SKU-00002,SKU-00003"
    "orderTotal": 1337.89
  };
};
```

Inköpsinformation skickas till mål när fältgruppen `commerce` har `purchases.value` inställt på `1`. Orderns ID och ordersumman mappas automatiskt från objektet `order`. Om `productListItems`-arrayen finns används `SKU`-värdena för `productPurchasedId`.

Exempel på plattformswebb-SDK med `sendEvent`:

>[!BEGINTABS]

>[!TAB JavaScript]

```JavaScript
alloy("sendEvent", {
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "ABC123",
        "priceTotal": 1337.89
      },
      "purchases": {
        "value": 1
      }
    },
    "productListItems": [{
      "SKU": "SKU-00002"
    }, {
      "SKU": "SKU-00003"
    }],
      "_experience": {
          "decisioning": {
              "propositions": [{
                  "scope": "<your_mbox>"
              }],
              "propositionEventType": {
                  "display": 1
              }
          }
      }
  }
});
```

>[!TAB Taggar]

I taggar använder du först ett [!UICONTROL XDM object]-dataelement för att mappa till de obligatoriska XDM-fälten (se JavaScript exempel) och valfritt anpassat omfång:

![Mappning till ett XDM-fält i ett XDM-objektdataelement](assets/params-tags-purchase.png){zoomable="yes"}

Ta sedan med din [!UICONTROL XDM object] i din [!UICONTROL Send event] [!UICONTROL action] (flera [!UICONTROL XDM objects] kan [sammanfogas](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/core/overview.html?lang=en#merged-objects)):

![Inkludera ett XDM-objektdataelement i en Send-händelse](assets/params-tags-sendEvent-purchase.png){zoomable="yes"}

>[!ENDTABS]

>[!IMPORTANT]
>
> `_experience.decisioning.propositionEventType` måste anges med `display: 1` för att anropet ska kunna användas för att öka ett Target-mått.

>[!NOTE]
>
> Om du vill använda ett anpassat plats-/mbox-namn i målmåttsdefinitionen, till exempel `orderConfirmPage`, fyller du i `_experience.decisioning.propositions`-arrayen med ett anpassat omfång som i exemplet ovan.

>[!NOTE]
>
>Värdet `productPurchasedId` kan också skickas som en kommaavgränsad lista med enhets-ID:n under objektet `data`.


## Kund-ID (mbox3rdPartyId)

Target tillåter profilsynkronisering mellan enheter och system med ett enda kund-ID. Med at.js kan detta anges som `mbox3rdPartyId` i Target-begäran eller som det första kund-ID som skickas till Experience Cloud Identity Service. Till skillnad från at.js kan du med en implementering av Platform Web SDK ange vilket kund-ID som ska användas som `mbox3rdPartyId` om det finns flera. Om ditt företag till exempel har ett globalt kund-ID och separata kund-ID för olika affärsområden, kan du konfigurera vilket ID Target som ska användas.

Det finns några steg för att konfigurera ID-synkronisering för användning av olika enheter och kundattribut:

1. Skapa en **[!UICONTROL identity namespace]** för kund-ID på skärmen **[!UICONTROL Identities]** i datainsamling eller plattform
1. Kontrollera att **[!UICONTROL alias]** i kundattribut matchar **[!UICONTROL identity symbol]** i namnutrymmet
1. Ange **[!UICONTROL identy symbol]** som **[!UICONTROL Target Third Party ID Namespace]** i målkonfigurationen för datastream
1. Kör ett `sendEvent`-kommando med fältgruppen `identityMap`

at.js-exempel med `targetPageParams()`:

```JavaScript
targetPageParams = function() {
  return {
    "mbox3rdPartyId": "TT8675309"
  };
};
```

Exempel på SDK för plattformswebben med kommandot `sendEvent`:

>[!BEGINTABS]

>[!TAB JavaScript]

```JavaScript
alloy("sendEvent", {
  "xdm": {
    "identityMap": {
      "GLOBAL_CUSTOMER_ID": [{
        "id": "TT8675309",
        "authenticatedState": "authenticated",
        "primary": true
      }]
    }
  }
});
```

>[!TAB Taggar]

[!UICONTROL ID]-värdet, [!UICONTROL Authenticated state] och [!UICONTROL Namespace] hämtas i ett [!UICONTROL Identity map]-dataelement:
![Identitetskarta - dataelement som hämtar kund-ID:t ](assets/params-tags-customerIdDataElement.png){zoomable="yes"}

Dataelementet [!UICONTROL Identity map] används sedan för att ställa in fältet [!UICONTROL identityMap] i dataelementet [!UICONTROL XDM object]:
![ Identitetskarta, dataelement som används i XDM-objektdataelement ](assets/params-tags-customerIdInXDMObject.png){zoomable="yes"}

[!UICONTROL XDM object] ingår sedan i åtgärden [!UICONTROL Send event] för en regel:

![Inkludera ett XDM-objektdataelement i en Send-händelse](assets/params-tags-sendEvent-xdm.png){zoomable="yes"}

I datastreams Adobe Target-tjänst måste du ange [!UICONTROL Target Third Party ID Namespace] till samma namnområde som används i dataelementet [!UICONTROL Identity map]:
![Ange namnutrymmet för mål-ID för tredje part i datastream ](assets/params-tags-customerIdNamespaceInDatastream.png){zoomable="yes"}

>[!ENDTABS]

>[!NOTE]
>
> Adobe rekommenderar att du som primär identitet skickar namnutrymmen som representerar en person, t.ex. autentiserade identiteter.



## Exempel på Platform Web SDK

Nu när du förstår hur de olika Target-parametrarna mappas med Platform Web SDK kan våra två exempelsidor migreras från at.js till Platform Web SDK enligt nedan. Exempelsidorna innehåller följande:

- Skapa ett fördolt fragment för en asynkron biblioteksimplementering
- Baskod för Platform Web SDK
- JavaScript-biblioteket Platform Web SDK
- Ett `configure`-kommando för att initiera biblioteket
- Ett `sendEvent`-kommando som skickar data och begär att Target-innehåll ska återges

+++Web SDK på en produktinformationssida:

```HTML
<!doctype html>
<html>
<head>
  <title>Product Details - Men's Shirt</title>

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

  <!--Configure Platform Web SDK and send event-->
  <script>
    alloy("configure", {
      "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
      "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
    });
    alloy("sendEvent", {
      "renderDecisions": true,
      "xdm": {
        "identityMap": {
          "GLOBAL_CUSTOMER_ID": [{
            "id": "TT8675309",
            "authenticatedState": "authenticated",
            "primary": true
          }]
        },
        "web": {
          "webPageDetails": {
            // Other attributes included according to XDM schema
            "pageName": "product detail"
          }
        }
      },
      "data": {
        "__adobe": {
          "target": {
            "profile.gender": "male",
            "user.categoryId": "clothing",
            "entity.id": "SKU-00001-LARGE",
            "entity.categoryId": "clothing,shirts",
            "entity.customEntity": "some value",
            "cartIds": "SKU-00002,SKU-00003",
            "excludedIds": "SKU-00001-SMALL"
          }
        }
      }
    });
  </script>
</head>
<body>
  <h1 id="title">Men's Large Shirt</h1>
  <p>SKU: SKU-00001-LARGE</p>
</body>
</html>
```

+++

+++Web SDK på en orderbekräftelsesida:

```HTML
<!doctype html>
<html>
<head>
  <title>Order Confirmation</title>


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

  <!--Configure Platform Web SDK and send event-->
  <script>
    alloy("configure", {
      "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
      "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
    });
    alloy("sendEvent", {
      "xdm": {
        "identityMap": {
          "GLOBAL_CUSTOMER_ID": [{
            "id": "TT8675309",
            "authenticatedState": "authenticated",
            "primary": true
          }]
        },
        "commerce": {
          "order": {
            "purchaseID": "ABC123",
            "priceTotal": 1337.89
          },
          "purchases": {
            "value": 1
          }
        },
        "productListItems": [{
          "SKU": "SKU-00002"
        }, {
          "SKU": "SKU-00003"
        }],
        "_experience": {
            "decisioning": {
                "propositions": [{
                    "scope": "<your_mbox>"
                }],
                "propositionEventType": {
                    "display": 1
                }
            }
        }
      }
    });
  </script>
</head>
<body>
  <h1 id="title">Order Confirmation</h1>
  <p>Thank you for your order</p>
</body>
</html>
```

+++

Läs sedan om hur du [spårar målkonverteringshändelser](track-events.md) med Platform Web SDK.

>[!NOTE]
>
>Vi vill hjälpa dig att lyckas med målmigreringen från at.js till Web SDK. Om du stöter på problem med din migrering eller om du känner att det saknas viktig information i den här guiden kan du meddela oss genom att publicera [den här communitydiskussionen](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
