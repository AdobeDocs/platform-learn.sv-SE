---
title: Godkännande
description: Lär dig hur du implementerar samtycke i en mobilapp.
feature: Mobile SDK,Consent
hide: true
source-git-commit: 1b09f81b364fe8cfa9d5d1ac801d7781d1786259
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 0%

---

# Godkännande

Lär dig hur du implementerar samtycke i en mobilapp.

Med mobiltillägget Adobe Experience Platform Consent kan du samla in medgivandeinställningar från din mobilapp när du använder Adobe Experience Platform Mobile SDK och Edge Network-tillägget. Läs mer om [Godkänn tillägg](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/), i dokumentationen.

## Förutsättningar

* App med SDK:er har installerats och konfigurerats.

## Utbildningsmål

I den här lektionen kommer du att:

* Fråga användaren om samtycke.
* Uppdatera tillägget baserat på användarens svar.
* Lär dig hur du får det aktuella tillståndet för samtycke.

## Be om samtycke

Om du följde självstudiekursen från början kanske du kommer ihåg att du har angett standardmedgivandet i tillägget Godkännande till **[!UICONTROL Väntande - Köa händelser som inträffar innan användaren ger sitt medgivande.]**

Om du vill börja samla in data måste du få användarens samtycke. I den här självstudiekursen får du användarens samtycke genom att bara be om det med en varning. I ett verkligt program vill du gärna få information om de effektivaste strategierna för samtycke i din region.

1. Du vill bara fråga användaren en gång. Så du vill kombinera det mobila SDK-medgivandet med de behörigheter som krävs för att spåra med Apple [App Tracking Transparency Framework](https://developer.apple.com/documentation/apptrackingtransparency). I den här appen antar du när användaren godkänner spårning att användaren också samtycker till att samla in händelser.

1. Navigera till **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Utils]** > **[!UICONTROL MobileSDK]** i Xcode Project-navigatorn.

   Lägg till den här koden i `updateConsent` funktion.

   ```swift
   // Update consent
   let collectConsent = ["collect": ["val": value]]
   let currentConsents = ["consents": collectConsent]
   Consent.update(with: currentConsents)
   MobileCore.updateConfigurationWith(configDict: currentConsents)
   ```

1. Navigera till **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Vyer]** > **[!UICONTROL Allmänt]** > **[!UICONTROL AnsvarsfriskrivningVisa]** i Xcodes projektnavigerare, som är den vy som visas när du har installerat eller installerat om programmet och startat programmet för första gången. Användaren uppmanas att godkänna spårning per Apple [App Tracking Transparency Framework](https://developer.apple.com/documentation/apptrackingtransparency). Om användaren godkänner det uppdaterar du även medgivandet.

   Lägg till följande kod i `ATTrackingManager.requestTrackingAuthorization { status in` stängning.

   ```swift
   // Add consent based on authorization
   if status == .authorized {
      // Set consent to yes
      MobileSDK.shared.updateConsent(value: "y")
   }
   else {
      // Set consent to yes
      MobileSDK.shared.updateConsent(value: "n")
   }
   ```

## Hämta aktuellt medgivandetillstånd

Tillägget för mobilen Consent undertrycker/häver automatiskt / tillåter spårning baserat på det aktuella medgivandevärdet. Du kan även komma åt det aktuella medgivandetillståndet själv:

1. Navigera till **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Utils]** > **[!UICONTROL MobileSDK]** i Xcodes projektnavigator.

   Lägg till följande kod i `getConsents` funktion:

   ```swift
   // Get consents
   Consent.getConsents { consents, error in
      guard error == nil, let consents = consents else { return }
      guard let jsonData = try? JSONSerialization.data(withJSONObject: consents, options: .prettyPrinted) else { return }
      guard let jsonStr = String(data: jsonData, encoding: .utf8) else { return }
      Logger.aepMobileSDK.info("Consent getConsents: \(jsonStr)")
   }
   ```

2. Navigera till **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Vyer]** > **[!UICONTROL Allmänt]** > **[!UICONTROL HomeView]** i Xcodes projektnavigator.

   Lägg till följande kod i `.task` modifierare:

   ```swift
   // Ask status of consents
   MobileSDK.shared.getConsents()   
   ```

I exemplet ovan loggar du bara medgivandestatus till konsolen i Xcode. I ett verkligt scenario kan du använda det för att ändra vilka menyer eller alternativ som visas för användaren.

## Validera med Assurance

1. Granska [Säkerhet](assurance.md) lektion.
1. Installera programmet.
1. Starta programmet med den Assurance-genererade URL:en.
1. Om du har lagt till ovanstående kod korrekt uppmanas du att ge ditt medgivande.

   Välj **[!UICONTROL Fortsätt...]** och sedan **[!UICONTROL Tillåt]**.

   <img src="./assets/consent-update-1.png" width="300" /> 
   <img src="./assets/consent-update-2.png" width="300" />

1. Du borde se en **[!UICONTROL Få svar på innehåll]** -händelse i Assurance-gränssnittet.
   ![validera samtycke](assets/consent-update.png)



>[!SUCCESS]
>
>Du har nu aktiverat appen så att användaren vid den första starten efter installationen (eller ominstallationen) kan godkänna med hjälp av Adobe Experience Platform Mobile SDK.<br/>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Mobile SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Nästa: **[Samla in livscykeldata](lifecycle-data.md)**
