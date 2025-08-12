---
title: Berika Experience Platform-målgrupper med federerade data
seo-title: Enrich Experience Platform audiences with federated data | Unlock cross-channel insights with Federated Audience Composition
breadcrumb-title: Berika Experience Platform-målgrupper med federerade data
description: I den här lektionen berikar vi en Experience Platform-publik med federerade data.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-enrich-audience-with-federated-data.jpg
hide: true
source-git-commit: a5ae2695763bc3d6dce786861dcbc15f3422c035
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 1%

---


# Federerad målgruppssammansättning

Med Federated Audience Composition kan ni berika befintliga målgrupper i Adobe Experience Platform (AEP) genom att utnyttja sammansatta målgruppsdata som har federerats från företagets datalager. Dessa data bevaras inte i Adobe Experience Platform kundprofiler.

## Olika sätt att utöka en federerad målgruppskomposition

Det finns två primära metoder för att berika en Federated Audience Composition.

### &#x200B;1. Läsa en AEP-publik i en federerad komposition

I det här första exemplet använder vi målgruppen **SecurFinancial Loan Application Page Visitor** som lagras i AEP Profile Service för att starta vår federerade komposition. Vi kommer att berika publiken med federerade data i Snowflake för att fastställa förhandsgodkännande baserat på kreditpoäng och låneverksamhet.

![federated-composition-example](assets/snowflake-preapproval.png)

1. **Mappa AEP-målgrupp** till sammansättningsmålet för den externa målgruppen.
2. **Bygg din komposition** med den mappade publiken som läsare.
3. **Stäm av identiteterna** i läsgruppen för att ansluta till federerade data.

![federated-method-1-1](assets/federated-method-1-1.png)

![federated-method-1-2](assets/federated-method-1-2.png)

### &#x200B;2. Förbättra Experience Platform Audience Rule med en federerad publik

I det andra exemplet kommer vi att använda den externa målgrupp som frågas med kreditpoäng och låneaktivitet för att berika den beteendemässiga målgruppen för besökare på webbsidor med låneansökningar.

Genom att utvärdera den här målgruppen på Edge kan vi omedelbart rikta om besökarna på den förgodkända lånesidan med personaliserade erbjudanden på webbplatsen.

![fulländad](assets/edge-audience-enrich.png)

1. **Spara och starta** din externa målgruppskomposition. När kompositionen är klar visas er externa målgrupp i målgruppsportalen.
2. **Bygg en målgruppsregel** med profilattribut och upplevelsehändelser från profiltjänsten, där din externa målgrupp ingår.

Låt oss sammanfatta detta med en [sammanfattning av inlärningar och slutliga åtgärder](conclusion.md)!
