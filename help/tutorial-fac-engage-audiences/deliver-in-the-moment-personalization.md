---
title: Leverera personalisering i ögonblicket med Edge Network
seo-title: Deliver "in-the moment" personalization using Edge Network | Engage with audiences directly from your data warehouse using Federated Audience Composition
breadcrumb-title: Leverera personalisering i ögonblicket med Edge Network
description: I den här övningen utvärderas den federerade publiken på Edge för omedelbar återmarknadsföring.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-drive-in-the-moment-personalization.jpg
exl-id: 20bfafb1-1d1b-48d8-84eb-97d4c9e03b76
source-git-commit: 93b787112134919444150974c7149dc10c2d0ca6
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 0%

---

# Leverera personalisering i ögonblicket med Edge Network

Med Federated Audience Composition kan ni berika befintliga målgrupper i Adobe Experience Platform (AEP) genom att utnyttja sammansatta målgruppsdata som har federerats från företagets datalager. Dessa data kommer inte att sparas i Adobe Experience Platform, men du kan använda funktionerna för [vidarebefordran av händelser](https://experienceleague.adobe.com/en/docs/experience-platform/tags/event-forwarding/overview){target="_blank"} för att skicka dessa data direkt till datalagret.

I den här övningen använder vi en federerad publik som frågas med kreditpoäng och låneaktivitet för att berika besökarna på webbsidan för låneansökningar.

Genom att utvärdera den här målgruppen på Edge kan vi omedelbart rikta om besökarna på den förgodkända lånesidan med personaliserade erbjudanden på webbplatsen.

![fulländad](assets/edge-audience-enrich.png)

## Steg

1. **Spara och starta** din externa målgruppskomposition. När kompositionen är klar visas den federerade publiken på målgruppsportalen.
2. **Bygg en målgruppsregel** med profilattribut och upplevelsehändelser från profiltjänsten, där din externa målgrupp ingår.

Låt oss sammanfatta detta med en [sammanfattning av inlärningar och slutliga åtgärder](conclusion.md)!
