---
title: Konfigurera ett datastream för plattformens SDK-implementeringar
description: Lär dig hur du skapar ett datastream i Experience Platform.
feature: Mobile SDK,Datastreams
jira: KT-14625
exl-id: 7b83f834-d1fb-45d1-8bcf-bc621f94725c
source-git-commit: 25f0df2ea09bb7383f45a698e75bd31be7541754
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 0%

---

# Skapa ett datastream

Lär dig hur du skapar ett datastream i Experience Platform.

En datastream är en konfiguration på serversidan på Platform Edge Network. Datastream säkerställer att inkommande data till Platform Edge Network dirigeras till Adobe Experience Cloud-program och -tjänster på rätt sätt. Mer information finns i [dokumentation](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html) eller [video](https://experienceleague.adobe.com/docs/platform-learn/data-collection/edge-network/configure-datastreams.html).

![Arkitektur](assets/architecture.png)

## Förutsättningar

Om du vill skapa en datastream måste din organisation ha etablerats för den här funktionen i gränssnittet för datainsamling (tidigare [!UICONTROL Starta]) och du måste ha användarbehörighet för att hantera och visa datastölar.

## Utbildningsmål

I den här lektionen kommer du att:

* Ta reda på när en datastream ska användas.
* Skapa en datastream.
* Konfigurera en datastream.

## Skapa ett datastream

Datastreams kan skapas i [!UICONTROL Datainsamling] -gränssnittet med [!UICONTROL Datastream] konfigurationsverktyg. Så här skapar du ett datastream:

1. Se till att du är i rätt Experience Platform-sandlåda, eftersom datastreams definieras på en sandlådenivå.
1. Välj **[!UICONTROL Datastreams]** till vänster.
1. Välj **[!UICONTROL Ny datastream]**.

   ![datastreams - startsida](assets/datastream-new.png)

1. Ange en **[!UICONTROL Namn]**, till exempel `Luma Mobile App` och **[!UICONTROL Beskrivning]**, till exempel `Datastream for Luma Mobile App`.

   >[!NOTE]
   >
   >Sista påminnelsen: Om du går igenom den här självstudiekursen med flera personer i en och samma sandlåda eller använder ett delat konto bör du överväga att lägga till eller föregå en identifiering som en del av namngivningskonventionerna. I stället för `Luma Mobile App Event Dataset`, använda `Luma Mobile App Event Dataset - Joe Smith`. Se även anteckningen i [Ökning](overview.md).

1. Välj schemat som du skapade i föregående lektion från **Händelseschema** lista.
1. Välj **[!UICONTROL Spara]**.

   ![nya datastreams](assets/datastream-name.png)


## Lägg till tjänster

När du går igenom (valfritt) [Analyser](analytics.md) och [Experience Platform](platform.md) lektioner i den här självstudiekursen lägger du till tjänster i din datastam så att data som skickas till Platform Edge Network vidarebefordras till dessa program.

<!--

### Adobe Analytics

1. Select **[!UICONTROL Add Service]**.

1. Add **[!UICONTROL Adobe Analytics]** from the [!UICONTROL Service] list, 

1. Enter the name of the report site that you want to use in **[!UICONTROL Report Suite ID]**.

1. Enable the service by switching **[!UICONTROL Enabled]** on.

1. Select **[!UICONTROL Save]**.

   ![Add Adobe Analytics as datastream service](assets/datastream-service-aa.png)


### Adobe Experience Platform

You might also want to enable the Adobe Experience Platform service. 

>[!IMPORTANT]
>
>You can only enable the Adobe Experience Platform service when having created an event dataset. If you don't already have an event dataset created, follow the instructions [here](platform.md).

1. Click ![Add](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Add Service]** to add another service.

1. Select **[!UICONTROL Adobe Experience Platform]** from the [!UICONTROL Service] list.

1. Enable the service by switching **[!UICONTROL Enabled]** on.

1. Select the **[!UICONTROL Event Dataset]** that you created as part of the [Create a dataset](platform.md#create-a-dataset) instructions, for example **Luma Mobile App Event Dataset**

1. Select **[!UICONTROL Save]**.

   ![Add Adobe Experience Platform as a datastream service](assets/datastream-service-aep.png)
1. The final configuration should look something like this.
   
   ![datastream settings](assets/datastream-settings.png)

-->


>[!NOTE]
>
>Genom att aktivera varje tjänst som din organisation använder ser du till att data som samlas in i mobilappen kan användas överallt. Mer information om datastream-inställningar finns i dokumentationen [här](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html).

När du implementerar Platform Mobile SDK i din egen app bör du skapa tre datastreams som kan kopplas till dina tre taggmiljöer (utveckling, scen och produktion). Om du använder Platform Mobile SDK med plattformsbaserade program som Adobe Real-time Customer Data Platform eller Adobe Journey Optimizer måste du se till att skapa dessa datastölar i rätt sandlåda.

>[!SUCCESS]
>
>Du har nu ett datastream att använda för resten av självstudiekursen.
>
>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Mobile SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Nästa: **[Konfigurera en taggegenskap](configure-tags.md)**
