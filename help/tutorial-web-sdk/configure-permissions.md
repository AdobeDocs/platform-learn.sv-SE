---
title: Konfigurera behörigheter för självstudiekursen
description: Lär dig hur du begär åtkomst till Experience Platform Web SDK och konfigurerar behörigheten som krävs för att slutföra självstudiekursen Implementera Adobe Experience Cloud med Web SDK.
feature: Access Control
exl-id: d7c4f2c3-cf3c-4587-88f8-82113d250084
source-git-commit: 4eaa7ae1cf4c4c1478484eaeb877733a43c6fdf5
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Konfigurera behörigheter för självstudiekursen

Lär dig hur du begär åtkomst till Experience Platform Web SDK och konfigurerar behörighet för att slutföra den här självstudiekursen. Om du vill implementera Platform Web SDK med hjälp av taggar i gränssnittet för datainsamling måste du ha rätt användarbehörigheter konfigurerade i [Admin Console](https://adminconsole.adobe.com).

## Datainsamling

* Har behörighet att **[!UICONTROL Utveckla]**, **[!UICONTROL Redigera]**, **[!UICONTROL Godkänn]**, **[!UICONTROL Publicera]**, **[!UICONTROL Hantera tillägg]**, **[!UICONTROL Hantera miljöer]** och **[!UICONTROL Hantera egenskaper]**. Mer information om taggbehörigheter finns i [dokumentationen](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html).
* Om du ska slutföra den valfria lektionen om vidarebefordran av händelser, ska du ha en produktlicens som innehåller vidarebefordran av edge-material och behörighetsobjekt **[!UICONTROL Plattformar]** > **[!UICONTROL Edge]**

## Experience Platform

Dessa funktioner bör vara tillgängliga för alla Experience Cloud-kunder, även om du inte är kund till en plattformsbaserad applikation som Real-Time CDP.

* Åtkomst till **standardproduktion**, **&quot;Prod&quot;** sandlåda.
* Åtkomst till **[!UICONTROL Hantera scheman]** och **[!UICONTROL Visa scheman]** under **[!UICONTROL Datamodellering]**
* Åtkomst till **[!UICONTROL Hantera identitetsnamnutrymmen]** och **[!UICONTROL Visa identitetsnamnutrymmen]** under **[!UICONTROL Identity Management]**
* Åtkomst till **[!UICONTROL Hantera datastreams]** och **[!UICONTROL Visa datastreams]** under **[!UICONTROL Datainsamling]**
* Om du är kund till ett plattformsbaserat program och kommer att fylla i [Konfigurera Experience Platform](setup-experience-platform.md) lektion:
   * Åtkomst till en **utveckling** sandlåda.
   * Alla behörighetsobjekt under **[!UICONTROL Datahantering]** och **[!UICONTROL Profilhantering]**:


Mer information om plattformsåtkomstkontroll finns i [dokumentationen](https://experienceleague.adobe.com/docs/experience-platform/access-control/home.html).

## Adobe Analytics

För Adobe Analytics-lektionen måste du ha [administratörsåtkomst till inställningar för Report Suite, bearbetningsregler och Analysis Workspace](https://experienceleague.adobe.com/docs/analytics/admin/admin-console/home.html)

## Adobe Target

För Adobe Target-lektionen måste du ha [Redigerare eller godkännare](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html#section_8C425E43E5DD4111BBFC734A2B7ABC80) åtkomst.

## Adobe Audience Manager

* För den valfria lektionen Audience Manager måste du ha tillgång till att skapa, läsa och skriva egenskaper, segment och mål. Mer information finns i självstudiekursen om [Audience Manager Role-baserad åtkomstkontroll](https://experienceleague.adobe.com/docs/audience-manager-learn/tutorials/setup-and-admin/user-management/setting-permissions-with-role-based-access-control.html?lang=en).

Nu kan du börja de inledande konfigurationsstegen.

[Nästa: ](configure-schemas.md)

>[!NOTE]
>
>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Web SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela med dig av dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
