---
title: Konfigurera ett datastream
description: Lär dig hur du aktiverar ett datastream och konfigurerar Experience Cloud-lösningar. Den här lektionen ingår i självstudiekursen Implementera Adobe Experience Cloud med Web SDK.
feature: Web SDK,Datastreams
exl-id: 20f770d1-eb0f-41a9-b451-4069a0a91fc4
source-git-commit: aeff30f808fd65370b58eba69d24e658474a92d7
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 0%

---

# Konfigurera ett datastream

Lär dig hur du aktiverar ett datastam och konfigurerar Experience Cloud-program.

Datastreams talar om för Adobe Experience Platform Edge Network var data som samlats in av Platform Web SDK ska skickas. I datastreams-konfigurationen aktiverar du dina Experience Cloud-program, ditt Experience Platform-konto och händelsevidarebefordran. Se [Grundläggande om att konfigurera ett datastream](https://experienceleague.adobe.com/en/docs/experience-platform/edge/fundamentals/datastreams) för mer detaljerad information.


![Web SDK, datastreams och Edge Network](assets/dc-websdk-datastreams.png)

## Utbildningsmål

När lektionen är klar kan du:

* Skapa ett datastream
* Kom igång med åsidosättningar av datastream

## Förutsättningar

Innan du konfigurerar din datastream måste du ha slutfört följande lektioner:

* [Konfigurera ett schema](configure-schemas.md)
* [Konfigurera ett identitetsnamnutrymme](configure-identities.md)

## Skapa ett datastream

Nu kan du skapa en datastream som anger för Platform Edge Network var data som samlas in av Web SDK ska skickas.

**Så här skapar du ett datastream:**

1. Öppna [Gränssnitt för datainsamling](https://launch.adobe.com/){target="_blank"}
1. Kontrollera att du befinner dig i rätt sandlåda

   >[!NOTE]
   >
   >Om du använder ett plattformsbaserat program som Real-Time CDP eller Journey Optimizer rekommenderar vi att du använder en utvecklingssandlåda för den här kursen. Om du inte gör det använder du **[!UICONTROL Prod]** sandlåda.

1. Gå till **[!UICONTROL Datastreams]** till vänster navigering
1. Välj **[!UICONTROL New Datastream]** till höger på skärmen.
1. Retur `Luma Web SDK: Development Environment` som **[!UICONTROL Name]**. Namnet refereras senare när du konfigurerar Web SDK-tillägget i taggegenskapen.
1. Välj `Luma Web Event Data` som **[!UICONTROL Event Schema]**
1. Välj **[!UICONTROL Save]**

   ![Skapa datastream](assets/datastream-create-new-datastream.png)

På nästa skärm kan du lägga till tjänster som Adobe i dataströmmen, men du kommer inte att lägga till några tjänster just nu i självstudiekursen. Du kommer att göra det senare i lektionerna [Konfigurera Experience Platform](setup-experience-platform.md), [Ställ in Analytics](setup-analytics.md), [Konfigurera Audience Manager](setup-audience-manager.md), [Konfigurera mål](setup-target.md), eller [Vidarebefordran av händelser](setup-event-forwarding.md).

>[!NOTE]
>
>När du implementerar Platform Web SDK på din egen webbplats bör du skapa tre datastreams som kan kopplas till dina tre taggmiljöer (utveckling, scen och produktion). Om du använder Platform Web SDK med plattformsbaserade program som Adobe Real-time Customer Data Platform eller Adobe Journey Optimizer måste du se till att skapa dessa dataströmmar i rätt plattformssandlåda.

## Åsidosätta ett datastream

Med åsidosättningar av dataströmmar kan du definiera ytterligare konfigurationer för dina dataströmmar och sedan åsidosätta din standardkonfiguration under vissa villkor från implementeringen.


Åsidosättning av dataströmskonfiguration är en tvåstegsprocess:

1. Först definierar du åsidosättningar av datastream i datastream-konfigurationen. Detta måste göras per Adobe-program som du vill åsidosätta.
1. Sedan skickar du åsidosättningarna till Edge Network antingen via en SDK-sändningsåtgärd för Web SDK eller genom en konfiguration i tillägget för Web SDK-taggen.

I [Konfigurera Adobe Analytics](setup-analytics.md) lektioner som du åsidosätter rapportsviten för en sida med hjälp av Platform Web SDK Send Event Action.

Se [information om åsidosättning av dataströmskonfiguration](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overrides) om du vill ha detaljerade anvisningar om hur du åsidosätter datastream-konfigurationer.

Du kan nu installera tillägget Platform Web SDK i taggegenskapen!

[Nästa: ](install-web-sdk.md)

>[!NOTE]
>
>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Web SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela med dig av dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
