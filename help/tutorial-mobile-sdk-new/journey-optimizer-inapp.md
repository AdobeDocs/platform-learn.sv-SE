---
title: Skapa och skicka meddelanden i appen
description: Lär dig hur du skapar och skickar meddelanden i appen till en mobilapp med Platform Mobile SDK och Adobe Journey Optimizer.
solution: Data Collection,Journey Optimizer
feature-set: Journey Optimizer
feature: In App
hide: true
exl-id: 6cb4d031-6172-4a84-b717-e3a1f5dc7d5d
source-git-commit: d1338390986a242c91051e94134f8d69e979c0b4
workflow-type: tm+mt
source-wordcount: '1536'
ht-degree: 0%

---

# Skapa och skicka meddelanden i appen

Lär dig skapa meddelanden i appen för mobilappar med Experience Platform Mobile SDK och Journey Optimizer.

Med Journey Optimizer kan ni skapa kampanjer för att skicka meddelanden i appen till riktade målgrupper. Kampanjer i Journey Optimizer används för att leverera engångsinnehåll till en viss målgrupp via olika kanaler. Med kampanjer utförs åtgärder samtidigt, antingen omedelbart eller baserat på ett angivet schema. Vid användning av resor (se [Journey Optimizer push-meddelanden](journey-optimizer-push.md) lektion) utförs åtgärderna i följd.

![Arkitektur](assets/architecture-ajo.png)

Innan du skickar meddelanden i appen med Journey Optimizer måste du se till att rätt konfigurationer och integreringar finns på plats. Om du vill veta mer om dataflödet för meddelanden i programmet i Journey Optimizer kan du läsa [dokumentationen](https://experienceleague.adobe.com/docs/journey-optimizer/using/in-app/inapp-configuration.html?lang=en).

>[!NOTE]
>
>Den här lektionen är valfri och gäller endast för Journey Optimizer-användare som vill skicka meddelanden i appen.


## Förutsättningar

* App med SDK:er har installerats och konfigurerats.
* Konfigurera appen för Adobe Experience Platform.
* Åtkomst till Journey Optimizer och tillräcklig behörighet enligt beskrivningen [här](https://experienceleague.adobe.com/docs/journey-optimizer/using/push/push-config/push-configuration.html). Du behöver även tillräcklig behörighet för följande Journey Optimizer-funktioner.
   * Hantera kampanjer.
* Fysisk iOS-enhet eller simulator för testning.


## Utbildningsmål

I den här lektionen ska du

* Skapa en appyta i AJO.
* Installera och konfigurera taggtillägget för Journey Optimizer.
* Uppdatera appen för att registrera Journey Optimizer-taggtillägget.
* Validera inställningar i Assurance.
* Definiera er egen kampanj och upplevelse av meddelanden i appen i Journey Optimizer.
* Skicka ditt eget meddelande i appen inifrån appen.

## Inställningar

>[!TIP]
>
>Om du har konfigurerat miljön redan som en del av [Journey Optimizer push-meddelanden](journey-optimizer-push.md) kan du redan ha utfört några av stegen i det här inställningsavsnittet.


### Lägg till en appyta i datainsamling

1. Från [Gränssnitt för datainsamling](https://experience.adobe.com/data-collection/), markera **[!UICONTROL Appytor]** till vänster.
1. Om du vill skapa en konfiguration väljer du **[!UICONTROL Skapa appyta]**.
   ![app surface home](assets/push-app-surface.png)
1. Ange en **[!UICONTROL Namn]** för konfigurationen, till exempel `Luma App Tutorial`  .
1. Från **[!UICONTROL Konfiguration av mobilprogram]**, markera **[!UICONTROL Apple iOS]**.
1. Ange programpaket-ID för mobilappen i **[!UICONTROL Program-ID (iOS Bundle-ID)]** fält. Exempel,  `com.adobe.luma.tutorial.swiftui`.
1. Välj **[!UICONTROL Spara]**.

   ![appytans konfiguration](assets/push-app-surface-config-inapp.png)

### Uppdatera datastream-konfiguration

Uppdatera Experience Edge-konfigurationen för att säkerställa att data som skickas från din mobilapp till Edge Network vidarebefordras till Journey Optimizer.



1. I gränssnittet för datainsamling väljer du **[!UICONTROL Datastreams]** och välj till exempel din datastream **[!DNL Luma Mobile App]**.
1. Välj ![Mer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MoreSmallList_18_N.svg) for **[!UICONTROL Experience Platform]** och markera ![Redigera](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) **[!UICONTROL Redigera]** på snabbmenyn.
1. I **[!UICONTROL Datastreams]** > ![Mapp](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) >  **[!UICONTROL Adobe Experience Platform]** skärm, se **[!UICONTROL Adobe Journey Optimizer]** är markerat. Se [Adobe Experience Platform-inställningar](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=en#aep) för mer information.
1. Om du vill spara din datastream-konfiguration väljer du **[!UICONTROL Spara]**.


   ![AEP-konfiguration för datastream](assets/datastream-aep-configuration.png)


### Installera tillägget Journey Optimizer-taggar

För att din app ska fungera med Journey Optimizer måste du uppdatera din taggegenskap.

1. Navigera till **[!UICONTROL Taggar]** > **[!UICONTROL Tillägg]** > **[!UICONTROL Katalog]**.
1. Öppna egenskapen, till exempel **[!DNL Luma Mobile App Tutorial]**.
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

1. I Xcode kontrollerar du att [AEP Messaging](https://github.com/adobe/aepsdk-messaging-ios) läggs till i listan över paket i paketberoenden. Se [Swift Package Manager](install-sdks.md#swift-package-manager).
1. Navigera till **[!DNL Luma]** > **[!DNL Luma]** > **[!UICONTROL AppDelegate]** i Xcode Project-navigatorn.
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


## Validera inställningar med Assurance

1. Granska [installationsanvisningar](assurance.md#connecting-to-a-session) för att ansluta simulatorn eller enheten till Assurance.
1. Välj **[!UICONTROL Konfigurera]**.
   ![konfigurera klicka](assets/push-validate-config.png)
1. Välj ![Plus](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) knapp bredvid **[!UICONTROL Meddelanden i appen]**.
1. Välj **[!UICONTROL Spara]**.
   ![spara](assets/assurance-in-app-config.png)
1. Välj **[!UICONTROL Meddelanden i appen]** från vänster navigering.
1. Välj **[!UICONTROL Validering]** -fliken. Bekräfta att inga fel visas.

   ![Validering i appen](assets/assurance-in-app-validate.png)


## Skapa ett eget meddelande i appen

Om du vill skapa ett eget meddelande i appen måste du definiera en kampanj i Journey Optimizer som utlöser ett meddelande i appen baserat på händelser som inträffar. Dessa händelser kan vara:

* data som skickas till Adobe Experience Platform,
* viktiga spårningshändelser, som åtgärd, eller tillstånd eller insamling av PII-data, via de allmänna API:erna för Mobile Core,
* livscykelhändelser, som start, installation, uppgradering, stängning eller krasch,
* geopositioneringshändelser, som att ange eller avsluta en intressepunkt.

I den här självstudiekursen kommer du att använda de allmänna och tilläggsoberoende API:erna för Mobile Core (se [Generiska API:er för Mobile Core](https://developer.adobe.com/client-sdks/documentation/mobile-core/#mobile-core-generic-apis)) för att underlätta händelsespårning av användarskärmar, åtgärder och PII-data. Händelser som genereras av dessa API:er publiceras till SDK-händelsehubben och kan användas av tillägg. SDK-händelsehubben tillhandahåller den grundläggande datastruktur som är knuten till alla SDK-tillägg för Mobile Platform, med en lista över registrerade tillägg och interna moduler, en lista över registrerade händelseavlyssnare och en delad tillståndsdatabas.

SDK-händelsehubben publicerar och tar emot händelsedata från registrerade tillägg för att förenkla integreringen med Adobe och tredjepartslösningar. När tillägget Optimera installeras hanteras till exempel alla förfrågningar och interaktioner med erbjudandemotorn Journey Optimizer - Beslutshantering av händelsehubben.

1. I användargränssnittet för Journey Optimizer väljer du **[!UICONTROL Kampanjer]** från den vänstra listen.
1. Välj **[!UICONTROL Skapa kampanj]**.
1. I **[!UICONTROL Skapa kampanj]** skärm:
   1. Välj **[!UICONTROL Meddelande i appen]** och välj en appyta på **[!UICONTROL Appyta]** lista, till exempel **[!DNL Luma Mobile App]**.
   1. Välj **[!UICONTROL Skapa]**
      ![Kampanjegenskaper](assets/ajo-campaign-properties.png)
1. På skärmen för Campaign-definitionen, på **[!UICONTROL Egenskaper]**, ange **[!UICONTROL Namn]** för kampanjen, till exempel `Luma - In-App Messaging Campaign`och en **[!UICONTROL Beskrivning]**, till exempel `In-app messaging campaign for Luma app`.
   ![Kampanjnamn](assets/ajo-campaign-properties-name.png)
1. Bläddra nedåt till **[!UICONTROL Åtgärd]** och markera **[!UICONTROL Redigera innehåll]**.
1. I **[!UICONTROL Meddelande i appen]** skärm:
   1. Välj **[!UICONTROL Modal]** som **[!UICONTROL Meddelandelayout]**.
   2. Retur `https://luma.enablementadobe.com/content/dam/luma/en/logos/Luma_Logo.png` för **[!UICONTROL Media-URL]**.
   3. Ange en **[!UICONTROL Sidhuvud]**, till exempel `Welcome to this Luma In-App Message` och ange **[!UICONTROL Brödtext]**, till exempel `Triggered by pushing that button in the app...`.
   4. Retur **[!UICONTROL Avvisa]** som **[!UICONTROL Knapp 1 text (primär)]**.
   5. Observera hur förhandsgranskningen uppdateras.
   6. Välj **[!UICONTROL Granska för aktivering]**.
      ![Redigerare i appen](assets/ajo-in-app-editor.png)
1. I **[!UICONTROL Granska för att aktivera (Luma - Meddelandekampanj i appen)]** skärm, välja ![Redigera](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) i **[!UICONTROL Schema]** platta.
   ![Välj Schema för granskning](assets/ajo-review-select-schedule.png)
1. Tillbaka i **[!DNL Luma - In-App Messaging Campaign]** skärm, välja ![Redigera](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) **[!UICONTROL Redigera utlösare]**.
1. I **[!UICONTROL Meddelandeutlösare i appen]** konfigurerar du information om den spårningsåtgärd som utlöser meddelandet i appen:
   1. Ta bort **[!UICONTROL Programstarthändelse]**, markera ![Stäng](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Close_18_N.svg) .
   1. Använd ![Lägg till](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Lägg till villkor]** att skapa följande logik för **[!UICONTROL Visa meddelande om]**.
   1. Klicka **[!UICONTROL Klar]**.
      ![Utlösarlogik](assets/ajo-trigger-logic.png)

   Du har definierat en spårningsåtgärd, där **[!UICONTROL Åtgärd]** är lika med `in-app` och **[!UICONTROL Kontextdata]** med funktionsmakrot är ett nyckelvärdepar med `"showMessage" : "true"`.

1. Tillbaka i **[!DNL Luma - In-App Messaging Campaign]** skärm, välja **[!UICONTROL Granska för aktivering]**.
1. I **[!UICONTROL Granska för att aktivera (Luma - Meddelandekampanj i appen)]** skärm, välja **[!UICONTROL Aktivera]**.
1. Du ser **[!DNL Luma - In-App Messaging Campaign]** med status **[!UICONTROL Live]** i **[!UICONTROL Kampanjer]** lista.
   ![Kampanjlista](assets/ajo-campaign-list.png)


## Utlös meddelandet i appen

Du har alla ingredienser på plats för att skicka ett meddelande i appen. Det som återstår är hur du utlöser det här meddelandet i appen i din app.

1. Gå till **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** i Xcode Project-navigatorn. Hitta `func sendTrackAction(action: String, data: [String: Any]?)` och lägg till följande kod som anropar [`MobileCore.track`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#trackaction) funktion, baserat på parametrarna `action` och `data`.


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

1. Återskapa och kör appen i simulatorn eller på en fysisk enhet från Xcode med ![Spela upp](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Play_18_N.svg).

1. Gå till **[!UICONTROL Inställningar]** -fliken.

1. Tryck **[!UICONTROL Meddelande i appen]**. Meddelandet visas i appen.

   <img src="assets/ajo-in-app-message.png" width="300" />


## Validera implementering i Assurance

Du kan validera dina meddelanden i appen i Assurance-gränssnittet.

1. Granska [installationsanvisningar](assurance.md#connecting-to-a-session) för att ansluta simulatorn eller enheten till Assurance.
1. Välj **[!UICONTROL Meddelanden i appen]**.
1. Välj **[!UICONTROL Händelselista]**.
1. Välj en **[!UICONTROL Visa meddelande]** post.
1. Inspect the raw event, speciellt `html`, som innehåller den fullständiga layouten och innehållet i meddelandet i appen.
   ![Meddelande för försäkring i appen](assets/assurance-in-app-display-message.png)


## Nästa steg

Nu bör du ha alla verktyg du behöver för att börja lägga till meddelanden i appen, där det är relevant och tillämpligt. Du kan till exempel marknadsföra produkter baserat på specifika interaktioner som du spårar i din app.

>[!SUCCESS]
>
>Du har aktiverat appen för meddelanden i appen och lagt till en meddelandekampanj i appen med Journey Optimizer och Journey Optimizer-tillägget för Experience Platform Mobile SDK.
>
>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Mobile SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Nästa: **[Skapa och visa erbjudanden](journey-optimizer-offers.md)**
