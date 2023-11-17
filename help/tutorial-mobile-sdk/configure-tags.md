---
title: Konfigurera en taggegenskap
description: Lär dig konfigurera en taggegenskap i [!UICONTROL Datainsamling] gränssnitt.
feature: Mobile SDK,Tags
exl-id: 0c4b00cc-34e3-4d08-945e-3fd2bc1b6ccf
source-git-commit: 94ca4a238c241518219fb2e8d73f775836f86d86
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 1%

---

# Konfigurera en taggegenskap

Lär dig konfigurera en taggegenskap i [!UICONTROL Datainsamling] gränssnitt.

>[!INFO]
>
> Den här självstudiekursen kommer att ersättas med en ny självstudiekurs om hur du använder en ny exempelapp i slutet av november 2023

Taggar i Adobe Experience Platform är nästa generation av tagghanteringsfunktioner från Adobe. Taggar ger kunderna ett enkelt sätt att driftsätta och hantera alla analys-, marknadsförings- och annonstaggar som behövs för att driva relevanta kundupplevelser. Läs mer om [taggar](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=sv) i produktdokumentationen.

## Förutsättningar

Du måste ha behörighet att skapa en taggegenskap för att kunna slutföra lektionen. Det är också praktiskt att ha en grundläggande förståelse för taggar.

>[!NOTE]
>
> Platforma launchen (klientsidan) är nu [taggar](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=en)

## Utbildningsmål

I den här lektionen kommer du att:

* Installera och konfigurera mobiltaggtilläggen.
* Generera installationsanvisningar för SDK.

## Inledande konfiguration

1. Skapa en ny mobil taggegenskap:
   1. I [Gränssnitt för datainsamling](https://experience.adobe.com/data-collection/){target="_blank"}, markera **[!UICONTROL Taggar]** till vänster navigering
   1. Välj **[!UICONTROL Ny egenskap]**
      ![skapa en taggegenskap](assets/mobile-tags-new-property.png).
   1. För **[!UICONTROL Namn]**, ange `Mobile SDK Course`.
   1. För **[!UICONTROL Plattform]**, markera **[!UICONTROL Mobil]**.
   1. Välj  **[!UICONTROL Spara]**.

      ![konfigurera taggegenskapen](assets/mobile-tags-property-config.png)

      >[!NOTE]
      >
      > Standardinställningar för godkännande av kantbaserade SDK-implementeringar för mobiler, som den du gör i den här självstudiekursen, kommer från [!UICONTROL Godkänn tillägg] och inte [!UICONTROL Integritet] inställning i taggegenskapskonfigurationen. Du kommer att lägga till och konfigurera tillägget för samtycke senare i den här lektionen. Mer information finns på [dokumentationen](https://developer.adobe.com/client-sdks/documentation/privacy-and-gdpr/).


1. Öppna den nya egenskapen
1. Skapa ett bibliotek:

   1. Gå till **[!UICONTROL Publiceringsflöde]** i den vänstra navigeringen.
   1. Välj **[!UICONTROL Lägg till bibliotek]**.

      ![Välj Lägg till bibliotek](assets/mobile-tags-create-library.png)

   1. För **[!UICONTROL Namn]**, ange `Initial Build`.
   1. För **[!UICONTROL Miljö]**, markera **[!UICONTROL Utveckling]**.
   1. Välj  **[!UICONTROL Lägg till alla ändrade resurser]**.
   1. Välj **[!UICONTROL Spara och bygg till utveckling]**.

      ![Bygg biblioteket](assets/mobile-tags-save-library.png)

   1. Äntligen kan du ange den som **[!UICONTROL Arbetsbibliotek]**.
      ![Välj som arbetsbibliotek](assets/mobile-tags-working-library.png)
1. Välj **[!UICONTROL Tillägg]**.

   Mobile Core- och Profile-tilläggen bör vara förinstallerade.

1. Välj **[!UICONTROL Katalog]**.

   ![inledande konfiguration](assets/mobile-tags-starting.png)

1. Använd [!UICONTROL Sök] för att hitta och installera följande tillägg. Inget av dessa tillägg kräver någon konfiguration:
   * Identitet
   * AEP Assurance

## Tilläggskonfiguration

1. Installera **Godkännande** tillägg.

   I den här självstudiekursen väljer du **[!UICONTROL Väntande]**. Läs mer om tillägget för samtycke i [dokumentationen](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/).

   ![inställningar för samtycke](assets/mobile-tags-extension-consent.png)

1. Installera **Adobe Experience Platform Edge Network** tillägg.

   I **[!UICONTROL Konfiguration av Edge]** väljer du den datastream du skapade i listrutan [föregående steg](create-datastream.md).

1. Välj **[!UICONTROL Spara i bibliotek och bygge]**.

   ![inställningar för Edge-nätverk](assets/mobile-tags-extension-edge.png)


## Generera installationsanvisningar för SDK

1. Välj **[!UICONTROL Miljö]**.

1. Välj **[!UICONTROL Utveckling]** installationsikon.

   ![miljöer, startskärm](assets/mobile-tags-environments.png)

1. Välj **[!UICONTROL iOS]**.

1. Välj **[!UICONTROL Swift]**.

   ![installationsanvisningar](assets/mobile-tags-install-instructions.png)

1. Installationsanvisningarna ger dig en bra startpunkt för implementeringen.

   Ytterligare information finns [här](https://developer.adobe.com/client-sdks/documentation/getting-started/get-the-sdk/).

   * **[!UICONTROL Miljöfil-ID]**: Detta unika ID pekar på din utvecklingsmiljö, observera detta värde. Produktion/mellanlagring/utveckling kommer att ha olika ID-värden.
   * **[!UICONTROL Podfile]**: CocoaPods används för att hantera SDK-versioner och -nedladdningar. Läs mer i [dokumentation](https://cocoapods.org/).
   * **[!UICONTROL Initieringskod]**: Det här kodblocket visar hur du importerar de SDK:er som krävs och registrerar tilläggen vid start.

>[!NOTE]
>Installationsanvisningarna ska betraktas som en startpunkt och inte som slutgiltig dokumentation. De senaste SDK-versionerna och kodexemplen finns i den officiella [dokumentation](https://developer.adobe.com/client-sdks/documentation/).

## Arkitektur för mobila taggar

Om du känner till webbversionen av taggar, tidigare Launch, är det viktigt att förstå skillnaderna på mobilen.

På webben återges en taggegenskap i JavaScript som sedan (vanligtvis) finns i molnet. JS-filen refereras direkt till på webbplatsen.

I en mobil taggegenskap återges regler och konfigurationer i JSON-filer som lagras i molnet. JSON-filerna hämtas och läses av tillägget Mobile Core i mobilappen. Tillägg är separata SDK:er som fungerar tillsammans. Om du lägger till ett tillägg i taggegenskapen måste du även uppdatera appen. Om du ändrar en tilläggsinställning eller skapar en regel återspeglas dessa ändringar i appen när du har publicerat det uppdaterade taggbiblioteket.

Nästa: **[Installera SDK:er](install-sdks.md)**

>[!NOTE]
>
>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Mobile SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela med dig av dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)