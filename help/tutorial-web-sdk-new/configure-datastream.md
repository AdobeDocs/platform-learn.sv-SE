---
title: Konfigurera ett datastream
description: Lär dig hur du aktiverar ett datastream och konfigurerar Experience Cloud-lösningar. Den här lektionen ingår i självstudiekursen Implementera Adobe Experience Cloud med Web SDK.
feature: Web SDK,Datastreams
source-git-commit: f08866de1bd6ede50bda1e5f8db6dbd2951aa872
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%

---

# Konfigurera ett datastream

Lär dig hur du aktiverar ett datastam och konfigurerar Experience Cloud-program.

Datastreams talar om för Adobe Experience Platform Edge Network var data som samlats in av Platform Web SDK ska skickas. I datastreams-konfigurationen aktiverar du dina Experience Cloud-program, ditt Experience Platform-konto och händelsevidarebefordran. Se [Grundläggande om att konfigurera ett datastream](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=en) för mer detaljerad information.

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
   >Om du använder ett plattformsbaserat program som Real-Time CDP rekommenderar vi att du använder en utvecklingssandlåda för den här självstudiekursen. Om du inte gör det använder du **[!UICONTROL Prod]** sandlåda.

1. Gå till **[!UICONTROL Datastreams]** till vänster navigering
1. Välj **[!UICONTROL Ny datastream]** till höger på skärmen.
1. Retur `Luma Web SDK: Development Environment` som **[!UICONTROL Namn]**. Namnet refereras senare när du konfigurerar Web SDK-tillägget i taggegenskapen.
1. Välj `Luma Web Event Data` som **[!UICONTROL Händelseschema]**
1. Välj **[!UICONTROL Spara]**

   ![Skapa datastream](assets/datastream-create-new-datastream.png)

   >[!AVAILABILITY]
   >
   >Mappningsfunktionen kommer att ingå i kursen vid ett senare tillfälle.




På nästa skärm kan du lägga till tjänster som Adobe i dataströmmen, men du kommer inte att lägga till några tjänster just nu i självstudiekursen. Du kommer att göra det senare i lektionerna [Konfigurera Experience Platform](setup-experience-platform.md), [Ställ in Analytics](setup-analytics.md), [Konfigurera Audience Manager](setup-audience-manager.md), [Konfigurera mål](setup-target.md), eller [Vidarebefordran av händelser](setup-event-forwarding.md).

>[!NOTE]
>
>När du implementerar Platform Web SDK på din egen webbplats bör du skapa tre datastreams som kan kopplas till dina tre taggmiljöer (utveckling, scen och produktion). Om du använder Platform Web SDK med plattformsbaserade program som Adobe Real-time Customer Data Platform eller Adobe Journey Optimizer måste du se till att skapa dessa dataströmmar i rätt plattformssandlåda.

## Åsidosätta ett datastream

Med åsidosättningar av dataströmmar kan du definiera ytterligare konfigurationer för dina dataströmmar och sedan åsidosätta din standardkonfiguration under vissa villkor från implementeringen.


Åsidosättning av dataströmskonfiguration är en tvåstegsprocess:

1. Först definierar du åsidosättningar av datastream i datastream-konfigurationen. Detta måste göras per Adobe-program som du vill åsidosätta.
1. Sedan skickar du åsidosättningarna till Edge Network antingen via en SDK-sändningshändelseåtgärd för Web SDK eller genom en konfiguration i taggtillägget för Web SDK.

Se [information om åsidosättning av dataströmskonfiguration](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overrides.html?lang=en) om du vill ha detaljerade anvisningar om hur du åsidosätter datastream-konfigurationer.

I Konfigurera Adobe Analytics-lektionen [åsidosätta rapportsviten för en sida med plattformens SDK-åtgärd för skicka händelse](setup-analytics.md).

Du kan nu installera tillägget Platform Web SDK i taggegenskapen!

[Nästa: ](install-web-sdk.md)

>[!NOTE]
>
>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Web SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela med dig av dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
