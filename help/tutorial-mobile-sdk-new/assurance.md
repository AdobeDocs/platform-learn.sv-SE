---
title: Ställ in försäkring
description: Lär dig hur du implementerar tillägget Assurance i en mobilapp.
feature: Mobile SDK,Assurance
hide: true
hidefromtoc: true
source-git-commit: ca83bbb571dc10804adcac446e2dba4fda5a2f1d
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 0%

---

# Säkerhet

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

Bekräfta att din organisation har åtkomst till Assurance genom att utföra följande steg:

1. Besök [https://experience.adobe.com/assurance](https://experience.adobe.com/assurance{target="_blank"}).
1. Logga in med dina Adobe ID-uppgifter för Experience Cloud.
1. Om du ser **[!UICONTROL Sessioner]** så får du åtkomst. Om du ser åtkomstsidan (beta) väljer du **[!UICONTROL Registrera]** för att registrera.

## Implementera

Förutom det allmänna [SDK-installation](install-sdks.md), som du slutförde i den tidigare lektionen, behöver iOS även följande tillägg för att starta Assurance-sessionen för din app. Lägg till följande kod i **[!UICONTROL SceneDelegate]**:

```swift {highlight="5"}
func scene(_ scene: UIScene, openURLContexts URLContexts: Set<UIOpenURLContext>) {
        // Called when the app in background is opened with a deep link.
        if let deepLinkURL = URLContexts.first?.url {
            // Start the Assurance session
            Assurance.startSession(url: deepLinkURL)
        }
    }
```

Mer information finns [här](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/api-reference/{target="_blank"}).

## Signering

Innan du kör programmet för första gången i Xcode måste du uppdatera signeringen.

1. Öppna projektet i Xcode.
1. Välj **[!UICONTROL Luma]** i Navigator.
1. Välj **[!UICONTROL Luma]** mål.
1. Välj **Signering och funktioner** -fliken.
1. Konfigurera **[!UICONTROL Hantera signering automatiskt]**, **[!UICONTROL Team]** och **[!UICONTROL Paketidentifierare]**.

   ![Xcode-signeringsfunktioner](assets/xcode-signing-capabilities.png)

## Konfigurera en bas-URL

1. Gå till projektet i Xcode.
1. Välj **[!UICONTROL Luma]** i Navigator.
1. Välj **[!UICONTROL Luma]** mål.
1. Välj **Info** -fliken.
1. Bläddra nedåt till om du vill lägga till en bas-URL **URL-typer** och väljer **+** -knappen.
1. Ange **Identifierare** till den paketidentifierare som du konfigurerade i [Signering](#signing) (till exempel `com.adobe.luma.tutorial.swiftui`) och **URL-scheman** till `lumatutorialswiftui`.

   ![försäkrings-URL](assets/assurance-url-type.png)

Mer information om URL-scheman i iOS finns i [Apple dokumentation](https://developer.apple.com/documentation/xcode/defining-a-custom-url-scheme-for-your-app{target="_blank"}).

Assurance fungerar genom att öppna en URL, antingen via webbläsaren eller QR-koden. Den URL:en börjar med den bas-URL som öppnar appen och innehåller ytterligare parametrar. Dessa unika parametrar används för att ansluta sessionen.


## Ansluta till en session

1. Kör programmet i simulatorn eller på en ansluten fysisk enhet.
1. Välj **[!UICONTROL Säkerhet]** från den vänstra listen i användargränssnittet för datainsamling.
1. Välj **[!UICONTROL Skapa session]**.
1. Välj **[!UICONTROL Starta]**.
1. Ange en **[!UICONTROL Sessionsnamn]** som `Luma Mobile App Session` och **[!UICONTROL Bas-URL]**, som är det URL-schema som du angav i Xcode, följt av `://`. Exempel: `lumatutorialswiftui://`.
1. Välj **[!UICONTROL Nästa]**.
   ![skapa trygghet, session](assets/assurance-create-session.png)
1. I dialogrutan Skapa ny session:

   Om du använder en fysisk enhet:

   * Välj **[!UICONTROL Skanna QR-kod]**. Använd kameran på din fysiska enhet för att skanna QR-koden och tryck på länken för att öppna appen.

     ![qa-kod för försäkring](assets/assurance-qr-code.png)

   Om du använder en simulator:

   1. Välj **[!UICONTROL Kopiera länk]**.
   1. Kopiera den djupa länken med kopian ![Kopiera](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) och använd länken till att öppna appen med Safari i simulatorn.
      ![Länk till Assurance-kopia](assets/assurance-copy-link.png)

1. När appen läses in visas en modal dialogruta där du ombeds ange den PIN-kod som visas i steg 7.

   <img src="assets/assurance-enter-pin.png" width="300">

   Ange PIN-koden och välj **[!UICONTROL Anslut]**.


1. Om anslutningen lyckades ser du:
   * En säkerhetsikon visas ovanpå din app.

   <img src="assets/assurance-modal.png" width="300">

   * Uppdateringar från Experience Cloud i det webbaserade gränssnittet för Assurance, som visar:

      1. Experience Events kommer från appen.
      1. Information om en markerad händelse.
      1. Enheten och tidslinjen.

     ![säkringshändelser](assets/assurance-events.png)

Om du stöter på några problem kan du läsa [teknisk](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/{target="_blank"}) och [allmän dokumentation](https://experienceleague.adobe.com/docs/experience-platform/assurance/home.html{target="_blank"}).

>[!SUCCESS]
>
>Du har nu konfigurerat din app att använda Assurance för resten av självstudiekursen.<br/>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Mobile SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela med dig av dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)


Nästa: **[Godkännande](consent.md)**
