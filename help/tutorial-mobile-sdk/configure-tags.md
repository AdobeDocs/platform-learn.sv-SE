---
title: Konfigurera en taggegenskap för plattformens SDK-implementeringar
description: Lär dig hur du konfigurerar en taggegenskap i [!UICONTROL Data Collection]-gränssnittet.
feature: Mobile SDK,Tags
jira: KT-14626
exl-id: 0c4b00cc-34e3-4d08-945e-3fd2bc1b6ccf
source-git-commit: 25f0df2ea09bb7383f45a698e75bd31be7541754
workflow-type: tm+mt
source-wordcount: '919'
ht-degree: 1%

---

# Konfigurera en taggegenskap

Lär dig hur du konfigurerar en taggegenskap i [!UICONTROL Data Collection]-gränssnittet.

Taggar i Adobe Experience Platform är nästa generation av tagghanteringsfunktioner från Adobe. Taggar ger kunderna ett enkelt sätt att driftsätta och hantera de analyser, marknadsförings- och annonstaggar som behövs för att skapa relevanta kundupplevelser. Läs mer om [Taggar](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=sv) i produktdokumentationen.

## Förhandskrav

Du måste ha behörighet att skapa en taggegenskap för att kunna slutföra lektionen. Det är också praktiskt att ha en grundläggande förståelse för taggar.

>[!NOTE]
>
> Platforma launchen (klientsidan) är nu [Taggar](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=en)

## Utbildningsmål

I den här lektionen kommer du att:

* Installera och konfigurera mobiltaggtilläggen.
* Generera installationsanvisningar för SDK.

## Inledande konfiguration

1. Skapa en ny mobil taggegenskap i datainsamlingsgränssnittet:
   1. Välj **[!UICONTROL Tags]** i den vänstra navigeringen.
   1. Välj **[!UICONTROL New Property]**
      ![skapa en taggegenskap](assets/tags-new-property.png).
   1. Ange `Luma Mobile App Tutorial` för **[!UICONTROL Name]**.
   1. För **[!UICONTROL Platform]** väljer du **[!UICONTROL Mobile]**.
   1. Välj **[!UICONTROL Save]**.

      ![konfigurera taggegenskapen](assets/tags-property-config.png)

      >[!NOTE]
      >
      > Standardinställningar för godkännande för kantbaserade SDK-implementeringar för mobiler, som den du gör i den här lektionen, kommer från [!UICONTROL Consent extension] och inte från inställningen [!UICONTROL Privacy] i taggegenskapskonfigurationen. Du lägger till och konfigurerar tillägget för samtycke senare i den här lektionen. Mer information finns i [dokumentationen](https://developer.adobe.com/client-sdks/edge/consent-for-edge-network/).


1. Öppna den nya egenskapen.
1. Skapa ett bibliotek:

   1. Gå till **[!UICONTROL Publishing Flow]** i den vänstra navigeringen.
   1. Välj **[!UICONTROL Add Library]**.

      ![Välj Lägg till bibliotek](assets/tags-create-library.png)

   1. Ange `Initial Build` för **[!UICONTROL Name]**.
   1. För **[!UICONTROL Environment]** väljer du **[!UICONTROL Development (development)]**.
   1. Välj ![Lägg till knapp](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Add All Changed Resources]**.
   1. Välj **[!UICONTROL Save and Build to Development]**.

      ![Skapa biblioteket](assets/tags-save-library.png)

   1. Välj slutligen **[!UICONTROL Initial Build]** som ditt arbetsbibliotek på menyn **[!UICONTROL Select a working library]**.
      ![Välj som arbetsbibliotek](assets/tags-working-library.png)
1. Kontrollera tillägg:

   1. Kontrollera att **[!UICONTROL Initial Build]** är valt som standardbibliotek.

   1. Välj **[!UICONTROL Extensions]** i den vänstra listen.

   1. Klicka på fliken **[!UICONTROL Installed]**.  

      Tilläggen [!UICONTROL Mobile Core] och [!UICONTROL Profile] bör vara förinstallerade.

      ![Taggar installerade](assets/tags-installed.png)

## Tilläggskonfiguration

1. Kontrollera att du är i **[!UICONTROL Extensions]** i din mobilappsegenskap.

1. Välj **[!UICONTROL Catalog]**.

   ![inledande konfiguration](assets/tags-starting.png)

1. Använd fältet ![Sök](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Search_18_N.svg) **[!UICONTROL Search]** för att hitta tillägget **Identitet**.

   1. Sök efter `Identity`.

   2. Välj tillägget **[!UICONTROL Identity]**.

   3. Välj **[!UICONTROL Install]**.

      ![Identitetsinstallation](assets/tags-identity-install.png)

   Det här tillägget kräver ingen ytterligare konfiguration.

1. Använd fältet ![Sök](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Search_18_N.svg) **[!UICONTROL Search]** för att hitta och installera tillägget **AEP Assurance**.

   Det här tillägget kräver ingen ytterligare konfiguration.

1. Använd fältet ![Sök](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Search_18_N.svg) **[!UICONTROL Search]** för att hitta och installera tillägget **Samtycke**. På konfigurationsskärmen:

   1. Välj **[!UICONTROL Pending]**.  I den här självstudiekursen hanterar du samtycke ytterligare i programmet. Läs mer om tillägget för samtycke i [dokumentationen](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/).
   1. Välj **[!UICONTROL Save to Library]**.

      ![inställningar för samtycke](assets/tags-extension-consent.png)

1. Använd fältet ![Sök](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Search_18_N.svg) **[!UICONTROL Search]** för att hitta och installera tillägget **Adobe Experience Platform Edge Network**.

   1. I **[!UICONTROL Datastreams]** väljer du **[!UICONTROL Datastream]** som du skapade i [föregående steg](create-datastream.md) för varje miljö, till exempel **[!DNL Luma Mobile App]**.

   1. Om den inte redan är ifylld anger du **[!UICONTROL Edge Network domain]** i **[!UICONTROL Domain Configuration]**. Domänen Edge Network är namnet på din organisation följt av `data.adobedc.net`, till exempel `techmarketingdemos.data.adobedc.net`.

   1. Välj **[!UICONTROL Save to Library and Build]** på menyn **[!UICONTROL Save to Library]**.

      ![inställningar för gränsnätverk](assets/tags-extension-edge.png)

Ditt bibliotek är byggt för de nya tilläggen och konfigurationerna. Ett lyckat bygge indikeras av en <span style="color:green"> ●</span> i knappen **[!UICONTROL Initial Build]**.


## Generera installationsanvisningar för SDK

1. Välj **[!UICONTROL Environments]** i den vänstra listen.

1. Välj installationsikonen **[!UICONTROL Development]** ![Box](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Box_18_N.svg) .

   ![Miljöer, startskärm](assets/tags-environments.png)

1. Välj fliken **[!UICONTROL iOS]** i dialogrutan **[!UICONTROL Mobile Install Instructions]**.

1. Du kan kopiera ![Kopiera](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) instruktionerna för att konfigurera ditt projekt med CocoaPods. CocoaPods används för att hantera SDK-versioner och -nedladdningar. Mer information finns i dokumentationen för [CocoaPods](https://cocoapods.org/). Om du använder Android™ som utvecklingsplattform är Gradle verktyget för att hantera SDK-version, hämtningsbara filer och beroenden. Mer information finns i dokumentationen för [Gradle](https://gradle.org/)

   Installationsanvisningarna ger dig en bra startpunkt för implementeringen. Ytterligare information [finns här](https://developer.adobe.com/client-sdks/documentation/getting-started/get-the-sdk/).

   >[!INFO]
   >
   >För resten av den här självstudiekursen använder du **inte** instruktionerna för CocoaPods, utan i stället en SPM-baserad konfiguration (Swift Package Manager).
   >

1. Välj fliken **[!UICONTROL Swift]** under **[!UICONTROL Add Initialization Code]**. Det här kodblocket visar hur du importerar de SDK:er som krävs och registrerar tilläggen vid start. Mer information finns i [Installera SDK](install-sdks.md).

1. Kopiera ![Kopiera](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) **[!UICONTROL Environment File ID]** och lagra den på en plats som du behöver senare. Detta unika ID pekar på din utvecklingsmiljö. Varje miljö (produktion, mellanlagring, utveckling) har ett eget unikt ID-värde.

   ![installationsanvisningar](assets/tags-install-instructions.png)

>[!NOTE]
>
>Installationsanvisningarna ska betraktas som en startpunkt och inte som slutgiltig dokumentation. De senaste SDK-versionerna och kodexemplen finns i den officiella [dokumentationen](https://developer.adobe.com/client-sdks/home/).

## Arkitektur för mobila taggar

Om du är bekant med webbversionen av taggar, tidigare Launch, är det viktigt att förstå skillnaderna på mobilen.

* På webben återges en taggegenskap i JavaScript som sedan (vanligtvis) lagras i molnet. Det finns en referens till den JavaScript-filen direkt på webbplatsen.

* I en mobil taggegenskap återges regler och konfigurationer i JSON-filer som lagras i molnet. JSON-filerna hämtas och läses av tillägget Mobile Core i mobilappen. Tillägg är separata SDK:er som fungerar tillsammans. Om du lägger till ett tillägg i taggegenskapen måste du även uppdatera appen. Om du ändrar en tilläggsinställning eller skapar en regel återspeglas dessa ändringar i appen när du har publicerat det uppdaterade taggbiblioteket. Tack vare den flexibiliteten kan du ändra inställningar (som Adobe Analytics Report Suite-id) eller till och med ändra appens beteende (med dataelement och regler, som du kommer att se i senare lektioner) utan att behöva ändra koden i appen och skicka appbutiken igen.

>[!SUCCESS]
>
>Du har nu en mobil taggegenskap att använda i resten av den här självstudien.
>
>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Mobile SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela dem i det här [Experience League-diskussionsinlägget](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Nästa: **[Installera SDK](install-sdks.md)**
