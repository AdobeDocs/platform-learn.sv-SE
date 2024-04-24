---
title: Skapa dataelement
description: Lär dig hur du skapar ett XDM-objekt och mappar dataelement till det i taggar. Den här lektionen ingår i självstudiekursen Implementera Adobe Experience Cloud med Web SDK.
feature: Tags
exl-id: d662ec46-de9b-44ba-974a-f81dfc842e68
source-git-commit: 100a6a9ac8d580b68beb7811f99abcdc0ddefd1a
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 0%

---

# Skapa dataelement

Lär dig hur du skapar dataelement i taggar för innehåll, handel och identitetsdata på [Luma demo site](https://luma.enablementadobe.com/content/luma/us/en.html). Fyll sedan i fälten i XDM-schemat med datatypen Variable för Platform Web SDK-tillägget.

## Utbildningsmål

När lektionen är slut kan du:

* Förstå olika metoder för att mappa ett datalager till XDM
* Skapa dataelement för datainhämtning
* Mappa dataelement till ett XDM-objekt


## Förutsättningar

Du har en förståelse för vad ett datalager är och har slutfört föregående lektioner i självstudien:

* [Konfigurera ett XDM-schema](configure-schemas.md)
* [Konfigurera ett identitetsnamnutrymme](configure-identities.md)
* [Konfigurera ett datastream](configure-datastream.md)
* [Web SDK-tillägget är installerat i taggegenskapen](install-web-sdk.md)


>[!IMPORTANT]
>
>Informationen i den här lektionen kommer från `[!UICONTROL digitalData]` datalager på Luma-webbplatsen. Om du vill visa datalagret öppnar du utvecklarkonsolen och skriver in `[!UICONTROL digitalData]` för att se hela datalagret.![digitalt datalager](assets/data-element-data-layer.png)


## Metoder för datalager

Det finns flera sätt att mappa data från datalagret till XDM med taggfunktionerna i Adobe Experience Platform. Nedan visas några fördelar och ikoner med tre olika strategier. Det är möjligt att kombinera metoder, om så önskas:

1. Implementera XDM i datalagret
1. Mappa till XDM i taggar
1. Mappa till XDM i datastream

>[!NOTE]
>
>Exemplen i den här självstudiekursen följer kartan till XDM när det gäller taggar.


### Implementera XDM i datalagret

Detta innebär att det fullständigt definierade XDM-objektet används som struktur för datalagret. Därefter mappar du hela datalagret till ett XDM-objektdataelement i -taggar. Om implementeringen inte använder en tagghanterare kan det här tillvägagångssättet vara idealiskt eftersom du kan skicka data till XDM direkt från programmet med [XDM-kommandot sendEvent](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#sending-xdm-data). Om du använder taggar kan du skapa ett anpassat kodelement som hämtar hela datalagret som ett genomströmningsJSON-objekt till XDM. Därefter mappar du genomströmnings-JSON till XDM-objektfältet i åtgärden Skicka händelse.

Nedan visas ett exempel på hur datalagret skulle se ut med formatet Adobe Client Data Layer:

+++XDM i datalagrets exempel

```JSON
window.adobeDataLayer.push({
"eventType": "web.webPageDetails.pageViews",
"web":{
         "webInteraction":{
            "linkClicks":{
               "id":"",
               "value":""
            },
            "URL":"",
            "name":"",
            "region":"",
            "type":""
         },
         "webPageDetails":{
            "pageViews":{
               "id":"",
               "value":"1"
            },
            "URL":"https://luma.enablementadobe.com/",
            "isErrorPage":"",
            "isHomePage":"",
            "name":"luma:home",
            "server":"enablementadobe.com",
            "siteSection":"home",
            "viewName":""
         },
         "webReferrer":{
            "URL":"",
            "type":""
         }
      }
});
```

+++

Proffs

* Eliminerar ytterligare steg som går vidare till datalagervariabler till XDM
* Kan vara snabbare att driftsätta om ditt utvecklingsteam äger taggning i digitalt beteende

Kon

* Fullständigt beroende av utvecklingsteamet och utvecklingscykeln för uppdatering av vilka data som skickas till XDM
* Begränsad flexibilitet eftersom XDM får exakt nyttolast från datalagret
* Det går inte att använda inbyggda taggfunktioner, till exempel skrapning, beständighet och funktioner för snabb distribution
* Det går inte att använda datalagret för pixlar från tredje part
* Ingen möjlighet att omvandla data mellan datalagret och XDM

### Mappa datalager i taggar

Detta innebär att mappa enskilda datalagervariabler ELLER datalagerobjekt till dataelement i taggar och slutligen till XDM. Detta är det traditionella sättet att implementera med hjälp av ett tagghanteringssystem.

#### Proffs

* Den mest flexibla metoden eftersom du kan styra enskilda variabler och omvandla data innan det når XDM
* Kan använda Adobe-taggar som utlöser och skrapningsfunktioner för att skicka data till XDM
* Kan mappa dataelement till pixlar från tredje part på klientsidan

#### Kon

* Det tar tid att rekonstruera datalagret som dataelement


>[!TIP]
>
> Google datalager
> 
> Om din organisation redan använder Google Analytics och har det traditionella Google dataLayer-objektet på din webbplats, kan du använda [Google Data Layer-tillägg](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/google-data-layer/overview.html?lang=en) in-taggar. På så sätt kan ni driftsätta Adobe-teknik snabbare utan att behöva be IT-avdelningen om support. Om datalagret för Google mappas till XDM följer du samma steg som ovan.

### Mappa till XDM i datastream

Den här metoden använder den inbyggda funktionaliteten i datastream-konfigurationen som kallas [Dataförberedelse för datainsamling](https://experienceleague.adobe.com/docs/experience-platform/datastreams/data-prep.html) och hoppar över mappning av datalagervariabler till XDM i taggar.

#### Proffs

* Flexibelt eftersom du kan mappa enskilda variabler till XDM
* Möjlighet att [beräkna nya värden](https://experienceleague.adobe.com/docs/experience-platform/data-prep/functions.html) eller [transformera datatyper](https://experienceleague.adobe.com/docs/experience-platform/data-prep/data-handling.html) från ett datalager innan det går till XDM
* Utnyttja [Mappningsgränssnitt](https://experienceleague.adobe.com/docs/experience-platform/datastreams/data-prep.html#create-mapping) för att mappa fält i källdata till XDM med ett användargränssnitt där du kan peka och klicka

#### Kon

* Det går inte att använda datalagervariabler som dataelement för pixlar från tredje part på klientsidan, men de kan användas med händelsevidarebefordran
* Det går inte att använda funktionen för att klippa i taggfunktionen i Adobe Experience Platform
* Underhållskomplexiteten ökar om datalagret mappas både i taggar och i datastream



>[!IMPORTANT]
>
>Som tidigare nämnts följer exemplen i den här självstudiekursen mappningen till XDM när det gäller taggar.

## Skapa dataelement för att hämta datalagret

Innan du skapar XDM-objektet skapar du följande uppsättning dataelement för [Luma demo site](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} datalager:

1. Gå till **[!UICONTROL Data Elements]** och markera **[!UICONTROL Add Data Element]** (eller **[!UICONTROL Create New Data Element]** om det inte finns några befintliga dataelement i taggegenskapen)

   ![Skapa dataelement](assets/data-element-create.png)

1. Namnge dataelementet `page.pageInfo.pageName`
1. Använd **[!UICONTROL JavaScript Variable]** **[!UICONTROL Data Element type]** för att peka på ett värde i Lumas datalager: `digitalData.page.pageInfo.pageName`

1. Markera rutorna för **[!UICONTROL Force lowercase value]** och **[!UICONTROL Clean text]** standardisera ärendet och ta bort ovidkommande utrymmen

1. Lämna `None` som **[!UICONTROL Storage Duration]** inställning eftersom det här värdet är olika på alla sidor

1. Välj **[!UICONTROL Save]**

   ![Dataelement för sidnamn](assets/data-element-pageName.png)

Skapa dessa ytterligare dataelement genom att följa samma steg:

* **`page.pageInfo.server`**  mappad till
  `digitalData.page.pageInfo.server`

* **`page.pageInfo.hierarchie1`**  mappad till
  `digitalData.page.pageInfo.hierarchie1`

* **`user.profile.attributes.username`**  mappad till
  `digitalData.user.0.profile.0.attributes.username`

* **`user.profile.attributes.loggedIn`** mappad till
  `digitalData.user.0.profile.0.attributes.loggedIn`

* **`product.productInfo.sku`** mappad till `digitalData.product.0.productInfo.sku`
<!--digitalData.product.0.productInfo.sku
    ```javascript
    var cart = digitalData.product;
    var cartItem;
    cart.forEach(function(item){
    cartItem = item.productInfo.sku;
    });
    return cartItem;
    ```
    -->
* **`product.productInfo.title`** mappad till `digitalData.product.0.productInfo.title`
* **`cart.orderId`** mappad till `digitalData.cart.orderId`
<!--
    ```javascript
    var cart = digitalData.product;
    var cartItem;
    cart.forEach(function(item){
    cartItem = item.productInfo.title;
    });
    return cartItem;
    ```
    -->
* **`product.category`** med **[!UICONTROL Custom Code]** **[!UICONTROL Data Element type]** och följande anpassade kod för att analysera webbplatsens URL för kategorin på den översta nivån:

  ```javascript
  var cat = location.pathname.split(/[/.]+/);
  if (cat[5] == 'products') {
     return (cat[6]);
  } else if (cat[5] != 'html') { 
     return (cat[5]);
  }
  ```

* **`cart.productInfo`** med följande anpassade kod:

  ```javascript
  var cart = digitalData.cart.cartEntries; 
  var cartItem = [];
  cart.forEach(function(item, index, array){
  cartItem.push({
  "SKU": item.sku
  });
  });
  return cartItem; 
  ```

* **`cart.productInfo.purchase`** med följande anpassade kod:

  ```javascript
  var cart = digitalData.cart.cartEntries; 
  var cartItem = [];
  cart.forEach(function(item, index, array){
  var qty = parseInt(item.qty);
  var price = parseInt(item.price);
  cartItem.push({
  "SKU": item.sku,
  "quantity": qty,
  "priceTotal": price
  });
  });
  return cartItem; 
  ```



>[!CAUTION]
>
>The [!UICONTROL JavaScript variable] dataelementtypen behandlar arrayreferenser som punkter i stället för hakparenteser, så att användarnamnets dataelement refereras som `digitalData.user[0].profile[0].attributes.username` **fungerar inte**.

## Skapa dataelement för variabel

mappa dataelementen till XDM med hjälp av **[!UICONTROL Variable]** dataelement som definierar det schema som används för XDM-objektet. Det här objektet bör följa XDM-schemat som du skapade under [Konfigurera ett schema](configure-schemas.md) lektion.

Så här skapar du ett variabeldataelement:

1. Välj **[!UICONTROL Add Data element]**
1. Namnge dataelementet `xdm.variable.content`. Vi rekommenderar att du prefix med &quot;xdm&quot; för dataelementen som är specifika för XDM för att bättre organisera taggegenskaperna
1. Välj **[!UICONTROL Adobe Experience Platform Web SDK]** som **[!UICONTROL Extension]**
1. Välj **[!UICONTROL Variable]** som **[!UICONTROL Data Element Type]**
1. Välj lämplig Experience Platform **[!UICONTROL Sandbox]**
1. Välj lämplig **[!UICONTROL Schema]**, i detta fall `Luma Web Event Data`
1. Välj **[!UICONTROL Save]**

   ![Variabeldataelement](assets/analytics-tags-data-element-xdm-variable.png)


I slutet av dessa steg bör du skapa följande dataelement:

| Dataelement för kärntillägg | Dataelement för plattforms-SDK-tillägg |
-----------------------------|-------------------------------
| `cart.orderId` | `xdm.variable.content` |
| `cart.productInfo` | |
| `cart.productInfo.purchase` | |
| `page.pageInfo.hierarchie1` | |
| `page.pageInfo.pageName` | |
| `page.pageInfo.server` | |
| `product.category` | |
| `product.productInfo.sku` | |
| `product.productInfo.title` | |
| `user.profile.attributes.loggedIn` | |
| `user.profile.attributes.username` | |

>[!TIP]
>
>I framtiden [Skapa taggregler](create-tag-rule.md) lektion, lär dig hur **[!UICONTROL Variable]** kan du stapla flera regler i taggar med hjälp av **[!UICONTROL Update Variable Action type]**.

Med dessa dataelement på plats är du redo att börja skicka data till Platform Edge Network med en taggregel. Men först lär du dig att samla in identiteter med Web SDK.

[Nästa: ](create-identities.md)

>[!NOTE]
>
>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Web SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela med dig av dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
