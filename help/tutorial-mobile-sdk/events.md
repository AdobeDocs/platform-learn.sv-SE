---
title: Händelser
description: Lär dig hur du samlar in händelsedata i en mobilapp.
exl-id: 4779cf80-c143-437b-8819-1ebc11a26852
source-git-commit: b2e1bf08d9fb145ba63263dfa078c96258342708
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 0%

---

# Händelser

Lär dig spåra händelser i en mobilapp.

Tillägget Edge Network tillhandahåller ett API för att skicka Experience Events till Platform Edge Network. En Experience Event är ett objekt som innehåller data som överensstämmer med XDM ExperienceEvent-schemadefinitionen. Enklare är det att de fångar upp vad andra gör i mobilappen. När data har tagits emot av Platform Edge Network kan de vidarebefordras till program och tjänster som konfigurerats i ditt datastam, som Adobe Analytics och Experience Platform. Läs mer om [Experience Events](https://developer.adobe.com/client-sdks/documentation/getting-started/track-events/) i produktdokumentationen.

## Förutsättningar

* Uppdaterad PodFile med nödvändiga SDK:er.
* Registrerade tillägg i AppDelegate.
* MobileCore har konfigurerats för att använda ditt utvecklar-AppId.
* Importerade SDK:er.
* Programmet har skapats och körts med ändringarna ovan.

## Utbildningsmål

I den här lektionen kommer du att:

* Lär dig strukturera XDM-data baserat på ett schema.
* Skicka en XDM-händelse baserad på en standardfältgrupp.
* Skicka en XDM-händelse baserad på en anpassad fältgrupp.
* Skicka en XDM-köphändelse.
* Validera med Assurance.

## Skapa en upplevelsehändelse

Tillägget Adobe Experience Platform Edge kan skicka händelser som följer ett tidigare definierat XDM-schema till Adobe Experience Platform Edge Network.

Processen går så här..

1. Identifiera den mobilappsinteraktion du försöker spåra.

1. Granska ditt schema och identifiera rätt händelse.

1. Granska ditt schema och identifiera eventuella ytterligare fält som ska användas för att beskriva händelsen.

1. Skapa och fyll i dataobjektet.

1. Skapa och skicka-händelse.

1. Validera.

Låt oss titta på några exempel.

### Exempel 1 - standardfältgrupper

Granska följande exempel utan att försöka implementera det i exempelprogrammet:

1. Identifiera i ditt schema vilken händelse du försöker samla in, i det här exemplet spårar vi en produktvy.
   ![produktvyschema](assets/mobile-datacollection-prodView-schema.png)

1. Börja skapa objektet:

   ```swift
   var xdmData: [String: Any] = [
       "eventType": "commerce.productViews",
       "commerce": [
           "productViews": [
           "value": 1
           ]
       ]
   ]
   ```

   * eventType: Beskriver händelsen som inträffade, använd en [känt värde](https://github.com/adobe/xdm/blob/master/docs/reference/classes/experienceevent.schema.md#xdmeventtype-known-values) när det är möjligt.
   * commerce.productViews.value: Ange händelsens numeriska värde. Om det är ett booleskt värde (eller &quot;Räknare&quot; i Adobe Analytics) är värdet alltid 1. Om det är en numerisk händelse eller valutakändelse kan värdet vara > 1.

1. Identifiera eventuella ytterligare data som är associerade med händelsen i ditt schema. I det här exemplet inkluderar du `productListItems` som är en standarduppsättning med fält som används för e-handelsrelaterade händelser:
   ![schema för produktlisteobjekt](assets/mobile-datacollection-prodListItems-schema.png)
   * Observera att `productListItems` är en matris så att flera produkter kan anges.

1. Expandera xdmData-objektet så att det innehåller ytterligare data:

   ```swift
   var xdmData: [String: Any] = [
       "eventType": "commerce.productViews",
           "commerce": [
           "productViews": [
               "value": 1
           ]
       ],
       "productListItems": [
           [
               "name":  productName,
               "SKU": sku,
               "priceTotal": priceString,
               "quantity": 1
           ]
       ]
   ]
   ```

1. Använd datastrukturen för att skapa en `ExperienceEvent`:

   ```swift
   let productViewEvent = ExperienceEvent(xdm: xdmData)
   ```

1. Skicka händelsen och data till Platform Edge Network:

   ```swift
   Edge.sendEvent(experienceEvent: productViewEvent)
   ```

### Exempel 2 - anpassade fältgrupper

Granska följande exempel utan att försöka implementera det i exempelprogrammet:

1. Identifiera i schemat händelsen som du försöker samla in. I det här exemplet spårar du en&quot;appinteraktion&quot; som består av en programåtgärdshändelse och ett namn.
   ![appinteraktionsschema](assets/mobile-datacollection-appInteraction-schema.png)

1. Börja konstruera objektet.

   >[!NOTE]
   >
   >  Standardfältgrupper börjar alltid i objektroten.
   >
   >  Anpassade fältgrupper börjar alltid under ett objekt som är unikt för din Experience Cloud-organisation, &quot;_techmarketingdemos&quot; i det här exemplet.

   ```swift
   var xdmData: [String: Any] = [
   "_techmarketingdemos": [
       "appInformation": [
           "appInteraction": [
               "name": actionName,
               "appAction": [
                   "value": 1
                   ]
               ]
           ]
       ]
   ]
   ```

   Eller...

   ```swift
   var xdmData: [String: Any] = [:]
   xdmData["_techmarketingdemos"] = [
       "appInformation": [
           "appInteraction": [
               "name": actionName,
               "appAction": [
                   "value": 1
               ]
           ]
       ]
   ]
   ```

1. Använd datastrukturen för att skapa en `ExperienceEvent`.

   ```swift
   let appInteractionEvent = ExperienceEvent(xdm: xdmData)
   ```

1. Skicka händelsen och data till Platform Edge Network.

   ```swift
   Edge.sendEvent(experienceEvent: appInteractionEvent)
   ```

### Lägga till skärmvyspårning i Luma-app

I exemplen ovan har man förhoppningsvis förklarat tankeprocessen när ett XDM-dataobjekt skapas. Nu ska vi lägga till skärmvyspårning i Luma-appen.

1. Navigera till `Home.swift`.
1. Lägg till följande kod i `viewDidAppear(...)`.

   ```swift
           let stateName = "luma: content: ios: us: en: home"
           var xdmData: [String: Any] = [:]
           //Page View
           xdmData["_techmarketingdemos"] = [
               "appInformation": [
                   "appStateDetails": [
                       "screenType": "App",
                       "screenName": stateName,
                       "screenView": [
                           "value": 1
                       ]
                   ]
               ]
           ]
           let experienceEvent = ExperienceEvent(xdm: xdmData)
           Edge.sendEvent(experienceEvent: experienceEvent)
   ```

1. Upprepa för varje skärm i appen och uppdatera `stateName` allt eftersom.



### Validering

1. Granska [installationsanvisningar](assurance.md) och koppla simulatorn eller enheten till Assurance.
1. Utför åtgärden och sök efter `hitReceived` från `com.adobe.edge.konductor` leverantör.
1. Markera händelsen och granska XDM-data i `messages` -objekt.
   ![validering av datainsamling](assets/mobile-datacollection-validation.png)

### Exempel 3 - köp

I det här exemplet antar vi att användaren har gjort följande köp:

* Produkt 1 - Yoga Mat.
   * 49,99 x1 USD
   * SKU: 5829
* Produkt 2 - vattenflaska.
   * $10.00 x3
   * SKU: 9841
* Ordersumma: 79,99 USD
* Unikt order-ID: 298234720
* Betalningstyp: Visa kreditkort
* Unikt transaktions-ID för betalning: 847361

#### Schema

Här är de relaterade schemafälten som ska användas:

* eventType: &quot;commerce.purchasing&quot;
* commerce.purchases
* commerce.order
* productsListItems
* _techmarketingdemos.appStateDetails (anpassad)

>[!TIP]
>
>Anpassade fältgrupper placeras alltid under din Experience Cloud-organisationsidentifierare.
>
>&quot;_techmarketingdemos&quot; ersätts med din organisations unika värde.

![inköpsschema](assets/mobile-datacollection-purchase-schema.png)


#### Code

Så här skapar och skickar du XDM-objektet i programmet.

```swift
let stateName = "luma: content: ios: us: en: orderconfirmation"
let currencyCode = "USD"
let orderTotal = "79.99"
let paymentType = "Visa Credit Card"
let orderId = "298234720"
let paymentTransactionId = "847361"
var xdmData: [String: Any] = [
  "eventType": "commerce.purchases",
  "commerce": [
    "purchases": [
      "value": 1
    ],
    "order": [
      "currencyCode": currencyCode,
      "priceTotal": orderTotal,
      "purchaseID": orderId,
      "purchaseOrderNumber": orderId,
      "payments": [ //Assuming only 1 payment type is used
        [
          "currencyCode": currencyCode,
          "paymentAmount": orderTotal,
          "paymentType": paymentType,
          "transactionID": paymentTransactionId
        ]
      ]
    ]
  ],
  "productListItems": [
      [
          "name":  "Yoga Mat",
          "SKU": "5829",
          "priceTotal": "49.99",
          "quantity": 1
      ],
      [
        "name":  "Water Bottle",
        "SKU": "9841",
        "priceTotal": "30.00",
        "quantity": 3
      ]
  ]
]

//Custom field group
xdmData["_techmarketingdemos"] = [
  "appInformation": [
    "appStateDetails": [
      "screenType": "App",
      "screenName": stateName,
      "screenView": [
        "value": 1
      ]
    ]
  ]
]
let experienceEvent = ExperienceEvent(xdm: xdmData)
Edge.sendEvent(experienceEvent: experienceEvent)
```

>[!NOTE]
>
>För tydlighetens skull bör alla värden vara hårdkodade. I en verklighetstrogen situation skulle värdena fyllas dynamiskt.


### Implementera i Luma-appen

Du bör ha alla verktyg du behöver för att börja lägga till datainsamling i Luma-exempelappen. Nedan finns en lista med hypotetiska spårningskrav som du kan följa.

* Spåra varje skärmvy.
   * Schemafält: screenType, screenName, screenView
* Spåra icke-handelsaktiviteter.
   * Schemafält: appInteraction.name, appAction
* Handelsåtgärder:
   * Produktsida: productViews
   * Lägg i kundvagnen: productListAdds
   * Ta bort från kundvagnen: productListRemovals
   * Starta utcheckning: utcheckningar
   * Visa kundvagn: productListViews
   * Lägg till i önskelista: saveForLaters
   * Köp: inköp, beställning

>[!TIP]
>
>Granska [fullständigt implementerad app](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) för fler exempel.

### Validering

1. Granska [installationsanvisningar](assurance.md) och koppla simulatorn eller enheten till Assurance.

1. Utför åtgärden och sök efter `hitReceived` från `com.adobe.edge.konductor` leverantör.

1. Markera händelsen och granska XDM-data i `messages` -objekt.
   ![validering av datainsamling](assets/mobile-datacollection-validation.png)

## Skicka händelser till Analytics och Platform

Nu när du har samlat in händelserna och skickat dem till Platform Edge Network, skickas de till de program och tjänster som konfigurerats i din [datastream](create-datastream.md). I senare lektioner kan du mappa dessa data till [Adobe Analytics](analytics.md) och [Adobe Experience Platform](platform.md).

Nästa: **[WebViews](web-views.md)**

>[!NOTE]
>
>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Mobile SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela med dig av dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)