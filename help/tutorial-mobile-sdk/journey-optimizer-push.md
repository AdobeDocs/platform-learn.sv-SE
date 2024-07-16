---
title: Skapa och skicka push-meddelanden med Platform Mobile SDK
description: Lär dig skapa push-meddelanden till en mobilapp med Platform Mobile SDK och Adobe Journey Optimizer.
solution: Data Collection,Journey Optimizer
feature-set: Journey Optimizer
feature: Push
jira: KT-14638
exl-id: e8e920d5-fd36-48b7-9185-a34231c0d336
source-git-commit: e316f881372a387b82f8af27f7f0ea032a99be99
workflow-type: tm+mt
source-wordcount: '2323'
ht-degree: 0%

---

# Skapa och skicka push-meddelanden

Lär dig skapa push-meddelanden för mobilappar med Experience Platform Mobile SDK och Journey Optimizer.

Med Journey Optimizer kan ni skapa resor och skicka meddelanden till utvalda målgrupper. Innan du skickar push-meddelanden med Journey Optimizer måste du se till att rätt konfigurationer och integreringar finns på plats. Mer information om dataflödet för push-meddelanden i Journey Optimizer finns i [dokumentationen](https://experienceleague.adobe.com/docs/journey-optimizer/using/push/push-config/push-gs.html).

![Arkitektur](assets/architecture-ajo.png)

>[!NOTE]
>
>Den här lektionen är valfri och gäller endast för Journey Optimizer-användare som vill skicka push-meddelanden.


## Förhandskrav

* Programmet har skapats och körts med SDK:er installerade och konfigurerade.
* Konfigurera appen för Adobe Experience Platform.
* Åtkomst till Journey Optimizer och tillräcklig behörighet enligt beskrivningen [här](https://experienceleague.adobe.com/docs/journey-optimizer/using/push/push-config/push-configuration.html?lang=en). Du behöver även tillräcklig behörighet för följande Journey Optimizer-funktioner.
   * Skapa en appyta.
   * Skapa en resa.
   * Skapa ett meddelande.
   * Skapa meddelandeförinställningar.
* **Betalat Apple-utvecklarkonto** med tillräcklig åtkomst för att skapa certifikat, identifierare och nycklar.
* Fysisk iOS-enhet eller simulator för testning.

## Utbildningsmål

I den här lektionen ska du

* Registrera program-ID med Apple Push Notification-tjänsten (APN:er).
* Skapa en appyta i Journey Optimizer.
* Uppdatera ditt schema så att det inkluderar push-meddelandefält.
* Installera och konfigurera taggtillägget för Journey Optimizer.
* Uppdatera appen för att registrera Journey Optimizer-taggtillägget.
* Validera inställningar i Assurance.
* Skicka ett testmeddelande från Assurance
* Definiera din egen push-meddelandehändelse, resa och upplevelse i Journey Optimizer.
* Skicka ditt eget push-meddelande inifrån appen.


## Inställningar

>[!TIP]
>
>Om du redan har konfigurerat din miljö som en del av [Journey Optimizer-lektionen för meddelanden i appen](journey-optimizer-inapp.md) kanske du redan har utfört några av stegen i det här installationsavsnittet.

### Registrera program-ID med APN:er

Följande steg är inte Adobe Experience Cloud-specifika och har utformats för att vägleda dig genom APN-konfigurationen.

#### Skapa en privat nyckel

1. Gå till **[!UICONTROL Keys]** på Apple utvecklarportal.
1. Välj **[!UICONTROL +]** om du vill skapa en nyckel.
   ![skapa ny nyckel](assets/mobile-push-apple-dev-new-key.png)

1. Ange en **[!UICONTROL Key Name]**.
1. Markera kryssrutan **[!UICONTROL Apple Push Notification service](APN:er)**.
1. Välj **[!UICONTROL Continue]**.
   ![konfigurera ny nyckel](assets/mobile-push-apple-dev-config-key.png)
1. Granska konfigurationen och välj **[!UICONTROL Register]**.
1. Hämta den privata nyckeln `.p8`. Den används senare i konfigurationen för appytan i den här lektionen.
1. Notera **[!UICONTROL Key ID]**. Den används i appytskonfigurationen.
1. Notera **[!UICONTROL Team ID]**. Den används i appytskonfigurationen.
   ![Nyckelinformation](assets/push-apple-dev-key-details.png)

Ytterligare dokumentation finns [här](https://help.apple.com/developer-account/#/devcdfbb56a3).

#### Lägg till en appyta i datainsamling

1. I [gränssnittet för datainsamling](https://experience.adobe.com/data-collection/) väljer du **[!UICONTROL App Surfaces]** i den vänstra panelen.
1. Välj **[!UICONTROL Create App Surface]** om du vill skapa en konfiguration.
   ![appyta - startsida](assets/push-app-surface.png)
1. Ange **[!UICONTROL Name]** som konfiguration, till exempel `Luma App Tutorial`.
1. Välj **[!UICONTROL Apple iOS]** från **[!UICONTROL Mobile Application Configuration]**.
1. Ange ID för mobilappspaket i fältet **[!UICONTROL App ID (iOS Bundle ID)]**. Exempel: `com.adobe.luma.tutorial.swiftui`.
1. Aktivera **[!UICONTROL Push Credentials]** för att lägga till dina autentiseringsuppgifter.
1. Dra och släpp `.p8` **Apple Push Notification Authentication Key**-filen.
1. Ange **[!UICONTROL Key ID]**, en sträng med 10 tecken som tilldelats när autentiseringsnyckeln `p8` skapades. Den finns på fliken **[!UICONTROL Keys]** på sidan **Certifikat, Identifierare och profiler** på sidorna på Apple Developer Portal. Se även [Skapa en privat nyckel](#create-a-private-key).
1. Ange **[!UICONTROL Team ID]**. Team-ID är ett värde som finns på fliken **Medlemskap** eller högst upp på sidan Apple Developer Portal. Se även [Skapa en privat nyckel](#create-a-private-key).
1. Välj **[!UICONTROL Save]**.

   ![appytans konfiguration](assets/push-app-surface-config.png)

### Uppdatera datastream-konfiguration

För att säkerställa att data som skickas från din mobilapp till Edge Network vidarebefordras till Journey Optimizer, ska du uppdatera Experience Edge-konfigurationen.

1. I användargränssnittet för datainsamling väljer du **[!UICONTROL Datastreams]** och markerar ditt datastream, till exempel **[!DNL Luma Mobile App]**.
1. Välj ![Mer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MoreSmallList_18_N.svg) för **[!UICONTROL Experience Platform]** och välj ![Redigera](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) **[!UICONTROL Edit]** på snabbmenyn.
1. På skärmen **[!UICONTROL Datastreams]** > ![Mapp](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) > **[!UICONTROL Adobe Experience Platform]**:

   1. Om det inte redan är markerat väljer du **[!UICONTROL AJO Push Profile Dataset]** från **[!UICONTROL Profile Dataset]**. Den här profildatauppsättningen krävs när du använder API-anropet `MobileCore.setPushIdentifier` (se [ Registrera enhetstoken för push-meddelanden ](#register-device-token-for-push-notifications)) som ser till att den unika identifieraren för push-meddelanden (t.ex. push-identifierare) lagras som en del av användarens profil.

   1. **[!UICONTROL Adobe Journey Optimizer]** har valts. Mer information finns i [Adobe Experience Platform-inställningar](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=en#aep).

   1. Välj **[!UICONTROL Save]** om du vill spara dataströmskonfigurationen.

   ![AEP-datastream-konfiguration](assets/datastream-aep-configuration.png)



### Installera tillägget Journey Optimizer-taggar

För att din app ska fungera med Journey Optimizer måste du uppdatera din taggegenskap.

1. Navigera till **[!UICONTROL Tags]** > **[!UICONTROL Extensions]** > **[!UICONTROL Catalog]**,
1. Öppna din egenskap, till exempel **[!DNL Luma Mobile App Tutorial]**.
1. Välj **[!UICONTROL Catalog]**.
1. Sök efter tillägget **[!UICONTROL Adobe Journey Optimizer]**.
1. Installera tillägget.
1. I dialogrutan **[!UICONTROL Install Extension]**
   1. Välj en miljö, till exempel **[!UICONTROL Development]**.
   1. Välj datauppsättningen **[!UICONTROL AJO Push Tracking Experience Event Dataset]** i listan **[!UICONTROL Event Dataset]**.
   1. Välj **[!UICONTROL Save to Library and Build]**.
      ![AJO-tilläggsinställningar](assets/push-tags-ajo.png)

>[!NOTE]
>
>Om du inte ser **[!UICONTROL AJO Push Tracking Experience Event Dataset]** som ett alternativ kontaktar du kundtjänst.
>

## Validera inställningar med Assurance

1. Granska avsnittet [Installationsanvisningar](assurance.md#connecting-to-a-session) för att ansluta simulatorn eller enheten till Assurance.
1. Välj **[!UICONTROL Configure]** i försäkringsgränssnittet.
   ![konfigurera klicka](assets/push-validate-config.png)
1. Välj ![Plus](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) bredvid **[!UICONTROL Push Debug]**.
1. Välj **[!UICONTROL Save]**.
   ![spara](assets/push-validate-save.png)
1. Välj **[!UICONTROL Push Debug]** i den vänstra navigeringen.
1. Klicka på fliken **[!UICONTROL Validate Setup]**.  
1. Välj din enhet i listan **[!UICONTROL Client]**.
1. Bekräfta att inga fel visas.
   ![validate](assets/push-validate-confirm.png)
1. Klicka på fliken **[!UICONTROL Send Test Push]**.  
1. (valfritt) Ändra standardinformationen för **[!UICONTROL Title]** och **[!UICONTROL Body]**
1. Välj ![Fel](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Bug_18_N.svg) **[!UICONTROL Send Test Push Notification]**.
1. Kontrollera **[!UICONTROL Test Results]**.
1. Du bör se push-meddelandet för testningen visas i din app.

   <img src="assets/luma-app-push.png" width="300" />


## Signering

Du måste signera Luma-appen för att skicka push-meddelanden och **kräver ett betalt Apple-utvecklarkonto**.

Så här uppdaterar du signeringen för din app:

1. Gå till appen i Xcode.
1. Välj **[!DNL Luma]** i projektnavigatorn.
1. Välj målet **[!DNL Luma]**.
1. Välj fliken **Signering och funktioner**.
1. Konfigurera **[!UICONTROL Automatic manage signing]**, **[!UICONTROL Team]** och **[!UICONTROL Bundle Identifier]**, eller använd din specifika information om etablering av Apple-utveckling.

   >[!IMPORTANT]
   >
   >Se till att du använder en _unik_-paketidentifierare och ersätt `com.adobe.luma.tutorial.swiftui`-paketidentifieraren, eftersom varje paketidentifierare måste vara unik. Vanligtvis använder du ett omvänt DNS-format för paket-ID-strängar, som `com.organization.brand.uniqueidentifier`. I den färdiga versionen av den här självstudien används till exempel `com.adobe.luma.tutorial.swiftui`.


   ![Xcode-signeringsfunktioner](assets/xcode-signing-capabilities.png){zoomable="yes"}


## Lägg till funktioner för push-meddelanden i appen

>[!IMPORTANT]
>
>Om du vill implementera och testa push-meddelanden i en iOS-app måste du ha ett **betalt** Apple-utvecklarkonto. Om du inte har ett betalt Apple-utvecklarkonto kan du hoppa över resten av den här lektionen.

1. I Xcode väljer du **[!DNL Luma]** i listan **[!UICONTROL TARGETS]**, väljer fliken **[!UICONTROL Signing & Capabilities]**, klickar på knappen **[!UICONTROL + Capability]** och väljer sedan **[!UICONTROL Push Notifications]**. Detta gör att din app kan ta emot push-meddelanden.

1. Sedan måste du lägga till ett meddelandetillägg i programmet. Gå tillbaka till fliken **[!DNL General]** och välj ikonen **[!UICONTROL +]** längst ned i avsnittet **[!UICONTROL TARGETS]**.

1. Du uppmanas att välja en mall för det nya målet. Välj **[!UICONTROL Notification Service Extension]** och sedan **[!UICONTROL Next]**.

1. I nästa fönster använder du `NotificationExtension` som namn på tillägget och klickar på knappen **[!UICONTROL Finish]**.

Du bör nu ha ett tillägg för push-meddelanden tillagt i appen, som liknar skärmen nedan.

![PUSN-meddelandetillägg](assets/xcode-signing-capabilities-pushnotifications.png)


## Implementera Journey Optimizer i appen

Som tidigare nämnts tillhandahåller installation av ett mobiltaggtillägg bara konfigurationen. Därefter måste du installera och registrera Messaging SDK. Om de här stegen inte är tydliga går du igenom avsnittet [Installera SDK](install-sdks.md).

>[!NOTE]
>
>Om du har slutfört avsnittet [Installera SDK:er](install-sdks.md) är SDK redan installerat och du kan hoppa över det här steget.
>

1. Kontrollera att [AEP Messaging](https://github.com/adobe/aepsdk-messaging-ios) har lagts till i listan över paket i paketberoenden i Xcode. Se [Hanteraren för wift-paket](install-sdks.md#swift-package-manager).
1. Navigera till **[!DNL Luma]** > **[!DNL Luma]** > **[!UICONTROL AppDelegate]** i Xcode Project-navigatorn.
1. Se till att `AEPMessaging` ingår i din lista över importer.

   `import AEPMessaging`

1. Kontrollera att `Messaging.self` är en del av den array med tillägg som du registrerar.

   ```swift
   let extensions = [
       AEPIdentity.Identity.self,
       Lifecycle.self,
       Signal.self,
       Edge.self,
       AEPEdgeIdentity.Identity.self,
       Consent.self,
       UserProfile.self,
       Places.self,
       Messaging.self,
       Optimize.self,
       Assurance.self
   ]
   ```

## Registrera enhetstoken för push-meddelanden

1. Lägg till API:t [`MobileCore.setPushIdentifier`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#setpushidentifier) i funktionen `func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data)`.

   ```swift
   // Send push token to Mobile SDK
   MobileCore.setPushIdentifier(deviceToken)
   ```

   Den här funktionen hämtar enhetstoken som är unik för den enhet som appen är installerad på. Ställer sedan in token för leverans av push-meddelanden med den konfiguration som du har konfigurerat och som är beroende av Apple Push Notification-tjänst (APN:er).

>[!IMPORTANT]
>
>`MobileCore.updateConfigurationWith(configDict: ["messaging.useSandbox": true])` avgör om push-meddelanden använder en APN-sandlåda eller produktionsserver för att skicka push-meddelanden. Kontrollera att `messaging.useSandbox` är inställt på `true` när du testar din app i simulatorn eller på en enhet så att du får push-meddelanden. När du distribuerar din app för produktion för att testa med Apple Testflight måste du ställa in `messaging.useSandbox` på `false`, annars kommer din produktionsapp inte att kunna ta emot push-meddelanden.


## Skapa ett eget push-meddelande

Om du vill skapa ett eget push-meddelande måste du definiera en händelse i Journey Optimizer som utlöser en resa som tar hand om att skicka ett push-meddelande.

### Uppdatera ditt schema

Du ska definiera en ny händelsetyp som ännu inte är tillgänglig som en del av listan med händelser som definieras i ditt schema. Du använder den här händelsetypen senare när du utlöser push-meddelanden.

1. I Journey Optimizer-gränssnittet väljer du **[!UICONTROL Schemas]** i den vänstra listen.
1. Välj **[!UICONTROL Browse]** i flikfältet.
1. Välj ditt schema, till exempel **[!DNL Luma Mobile App Event Schema]**, för att öppna det.
1. I schemaredigeraren:
   1. Markera fältet **[!UICONTROL eventType]**.
   1. I rutan **[!UICONTROL Field properties]** rullar du nedåt för att se en lista över möjliga värden för händelsetypen. Välj **[!UICONTROL Add row]** och lägg till `application.test` som **[!UICONTROL VALUE]** och `[!UICONTROL Test event for push notification]` som `DISPLAY NAME`.
   1. Välj **[!UICONTROL Apply]**.
   1. Välj **[!UICONTROL Save]**.
      ![Lägg till värde i händelsetyper](assets/ajo-update-schema-eventtype-enum.png)

### Definiera en händelse

Med händelser i Journey Optimizer kan du utlösa resor åt gången för att skicka meddelanden, till exempel push-meddelanden. Mer information finns i [Om händelser](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configure-journeys/events-journeys/about-events.html?lang=en).

1. I Journey Optimizer-gränssnittet väljer du **[!UICONTROL Configurations]** i den vänstra listen.

1. På skärmen **[!UICONTROL Dashboard]** väljer du knappen **[!UICONTROL Manage]** i rutan **[!UICONTROL Events]**.

1. Välj **[!UICONTROL Create Event]** på skärmen **[!UICONTROL Events]**.

1. I rutan **[!UICONTROL Edit event event1]**:

   1. Ange `LumaTestEvent` som **[!UICONTROL Name]** för händelsen.
   1. Ange en **[!UICONTROL Description]**, till exempel `Test event to trigger push notifications in Luma app`.

   1. Välj det händelseschema för mobilappsupplevelse som du skapade tidigare i [Skapa ett XDM-schema](create-schema.md) från listan **[!UICONTROL Schema]**, till exempel **[!DNL Luma Mobile App Event Schema v.1]**.
   1. Välj ![Redigera](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) bredvid listan **[!UICONTROL Fields]**.

      ![Redigera händelsesteg 1](assets/ajo-edit-event1.png)

      I dialogrutan **[!UICONTROL Fields]** ser du till att följande fält är markerade (ovanpå de standardfält som alltid är markerade (**[!UICONTROL _id]**, **[!UICONTROL id]** och **[!UICONTROL timestamp]**)). Du kan växla mellan **[!UICONTROL Selected]**, **[!UICONTROL All]** och **[!UICONTROL Primary]** i listrutan eller använda fältet ![Sök](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Search_18_N.svg).

      * **[!UICONTROL Application Identified (id)]**,
      * **[!UICONTROL Event Type (eventType)]**,
      * **[!UICONTROL Primary (primary)]**.

      ![Redigera händelsefält](assets/ajo-event-fields.png)

      Välj sedan **[!UICONTROL Ok]**.

   1. Välj ![Redigera](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) bredvid fältet **[!UICONTROL Event id condition]**.

      1. Dra och släpp **[!UICONTROL Event Type (eventType)]** i dialogrutan **[!UICONTROL Add an event id condition]** till **[!UICONTROL Drag and drop an element here]**.
      1. Bläddra längst ned i povern och välj **[!UICONTROL application.test]** (som är den händelsetyp som du lade till tidigare i listan över händelsetyper som en del av [Uppdatera ditt schema](#update-your-schema)). Bläddra sedan uppåt till toppen och välj **[!UICONTROL Ok]**.
      1. Välj **[!UICONTROL Ok]** om du vill spara villkoret.
         ![Redigera händelsevillkor](assets/ajo-edit-condition.png)

   1. Välj **[!UICONTROL ECID (ECID)]** i listan **[!UICONTROL Namespace]**. Fältet **[!UICONTROL Profile identifier]** fylls i automatiskt med **[!UICONTROL The id of the first element of the key ECID for the map identityMap]**.
   1. Välj **[!UICONTROL Save]**.
      ![Redigera händelsesteg 2](assets/ajo-edit-event2.png)

Du har just skapat en händelsekonfiguration som baseras på det händelseschema för mobilappsupplevelser som du skapade tidigare som en del av den här självstudien. Den här händelsekonfigurationen filtrerar inkommande upplevelsehändelser med din specifika händelsetyp (`application.test`), så bara händelser med den typen, som initieras från din mobilapp, utlöser den resa du bygger i nästa steg. I ett verkligt scenario kanske du vill skicka push-meddelanden från en extern tjänst, men samma koncept gäller: från det externa programmet skickar du en upplevelsehändelse till Experience Platform som innehåller specifika fält som du kan använda för att tillämpa villkor på innan dessa händelser utlöser en resa.

### Skapa resan

Nästa steg är att skapa den resa som utlöser sändningen av push-meddelandet när du får den rätta händelsen.

1. I Journey Optimizer-gränssnittet väljer du **[!UICONTROL Journeys]** i den vänstra listen.
1. Välj **[!UICONTROL Create Journey]**.
1. På panelen **[!UICONTROL Journey Properties]**:

   1. Ange en **[!UICONTROL Name]** för resan, till exempel `Luma - Test Push Notification Journey`.
   1. Ange en **[!UICONTROL Description]** för resan, till exempel `Journey for test push notifications in Luma mobile app`.
   1. Kontrollera att **[!UICONTROL Allow re-entrance]** är markerat och ange **[!UICONTROL Re-entrance wait period]** till **[!UICONTROL 30]** **[!UICONTROL Seconds]**.
   1. Välj **[!UICONTROL Ok]**.
      ![Resans egenskaper](assets/ajo-journey-properties.png)

1. Tillbaka på arbetsytan på resan, från **[!UICONTROL EVENTS]**, dra och släpp ![ Event](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Globe_18_N.svg) **[!DNL LumaTestEvent]** på arbetsytan där den visas **[!UICONTROL Select an entry event or a read audience activity]**.

   * Ange **[!UICONTROL Label]**, till exempel `Luma Test Event`, på panelen **[!UICONTROL Events: LumaTestEvent]**.

1. I listrutan **[!UICONTROL ACTIONS]** drar och släpper du ![Push](https://spectrum.adobe.com/static/icons/workflow_18/Smock_PushNotification_18_N.svg) **[!UICONTROL Push]** på ![Add](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) som visas till höger om din **[!DNL LumaTestEvent]**-aktivitet. I rutan **[!UICONTROL Actions: Push]**:

   1. Ange en **[!UICONTROL Label]**, till exempel `Luma Test Push Notification`, ge en **[!UICONTROL Description]**, till exempel `Test push notification for Luma mobile app`, välj **[!UICONTROL Transactional]** i listan **[!UICONTROL Category]** och välj **[!DNL Luma]** i listan **[!UICONTROL Push surface]**.
   1. Välj ![Redigera](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) **[!UICONTROL Edit content]** om du vill börja redigera det faktiska push-meddelandet.
      ![Push-egenskaper](assets/ajo-push-properties.png)

      I **[!UICONTROL Push Notification]**-redigeraren:

      1. Ange en **[!UICONTROL Title]**, till exempel `Luma Test Push Notification`, och ange en **[!UICONTROL Body]**, till exempel `Test push notification for Luma mobile app`.
      1. Du kan också ange en länk till en bild (.png eller .jpg) i **[!UICONTROL Add media]**. Om du gör det blir bilden en del av push-meddelandet.
      1. Om du vill spara och lämna redigeraren väljer du ![Sparron till vänster](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronLeft_18_N.svg).
         ![Push-redigerare](assets/ajo-push-editor.png)

   1. Om du vill spara och slutföra definitionen av push-meddelanden väljer du **[!UICONTROL Ok]**.

1. Resan ska se ut så här nedan. Välj **[!UICONTROL Publish]** om du vill publicera och aktivera din resa.
   ![Färdig resa](assets/ajo-journey-finished.png)


## Utlös push-meddelandet

Du har alla ingredienser på plats för att skicka ett push-meddelande. Det som återstår är hur detta push-meddelande ska utlösas. Det är alltså samma sak som du har sett tidigare: skicka bara en upplevelsehändelse med rätt nyttolast (som i [Händelser](events.md)).

Den här gången har den upplevelsehändelse du ska skicka inte skapats för att skapa en enkel XDM-ordlista. Du kommer att använda en `struct` som representerar en nyttolast för push-meddelanden. Att definiera en dedikerad datatyp är ett annat sätt att implementera händelsenyttolaster för att skapa upplevelser i ditt program.

1. Navigera till **[!DNL Luma]** > **[!DNL Luma]** > **[!UICONTROL Model]** > **[!UICONTROL XDM]** > **[!UICONTROL TestPushPayload]** i Xcode Project-navigatorn och kontrollera koden.

   ```swift
   import Foundation
   
   // MARK: - TestPush
   struct TestPushPayload: Codable {
      let application: Application
      let eventType: String
   }
   
   // MARK: - Application
   struct Application: Codable {
      let id: String
   }
   ```

   Koden är en representation av följande enkla nyttolast som du ska skicka för att utlösa testresan för push-meddelanden

   ```json
   {
      "eventType": string,
      "application" : [
          "id": string
      ]
   }
   ```

1. Navigera till **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** i Xcode Project-navigatorn och lägg till följande kod i `func sendTestPushEvent(applicationId: String, eventType: String)`:

   ```swift
   // Create payload and send experience event
   Task {
       let testPushPayload = TestPushPayload(
           application: Application(
               id: applicationId
           ),
           eventType: eventType
       )
       // send the final experience event
       await sendExperienceEvent(
           xdm: testPushPayload.asDictionary() ?? [:]
       )
   }
   ```

   Den här koden skapar en `testPushPayload`-instans med de parametrar som har angetts för funktionen (`applicationId` och `eventType`) och anropar sedan `sendExperienceEvent` när nyttolasten konverteras till ett lexikon. Den här koden, den här gången, tar även hänsyn till asynkrona aspekter av att anropa Adobe Experience Platform SDK genom att använda Swift-samtidighetsmodellen som baseras på `await` och `async`.

1. Navigera till **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL ConfigView]** i Xcode Project-navigatorn. I definitionen för knappen Push Notification (Push-meddelande) lägger du till följande kod för att skicka händelsenyttolasten för testpush-meddelanden för att utlösa din resa när användaren trycker på knappen.

   ```swift
   // Setting parameters and calling function to send push notification
   Task {
       let eventType = testPushEventType
       let applicationId = Bundle.main.bundleIdentifier ?? "No bundle id found"
       await MobileSDK.shared.sendTestPushEvent(applicationId: applicationId, eventType: eventType)
   }
   ```


## Validera med din app

1. Återskapa och kör appen i simulatorn eller på en fysisk enhet från Xcode med ![Play](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Play_18_N.svg).

1. Gå till fliken **[!UICONTROL Settings]**.

1. Tryck på **[!UICONTROL Push Notification]**. Push-meddelandet visas i din app.

   <img src="assets/ajo-test-push.png" width="300" />


## Nästa steg

Nu bör du ha alla verktyg som behövs för att hantera push-meddelanden i appen. Du kan till exempel skapa en resa i Journey Optimizer som skickar ett välkomstmeddelande när en användare av appen loggar in. Eller ett bekräftelsemeddelande när en användare köper en produkt i appen. Eller anger geofence för en plats (som du kommer att se i lektionen [Platser](places.md)).

>[!SUCCESS]
>
>Du har nu aktiverat appen för push-meddelanden med Journey Optimizer och Journey Optimizer-tillägget för Experience Platform Mobile SDK.
>
>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Mobile SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela dem i det här [Experience League-diskussionsinlägget](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Nästa: **[Skapa och skicka meddelanden i appen](journey-optimizer-inapp.md)**
