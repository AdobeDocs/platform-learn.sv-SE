---
title: Händelser
description: Lär dig hur du samlar in händelsedata i en mobilapp.
hide: true
hidefromtoc: true
source-git-commit: ca83bbb571dc10804adcac446e2dba4fda5a2f1d
workflow-type: tm+mt
source-wordcount: '1121'
ht-degree: 0%

---

# Händelser

Lär dig spåra händelser i en mobilapp.

Tillägget Edge Network tillhandahåller ett API för att skicka Experience Events till Platform Edge Network. En Experience Event är ett objekt som innehåller data som överensstämmer med XDM ExperienceEvent-schemadefinitionen. Enklare är det att de fångar upp vad andra gör i mobilappen. När data har tagits emot av Platform Edge Network kan de vidarebefordras till program och tjänster som konfigurerats i ditt datastam, som Adobe Analytics och Experience Platform. Läs mer om [Experience Events](https://developer.adobe.com/client-sdks/documentation/getting-started/track-events/) i produktdokumentationen.

## Förutsättningar

* Alla paketberoenden finns på plats i Xcode-projektet.
* Registrerade tillägg i AppDelegate.
* MobileCore har konfigurerats för att använda ditt utvecklingsprogram-ID.
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


### Standardfältgrupper

För standardfältgrupperna ser processen ut så här:

* Identifiera de händelser som du försöker samla in i ditt schema. I det här exemplet spårar du händelser för e-handelsupplevelser, till exempel en produktvy (**[!UICONTROL productViews]**).

  ![produktvyschema](assets/datacollection-prodView-schema.png)

* Om du vill konstruera ett objekt som innehåller händelsedata för upplevelsen i din app använder du kod som:

  ```swift {highlight="2-8"}
  var xdmData: [String: Any] = [
      "eventType": "commerce.productViews",
      "commerce": [
          "productViews": [
            "id": sku,
            "value": 1
          ]
      ]
  ]
  ```

   * `eventType`: Beskriver händelsen som inträffade, använd en [känt värde](https://github.com/adobe/xdm/blob/master/docs/reference/classes/experienceevent.schema.md#xdmeventtype-known-values) om möjligt.
   * `commerce.productViews.id`: ett strängvärde som representerar SKU:n för produkten
   * `commerce.productViews.value`: Ange händelsens numeriska värde. Om det är ett booleskt värde (eller &quot;Räknare&quot; i Adobe Analytics) är värdet alltid 1. Om det är en numerisk händelse eller valutakändelse kan värdet vara > 1.

* Identifiera eventuella ytterligare data som är associerade med händelsen för e-handelsproduktvyn i ditt schema. I det här exemplet inkluderar du `productListItems` som är en standarduppsättning med fält som används för e-handelsrelaterade händelser:

  ![schema för produktlisteobjekt](assets/datacollection-prodListItems-schema.png)
   * Observera att `productListItems` är en matris så att flera produkter kan anges.

* Om du vill lägga till dessa data expanderar du `xdmData` objekt som ska innehålla tilläggsdata:

```swift {highlight="9-16"}
var xdmData: [String: Any] = [
    "eventType": "commerce.productViews",
        "commerce": [
        "productViews": [
            "id": sku,
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

* Sedan använder du datastrukturen för att skapa en `ExperienceEvent`:

  ```swift
  let productViewEvent = ExperienceEvent(xdm: xdmData)
  ```

* Och skicka händelsen och data till Platform Edge Network med API:t sendEvent:

  ```swift
  Edge.sendEvent(experienceEvent: productViewEvent)
  ```

Nu ska vi implementera koden i Xcode-projektet.
Du har olika affärsproduktrelaterade åtgärder (visa, lägg till i kundvagn, spara för senare, köp) i din app och du vill skicka händelser baserat på de här åtgärderna som utförts av användaren.

1. Om du vill strukturera skickade upplevelsehändelser går du till `MobileSDK`och lägg till följande i `sendCommerceExperienceEvent` funktion. Den här funktionen tar händelsen och produkten för e-handelsupplevelsen som parametrar:

   ```swift {highlight="2-22"}
   func sendCommerceExperienceEvent(commerceEventType: String, product: Product) {
     let xdmData: [String: Any] = [
         "eventType": "commerce." + commerceEventType,
         "commerce": [
             commerceEventType: [
                 "id": product.sku,
                 "value": 1
             ]
         ],
         "productListItems": [
             [
                 "name": product.name,
                 "priceTotal": product.price,
                 "SKU": product.sku
             ]
         ]
     ]
   
     Logger.viewCycle.info("About to send commerce experience event of type  \(commerceEventType)..."
     let commerceExperienceEvent = ExperienceEvent(xdm: xdmData)
     Edge.sendEvent(experienceEvent: commerceExperienceEvent)
   }
   ```

1. I `ProductView` lägga till olika anrop till `sendCommerceExperienceEvent` funktion:

   1. På `.task` modifierare i `ATTrackingManager.trackingAuthorizationStatus` stängning. The `.task` modifieraren anropas när produktvyn initieras och visas, så du vill skicka en produktvyhändelse vid det tillfället.

      ```swift {highlight="4-5"}
      .task {
          if ATTrackingManager.trackingAuthorizationStatus == .authorized {
               // Send commerce experience event
              MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "productView", product: product)
          }
      }
      ```

   1. För var och en av knapparna (Sparad för senare, Lägg till i kundvagn och Köp) i verktygsfältet, som finns i produktvyn, lägger du till det relevanta samtalet.

      * För Spara för senare/Lägg till i önskelista:

        ```swift {highlight="5-6"}
        Button {
            Task {
                if ATTrackingManager.trackingAuthorizationStatus == .authorized {
                // Send saveForLater commerce experience event
                    MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "saveForLaters", product: product)
                }
            }
            showSaveForLaterDialog.toggle()
        } label: {
            Label("", systemImage: "heart")
        }
        .alert(isPresented: $showSaveForLaterDialog, content: {
            Alert(title: Text( "Saved for later"), message: Text("The selected item is saved to your wishlist…"))
        })
        ```

      * För Lägg till i kundvagnen:

        ```swift {highlight="5-6"}
        Button {
            Task {
                if ATTrackingManager.trackingAuthorizationStatus == .authorized {
                    // Send productListAdds commerce experience event
                    MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "productListAdds", product: product)
                }
            }
            showAddToCartDialog.toggle()
        } label: {
                Label("", systemImage: "cart.badge.plus")
        }
        alert(isPresented: $showAddToCartDialog, content: {
            Alert(title: Text( "Added to basket"), message: Text("The selected item is added to your basket…"))
        })
        ```

      * Köp:

        ```swift {highlight="5-6"}
        Button {
            Task {
                if ATTrackingManager.trackingAuthorizationStatus == .authorized {
                    // Send purchase commerce experience event
                    MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "purchases", product: product)
                }
            }
            showPurchaseDialog.toggle()
        } label: {
            Label("", systemImage: "creditcard")
        }
        .alert(isPresented: $showPurchaseDialog, content: {
            Alert(title: Text( "Purchases"), message: Text("The selected item is purchased…"))
        })
        ```

### Anpassade fältgrupper

Tänk dig att du vill spåra skärmvisningar och interaktioner i själva appen. Kom ihåg att du har definierat en anpassad fältgrupp för den här typen av händelser.

* Identifiera de händelser du försöker samla in i ditt schema.
  ![appinteraktionsschema](assets/datacollection-appInteraction-schema.png)

* Börja konstruera objektet.

  >[!NOTE]
  >
  >  Standardfältgrupper börjar alltid i objektroten.
  >
  >  Anpassade fältgrupper börjar alltid under ett objekt som är unikt för din Experience Cloud-organisation, `_techmarketingdemos` i detta exempel.

  För programinteraktionshändelsen skapar du ett objekt som:

  ```swift
  let xdmData: [String: Any] = [
    "eventType": "application.interaction",
    "_techmarketingdemos": [
      "appInformation": [
          "appInteraction": [
              "name": "login",
              "appAction": [
                  "value": 1
                  ]
              ]
          ]
      ]
  ]
  ```

  För händelsen skärmspårning skapar du ett objekt som:

  ```swift
  var xdmData: [String: Any] = [
    "eventType": "application.scene",
    "_techmarketingdemos": [
        "appInformation": [
            "appStateDetails": [
                "screenType": "App",
                    "screenName": "luma: content: ios: us: en: login",
                    "screenView": [
                        "value": 1
                    ]
                ]
            ] 
        ]
  ]
  ```


* Sedan skapar datastrukturen en `ExperienceEvent`.

  ```swift
  let event = ExperienceEvent(xdm: xdmData)
  ```

* Skicka händelsen och data till Platform Edge Network.

  ```swift
  Edge.sendEvent(experienceEvent: event)
  ```


Här kan du implementera koden i Xcode-projektet.

1. För enkelhetens skull definierar du två funktioner i `MobileSDK`.

   Ett för appinteraktioner. Lägg till den markerade koden i `sendAppInteractionEvent(actionName)` function in **[!UICONTROL MobileSDK]**:

   ```swift {highlight="2-16"}
   func sendAppInteractionEvent(actionName: String) {
        let xdmData: [String: Any] = [
           "eventType": "application.interaction",
           tenant : [
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
       let appInteractionEvent = ExperienceEvent(xdm: xdmData)
       Edge.sendEvent(experienceEvent: appInteractionEvent)
   }
   ```

   Och en för skärmspårning. Lägg till den markerade koden i `sendTrackScreenEvent(stateName)` function in **[!UICONTROL MobileSDK]**:

   ```swift {highlight="2-17"}
   func sendTrackScreenEvent(stateName: String) {
      let xdmData: [String: Any] = [
          "eventType": "application.scene",
          tenant : [
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
      ]
      let trackScreenEvent = ExperienceEvent(xdm: xdmData)
      Edge.sendEvent(experienceEvent: trackScreenEvent)
   }
   ```

1. Navigera till **[!UICONTROL LoginSheet]**.

   * Lägg till följande markerade kod i avslutningsknappen Inloggning:

     ```swift {highlight="3"}
     Button("Login") {                               
        // Send app interaction event
        MobileSDK.shared.sendAppInteractionEvent(actionName: "login")
        dismiss()
     }
     .disabled(currentEmailId.isValidEmail == false)
     .buttonStyle(.bordered)
     ```

   * Lägg till följande markerade kod i `onAppear` modifierare:

     ```swift {highlight="13"}
     .onAppear {
        Task {
            if currentEmailId == "testUser@gmail.com" || currentEmailId.isValidEmail == false {
                // still allow to log in
                disableLogin = false
            }
            else {
                disableLogin = true
            }
        }
        // Send track screen event
        MobileSDK.shared.sendTrackScreenEvent(stateName: "luma: content: ios: us: en: login")
     }
     ```

### Validering

1. Granska [installationsanvisningar](assurance.md) och koppla simulatorn eller enheten till Assurance.
1. Kör appen för att logga in och interagera med en produkt.

   1. Flytta Assurance-ikonen åt vänster.
   1. Välj **[!UICONTROL Startsida]** i tabbfältet.
   1. Välj **[!UICONTROL Inloggning]** för att öppna inloggningsbladet.
   1. Välj **[!UICONTROL A|]** om du vill infoga ett slumpmässigt e-postmeddelande och ett kund-ID.
   1. Välj **[!UICONTROL Inloggning]**.
   1. Välj **[!UICONTROL Produkter]** i tabbfältet.
   1. Välj en produkt.
   1. Välj **[!UICONTROL Spara senare]**.
   1. Välj **[!UICONTROL Lägg i kundvagnen]**.
   1. Välj **[!UICONTROL Inköp]**.

      <img src="./assets/mobile-app-events-1.png" width="200"> <img src="./assets/mobile-app-events-2.png" width="200"> <img src="./assets/mobile-app-events-3.png" width="200">


1. Leta efter **[!UICONTROL hitReceived]** händelser från **[!UICONTROL com.adobe.edge.konductor]** leverantör.
1. Markera händelsen och granska XDM-data i **[!UICONTROL meddelanden]** -objekt.
   ![validering av datainsamling](assets/datacollection-validation.png)


### Implementera i Luma-appen

Nu bör du ha alla verktyg du behöver för att börja lägga till datainsamling i Luma-appen. Du kan lägga till mer information om hur användaren interagerar med dina produkter och du kan lägga till fler appinteraktioner och uppringningsanrop till din app:

* Implementera beställning, utcheckning, tom varukorg och andra funktioner i appen och lägg till relevanta händelser om handelsupplevelser i den här funktionen.
* Upprepa samtalet till `sendAppInteractionEvent` med rätt parameter för att spåra andra appinteraktioner i appen av användaren.
* Upprepa samtalet till `sendTrackScreenEvent` med rätt parameter för att spåra varje skärm som visas av användaren i appen.

>[!TIP]
>
>Granska [fullständigt implementerad app](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) för fler exempel.


## Skicka händelser till Analytics och Platform

Nu när du har samlat in händelserna och skickat dem till Platform Edge Network skickas de till de program och tjänster som är konfigurerade i din [datastream](create-datastream.md). I senare lektioner mappar du dessa data till [Adobe Analytics](analytics.md) och [Adobe Experience Platform](platform.md).

>[!SUCCESS]
>
>Du har nu konfigurerat din app för att spåra e-handel, appinteraktion och händelser för skärmspårning till Adobe Experience Platform Edge Network och alla tjänster som du har definierat i din datastam.<br/>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Mobile SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Nästa: **[WebViews](web-views.md)**
