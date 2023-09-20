---
title: Ställ in försäkring
description: Lär dig hur du implementerar tillägget Assurance i en mobilapp.
feature: Mobile SDK,Assurance
hide: true
source-git-commit: 5f178f4bd30f78dff3243b3f5bd2f9d11c308045
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 0%

---

# Ställ in försäkring

Lär dig hur du konfigurerar Adobe Experience Platform Assurance i en mobilapp.

Assurance, som formellt kallas Project Griffon, är utformat för att hjälpa er att inspektera, verifiera, simulera och validera hur ni samlar in data eller levererar upplevelser i er mobilapp.

Med Assurance kan du inspektera SDK-råhändelser som genererats av Adobe Experience Platform Mobile SDK. Alla händelser som samlas in av SDK är tillgängliga för inspektion. SDK-händelser läses in i en listvy, sorterade efter tid. Varje händelse har en detaljerad vy som ger mer information. Det finns även ytterligare vyer för att bläddra bland SDK-konfigurationer, dataelement, delade lägen och SDK-tilläggsversioner. Läs mer om [Säkerhet](https://experienceleague.adobe.com/docs/experience-platform/assurance/home.html) i produktdokumentationen.


## Förutsättningar

* Appen har konfigurerats med SDK:er installerade och konfigurerade.

## Utbildningsmål

I den här lektionen kommer du att:

* Bekräfta att din organisation har åtkomst (och begär det om du inte har det).
* Ange din bas-URL.
* Lägg till nödvändig iOS-specifik kod.
* Anslut till en session.

## Bekräfta åtkomst

Bekräfta att din organisation har åtkomst till Assurance. Som användare bör du läggas till i profilen för Adobe Experience Platform. Se [Användaråtkomst](https://experienceleague.adobe.com/docs/experience-platform/assurance/user-access.html?lang=en) i Assurance-guiden för mer information.

## Implementera

Förutom det allmänna [SDK-installation](install-sdks.md), som du slutförde i den tidigare lektionen, behöver iOS även följande tillägg för att starta Assurance-sessionen för din app.

1. Navigera till **[!DNL Luma]** > **[!DNL Luma]** > **[!UICONTROL SceneDelegate]** i Xcodes projektnavigerare.

1. Lägg till följande kod i `func scene(_ scene: UIScene, openURLContexts URLContexts: Set<UIOpenURLContext>`:

   ```swift
   // Called when the app in background is opened with a deep link.
   if let deepLinkURL = URLContexts.first?.url {
       // Start the Assurance session
       Assurance.startSession(url: deepLinkURL)
   }
   ```

   Den här koden startar en säkringssession när appen finns i bakgrunden och öppnas via en djuplänk.

Mer information finns [här](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/api-reference/){target="_blank"}.

## Signering

Innan du kör programmet för första gången i Xcode måste du uppdatera signeringen.

1. Öppna projektet i Xcode.
1. Välj **[!DNL Luma]** i projektnavigatorn.
1. Välj **[!DNL Luma]** mål.
1. Välj **Signering och funktioner** -fliken.
1. Konfigurera **[!UICONTROL Hantera signering automatiskt]**, **[!UICONTROL Team]** och **[!UICONTROL Paketidentifierare]** eller använd dina specifika Apple-utvecklingskonfigurationer.

   >[!IMPORTANT]
   >
   >Se till att du använder en unik källidentifierare som skiljer sig från standardinställningen `com.adobe.luma.tutorial.swiftui`  anges i Start-projektet eftersom varje källidentifierare måste vara unik.


   ![Xcode-signeringsfunktioner](assets/xcode-signing-capabilities.png){zoomable=&quot;yes&quot;}

## Konfigurera en bas-URL

1. Gå till projektet i Xcode.
1. Välj **[!DNL Luma]** i projektnavigatorn.
1. Välj **[!DNL Luma]** mål.
1. Välj **Info** -fliken.
1. Bläddra nedåt till om du vill lägga till en bas-URL **URL-typer** och väljer **+** -knappen.
1. Ange **Identifierare** till den paketidentifierare som du konfigurerade i [Signering](#signing) (till exempel `com.adobe.luma.tutorial.swiftui`) och ange en **URL-scheman**, till exempel `lumatutorialswiftui`.

   ![försäkrings-URL](assets/assurance-url-type.png)

Mer information om URL-scheman i iOS finns i [Apple dokumentation](https://developer.apple.com/documentation/xcode/defining-a-custom-url-scheme-for-your-app){target="_blank"}.

Assurance fungerar genom att öppna en URL, antingen via webbläsaren eller QR-koden. Den URL:en börjar med den bas-URL som öppnar appen och innehåller ytterligare parametrar. Dessa unika parametrar används för att ansluta sessionen.


## Ansluta till en session

1. Kör programmet i simulatorn eller på en ansluten fysisk enhet.
1. Välj **[!UICONTROL Säkerhet]** från den vänstra listen i användargränssnittet för datainsamling.
1. Välj **[!UICONTROL Skapa session]**.
1. Välj **[!UICONTROL Starta]**.
1. Ange en **[!UICONTROL Sessionsnamn]** som `Luma Mobile App Session` och **[!UICONTROL Bas-URL]**, som är det URL-schema som du angav i Xcode, följt av `://` Till exempel: `lumatutorialswiftui://`
1. Välj **[!UICONTROL Nästa]**.
   ![skapa trygghet, session](assets/assurance-create-session.png)
1. I **[!UICONTROL Skapa ny session]** modal dialog:

   Om du använder en fysisk enhet:

   * Välj **[!UICONTROL Skanna QR-kod]**. Använd kameran på din fysiska enhet för att skanna QR-koden och tryck på länken för att öppna appen.

     ![qa-kod för försäkring](assets/assurance-qr-code.png)

   Om du använder en simulator:

   1. Välj **[!UICONTROL Kopiera länk]**.
   1. Kopiera den djupa länken med ![Kopiera](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg)  och använd länken till att öppna appen med Safari i simulatorn.
      ![Länk till Assurance-kopia](assets/assurance-copy-link.png)

1. När appen läses in visas en modal dialogruta där du ombeds ange den PIN-kod som visas i steg 7.

   <img src="assets/assurance-enter-pin.png" width="300">

   Ange PIN-koden och välj **[!UICONTROL Anslut]**.


1. Om anslutningen lyckades ser du:
   * En säkerhetsikon visas ovanpå din app.

     <img src="assets/assurance-modal.png" width="300">

   * Uppdateringar från Experience Cloud i försäkringsgränssnittet som visar:

      1. Experience Events kommer från appen.
      1. Information om en markerad händelse.
      1. Enheten och tidslinjen.

         ![säkringshändelser](assets/assurance-events.png)

Om du stöter på några problem kan du läsa [teknisk](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/){target="_blank"} and [general documentation](https://experienceleague.adobe.com/docs/experience-platform/assurance/home.html){target="_blank"}.

>[!SUCCESS]
>
>Du har nu konfigurerat din app att använda Assurance för resten av självstudiekursen.<br/>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Mobile SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela med dig av dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)


Nästa: **[Implementera medgivande](consent.md)**
