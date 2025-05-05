---
title: Skapa och skicka meddelanden i appen med Platform Mobile SDK
description: Lär dig hur du skapar och skickar meddelanden i appen till en mobilapp med Platform Mobile SDK och Adobe Journey Optimizer.
solution: Data Collection,Journey Optimizer
feature-set: Journey Optimizer
feature: In App
jira: KT-14639
exl-id: 6cb4d031-6172-4a84-b717-e3a1f5dc7d5d
source-git-commit: f73f0fc345fc605e60b19be1abe2e328795898aa
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 0%

---

# Skapa och skicka meddelanden i appen

Lär dig skapa meddelanden i appen för mobilappar med Experience Platform Mobile SDK och Journey Optimizer.

Med Journey Optimizer kan ni skapa kampanjer för att skicka meddelanden i appen till riktade målgrupper. Kampanjer i Journey Optimizer används för att leverera engångsinnehåll till en viss målgrupp via olika kanaler. Med kampanjer utförs åtgärder samtidigt, antingen omedelbart eller baserat på ett angivet schema. När du använder resor (se lektionen [Journey Optimizer push-meddelanden](journey-optimizer-push.md)) utförs åtgärder i sekvens.

![Arkitektur](assets/architecture-ajo.png)

Innan du skickar meddelanden i appen med Journey Optimizer måste du se till att rätt konfigurationer och integreringar finns på plats. Mer information om dataflödet för meddelanden i programmet i Journey Optimizer finns i [dokumentationen](https://experienceleague.adobe.com/docs/journey-optimizer/using/in-app/inapp-configuration.html?lang=sv-SE).

>[!NOTE]
>
>Den här lektionen är valfri och gäller endast för Journey Optimizer-användare som vill skicka meddelanden i appen.


## Förhandskrav

* App med SDK:er har installerats och konfigurerats.
* Konfigurera appen för Adobe Experience Platform.
* Åtkomst till Journey Optimizer och tillräcklig behörighet enligt beskrivningen [här](https://experienceleague.adobe.com/docs/journey-optimizer/using/push/push-config/push-configuration.html?lang=sv-SE). Du behöver även tillräcklig behörighet för följande Journey Optimizer-funktioner.
   * Hantera kampanjer.
* Fysisk iOS-enhet eller simulator för testning.


## Utbildningsmål

I den här lektionen ska du

* Skapa en appyta i AJO.
* Installera och konfigurera taggtillägget för Journey Optimizer.
* Uppdatera appen för att registrera Journey Optimizer-taggtillägget.
* Validera konfigurationen i Assurance.
* Definiera er egen kampanj och upplevelse av meddelanden i appen i Journey Optimizer.
* Skicka ditt eget meddelande i appen inifrån appen.

## Inställningar

>[!TIP]
>
>Om du redan har konfigurerat din miljö som en del av [Journey Optimizer push messaging](journey-optimizer-push.md) -lektionen kanske du redan har utfört några av stegen i det här installationsavsnittet.


### Skapa en kanalkonfiguration i Journey Optimizer

Till att börja med måste du skapa en kanalkonfiguration som gör att du kan skicka meddelanden från Journey Optimizer i appmeddelanden.

1. I Journey Optimizer-gränssnittet öppnar du menyn **[!UICONTROL Channels]** > **[!UICONTROL General settings]** > **[!UICONTROL Channel configurations]** och väljer sedan **[!UICONTROL Create channel configuration]**.

   ![Skapa en kanalkonfiguration](assets/push-config-9.png)

1. Ange ett namn och en beskrivning (valfritt) för konfigurationen.

   >[!NOTE]
   >
   > Namn måste börja med en bokstav (A-Z). Det får bara innehålla alfanumeriska tecken. Du kan också använda understreck `_`, punkt `.` och bindestreck `-`.


1. Om du vill tilldela anpassade eller grundläggande dataanvändningsetiketter till konfigurationen kan du välja **[!UICONTROL Manage access]**. [Läs mer om OLAC (Object Level Access Control)](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/access-control/object-based-access).

1. Välj kanalen **Meddelanden i appen**.

1. Välj **[!UICONTROL Marketing action]** om du vill associera medgivandeprinciper till meddelanden som använder den här konfigurationen. Alla policyer för samtycke som är kopplade till marknadsföringsåtgärden utnyttjas för att ta hänsyn till kundernas preferenser. [Läs mer om marknadsföringsåtgärder](https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/privacy/consent/consent#surface-marketing-actions).

1. Välj den plattform som du vill definiera inställningarna för. På så sätt kan ni ange målappen för varje plattform och säkerställa enhetlig innehållsleverans på flera plattformar.

   >[!NOTE]
   >
   >För iOS- och Android-plattformar baseras leveransen enbart på program-ID:t. Om båda apparna har samma program-ID levereras innehåll till båda, oavsett vilken plattform som valts i **[!UICONTROL Channel configuration]**.

1. Välj **[!UICONTROL Submit]** om du vill spara ändringarna.

   ![Konfigurera appkanalen](assets/inapp_config_10.png)

### Uppdatera datastream-konfiguration

Uppdatera Experience Edge-konfigurationen för att se till att data som skickas från din mobilapp till Edge Network vidarebefordras till Journey Optimizer.



1. I användargränssnittet för datainsamling väljer du **[!UICONTROL Datastreams]** och markerar ditt datastream, till exempel **[!DNL Luma Mobile App]**.
1. Välj ![Mer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MoreSmallList_18_N.svg) för **[!UICONTROL Experience Platform]** och välj ![Redigera](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) **[!UICONTROL Edit]** på snabbmenyn.
1. Kontrollera att **[!UICONTROL Adobe Journey Optimizer]** är markerat på skärmen **[!UICONTROL Datastreams]** > ![Mapp](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) > **[!UICONTROL Adobe Experience Platform]**. Mer information finns i [Adobe Experience Platform-inställningar](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=sv-SE#aep).
1. Välj **[!UICONTROL Save]** om du vill spara dataströmskonfigurationen.


   ![AEP datastream-konfiguration](assets/datastream-ajo-inapp-configuration.png)


### Installera tillägget Journey Optimizer-taggar

För att din app ska fungera med Journey Optimizer måste du uppdatera din taggegenskap.

1. Navigera till **[!UICONTROL Tags]** > **[!UICONTROL Extensions]** > **[!UICONTROL Catalog]**.
1. Öppna din egenskap, till exempel **[!DNL Luma Mobile App Tutorial]**.
1. Välj **[!UICONTROL Catalog]**.
1. Sök efter tillägget **[!UICONTROL Adobe Journey Optimizer]**.
1. Installera tillägget.

När *endast* använder meddelanden i appen i **[!UICONTROL Install Extension]** eller **[!UICONTROL Configure Extension]** behöver du inte konfigurera någonting. Om du redan har följt lektionen [Push-meddelanden](journey-optimizer-push.md) i självstudiekursen kommer du att se att **[!UICONTROL AJO Push Tracking Experience Event Dataset]**-datauppsättningen är vald i **[!UICONTROL Event Dataset]** -listan för **[!UICONTROL Development]** -miljön.


### Implementera Journey Optimizer i appen

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


## Validera installationen med Assurance

1. Granska avsnittet [installationsanvisningar](assurance.md#connecting-to-a-session) för att ansluta simulatorn eller enheten till Assurance.
1. I Assurance-gränssnittet väljer du **[!UICONTROL Configure]**.
   ![konfigurera klicka](assets/push-validate-config.png)
1. Välj knappen ![Plus](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) bredvid **[!UICONTROL In-App Messaging]**.
1. Välj **[!UICONTROL Save]**.
   ![spara](assets/assurance-in-app-config.png)
1. Välj **[!UICONTROL In-App Messaging]** i den vänstra navigeringen.
1. Klicka på fliken **[!UICONTROL Validation]**.  Bekräfta att inga fel visas.

   ![Validering i appen](assets/assurance-in-app-validate.png)


## Skapa ett eget meddelande i appen

Om du vill skapa ett eget meddelande i appen måste du definiera en kampanj i Journey Optimizer som utlöser ett meddelande i appen baserat på händelser som inträffar. Dessa händelser kan vara:

* data som skickas till Adobe Experience Platform,
* viktiga spårningshändelser, som åtgärd, eller tillstånd eller insamling av PII-data, via de allmänna API:erna för Mobile Core,
* livscykelhändelser, som start, installation, uppgradering, stängning eller krasch,
* geopositioneringshändelser, som att ange eller avsluta en intressepunkt.

I den här självstudiekursen ska du använda de generiska och tilläggsoberoende API:erna för Mobile Core (se [Generiska API:er för Mobile Core](https://developer.adobe.com/client-sdks/documentation/mobile-core/#mobile-core-generic-apis)) för att underlätta händelsespårning av användarskärmar, åtgärder och PII-data. Händelser som genereras av dessa API:er publiceras till händelsehubben i SDK och kan användas av tillägg. SDK händelsehubb tillhandahåller den grundläggande datastruktur som är knuten till alla SDK-tillägg för Mobile Platform, med en lista över registrerade tillägg och interna moduler, en lista över registrerade händelseavlyssnare och en delad tillståndsdatabas.

SDK händelsehubb publicerar och tar emot händelsedata från registrerade tillägg för att förenkla integreringen med Adobe och tredjepartslösningar. När tillägget Optimera installeras hanteras till exempel alla förfrågningar och interaktioner med erbjudandemotorn Journey Optimizer - Beslutshantering av händelsehubben.

1. I Journey Optimizer-gränssnittet väljer du **[!UICONTROL Campaigns]** i den vänstra listen.
1. Välj **[!UICONTROL Create Campaign]**.
1. På skärmen **[!UICONTROL Create Campaign]**:
   1. Välj **[!UICONTROL In-app message]** och välj en appyta i listan **[!UICONTROL App surface]**, till exempel **[!DNL Luma Mobile App]**.
   1. Välj **[!UICONTROL Create]**

      ![Kampanjegenskaper](assets/ajo-campaign-properties.png)
1. På skärmen för Campaign-definitionen, på **[!UICONTROL Properties]**, anger du ett **[!UICONTROL Name]** för kampanjen, till exempel `Luma - In-App Messaging Campaign`, och ett **[!UICONTROL Description]**, till exempel `In-app messaging campaign for Luma app`.
   ![Kampanjnamn](assets/ajo-campaign-properties-name.png)
1. Bläddra ned till **[!UICONTROL Action]** och välj **[!UICONTROL Edit Content]**.
1. På skärmen **[!UICONTROL In-App Message]**:
   1. Välj **[!UICONTROL Modal]** som **[!UICONTROL Message Layout]**.
   2. Ange `https://luma.enablementadobe.com/content/dam/luma/en/logos/Luma_Logo.png` som **[!UICONTROL Media URL]**.
   3. Ange en **[!UICONTROL Header]**, till exempel `Welcome to this Luma In-App Message`, och ange en **[!UICONTROL Body]**, till exempel `Triggered by pushing that button in the app...`.
   4. Ange **[!UICONTROL Dismiss]** som **[!UICONTROL Button #1 text (primary)]**.
   5. Observera hur förhandsgranskningen uppdateras.
   6. Välj **[!UICONTROL Review to activate]**.

      ![Redigerare i appen](assets/ajo-in-app-editor.png)
1. På skärmen **[!UICONTROL Review to activate (Luma - In-App Messaging Campaign)]** väljer du ![Redigera](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) i rutan **[!UICONTROL Schedule]**.
   ![Välj Schema](assets/ajo-review-select-schedule.png) för granskning av schema
1. Gå tillbaka till skärmen **[!DNL Luma - In-App Messaging Campaign]** och välj ![Redigera](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) **[!UICONTROL Edit triggers]**.
1. I dialogrutan **[!UICONTROL In-app message trigger]** konfigurerar du information om spårningsåtgärden som utlöser meddelandet i appen:
   1. Om du vill ta bort **[!UICONTROL Application launch event]** väljer du ![Stäng](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Close_18_N.svg) .
   1. Använd ![Lägg till](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Add condition]** upprepade gånger för att skapa följande logik för **[!UICONTROL Show message if]**.
   1. Klicka på **[!UICONTROL Done]**.

      ![Utlösarlogik](assets/ajo-trigger-logic.png)

   Du har definierat en spårningsåtgärd där **[!UICONTROL Action]** är lika med `in-app` och **[!UICONTROL Context data]** med åtgärden är ett nyckelvärdepar på `"showMessage" : "true"`.

1. Välj **[!UICONTROL Review to activate]** på skärmen **[!DNL Luma - In-App Messaging Campaign]**.
1. Välj **[!UICONTROL Activate]** på skärmen **[!UICONTROL Review to activate (Luma - In-App Messaging Campaign)]**.
1. Du ser din **[!DNL Luma - In-App Messaging Campaign]** med status **[!UICONTROL Live]** i listan **[!UICONTROL Campaigns]**.
   ![Kampanjlista](assets/ajo-campaign-list.png)


## Utlös meddelandet i appen

Du har alla ingredienser på plats för att skicka ett meddelande i appen. Det som återstår är hur du utlöser det här meddelandet i appen i din app.

1. Gå till **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** i Xcode Project-navigatorn. Hitta funktionen `func sendTrackAction(action: String, data: [String: Any]?)` och lägg till följande kod som anropar funktionen [`MobileCore.track`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#trackaction) baserat på parametrarna `action` och `data`.


   ```swift
   // Send trackAction event
   MobileCore.track(action: action, data: data)
   ```

1. Gå till **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL ConfigView]** i Xcode Project Navigator. Sök efter koden för knappen Meddelande i appen och lägg till följande kod:

   ```swift
   // Setting parameters and calling function to send in-app message
   Task {
       MobileSDK.shared.sendTrackAction(action: "in-app", data: ["showMessage": "true"])
   }
   ```

## Validera med din app

1. Återskapa och kör appen i simulatorn eller på en fysisk enhet från Xcode med ![Play](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Play_18_N.svg).

1. Gå till fliken **[!UICONTROL Settings]**.

1. Tryck på **[!UICONTROL In-App Message]**. Meddelandet visas i appen.

   <img src="assets/ajo-in-app-message.png" width="300" />


## Validera implementering i Assurance

Du kan validera dina meddelanden i appen i Assurance-gränssnittet.

1. Granska avsnittet [installationsanvisningar](assurance.md#connecting-to-a-session) för att ansluta simulatorn eller enheten till Assurance.
1. Välj **[!UICONTROL In-App Messaging]**.
1. Välj **[!UICONTROL Event List]**.
1. Välj en **[!UICONTROL Display message]**-post.
1. Granska raw-händelsen, särskilt `html`, som innehåller den fullständiga layouten och innehållet i meddelandet i appen.
   ![Assurance-meddelande i appen](assets/assurance-in-app-display-message.png)


## Nästa steg

Nu bör du ha alla verktyg du behöver för att börja lägga till meddelanden i appen, där det är relevant och tillämpligt. Du kan till exempel marknadsföra produkter baserat på specifika interaktioner som du spårar i din app.

>[!SUCCESS]
>
>Du har aktiverat appen för meddelanden i appen och lagt till en meddelandekampanj i appen med Journey Optimizer och Journey Optimizer-tillägget för Experience Platform Mobile SDK.
>
>Tack för att du har lagt ned din tid på att lära dig om Adobe Experience Platform Mobile SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela dem i det här [Experience League Community-diskussionsinlägget](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Nästa: **[Skapa och visa erbjudanden](journey-optimizer-offers.md)**
