---
title: Självstudiekurs om att implementera Adobe Experience Cloud med webb-SDK
description: Lär dig implementera Experience Cloud-program med Adobe Experience Platform Web SDK.
recommendations: catalog, noDisplay
exl-id: cf0ff74b-e81e-4f6d-ab7d-6c70e9b52d78
source-git-commit: 7ccbaaf4db43921f07c971c485e1460a1a7f0334
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 2%

---

# Självstudiekurs om att implementera Adobe Experience Cloud med webb-SDK

Lär dig implementera Experience Cloud-program med Adobe Experience Platform Web SDK.

Experience Platform Web SDK är ett JavaScript-bibliotek på klientsidan som gör det möjligt för Adobe Experience Cloud-kunder att interagera med både Adobe-program och tredjepartstjänster via Adobe Experience Platform Edge Network. Mer information finns i [Adobe Experience Platform Web SDK Overview](https://experienceleague.adobe.com/sv/docs/experience-platform/edge/home).

![Experience Platform Web SDK-arkitektur](assets/dc-websdk.png)

I den här självstudiekursen får du hjälp med att implementera Platform Web SDK på en exempelwebbplats som heter Luma. [Luma-webbplatsen](https://luma.enablementadobe.com/content/luma/us/en.html) har ett omfattande datalager och funktioner som gör att du kan skapa en realistisk implementering. I den här självstudiekursen:

* Skapa en egen taggegenskap, på ditt eget konto, med en Platform Web SDK-implementering för Luma-webbplatsen.
* Konfigurera alla datainsamlingsfunktioner för Web SDK-implementeringar som datastreams, scheman och identitetsnamnutrymmen.
* Lägg till följande Adobe Experience Cloud-program:
   * **[Adobe Experience Platform](setup-experience-platform.md)** (och program som är byggda på en plattform som Adobe Real-Time Customer Data Platform, Adobe Journey Optimizer och Adobe Customer Journey Analytics)
   * **[Adobe Analytics](setup-analytics.md)**
   * **[Adobe Audience Manager](setup-audience-manager.md)**
   * **[Adobe Target](setup-target.md)**
* Implementera vidarebefordran av händelser för att skicka data som samlats in av Web SDK till destinationer utanför Adobe.
* Validera din egen Platform Web SDK-implementering med Experience Platform Debugger och Assurance.

När du är klar med den här självstudiekursen kan du börja implementera alla dina marknadsföringsprogram via Platform Web SDK på din egen webbplats!


>[!NOTE]
>
>Det finns en liknande självstudiekurs om flera lösningar för [Mobile SDK](../tutorial-mobile-sdk/overview.md).

## Förhandskrav

Alla Experience Cloud-kunder kan använda Platform Web SDK. Det är inte ett krav att licensiera ett plattformsbaserat program som Real-Time Customer Data Platform eller Journey Optimizer att använda Web SDK.

I den här lektionen antas du ha ett Adobe-konto och de behörigheter som krävs för att slutföra lektionerna. Annars måste du kontakta en Experience Cloud-administratör på ditt företag för att få åtkomst.

* För **datainsamling** måste du ha:
   * **[!UICONTROL Platforms]** - behörighet för **[!UICONTROL Web]** och, om den är licensierad, **[!UICONTROL Edge]**
   * **[!UICONTROL Property Rights]** - behörighet till **[!UICONTROL Approve]**, **[!UICONTROL Develop]**, **[!UICONTROL Edit Property]**, **[!UICONTROL Manage Environments]**, **[!UICONTROL Manage Extensions]** och **[!UICONTROL Publish]**,
   * **[!UICONTROL Company Rights]** - behörighet till **[!UICONTROL Manage Properties]**

     Mer information om taggbehörigheter finns i [dokumentationen](https://experienceleague.adobe.com/sv/docs/experience-platform/tags/admin/user-permissions).

* För **Experience Platform** måste du ha

   * Åtkomst till sandlådan **standardproduktion**, **&quot;Prod&quot;**.
   * Åtkomst till **[!UICONTROL Manage Schemas]** och **[!UICONTROL View Schemas]** under **[!UICONTROL Data Modeling]**.
   * Åtkomst till **[!UICONTROL Manage Identity Namespaces]** och **[!UICONTROL View Identity Namespaces]** under **[!UICONTROL Identity Management]**.
   * Åtkomst till **[!UICONTROL Manage Datastreams]** och **[!UICONTROL View Datastreams]** under **[!UICONTROL Data Collection]**.
   * Om du använder ett plattformsbaserat program och kommer att slutföra lektionen [Konfigurera Experience Platform](setup-experience-platform.md) bör du även ha:
      * Åtkomst till en **utvecklingssandlåda**.
      * Alla behörighetsobjekt under **[!UICONTROL Data Management]** och **[!UICONTROL Profile Management]**:

     De funktioner som krävs bör vara tillgängliga för alla Experience Cloud-kunder, även om du inte är kund till ett plattformsbaserat program som Real-Time CDP.

     Mer information om plattformsåtkomstkontroll finns i [dokumentationen](https://experienceleague.adobe.com/sv/docs/experience-platform/access-control/home).

* För den valfria lektionen **Adobe Analytics** måste du ha [administratörsåtkomst till inställningar för Report Suite, bearbetningsregler och Analysis Workspace](https://experienceleague.adobe.com/sv/docs/analytics/admin/admin-console/home)

* För den valfria **Adobe Target**-lektionen måste du ha tillgång till [redigeraren eller godkännaren](https://experienceleague.adobe.com/sv/docs/target/using/administer/manage-users/enterprise/properties-overview#section_8C425E43E5DD4111BBFC734A2B7ABC80).

* För den valfria **Audience Manager**-lektionen måste du ha tillgång till egenskaperna, segmenten och målen för att kunna skapa, läsa och skriva. Mer information finns i självstudiekursen om [Audience Manager rollbaserade åtkomstkontroll](https://experienceleague.adobe.com/sv/docs/audience-manager-learn/tutorials/setup-and-admin/user-management/setting-permissions-with-role-based-access-control).


>[!NOTE]
>
>Man utgår ifrån att man känner till utvecklingsspråk som HTML och JavaScript. Du behöver inte vara expert på de här språken, men du får ut mer av den här självstudiekursen om du kan läsa och förstå kod.

## Uppdateringar

* 24 april 2024: Viktiga uppdateringar inklusive tillägg av begäran om Set Variable/Update Variable, delad personalisering och analys, Journey Optimizer-lektioner

## Läs in Luma-webbplatsen

Läs in [Luma-webbplatsen](https://luma.enablementadobe.com/content/luma/us/en.html){target="blank"} på en separat webbläsarflik och skapa ett bokmärke så att du enkelt kan läsa in den när det behövs under självstudiekursen. Du behöver inte ha någon annan åtkomst till Luma än att kunna läsa in vår värdbaserade produktionsplats.

[![Luma-webbplats](assets/old-overview-luma.png)](https://luma.enablementadobe.com/content/luma/us/en.html){target="blank"}

Kom så börjar vi!

>[!NOTE]
>
>Tack för att du har lagt ned din tid på att lära dig om Adobe Experience Platform Web SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela dem i det här [Experience League diskussionsgruppsinlägget](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996?profile.language=sv)
