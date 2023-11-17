---
title: Konfigurera ett datastream
description: Lär dig hur du skapar ett datastream i Experience Platform.
feature: Mobile SDK,Datastreams
exl-id: 7b83f834-d1fb-45d1-8bcf-bc621f94725c
source-git-commit: bc53cb5926f708408a42aa98a1d364c5125cb36d
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 0%

---

# Skapa ett datastream

Lär dig hur du skapar ett datastream i Experience Platform.

>[!INFO]
>
> Den här självstudiekursen kommer att ersättas med en ny självstudiekurs om hur du använder en ny exempelapp i slutet av november 2023

En datastream är en konfiguration på serversidan på Platform Edge Network.  Datastream säkerställer att inkommande data till Platform Edge Network dirigeras till Adobe Experience Cloud-program och -tjänster på rätt sätt. Mer information finns i [dokumentation](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html) eller [video](https://experienceleague.adobe.com/docs/platform-learn/data-collection/edge-network/configure-datastreams.html).

## Förutsättningar

Om du vill skapa en datastream måste din organisation ha etablerats för den här funktionen i gränssnittet för datainsamling (tidigare [!UICONTROL Starta]) och du måste ha användarbehörighet för [!UICONTROL Experience Platform] > [!UICONTROL Datainsamling] > **[!UICONTROL Hantera datastreams]** och **[!UICONTROL Visa datastreams]**.

## Utbildningsmål

I den här lektionen kommer du att:

* Ta reda på när en datastream ska användas.
* Skapa en datastream.
* Konfigurera en datastream.

## Skapa ett datastream

Datastreams kan skapas i [!UICONTROL Datainsamling] -gränssnittet med [!UICONTROL Datastream] konfigurationsverktyg. Så här skapar du ett datastream:

1. Kontrollera att du använder rätt plattformssandlåda.
1. Välj **[!UICONTROL Ny datastream]**.

   ![datastreams - startsida](assets/mobile-datastream-new.png)

1. Ange ett namn, till exempel `Luma App`.
1. Välj schemat som du skapade i föregående lektion.
1. Välj **[!UICONTROL Spara]**.

   ![nya datastreams](assets/mobile-datastream-name.png)


## Lägg till tjänster

Därefter kan du ansluta dina Experience Cloud-tjänster till ditt datastream. När Platform Mobile SDK skickar data till Edge Network skickar datastream data till dessa tjänster:

1. Lägg till **[!UICONTROL Adobe Analytics]** och ta fram en rapportserie.

1. Aktivera **[!UICONTROL Adobe Audience Manager]** (valfritt).

1. Aktivera **[!UICONTROL Adobe Experience Platform]** och tillhandahåller **[!UICONTROL datauppsättning]** (valfritt).
   * Om du inte redan har skapat en datauppsättning följer du instruktionerna [här](platform.md).

1. Den slutliga konfigurationen bör se ut ungefär så här.
   ![datastream-inställningar](assets/mobile-datastream-settings.png)


>[!NOTE]
>
>Genom att aktivera varje tjänst som din organisation använder ser du till att data som samlas in i mobilappen kan användas överallt. Mer information om datastream-inställningar finns i dokumentationen [här](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html#adobe-experience-platform-settings).

När du implementerar Platform Mobile SDK på din egen webbplats bör du skapa tre datastreams som kan kopplas till dina tre taggmiljöer (utveckling, scen och produktion). Om du använder Platform Mobile SDK med plattformsbaserade program som Adobe Real-time Customer Data Platform eller Adobe Journey Optimizer måste du se till att skapa dessa dataströmmar i rätt plattformssandlåda.

Nästa: **[Konfigurera taggar](configure-tags.md)**

>[!NOTE]
>
>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Mobile SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)
