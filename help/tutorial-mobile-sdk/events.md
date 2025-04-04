---
title: Spåra händelsedata i mobilappar med Platform Mobile SDK
description: Lär dig spåra händelsedata i en mobilapp.
jira: KT-14631
exl-id: 4779cf80-c143-437b-8819-1ebc11a26852
source-git-commit: afb15c561179386e7846e8cd8963f67820af09f1
workflow-type: tm+mt
source-wordcount: '1308'
ht-degree: 0%

---

# Spåra händelsedata

Lär dig spåra händelser i en mobilapp.

Tillägget Edge Network tillhandahåller ett API för att skicka Experience Events till Platform Edge Network. En Experience Event är ett objekt som innehåller data som överensstämmer med XDM ExperienceEvent-schemadefinitionen. Enklare är det att de fångar upp vad andra gör i mobilappen. När data har tagits emot av Platform Edge Network kan de vidarebefordras till program och tjänster som konfigurerats i ditt datastam, som Adobe Analytics och Experience Platform. Läs mer om [Experience Events](https://developer.adobe.com/client-sdks/documentation/getting-started/track-events/) i produktdokumentationen.

## Förhandskrav

* Alla paketberoenden finns på plats i Xcode-projektet.
* Registrerade tillägg i **[!UICONTROL AppDelegate]**.
* MobileCore-tillägget har konfigurerats för att använda din utveckling `appId`.
* Importerade SDK:er.
* Programmet har skapats och körts med ändringarna ovan.

## Utbildningsmål

I den här lektionen ska du

* Lär dig strukturera XDM-data baserat på ett schema.
* Skicka en XDM-händelse baserad på en standardfältgrupp.
* Skicka en XDM-händelse baserad på en anpassad fältgrupp.
* Skicka en XDM-köphändelse.
* Validera med Assurance.

## Skapa en upplevelsehändelse

Adobe Experience Platform Edge-tillägget kan skicka händelser som följer ett tidigare definierat XDM-schema till Adobe Experience Platform Edge Network.

Processen går så här..

1. Identifiera den mobilappsinteraktion du försöker spåra.

1. Granska ditt schema och identifiera rätt händelse.

1. Granska ditt schema och identifiera eventuella ytterligare fält som ska användas för att beskriva händelsen.

1. Skapa och fyll i dataobjektet.

1. Skapa och skicka-händelse.

1. Validera.


### Standardfältgrupper

För standardfältgrupperna ser processen ut så här:

* Identifiera de händelser som du försöker samla in i ditt schema. I det här exemplet spårar du händelser för e-handelsupplevelser, till exempel en produktvyhändelse (**[!UICONTROL productViews]**).

  ![produktvyschema](assets/datacollection-prodView-schema.png)

* Om du vill konstruera ett objekt som innehåller händelsedata för upplevelsen i din app använder du kod som:

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

   * `eventType`: Beskriver händelsen som inträffade, använd ett [känt värde](https://github.com/adobe/xdm/blob/master/docs/reference/classes/experienceevent.schema.md#xdmeventtype-known-values) när det är möjligt.
   * `commerce.productViews.value`: händelsens numeriska eller booleska värde. Om det är ett booleskt värde (eller &quot;Räknare&quot; i Adobe Analytics) är värdet alltid 1. Om det är en numerisk händelse eller valutakändelse kan värdet vara > 1.

* Identifiera eventuella ytterligare data som är associerade med händelsen för e-handelsproduktvyn i ditt schema. I det här exemplet inkluderar du **[!UICONTROL productListItems]**, som är en standarduppsättning med fält som används med alla e-handelsrelaterade händelser:

  ![objektschema för produktlista](assets/datacollection-prodListItems-schema.png)
   * Observera att **[!UICONTROL productListItems]** är en matris så att flera produkter kan anges.

* Om du vill lägga till dessa data expanderar du objektet `xdmData` så att det innehåller ytterligare data:

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

* Du kan nu använda den här datastrukturen för att skapa en `ExperienceEvent`:

  ```swift
  let productViewEvent = ExperienceEvent(xdm: xdmData)
  ```

* Och skicka händelsen och data till Platform Edge Network med API:t `sendEvent`:

  ```swift
  Edge.sendEvent(experienceEvent: productViewEvent)
  ```

API:t [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent) är det AEP Mobile SDK som motsvarar API-anropen [`MobileCore.trackAction`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#trackaction) och [`MobileCore.trackState`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#trackstate). Mer information finns i [Migrera från mobiltillägget Analytics till Adobe Experience Platform Edge Network](https://developer.adobe.com/client-sdks/documentation/adobe-analytics/migrate-to-edge-network/).

Du kommer nu att implementera den här koden i ditt Xcode-projekt.
Du har olika affärsproduktrelaterade åtgärder i din app och du vill skicka händelser baserat på de åtgärder som användaren har utfört:

* vy: inträffar när en användare tittar på en viss produkt,
* lägg till i kundvagn: när en användare trycker <img src="assets/addtocart.png" width="20"/> i en produktinformationsskärm,
* spara för senare: när en användare trycker <img src="assets/saveforlater.png" width="15"/> i en produktinformationsskärm,
* köp: när en användare trycker <img src="assets/purchase.png" width="20"/> i en produktinformationsskärm.

Om du vill implementera sändning av e-handelsrelaterade upplevelsehändelser på ett återanvändbart sätt använder du en dedikerad funktion:

1. Navigera till **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** i Xcode Project navigator och lägg till följande i funktionen `func sendCommerceExperienceEvent(commerceEventType: String, product: Product)`.

   ```swift
   // Set up a data dictionary, create an experience event and send the event.
   let xdmData: [String: Any] = [
       "eventType": "commerce." + commerceEventType,
       "commerce": [
           commerceEventType: [
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
   
   let commerceExperienceEvent = ExperienceEvent(xdm: xdmData)
   Edge.sendEvent(experienceEvent: commerceExperienceEvent)
   ```

   Den här funktionen tar händelsetypen och produkten för upplevelseupplevelsen som parametrar och

   * ställer in XDM-nyttolasten som en ordlista med hjälp av funktionens parametrar,
   * ställer in en upplevelsehändelse med hjälp av ordlistan,
   * skickar upplevelsehändelsen med API:t [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent).

1. Navigera till **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL Products]** > **[!UICONTROL ProductView]** i Xcode Project navigator och lägg till olika anrop till funktionen `sendCommerceExperienceEvent`:

   1. Vid modifieraren `.task`, inom stängningen av `ATTrackingManager.trackingAuthorizationStatus`. Den här `.task`-modifieraren anropas när produktvyn initieras och visas, så du vill skicka en produktvyhändelse vid det tillfället.

      ```swift
      // Send productViews commerce experience event
      MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "productViews", product: product)
      ```

   1. För varje knapp (<img src="assets/saveforlater.png" width="15"/>, <img src="assets/addtocart.png" width="20"/> och <img src="assets/purchase.png" width="20"/>) i verktygsfältet lägger du till det relevanta samtalet i `ATTrackingManager.trackingAuthorizationStatus == .authorized`-stängningen:

      1. För <img src="assets/saveforlater.png" width="15"/>:

         ```swift
         // Send saveForLater commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "saveForLaters", product: product)
         ```

      1. För <img src="assets/addtocart.png" width="20"/>:

         ```swift
         // Send productListAdds commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "productListAdds", product: product)
         ```

      1. För <img src="assets/purchase.png" width="20"/>:

         ```swift
         // Send purchase commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "purchases", product: product)
         ```

>[!TIP]
>
>Om du utvecklar för Android™ använder du karta (`java.util.Map`) som grundgränssnitt för att skapa din XDM-nyttolast.


### Anpassade fältgrupper

Tänk dig att du vill spåra skärmvisningar och interaktioner i själva appen. Kom ihåg att du har definierat en anpassad fältgrupp för den här typen av händelser.

* Identifiera de händelser du försöker samla in i ditt schema.
  ![appinteraktionsschema](assets/datacollection-appInteraction-schema.png)

* Börja konstruera objektet.

  >[!NOTE]
  >
  >* Standardfältgrupper börjar alltid i objektroten.
  >
  >* Anpassade fältgrupper börjar alltid under ett objekt som är unikt för din Experience Cloud-organisation, `_techmarketingdemos` i det här exemplet.

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


* Du kan nu använda den här datastrukturen för att skapa en `ExperienceEvent`.

  ```swift
  let event = ExperienceEvent(xdm: xdmData)
  ```

* Skicka händelsen och data till Platform Edge Network.

  ```swift
  Edge.sendEvent(experienceEvent: event)
  ```


Här kan du implementera koden i Xcode-projektet.

1. För enkelhetens skull definierar du två funktioner i **[!UICONTROL MobileSDK]**. Navigera till **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** i Xcode Project-navigatorn.

   1. Ett för appinteraktioner. Lägg till den här koden i funktionen `func sendAppInteractionEvent(actionName: String)`:

      ```swift
      // Set up a data dictionary, create an experience event and send the event.
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
      ```

      Den här funktionen använder åtgärdsnamnet som en parameter och

      * ställer in XDM-nyttolasten som en ordlista med hjälp av parametern från funktionen,
      * ställer in en upplevelsehändelse med hjälp av ordlistan,
      * skickar upplevelsehändelsen med API:t [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent).


   1. Och en för skärmspårning. Lägg till den här koden i funktionen `func sendTrackScreenEvent(stateName: String) `:

      ```swift
      // Set up a data dictionary, create an experience event and send the event.
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
      ```

      Den här funktionen använder lägesnamnet som en parameter och

      * ställer in XDM-nyttolasten som en ordlista med hjälp av parametern från funktionen,
      * ställer in en upplevelsehändelse med hjälp av ordlistan,
      * skickar upplevelsehändelsen med API:t [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent).

1. Navigera till **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL LoginSheet]**.

   1. Lägg till följande markerade kod i avslutningsknappen Inloggning:

      ```swift
      // Send app interaction event
      MobileSDK.shared.sendAppInteractionEvent(actionName: "login")
      ```

   1. Lägg till följande markerade kod i modifieraren `onAppear`:

      ```swift
      // Send track screen event
      MobileSDK.shared.sendTrackScreenEvent(stateName: "luma: content: ios: us: en: login")
      ```

## Validering

1. Granska avsnittet [installationsanvisningar](assurance.md#connecting-to-a-session) för att ansluta simulatorn eller enheten till Assurance.

   1. Flytta ikonen Assurance åt vänster.
   1. Välj **[!UICONTROL Home]** i flikfältet och kontrollera att du ser en **[!UICONTROL ECID]**, **[!UICONTROL Email]** och **[!UICONTROL CRM ID]** på hemskärmen.
   1. Välj **[!DNL Products]** i flikfältet.
   1. Välj en produkt.
   1. Välj <img src="assets/saveforlater.png" width="15"/>.
   1. Välj <img src="assets/addtocart.png" width="20"/>.
   1. Välj <img src="assets/purchase.png" width="15"/>.

      <img src="./assets/mobile-app-events-3.png" width="300">


1. I Assurance UI söker du efter **[!UICONTROL hitReceived]**-händelserna från **[!UICONTROL com.adobe.edge.konductor]**-leverantören.
1. Markera händelsen och granska XDM-data i objektet **[!UICONTROL messages]**. Du kan också använda ![Kopiera](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) **[!UICONTROL Copy Raw Event]** och en text- eller kodredigerare som du föredrar för att klistra in och inspektera händelsen.

   ![datainsamlingsvalidering](assets/datacollection-validation.png)


## Nästa steg

Nu bör du ha alla verktyg du behöver för att börja lägga till datainsamling i appen. Du kan lägga till mer information om hur användaren interagerar med dina produkter i appen och du kan lägga till fler appinteraktioner och skärmsspårningsanrop till appen:

* Implementera beställning, utcheckning, tom varukorg och andra funktioner i appen och lägg till relevanta händelser för e-handelsupplevelser i den här funktionen.
* Upprepa anropet till `sendAppInteractionEvent` med rätt parameter för att spåra andra appinteraktioner av användaren.
* Upprepa anropet till `sendTrackScreenEvent` med rätt parameter för att spåra skärmar som visas av användaren i appen.

>[!TIP]
>
>Granska den [färdiga appen](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) för fler exempel.


## Skicka händelser till Analytics och Platform

Nu när du har samlat in händelserna och skickat dem till Platform Edge Network skickas de till de program och tjänster som konfigurerats i [datastream](create-datastream.md). I senare lektioner mappar du dessa data till [Adobe Analytics](analytics.md), [Adobe Experience Platform](platform.md) och andra Adobe Experience Cloud-lösningar som [Adobe Target](target.md) och Adobe Journey Optimizer.

>[!SUCCESS]
>
>Du har nu konfigurerat din app för att spåra händelser i samband med handel, appinteraktion och skärmspårning till Adobe Experience Platform Edge Network och alla tjänster som du har definierat i din datastam.
>
>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Mobile SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela dem i det här [Experience League-diskussionsinlägget](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Nästa: **[Hantera WebViews](web-views.md)**
