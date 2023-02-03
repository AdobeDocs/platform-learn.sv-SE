---
title: Skicka parametrar | Migrera mål från at.js 2.x till Web SDK
description: Lär dig hur du skickar mbox-, profile- och enhetsparametrar till Adobe Target med Experience Platform Web SDK.
source-git-commit: 8209b13b745dbea418003b133a6834825947950e
workflow-type: tm+mt
source-wordcount: '1269'
ht-degree: 0%

---

# Skicka parametrar till Target med Platform Web SDK

Målimplementeringarna skiljer sig åt på olika webbplatser på grund av webbplatsens arkitektur, affärskrav och vilka funktioner som används. De flesta Target-implementeringar omfattar att skicka olika parametrar för sammanhangsberoende information, målgrupper och innehållsrekommendationer.

Vi använder en enkel produktinformationssida och en orderbekräftelsesida för att visa skillnaderna mellan biblioteken när parametrar skickas till Target.

Anta följande exempelsida med at.js:

<!--Assume the following two example pages using at.js:-->

Produktinformation:

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
        "siteSection": "product details",
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



Orderbekräftelse:

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


## Sammanfattning av parametermappning

Målparametrarna som används på dessa två exempelsidor måste skickas lite annorlunda med Platform Web SDK. Det finns flera sätt att skicka parametrar till Target med at.js:

- Använd `targetPageParams()` funktion för sidans load-händelse
- Använd `targetPageParamsAll()` funktion för alla Target-begäranden på sidan
- Skicka parametrar direkt med `getOffer()` funktion för en enda plats
- Skicka parametrar direkt med `getOffers()` funktion för en eller flera platser

I det här exemplet gäller följande: `targetPageParams()` -metoden används.

Platform Web SDK förenklar detta genom att tillhandahålla ett enda konsekvent sätt att skicka data utan behov av extra funktioner. Alla parametrar måste skickas i nyttolasten med `sendEvent` -kommando.

Parametrar som skickas med Platform Web SDK `sendEvent` nyttolasten faller under två kategorier:

1. Mappas automatiskt från `xdm` object
1. Manuellt skickad med `data.__adobe.target` object

Tabellen nedan visar hur exempelparametrarna skulle ommappas med Platform Web SDK:

| Exempel på parametern at.js | Platform Web SDK, alternativ | Anteckningar |
| --- | --- | --- |
| `at_property` | Ej tillämpligt | Egenskapstoken har konfigurerats i [datastream](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html#target) och kan inte anges i `sendEvent` ring. |
| `siteSection` | `xdm.web.webPageDetails.siteSection` | Alla Target-parametrar måste skickas som en del av `xdm` och anpassa till ett schema med klassen XDM ExperienceEvent. Mbox-parametrar kan inte skickas som en del av `data` -objekt. |
| `profile.gender` | `data.__adobe.target.profile.gender` | Alla målprofilsparametrar måste skickas som en del av `data` objekt och prefix med `profile.` mappas på lämpligt sätt. |
| `user.categoryId` | `data.__adobe.target.user.categoryId` | Reserverad parameter som används för målets kategoritillhörighetsfunktion som måste skickas som en del av `data` -objekt. |
| `entity.id` | `data.__adobe.target.entity.id` <br>ELLER<br> `xdm.productListItems[0].SKU` | Enhets-ID används för Recommendations-målräknare. Dessa enhets-ID kan antingen skickas som en del av `data` eller automatiskt mappas från det första objektet i `xdm.productListItems` -array om implementeringen använder den fältgruppen. |
| `entity.categoryId` | `data.__adobe.target.entity.categoryId` | Enhetskategori-ID:n kan skickas som en del av `data` -objekt. |
| `entity.customEntity` | `data.__adobe.target.entity.customEntity` | Anpassade enhetsparametrar används för att uppdatera Recommendations produktkatalog. Dessa anpassade parametrar måste skickas som en del av `data` -objekt. |
| `cartIds` | `data.__adobe.target.cartIds` | Används för Target-s kundvagnsbaserade rekommendationsalgoritmer. |
| `excludedIds` | `data.__adobe.target.excludedIds` | Används för att förhindra att specifika enhets-ID returneras i en rekommendationsdesign. |
| `mbox3rdPartyId` | Anges i identityMap. Se [Synkronisera profiler med ett kund-ID](#synching-profiles-with-a-customer-id) | Används för synkronisering av målprofiler mellan enheter och kundattribut. Namnutrymmet som ska användas för kund-ID:t måste anges i [Målkonfiguration för datastream](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/using-mbox-3rdpartyid.html). |
| `orderId` | `xdm.commerce.order.purchaseID` | Används för att identifiera en unik order för målkonverteringsspårning. |
| `orderTotal` | `xdm.commerce.order.priceTotal` | Används för att spåra ordersummor för målkonverterings- och optimeringsmål. |
| `productPurchasedId` | `data.__adobe.target.productPurchasedId` <br>ELLER<br> `xdm.productListItems[0-n].SKU` | Används för spårning av målkonvertering och rekommendationsalgoritmer. Se [enhetsparametrar](#entity-parameters) för mer information. |
| `mboxPageValue` | `data.__adobe.target.mboxPageValue` | Används för [egen poängsättning](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/capture-score.html) verksamhetsmål. |

{style=&quot;table-layout:auto&quot;}

## Egna parametrar

Alla anpassade mbox-parametrar måste skickas som XDM-data med `sendEvent` -kommando. Det är viktigt att se till att XDM-schemat innehåller alla datapunkter som krävs för målinsimplementeringen.

at.js-exempel med `targetPageParams()`:

```JavaScript
targetPageParams = function() {
  return {
    "siteSection": "product detail"
  };
};
```

Exempel på SDK för plattformar med `sendEvent` kommando:

```JavaScript
alloy("sendEvent", {
  "xdm": {
    "web": {
      "webPageDetails": {
        // Other attributes included according to xdm schema
        "siteSection": "product detail"
      }
    }
  }
});
```

>[!NOTE]
>
>Eftersom anpassade mbox-parametrar måste skickas som en del av `xdm` objekt i `sendEvent` måste alla mbox-parametrar som används i implementeringen av at.js Target tilldelas om till en XDM-motsvarighet. Det innebär att du måste uppdatera målgrupper, aktiviteter eller profilskript som refererar till dessa mbox-parametrar.


## Profilparametrar

Målprofilsparametrar måste skickas under `data.__adobe.target` objekt i Platform Web SDK `sendEvent` kommandots nyttolast.

Precis som at.js måste alla profilparametrar också ha prefix med `profile.` för att värdet ska lagras korrekt som ett beständigt Target-profilattribut. Den reserverade `user.categoryId` parametern för målets kategoritillhörighet har prefixet `user.`.

at.js-exempel med `targetPageParams()`:

```JavaScript
targetPageParams = function() {
  return {
    "profile.gender": "male",
    "user.categoryId": "clothing"
  };
};
```

Exempel på SDK för plattformar med `sendEvent` kommando:

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

## Enhetsparametrar

Enhetsparametrar används för att skicka beteendedata och kompletterande kataloginformation för Target Recommendations. Precis som profilparametrar måste alla enhetsparametrar skickas under `data.__adobe.target` objekt i Platform Web SDK `sendEvent` kommandots nyttolast.

Entitetsparametrar för ett specifikt objekt måste föregås av `entity.` för korrekt datainhämtning. Den reserverade `cartIds` och `excludedIds` parametrar för rekommendationsalgoritmer ska inte prefixas och värdet för var och en måste innehålla en kommaavgränsad lista med enhets-ID:n.

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

Exempel på SDK för plattformar med `sendEvent` kommando:

```JavaScript
alloy("sendEvent", {
  "data": {
    "__adobe": {
      "target": {
        "entity.id": "SKU-00001-LARGE",
        "entity.categoryId": "clothing,shirts"
        "entity.customEntity": "some value",
        "cartIds": "SKU-00002,SKU-00003",
        "excludedIds": "SKU-00001-SMALL"
      }
    }
  }
});
```

Alla [enhetsparametrar](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html) som stöds av at.js stöds även av Platform Web SDK.

>[!NOTE]
>
>Om `commerce` fältgruppen används och `productListItems` -arrayen ingår i XDM-nyttolasten och sedan den första `SKU` värdet i den här arrayen mappas till `entity.id` för att öka en produktvy.


## Inköpsparametrar

Inköpsparametrar skickas till en orderbekräftelsesida efter en lyckad beställning och används för målkonverterings- och optimeringsmål. Med en plattformsbaserad Web SDK-implementering mappas dessa parametrar och automatiskt från XDM-data som skickas som en del av `commerce` fältgrupp.

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

Inköpsinformation skickas till Target när `commerce` fältgruppen har `puchases.value` ange till `1`. Orderns-ID och ordersumman mappas automatiskt från `order` -objekt. Om `productListItems` arrayen finns, sedan `SKU` värden används för `productPurchasedId`.

Exempel på SDK för plattformar med `sendEvent` kommando:

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
    }]
  }
});
```

>[!NOTE]
>
>The `productPurchasedId` värdet kan också skickas som en kommaavgränsad lista med enhets-ID:n under `data` -objekt.


## Synkronisera profiler med ett kund-ID

Target tillåter profilsynkronisering mellan enheter och system med ett enda kund-ID. Med at.js kan detta anges som `mbox3rdPartyId` i Target-begäran eller som det första kund-ID som skickas till Experience Cloud Identity Service. Till skillnad från at.js kan du med en implementering av Platform Web SDK ange vilket kund-ID som ska användas som `mbox3rdPartyId` om det finns flera. Om ditt företag till exempel har ett globalt kund-ID och separata kund-ID för olika affärsområden, kan du konfigurera vilket ID Target som ska användas.

Det finns några steg för att konfigurera ID-synkronisering för olika målenheter och för att använda kundattribut:

1. Skapa en **[!UICONTROL identity namespace]** för kund-ID:t i **[!UICONTROL Identiteter]** skärm för datainsamling eller -plattform
1. Se till att **[!UICONTROL alias]** i kundattribut matchar **[!UICONTROL identitetssymbol]** namnutrymmet
1. Ange **[!UICONTROL identy symbol]** som **[!UICONTROL Namnområde för tredje parts ID-mål]** i målkonfigurationen för datastream
1. Kör en `sendEvent` med `identityMap` fältgrupp

at.js-exempel med `targetPageParams()`:

```JavaScript
targetPageParams = function() {
  return {
    "mbox3rdPartyId": "TT8675309"
  };
};
```

Exempel på SDK för plattformar med `sendEvent` kommando:

```JavaScript
alloy("sendEvent", {
  "xdm": {
    "identityMap": {
      "GLOBAL_CUSTOMER_ID": [{
        "id": "TT8675309",
        "authenticatedState": "authenticated"
      }]
    }
  }
});
```


## Exempel på Platform Web SDK

Nu när du förstår hur de olika Target-parametrarna mappas med Platform Web SDK kan våra två exempelsidor migreras från at.js till Platform Web SDK enligt nedan. Exempelsidorna innehåller följande:

- Skapa ett fördolt fragment för en asynkron biblioteksimplementering
- Baskod för Platform Web SDK
- Platform Web SDK JavaScript-biblioteket
- A `configure` för att initiera biblioteket
- A `sendEvent` för att skicka data och begära att Target-innehåll återges

Produktinformation:

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
            "authenticatedState": "authenticated"
          }]
        },
        "web": {
          "webPageDetails": {
            // Other attributes included according to XDM schema
            "siteSection": "product detail"
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


Orderbekräftelse:

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
            "authenticatedState": "authenticated"
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
        }]
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

Lär dig sedan hur du [spåra konverteringshändelser för mål](track-events.md) med Platform Web SDK.

>[!NOTE]
>
>Vi vill hjälpa dig att lyckas med målmigreringen från at.js till Web SDK. Om du stöter på problem med din migrering eller känner att det saknas viktig information i den här guiden ber vi dig att meddela oss genom att publicera i [den här communitydiskussionen](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).
