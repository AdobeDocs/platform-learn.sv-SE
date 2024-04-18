---
title: Konfigurera behörigheter för självstudien
description: Lär dig hur du begär åtkomst till Experience Platform Web SDK och konfigurerar behörighet för att slutföra självstudiekursen Implementera Adobe Experience Cloud med Web SDK.
feature: Web SDK,Tags,Access Control
exl-id: d7c4f2c3-cf3c-4587-88f8-82113d250084
source-git-commit: 15bc08bdbdcb19f5b086267a6d94615cbfe1bac7
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 3%

---

# Konfigurera behörigheter för självstudien


>[!CAUTION]
>
>Vi räknar med att kunna publicera viktiga ändringar av den här självstudiekursen tisdagen den 23 april 2024. Därefter kommer många övningar att ändras och du kan behöva starta om självstudiekursen från början för att kunna slutföra alla lektioner.

Lär dig hur du begär åtkomst till Experience Platform Web SDK och konfigurerar behörighet för att slutföra den här självstudiekursen. Om du vill implementera Platform Web SDK med hjälp av taggar i gränssnittet för datainsamling måste du ha rätt användarbehörigheter konfigurerade i [Admin Console](https://adminconsole.adobe.com).

## Datainsamling

* Har behörighet att **[!UICONTROL Develop]**, **[!UICONTROL Edit]**, **[!UICONTROL Approve]**, **[!UICONTROL Publish]**, **[!UICONTROL Manage Extensions]**, **[!UICONTROL Manage Environments]** och **[!UICONTROL Manage Properties]**. Mer information om taggbehörigheter finns i [dokumentationen](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html).
* Om du ska slutföra den valfria lektionen om vidarebefordran av händelser, ska du ha en produktlicens som innehåller vidarebefordran av edge-material och behörighetsobjekt **[!UICONTROL Platforms]** > **[!UICONTROL Edge]**

## Experience Platform

Dessa funktioner bör vara tillgängliga för alla Experience Cloud-kunder, även om du inte är kund till en plattformsbaserad applikation som Real-Time CDP.

* Åtkomst till **standardproduktion**, **&quot;Prod&quot;** sandlåda.
* Åtkomst till **[!UICONTROL Manage Schemas]** och **[!UICONTROL View Schemas]** under **[!UICONTROL Data Modeling]**
* Åtkomst till **[!UICONTROL Manage Identity Namespaces]** och **[!UICONTROL View Identity Namespaces]** under **[!UICONTROL Identity Management]**
* Åtkomst till **[!UICONTROL Manage Datastreams]** och **[!UICONTROL View Datastreams]** under **[!UICONTROL Data Collection]**
* Om du är kund till ett plattformsbaserat program och kommer att fylla i [Konfigurera Experience Platform](setup-experience-platform.md) lektion:
   * Åtkomst till en **utveckling** sandlåda.
   * Alla behörighetsobjekt under **[!UICONTROL Data Management]** och **[!UICONTROL Profile Management]**:


Mer information om plattformsåtkomstkontroll finns i [dokumentationen](https://experienceleague.adobe.com/docs/experience-platform/access-control/home.html).

## Adobe Analytics

För Adobe Analytics-lektionen måste du ha [administratörsåtkomst till inställningar för Report Suite, bearbetningsregler och Analysis Workspace](https://experienceleague.adobe.com/docs/analytics/admin/admin-console/home.html)

## Adobe Target

För Adobe Target-lektionen måste du ha [Redigerare eller godkännare](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html#section_8C425E43E5DD4111BBFC734A2B7ABC80) åtkomst.

## Adobe Audience Manager

* För den valfria lektionen Audience Manager måste du ha tillgång till att skapa, läsa och skriva egenskaper, segment och mål. Mer information finns i självstudiekursen [Audience Manager Role-baserad åtkomstkontroll](https://experienceleague.adobe.com/docs/audience-manager-learn/tutorials/setup-and-admin/user-management/setting-permissions-with-role-based-access-control.html?lang=en).

Nu kan du börja de inledande konfigurationsstegen.

[Nästa: ](configure-schemas.md)

>[!NOTE]
>
>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Web SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
