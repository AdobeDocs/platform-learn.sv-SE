---
title: Adobe Journey Optimizer-meddelanden i appen
description: Lär dig hur du skapar meddelanden i appen till en mobilapp med Platform Mobile SDK och Adobe Journey Optimizer.
solution: Data Collection,Journey Optimizer
feature-set: Journey Optimizer
feature: In App
hide: true
source-git-commit: 5f0fa0b524cd4a12aaab8c8c0cd560a31003fbd8
workflow-type: tm+mt
source-wordcount: '1607'
ht-degree: 0%

---

# Journey Optimizer-meddelanden i appen

Lär dig hur du skapar meddelanden i appen för mobilappar med Platform Mobile SDK och Journey Optimizer.

Med Journey Optimizer kan ni skapa kampanjer för att skicka meddelanden i appen till riktade målgrupper. Innan du skickar meddelanden i appen med Journey Optimizer måste du se till att rätt konfigurationer och integreringar finns på plats. Om du vill veta mer om dataflödet för meddelanden i programmet i Journey Optimizer kan du läsa [dokumentationen](https://experienceleague.adobe.com/docs/journey-optimizer/using/in-app/inapp-configuration.html?lang=en).

>[!NOTE]
>
>Den här lektionen är valfri och gäller endast för Journey Optimizer-användare som vill skicka meddelanden i appen.


## Förutsättningar

* App med SDK:er har installerats och konfigurerats.
* Åtkomst till Journey Optimizer och tillräcklig behörighet enligt beskrivningen [här](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configuration-message/push-config/push-configuration.html?lang=en). Du behöver även tillräcklig behörighet för följande Journey Optimizer-funktioner.
   * Hantera kampanjer.
* Betalat Apple-utvecklarkonto med tillräcklig behörighet för att skapa certifikat, identifierare och nycklar.
* Fysisk iOS-enhet eller simulator för testning.
* Registrerat program-ID med Apple push-meddelandetjänst
* Dina push-autentiseringsuppgifter för appen har lagts till i datainsamlingen
* Tillägget Journey Optimizer-taggar har installerats
* Implementerat Journey Optimizer i appen


## Utbildningsmål

I den här lektionen ska du

* Registrera program-ID med Apple Push Notification-tjänsten (APN).
* Skapa en appyta i AJO.
* Installera och konfigurera taggtillägget för Journey Optimizer.
* Uppdatera appen så att den innehåller taggtillägget Journey Optimizer.
* Validera inställningar i Assurance.
* Definiera er egen kampanj och upplevelse av meddelanden i appen i Journey Optimizer.
* Skicka ditt eget meddelande i appen inifrån appen.

## Konfigurera din app

>[!TIP]
>
>Om du redan har konfigurerat ditt program som en del av [Journey Optimizer push-meddelanden](journey-optimizer-push.md) kan du hoppa över det här avsnittet.

### Registrera program-ID med APNS

Följande steg är inte Adobe Experience Cloud-specifika och har utformats för att vägleda dig genom APNS-konfigurationen.

### Skapa en privat nyckel

1. Gå till Apple utvecklarportal **[!UICONTROL Tangenter]**.
1. Om du vill skapa en nyckel väljer du **[!UICONTROL +]**.
   ![skapa ny nyckel](assets/mobile-push-apple-dev-new-key.png)

1. Ange en **[!UICONTROL Nyckelnamn]**.
1. Välj **[!UICONTROL Tjänsten Apple Push Notification] (APN)** kryssrutan.
1. Välj **[!UICONTROL Fortsätt]**.
   ![konfigurera ny nyckel](assets/mobile-push-apple-dev-config-key.png)
1. Granska konfigurationen och välj **[!UICONTROL Registrera]**.
1. Ladda ned `.p8` privat nyckel. Den används i appytskonfigurationen.
1. Anteckna **[!UICONTROL Nyckel-ID]**. Den används i appytskonfigurationen.
1. Anteckna **[!UICONTROL Team-ID]**. Den används i appytskonfigurationen.
   ![Nyckelinformation](assets/push-apple-dev-key-details.png)

Ytterligare dokumentation kan [hittades här](https://help.apple.com/developer-account/#/devcdfbb56a3).

### Lägg till push-autentiseringsuppgifter för appen i datainsamlingen

1. Från [Gränssnitt för datainsamling](https://experience.adobe.com/data-collection/), markera **[!UICONTROL Appytor]** till vänster.
1. Om du vill skapa en konfiguration väljer du **[!UICONTROL Skapa appyta]**.
   ![app surface home](assets/push-app-surface.png)
1. Ange en **[!UICONTROL Namn]** för konfigurationen, till exempel `Luma App Tutorial`  .
1. Från **[!UICONTROL Konfiguration av mobilprogram]**, markera **[!UICONTROL Apple iOS]**.
1. Ange programpaket-ID för mobilappen i **[!UICONTROL Program-ID (iOS Bundle-ID)]** fält. Exempel,  `com.adobe.luma.tutorial.swiftui`.
1. Aktivera **[!UICONTROL Push-autentiseringsuppgifter]** för att lägga till dina inloggningsuppgifter.
1. Dra och släpp `.p8` **Autentiseringsnyckel för push-meddelanden i Apple** -fil.
1. Ange **[!UICONTROL Nyckel-ID]**, en sträng med 10 tecken som tilldelas när `p8` auth key. Den finns under **[!UICONTROL Tangenter]** i **Certifikat, identifierare och profiler** på Apple Developer Portal. Se även [Skapa en privat nyckel](#create-a-private-key).
1. Ange **[!UICONTROL Team-ID]**. Team-ID är ett värde som finns under **medlemskap** eller högst upp på Apple Developer Portal-sidan. Se även [Skapa en privat nyckel](#create-a-private-key).
1. Välj **[!UICONTROL Spara]**.

   ![appytans konfiguration](assets/push-app-surface-config.png)

### Installera tillägget Journey Optimizer-taggar

För att din app ska fungera med Journey Optimizer måste du uppdatera din taggegenskap.

1. Navigera till **[!UICONTROL Taggar]** > **[!UICONTROL Tillägg]** > **[!UICONTROL Katalog]**,
1. Öppna egenskapen, till exempel **[!UICONTROL Luma Mobile App Tutorial]**.
1. Välj **[!UICONTROL Katalog]**.
1. Sök efter **[!UICONTROL Adobe Journey Optimizer]** tillägg.
1. Installera tillägget.
1. I **[!UICONTROL Installera tillägg]** dialog
   1. Välj en miljö, till exempel **[!UICONTROL Utveckling]**.
   1. Välj **[!UICONTROL AJO Push Tracking Experience, händelsedatauppsättning]** datauppsättning från **[!UICONTROL Händelsedatauppsättning]** lista.
   1. Välj **[!UICONTROL Spara i bibliotek och bygge]**.
      ![Inställningar för AJO-tillägg](assets/push-tags-ajo.png)

>[!NOTE]
>
>Om du inte ser `AJO Push Tracking Experience Event Dataset` som ett alternativ, kontakta kundtjänst.
>

### Implementera Journey Optimizer i appen

Som tidigare nämnts tillhandahåller installation av ett mobiltaggtillägg bara konfigurationen. Därefter måste du installera och registrera Messaging SDK. Om de här stegen inte är tydliga går du igenom [Installera SDK:er](install-sdks.md) -avsnitt.

>[!NOTE]
>
>Om du har slutfört [Installera SDK:er](install-sdks.md) är SDK redan installerat och du kan hoppa över det här steget.
>

1. I Xcode kontrollerar du att [AEP Messaging](https://github.com/adobe/aepsdk-messaging-ios.git) läggs till i listan över paket i paketberoenden. Se [Swift Package Manager](install-sdks.md#swift-package-manager).
1. Navigera till **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL AppDelegate]** i Xcode Project-navigatorn.
1. Säkerställ `AEPMessaging` är en del av din lista över importer.

   `import AEPMessaging`

1. Säkerställ `Messaging.self` är en del av den array med tillägg som du registrerar.

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

1. Lägg till `MobileCore.setPushIdentifier` till `func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data)` funktion.

   ```swift
   // Send push token to Experience Platform
   MobileCore.setPushIdentifier(deviceToken)
   ```

   Den här funktionen hämtar enhetstoken som är unik för den enhet som appen är installerad på. Ställer sedan in token för leverans av push-meddelanden med den konfiguration som du har konfigurerat och som är beroende av Apple Push Notification-tjänst (APN:er).


## Validera inställningssäkring

1. Granska [installationsanvisningar](assurance.md) -avsnitt.
1. Installera appen på den fysiska enheten eller i simulatorn.
1. Starta appen med den URL som skapas av försäkringen.
1. Välj **[!UICONTROL Konfigurera]**.
   ![konfigurera klicka](assets/push-validate-config.png)
1. Välj ![Plus](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) knapp bredvid **[!UICONTROL Meddelanden i appen]**.
1. Välj **[!UICONTROL Spara]**.
   ![spara](assets/assurance-in-app-config.png)
1. Välj **[!UICONTROL Meddelanden i appen]** från vänster navigering.
1. Välj **[!UICONTROL Validering]** -fliken.
1. Bekräfta att inga fel visas.
   ![Validering i appen](assets/assurance-in-app-validate.png)


## Skapa ett eget meddelande i appen

Om du vill skapa ett eget meddelande i appen måste du definiera en kampanj i Journey Optimizer som utlöser ett meddelande i appen baserat på händelser som inträffar. Dessa händelser kan vara:

* data som skickas till Adobe Experience Platform,
* viktiga spårningshändelser, som åtgärd, eller tillstånd eller insamling av PII-data, via de allmänna API:erna för Mobile Core,
* livscykelhändelser, som start, installation, uppgradering, stängning eller krasch,
* geopositioneringshändelser, som att ange eller avsluta en intressepunkt.

I den här självstudiekursen kommer du att använda de generiska och tilläggsoberoende API:erna för Mobile Core för att underlätta händelsespårning av användarskärmar, åtgärder och PII-data. Händelser som genereras av dessa API:er publiceras till SDK-händelsehubben och kan användas av tillägg. När till exempel Analytics-tillägget installeras skickas alla användaråtgärder och händelsedata för appskärmar till rätt analytiska rapportslutpunkter.

1. I användargränssnittet för Journey Optimizer väljer du **[!UICONTROL Kampanjer]** från den vänstra listen.
1. Välj **[!UICONTROL Skapa kampanj]**.
1. I **[!UICONTROL Skapa kampanj]** skärm:
   1. Välj **[!UICONTROL Meddelande i appen]** och välj en appyta på **[!UICONTROL Appyta]** lista, till exempel **[!UICONTROL Mobilappen Luma]**.
   1. Välj **[!UICONTROL Skapa]**
      ![Kampanjegenskaper](assets/ajo-campaign-properties.png)
1. På skärmen för Campaign-definitionen, på **[!UICONTROL Egenskaper]**, ange **[!UICONTROL Namn]** för kampanjen, till exempel `Luma - In-App Messaging Campaign`och en **[!UICONTROL Beskrivning]**, till exempel `In-app messaging campaign for Luma app`.
   ![Kampanjnamn](assets/ajo-campaign-properties-name.png)
1. Bläddra nedåt till **[!UICONTROL Åtgärd]** och markera **[!UICONTROL Redigera innehåll]**.
1. I **[!UICONTROL Meddelande i appen]** skärm:
   1. Välj **[!UICONTROL Modal]** som **[!UICONTROL Meddelandelayout]**.
   2. Retur `https://luma.enablementadobe.com/content/dam/luma/en/logos/Luma_Logo.png` for **[!UICONTROL Media-URL]**.
   3. Ange en **[!UICONTROL Sidhuvud]**, till exempel `Welcome to this Luma In-App Message` och ange **[!UICONTROL Brödtext]**, till exempel `Triggered by pushing that button in the app...`.
   4. Retur **[!UICONTROL Avvisa]** som **[!UICONTROL Knapp 1 text (primär)]**.
   5. Observera hur förhandsgranskningen uppdateras.
   6. Välj **[!UICONTROL Granska för aktivering]**.
      ![Redigerare i appen](assets/ajo-in-app-editor.png)
1. I **[!UICONTROL Granska för att aktivera (Luma - Meddelandekampanj i appen)]** skärm, välja ![Redigera](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) i **[!UICONTROL Schema]** platta.
   ![Välj Schema för granskning](assets/ajo-review-select-schedule.png)
1. Tillbaka i **[!UICONTROL Luma - kampanj för meddelanden i appen]** skärm, välja ![Redigera](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) **[!UICONTROL Redigera utlösare]**.
1. I **[!UICONTROL Meddelandeutlösare i appen]** konfigurerar du information om den spårningsåtgärd som utlöser meddelandet i appen:
   1. Ta bort **[!UICONTROL Programstarthändelse]**, markera ![Stäng](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Close_18_N.svg) .
   1. Använd ![Lägg till](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Lägg till villkor]** att skapa följande logik för **[!UICONTROL Visa meddelande om]**.
   1. Klicka **[!UICONTROL Klar]**.
      ![Utlösarlogik](assets/ajo-trigger-logic.png)

   Du har definierat en spårningsåtgärd, där **[!UICONTROL Åtgärd]** är lika med `in-app` och **[!UICONTROL Kontextdata]** med funktionsmakrot är ett nyckelvärdepar med `"showMessage" : "true"`.

1. Tillbaka i **[!UICONTROL Luma - kampanj för meddelanden i appen]** skärm, välja **[!UICONTROL Granska för aktivering]**.
1. I **[!UICONTROL Granska för att aktivera (Luma - Meddelandekampanj i appen)]** skärm, välja **[!UICONTROL Aktivera]**.
1. Du ser **[!UICONTROL Luma - kampanj för meddelanden i appen]** med status **[!UICONTROL Live]** i **[!UICONTROL Kampanjer]** lista.
   ![Kampanjlista](assets/ajo-campaign-list.png)


## Startar meddelandet i appen

Du har alla ingredienser på plats för att skicka ett meddelande i appen. Det som återstår är hur du utlöser det här meddelandet i appen i din app.

1. Gå till **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Utils]** > **[!UICONTROL MobileSDK]** i Xcode Project-navigatorn. Hitta `func sendTrackAction(action: String, data: [String: Any]?)` och lägg till följande kod som anropar `MobileCore.track` funktion, baserat på parametrarna `action` och `data`.


   ```swift
   // send trackAction event
   MobileCore.track(action: action, data: data)
   ```

1. Gå till **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Vyer]** > **[!UICONTROL Allmänt]** > **[!UICONTROL ConfigView]** i Xcode Project Navigator. Sök efter koden för knappen Meddelande i appen och lägg till följande kod:

   ```swift
   Task {
       AEPService.shared.sendTrackAction(action: "in-app", data: ["showMessage": "true"])
   }
   ```

## Validera med din app

1. Öppna appen på en enhet eller i simulatorn.

1. Gå till **[!UICONTROL Inställningar]** -fliken.

1. Tryck **[!UICONTROL Meddelande i appen]**. Meddelandet visas i appen.

   <img src="assets/ajo-in-app-message.png" width="300" />


## Validera implementering i Assurance

Du kan validera dina meddelanden i appen i Assurance-gränssnittet.

1. Välj **[!UICONTROL Meddelanden i appen]**.
1. Välj **[!UICONTROL Händelselista]**.
1. Välj en **[!UICONTROL Visa meddelande]** post.
1. Inspect the raw event, speciellt `html`, som innehåller den fullständiga layouten och innehållet i meddelandet i appen.
   ![Meddelande för försäkring i appen](assets/assurance-in-app-display-message.png)


## Nästa steg

Nu bör du ha alla verktyg du behöver för att börja lägga till meddelanden i appen, där det är relevant och tillämpligt, i Luma-appen. Du kan till exempel marknadsföra produkter baserat på specifika interaktioner som du har spårat i appen.

>[!SUCCESS]
>
>Du har aktiverat appen för meddelanden i appen och lagt till en meddelandekampanj i appen med Journey Optimizer och Journey Optimizer-tillägget för Experience Platform Mobile SDK.<br/>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Mobile SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Nästa: **[Visa erbjudanden med Journey Optimizer](journey-optimizer-offers.md)**
