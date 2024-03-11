---
title: Självstudiekurs om att implementera Adobe Experience Cloud med webb-SDK
description: Lär dig hur du implementerar Experience Cloud-program med Adobe Experience Platform Web SDK.
recommendations: catalog, noDisplay
source-git-commit: b46666013f39a5a71323810ee69876d9e32e02e3
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 2%

---

# Självstudiekurs om att implementera Adobe Experience Cloud med webb-SDK

Lär dig hur du implementerar Experience Cloud-program med Adobe Experience Platform Web SDK.

Experience Platform Web SDK är ett JavaScript-bibliotek på klientsidan som gör det möjligt för Adobe Experience Cloud kunder att interagera med både Adobe-program och tredjepartstjänster via Adobe Experience Platform Edge Network. Se [Adobe Experience Platform Web SDK - översikt](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html) för mer detaljerad information.

![Experience Platform Web SDK-arkitektur](assets/dc-websdk.png)

I den här självstudiekursen får du hjälp med att implementera Platform Web SDK på en exempelwebbplats som heter Luma. The [Luma-webbplats](https://luma.enablementadobe.com/content/luma/us/en.html) har ett omfattande datalager och funktioner som gör att du kan skapa en realistisk implementering. I den här självstudiekursen:

* Skapa en egen taggegenskap på ditt eget konto med en Platform Web SDK-implementering för Luma-webbplatsen.
* Konfigurera alla datainsamlingsfunktioner för Web SDK-implementeringar som datastreams, scheman och identitetsnamnutrymmen.
* Lägg till följande Adobe Experience Cloud-program:
   * **[Adobe Experience Platform](setup-experience-platform.md)** (och program som bygger på Platform som Adobe Real-time Customer Data Platform, Adobe Journey Optimizer och Adobe Customer Journey Analytics)
   * **[Adobe Analytics](setup-analytics.md)**
   * **[Adobe Audience Manager](setup-audience-manager.md)**
   * **[Adobe Target](setup-target.md)**
* Implementera vidarebefordran av händelser för att skicka data som samlats in av Web SDK till andra mål än Adobe.
* Validera din egen implementering av Platform Web SDK med Experience Platform Debugger and Assurance.

När du är klar med den här självstudiekursen kan du börja implementera alla dina marknadsföringsprogram via Platform Web SDK på din egen webbplats!


>[!NOTE]
>
>En liknande självstudiekurs om flera lösningar finns tillgänglig för [Mobile SDK](../tutorial-mobile-sdk/overview.md).

## Förutsättningar

Alla Experience Cloud-kunder kan använda Platform Web SDK. Det är inte ett krav att licensiera ett plattformsbaserat program som Real-time Customer Data Platform eller Journey Optimizer att använda Web SDK.

I den här lektionen antas du ha ett Adobe-konto och de behörigheter som krävs för att slutföra lektionerna. Annars måste du kontakta en Experience Cloud-administratör på ditt företag för att få åtkomst.

* För **Datainsamling** måste du ha:
   * **[!UICONTROL Platforms]**—behörighet för **[!UICONTROL Web]** och, om licens finns, **[!UICONTROL Edge]**
   * **[!UICONTROL Property Rights]**—behörighet till **[!UICONTROL Approve]**, **[!UICONTROL Develop]**, **[!UICONTROL Edit Property]**, **[!UICONTROL Manage Environments]**, **[!UICONTROL Manage Extensions]** och **[!UICONTROL Publish]**,
   * **[!UICONTROL Company Rights]**—behörighet till **[!UICONTROL Manage Properties]**

     Mer information om taggbehörigheter finns i [dokumentationen](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html).

* För **Experience Platform** måste du ha:

   * Åtkomst till **standardproduktion**, **&quot;Prod&quot;** sandlåda.
   * Åtkomst till **[!UICONTROL Manage Schemas]** och **[!UICONTROL View Schemas]** under **[!UICONTROL Data Modeling]**.
   * Åtkomst till **[!UICONTROL Manage Identity Namespaces]** och **[!UICONTROL View Identity Namespaces]** under **[!UICONTROL Identity Management]**.
   * Åtkomst till **[!UICONTROL Manage Datastreams]** och **[!UICONTROL View Datastreams]** under **[!UICONTROL Data Collection]**.
   * Om du är kund till ett plattformsbaserat program och kommer att fylla i [Konfigurera Experience Platform](setup-experience-platform.md) lektion:
      * Åtkomst till en **utveckling** sandlåda.
      * Alla behörighetsobjekt under **[!UICONTROL Data Management]** och **[!UICONTROL Profile Management]**:

     De funktioner som krävs bör vara tillgängliga för alla Experience Cloud-kunder, även om du inte är kund till en plattformsbaserad applikation som Real-Time CDP.

     Mer information om plattformsåtkomstkontroll finns i [dokumentationen](https://experienceleague.adobe.com/docs/experience-platform/access-control/home.html).

* För det valfria **Adobe Analytics** lektion måste du ha [administratörsåtkomst till inställningar för Report Suite, bearbetningsregler och Analysis Workspace](https://experienceleague.adobe.com/docs/analytics/admin/admin-console/home.html)

* För det valfria **Adobe Target** lektion måste du ha [Redigerare eller godkännare](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html#section_8C425E43E5DD4111BBFC734A2B7ABC80) åtkomst.

* För det valfria **Audience Manager** lektion måste du ha tillgång till för att skapa, läsa och skriva egenskaper, segment och mål. Mer information finns i självstudiekursen [Audience Manager Role-baserad åtkomstkontroll](https://experienceleague.adobe.com/docs/audience-manager-learn/tutorials/setup-and-admin/user-management/setting-permissions-with-role-based-access-control.html?lang=en).


>[!NOTE]
>
>Du måste känna till utvecklingsspråk som HTML och JavaScript. Du behöver inte vara expert på de här språken, men du får ut mer av den här självstudiekursen om du kan läsa och förstå kod.

## Läs in Luma-webbplatsen

Läs in [Lumas webbplats](https://luma.enablementadobe.com/content/luma/us/en.html){target="blank"} i en separat webbläsarflik och bokmärk den så att du enkelt kan läsa in den när det behövs under självstudiekursen. Du behöver inte ha någon annan åtkomst till Luma än att kunna läsa in vår värdbaserade produktionsplats.

[![Lumas webbplats](assets/old-overview-luma.png)](https://luma.enablementadobe.com/content/luma/us/en.html){target="blank"}

Kom så börjar vi!

[Nästa: ](configure-schemas.md)

>[!NOTE]
>
>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Web SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela med dig av dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
