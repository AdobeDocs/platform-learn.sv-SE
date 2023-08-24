---
title: Adobe Journey Optimizer-meddelanden i appen
description: Lär dig hur du skapar meddelanden i appen till en mobilapp med Platform Mobile SDK och Adobe Journey Optimizer.
solution: Data Collection,Journey Optimizer
feature-set: Journey Optimizer
hide: true
source-git-commit: c3c12d63762f439faa9c45d27e66468455774b43
workflow-type: tm+mt
source-wordcount: '994'
ht-degree: 0%

---

# Adobe Journey Optimizer-meddelanden i appen

Lär dig hur du skapar meddelanden i appen för mobilappar med Platform Mobile SDK och Adobe Journey Optimizer.

Med Journey Optimizer kan ni skapa resor och skicka meddelanden i appen till riktade målgrupper. Innan du skickar meddelanden i appen med Journey Optimizer måste du se till att rätt konfigurationer och integreringar finns på plats. Om du vill veta mer om dataflödet för meddelanden i programmet i Adobe Journey Optimizer kan du läsa [dokumentationen](https://experienceleague.adobe.com/docs/journey-optimizer/using/in-app/inapp-configuration.html?lang=en).

>[!NOTE]
>
>Den här lektionen är valfri och gäller endast för Adobe Journey Optimizer-användare som vill skicka meddelanden i appen.


## Förutsättningar

* App med SDK:er har installerats och konfigurerats.
* Åtkomst till Adobe Journey Optimizer och tillräcklig behörighet enligt beskrivningen [här](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configuration-message/push-config/push-configuration.html?lang=en). Du behöver även tillräcklig behörighet för följande Adobe Journey Optimizer-funktioner.
   * Skapa en kampanj.
* Betalat Apple-utvecklarkonto med tillräcklig behörighet för att skapa certifikat, identifierare och nycklar.
* Fysisk iOS-enhet eller simulator för testning.
* [Registrerat program-ID med APN](journey-optimizer-push.md#register-app-id-with-apn)
* [Dina push-autentiseringsuppgifter för appen har lagts till i datainsamlingen](journey-optimizer-push.md#add-your-app-push-credentials-in-data-collection)
* [Tillägget Adobe Journey Optimizer-taggar har installerats](journey-optimizer-push.md#install-adobe-journey-optimizer-tags-extension)
* [Implementerat Adobe Journey Optimizer i appen](journey-optimizer-push.md#implement-adobe-journey-optimizer-in-the-app)


## Validera med Assurance

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
   1. Välj **[!UICONTROL Meddelande i appen]** och markera **[!UICONTROL Mobilappen Luma]** från **[!UICONTROL Appyta]** lista.
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

Du har alla ingredienser på plats för att skicka ett meddelande i appen. Det som återstår är hur detta meddelande i appen ska utlösas i koden.

1. Gå till Luma > Luma > Utils > MobileSDK i Xcode Project navigator och hitta `func sendTrackAction(action: String, data: [String: Any]?)` och lägg till följande kod som anropar `MobileCore.track` funktion, baserat på parametrarna `action` och `data`.


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


## Validera i försäkring

Du kan validera dina meddelanden i appen i Assurance-gränssnittet.

1. Välj **[!UICONTROL Meddelanden i appen]**.
1. Välj **[!UICONTROL Händelselista]**.
1. Välj en **[!UICONTROL Visa meddelande]** post.
1. Inspect the raw event, speciellt `html`, som innehåller den fullständiga layouten och innehållet i meddelandet i appen.
   ![Meddelande för försäkring i appen](assets/assurance-in-app-display-message.png)


## Implementera i din app

Nu bör du ha alla verktyg du behöver för att börja lägga till push-meddelanden, där det är relevant och tillämpligt, i Luma-appen. Du kan till exempel välkomna användaren när han eller hon loggar in i appen eller när han eller hon närmar sig en viss geografisk plats.

>[!SUCCESS]
>
>Du har nu aktiverat appen för meddelanden i appen och lagt till en meddelandekampanj i appen med Adobe Journey Optimizer och Adobe Journey Optimizer-tillägget för Adobe Experience Platform Mobile SDK.<br/>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Mobile SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Nästa: **[Slutsats och nästa steg](conclusion.md)**
