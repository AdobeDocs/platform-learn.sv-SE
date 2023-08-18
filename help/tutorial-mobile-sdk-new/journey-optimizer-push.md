---
title: Adobe Journey Optimizer push-meddelanden
description: Lär dig skapa push-meddelanden till en mobilapp med Platform Mobile SDK och Adobe Journey Optimizer.
solution: Data Collection,Journey Optimizer
feature-set: Journey Optimizer
feature: Push
hide: true
hidefromtoc: true
source-git-commit: ca83bbb571dc10804adcac446e2dba4fda5a2f1d
workflow-type: tm+mt
source-wordcount: '942'
ht-degree: 0%

---

# Adobe Journey Optimizer push-meddelanden

Lär dig skapa push-meddelanden för mobilappar med Platform Mobile SDK och Adobe Journey Optimizer.

Med Journey Optimizer kan ni skapa resor och skicka meddelanden till riktade målgrupper. Innan du skickar push-meddelanden med Journey Optimizer måste du se till att rätt konfigurationer och integreringar finns på plats. Om du vill veta mer om dataflödet för push-meddelanden i Adobe Journey Optimizer går du till [dokumentationen](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configuration-message/push-config/push-gs.html).

>[!NOTE]
>
>Den här lektionen är valfri och gäller endast för Adobe Journey Optimizer-användare som vill skicka push-meddelanden.


## Förutsättningar

* App med SDK:er har installerats och konfigurerats.
* Åtkomst till Adobe Journey Optimizer och tillräcklig behörighet enligt beskrivningen [här](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configuration-message/push-config/push-configuration.html?lang=en). Du behöver även tillräcklig behörighet för följande Adobe Journey Optimizer-funktioner.
   * Skapa en appyta.
   * Skapa en resa
   * Skapa ett meddelande.
   * Skapa meddelandeförinställningar.
* Betalat Apple-utvecklarkonto med tillräcklig behörighet för att skapa certifikat, identifierare och nycklar.
* Fysisk iOS-enhet för testning.

## Utbildningsmål

I den här lektionen kommer du att:

* Registrera program-ID med Apple Push Notification service (APN).
* Skapa en **[!UICONTROL Appyta]** i AJO.
* Uppdatera dina **[!UICONTROL schema]** för att inkludera push-meddelandefält.
* Installera och konfigurera **[!UICONTROL Adobe Journey Optimizer]** taggtillägg.
* Uppdatera programmet så att det innehåller AJO-taggtillägget.
* Validera inställningar i Assurance.
* Skicka ett testmeddelande.


## Registrera program-ID med APN

Följande steg är inte Adobe Experience Cloud-specifika och har utformats för att vägleda dig genom APN-konfigurationen.

### Skapa en privat nyckel

1. Gå till Apple utvecklarportal **[!UICONTROL Tangenter]**.
1. Om du vill skapa en nyckel väljer du **[!UICONTROL +]**.
   ![skapa ny nyckel](assets/mobile-push-apple-dev-new-key.png)

1. Ange en **[!UICONTROL Nyckelnamn]**.
1. Välj **[!UICONTROL APN]** kryssrutan.
1. Välj **[!UICONTROL Fortsätt]**.
   ![konfigurera ny nyckel](assets/mobile-push-apple-dev-config-key.png)
1. Granska konfigurationen och välj **[!UICONTROL Registrera]**.
1. Ladda ned `.p8` privat nyckel. Den används i appytskonfigurationen.
1. Anteckna [!UICONTROL Nyckel-ID]. Den används i appytskonfigurationen.
1. Anteckna [!UICONTROL Team-ID]. Den används i appytskonfigurationen.
   ![Nyckelinformation](assets/push-apple-dev-key-details.png)

Ytterligare dokumentation kan [hittades här](https://help.apple.com/developer-account/#/devcdfbb56a3).

## Lägg till push-autentiseringsuppgifter för appen i datainsamlingen

1. Från [Gränssnitt för datainsamling](https://experience.adobe.com/data-collection/), markera **[!UICONTROL Appytor]** till vänster.
1. Om du vill skapa en konfiguration väljer du **[!UICONTROL Skapa appytor]**.
   ![app surface home](assets/push-app-surface.png)
1. Ange en **[!UICONTROL Namn]** för konfigurationen, till exempel `Luma App Tutorial`  .
1. Från Mobile Application Configuration (Konfigurera mobilprogram) väljer du **[!UICONTROL Apple iOS]**.
1. Ange mobilappens paket-ID i fältet Program-ID (iOS Bundle-ID). Om du följer med i Luma-appen är värdet `com.adobe.luma.tutorial.swiftui`.
1. Aktivera **[!UICONTROL Push-autentiseringsuppgifter]** för att lägga till dina inloggningsuppgifter.
1. Dra och släpp `.p8` **Autentiseringsnyckel för push-meddelanden i Apple** -fil.
1. Ange **[!UICONTROL Nyckel-ID]**, en sträng med 10 tecken som tilldelas när `p8` auth key. Den finns under **[!UICONTROL Tangenter]** tabba in **Certifikat, identifierare och profiler** på Apple Developer Portal.
1. Ange **[!UICONTROL Team-ID]**. Team-ID är ett värde som finns under **medlemskap** eller högst upp på Apple Developer Portal-sidorna.
1. Välj **[!UICONTROL Spara]**.

   ![appytans konfiguration](assets/push-app-surface-config.png)

## Installera tillägget Adobe Journey Optimizer-taggar

1. Navigera till **[!UICONTROL Taggar]** > **[!UICONTROL Tillägg]** > **[!UICONTROL Katalog]**,
1. Öppna egenskapen, till exempel **[!UICONTROL Luma Mobile App Tutorial]**.
1. Välj **[!UICONTROL Katalog]**.
1. Sök efter **[!UICONTROL Adobe Journey Optimizer]** tillägg.
1. Installera tillägget.
1. I **[!UICONTROL Installera tillägg]** dialog
   1. Välj en miljö, till exempel **[!UICONTROL Utveckling]**.
   1. Välj **[!UICONTROL AJO Push Tracking Experience, händelsedatauppsättning]** datauppsättning från **[!UICONTROL Händelsedatauppsättning]** listruta.
      ![Inställningar för AJO-tillägg](assets/push-tags-ajo.png)
   1. Välj **[!UICONTROL Spara i bibliotek och bygge]**.

>[!NOTE]
>
>Om du inte ser `AJO Push Tracking Experience Event Dataset` som ett alternativ, kontakta kundtjänst.
>

## Implementera Adobe Journey Optimizer i appen

Som tidigare nämnts tillhandahåller installation av ett mobiltaggtillägg bara konfigurationen. Därefter måste du installera och registrera SDK för meddelanden. Om de här stegen inte är tydliga går du igenom [Installera SDK:er](install-sdks.md) -avsnitt.

>[!NOTE]
>
>Om du har slutfört [Installera SDK:er](install-sdks.md) är SDK redan installerat och du kan hoppa till steg 7.
>

1. I Xcode kontrollerar du att [AEP Messaging](https://github.com/adobe/aepsdk-messaging-ios.git) läggs till i listan över paket i paketberoenden. Se [Swift Package Manager](install-sdks.md#swift-package-manager).
1. Öppna Xcode och navigera till **[!UICONTROL AppDelegate]**.
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

1. Lägg till `MobileCore.setPushIdentifier` till `application(_, didRegisterForRemoteNotificationsWithDeviceToken)` funktion.

   ```swift {highlight="7"}
   func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
       // Required to log the token
       let tokenParts = deviceToken.map { data in String(format: "%02.2hhx", data) }
       let token = tokenParts.joined()
       Logger.notifications.info("didRegisterForRemoteNotificationsWithDeviceToken - device token: \(token)")
   
       // Send push token to Experience Platform
       MobileCore.setPushIdentifier(deviceToken)
       currentDeviceToken = token
   }
   ```

   Den här funktionen hämtar den enhetstoken som är unik för den enhet som appen är installerad på och skickar token till Adobe Apple för push-meddelandeleverans.

## Validera genom att skicka ett push-testmeddelande

1. Granska [installationsanvisningar](assurance.md) -avsnitt.
1. Installera appen på den fysiska enheten eller i simulatorn.
1. Starta appen med den URL som skapas av försäkringen.
1. Välj **[!UICONTROL Konfigurera]**.
   ![konfigurera klicka](assets/push-validate-config.png)
1. Välj ![Plus](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) knapp bredvid **[!UICONTROL Push-felsökning]**.
1. Välj **[!UICONTROL Spara]**.
   ![spara](assets/push-validate-save.png)
1. Välj **[!UICONTROL Push-felsökning]** från vänster navigering.
1. Välj **[!UICONTROL Validera inställningar]** -fliken.
1. Välj din enhet från **[!UICONTROL Klient]** lista.
1. Bekräfta att inga fel visas.
   ![validera](assets/push-validate-confirm.png)
1. Välj **[!UICONTROL Skicka testöverföring]** -fliken.
1. (valfritt) Ändra standardinformationen för **[!UICONTROL Titel]** och **[!UICONTROL Brödtext]**
1. Välj ![Fel](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Bug_18_N.svg) **[!UICONTROL Skicka meddelande om testpush]**.
1. Kontrollera **[!UICONTROL Testresultat]**.
1. Du bör se push-meddelandet i din app.

   <img src="assets/luma-app-push.png" width="300" />


>[!SUCCESS]
>
>Du har nu aktiverat appen för push-meddelanden med Adobe Journey Optimizer-tillägget för Adobe Experience Platform Mobile SDK.<br/>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Mobile SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Nästa: **[Slutsats och nästa steg](conclusion.md)**
