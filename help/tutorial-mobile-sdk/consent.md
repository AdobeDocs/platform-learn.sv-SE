---
title: Implementera medgivande för implementeringar av SDK för plattformsmobiler
description: Lär dig hur du implementerar samtycke i en mobilapp.
feature: Mobile SDK,Consent
jira: KT-14629
exl-id: 08042569-e16e-4ed9-9b5a-864d8b7f0216
source-git-commit: 008d3ee066861ea9101fe9fe99ccd0a088b63f23
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 0%

---

# Genomför samtycke

Lär dig hur du implementerar samtycke i en mobilapp.

Med mobiltillägget Adobe Experience Platform Consent kan du samla in medgivandeinställningar från din mobilapp när du använder Adobe Experience Platform Mobile SDK och Edge Network-tillägget. Läs mer om tillägget [Samtycke](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/) i dokumentationen.

## Förhandskrav

* App med SDK:er har installerats och konfigurerats.

## Utbildningsmål

I den här lektionen kommer du att:

* Fråga användaren om samtycke.
* Uppdatera tillägget baserat på användarens svar.
* Lär dig hur du får det aktuella tillståndet för samtycke.

## Be om samtycke

Om du följde självstudiekursen från början kanske du kommer ihåg att du har angett standardmedgivandet i tillägget för samtycke till **[!UICONTROL Pending - Queue events that occur before the user provides consent preferences.]**

Om du vill börja samla in data måste du få användarens samtycke. I ett verkligt program vill du gärna få information om de effektivaste strategierna för samtycke i din region. I den här självstudiekursen får du användarens samtycke genom att bara be om det med en varning:

>[!BEGINTABS]

>[!TAB iOS]

1. Du vill bara fråga användaren en gång för godkännande. Du kombinerar SDK-medgivandet för mobilen med den nödvändiga behörigheten för spårning med Apple ramverk för [appspårning och genomskinlighet](https://developer.apple.com/documentation/apptrackingtransparency). I den här appen antar du att när användaren godkänner spårning godkänner de att samla in händelser.

1. Navigera till **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** i Xcode Project-navigatorn.

   Lägg till den här koden i funktionen `updateConsent`.

   ```swift
   // Update consent
   let collectConsent = ["collect": ["val": value]]
   let currentConsents = ["consents": collectConsent]
   Consent.update(with: currentConsents)
   MobileCore.updateConfigurationWith(configDict: currentConsents)
   ```

1. Navigera till **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL DisclaimerView]** i Xcodes projektnavigerare. Xodes projektnavigerare är den vy som visas när du har installerat eller installerat om programmet och startat programmet för första gången. Användaren uppmanas att godkänna spårning enligt Apple [ramverk för appspårning av genomskinlighet](https://developer.apple.com/documentation/apptrackingtransparency). Om användaren godkänner det uppdaterar du även medgivandet.

   Lägg till följande kod i `ATTrackingManager.requestTrackingAuthorization { status in`-stängningen.

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

>[!TAB Android]

1. Du vill bara fråga användaren en gång för godkännande. I den här appen antar du att när användaren godkänner spårning godkänner de att samla in händelser.

1. Navigera till **[!UICONTROL app]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL models]** > **[!UICONTROL MobileSDK]** i Android Studio-navigatorn.

   Lägg till den här koden i funktionen `updateConsent(value: String)`.

   ```kotlin
   // Update consent
   val collectConsent = mapOf("collect" to mapOf("val" to value))
   val currentConsents = mapOf("consents" to collectConsent)
   Consent.update(currentConsents)
   MobileCore.updateConfiguration(currentConsents)
   ```

1. Navigera till **[!UICONTROL app]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL views]** > **[!UICONTROL DisclaimerView.kt]** i Android Studio-navigatorn.

   Lägg till följande kod i funktionen `DisclaimerView(navController: NavController)` under `// Set content to yes` och `// Set content to no`.

   ```kotlin
   // Add consent based on authorization
   if (status) {
      showPersonalizationWarning = false
   
      // Set consent to yes
      MobileSDK.shared.updateTrackingStatus(TrackingStatus.AUTHORIZED)
      MobileSDK.shared.updateConsent("y")
   } else {
      Toast.makeText(
            context,
            "You will not receive offers and location tracking will be disabled.",
            Toast.LENGTH_LONG
      ).show()
      showPersonalizationWarning = true
   
      // Set consent to no
      MobileSDK.shared.updateTrackingStatus(TrackingStatus.DENIED)
      MobileSDK.shared.updateConsent("n")
   }
   ```

>[!ENDTABS]

## Hämta aktuellt medgivandetillstånd

Tillägget för mobilen Consent undertrycker/häver automatiskt / tillåter spårning baserat på det aktuella medgivandevärdet. Du kan även komma åt det aktuella medgivandetillståndet själv:

>[!BEGINTABS]

>[!TAB iOS]

1. Navigera till **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** i Xcodes projektnavigerare.

   Lägg till följande kod i funktionen `getConsents`:

   ```swift
   // Get consents
   Consent.getConsents { consents, error in
      guard error == nil, let consents = consents else { return }
      guard let jsonData = try? JSONSerialization.data(withJSONObject: consents, options: .prettyPrinted) else { return }
      guard let jsonStr = String(data: jsonData, encoding: .utf8) else { return }
      Logger.aepMobileSDK.info("Consent getConsents: \(jsonStr)")
   }
   ```

2. Navigera till **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL HomeView]** i Xcodes projektnavigerare.

   Lägg till följande kod i modifieraren `.task`:

   ```swift
   // Ask status of consents
   MobileSDK.shared.getConsents()   
   ```

I exemplet ovan loggar du bara medgivandestatus till konsolen i Xcode. I ett verkligt scenario kan du använda det för att ändra vilka menyer eller alternativ som visas för användaren.

>[!TAB Android]

1. Navigera till **[!UICONTROL app]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL models]** > **[!UICONTROL MobileSDK]** i Android Studio-navigatorn.

   Lägg till följande kod i funktionen `getConsents()`:

   ```kotlin
   // Get consents
   Consent.getConsents { callback ->
      if (callback != null) {
            val jsonStr = JSONObject(callback).toString(4)
            Log.i("MobileSDK", "Consent getConsents: $jsonStr")
      }
   }
   ```

1. Navigera till **[!UICONTROL app]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL views]** > **[!UICONTROL HomeView.kt]** i Android Studio-navigatorn.

   Lägg till följande kod i `LaunchedEffect(unit)`:

   ```kotlin
   // Ask status of consents
   MobileSDK.shared.getConsents()   
   ```

I ovanstående exempel loggar du bara medgivandestatus till konsolen i Android Studio. I ett verkligt scenario kan du använda det för att ändra vilka menyer eller alternativ som visas för användaren.

>[!ENDTABS]

## Validera med Assurance

1. Ta bort programmet från enheten eller simulatorn för att återställa och initiera spårning och samtycke på rätt sätt.
1. Om du vill ansluta simulatorn eller enheten till Assurance går du igenom avsnittet [installationsanvisningar](assurance.md#connecting-to-a-session).
1. När du flyttar appen från skärmen **[!UICONTROL Home]** till skärmen **[!UICONTROL Products]** och tillbaka till skärmen **[!UICONTROL Home]** bör du se en **[!UICONTROL Get Consents Response]** -händelse i Assurance-gränssnittet.
   ![validera samtycke](assets/consent-update.png){zoomable="yes"}


>[!SUCCESS]
>
>Du har nu aktiverat appen så att användaren vid den första starten efter installationen (eller ominstallationen) kan godkänna med hjälp av Adobe Experience Platform Mobile SDK.
>
>Tack för att du har lagt ned din tid på att lära dig om Adobe Experience Platform Mobile SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela dem i det här [Experience League Community-diskussionsinlägget](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Nästa: **[Samla in livscykeldata](lifecycle-data.md)**
