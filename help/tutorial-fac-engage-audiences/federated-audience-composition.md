---
title: Berika målgrupper med lagerdata
seo-title: Enrich Audiences with warehouse data | Engage with audiences directly from your data warehouse using Federated Audience Composition
breadcrumb-title: Berika målgrupper med lagerdata
description: I den här övningen berikas en Experience Platform-publik med lagerdata.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-enrich-audience-with-federated-data.jpg
exl-id: 3f6aa121-0dbd-4ad9-b136-d1455eed03ca
source-git-commit: 93b787112134919444150974c7149dc10c2d0ca6
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# Berika målgrupper med lagerdata

Med Federated Audience Composition kan ni berika befintliga målgrupper i Adobe Experience Platform (AEP) genom att utnyttja sammansatta målgruppsdata som har federerats från företagets datalager. Dessa data bevaras inte i Adobe Experience Platform kundprofiler.

## Läsa en målgrupp i en sammansatt bild

I den här övningen använder vi målgruppen **SecurFinancial Loan Application Page Visitor** som lagras i Experience Platform Profile Service för att starta vår federerade komposition. Företaget använder federerade data i Snowflake för att fastställa förhandsgodkännande baserat på kreditpoäng och låneaktivitet.

![federated-composition-example](assets/snowflake-preapproval.png)

### Steg

1. **Mappa AEP-målgrupp** till sammansättningsmålet för den externa målgruppen.
2. **Bygg din komposition** med den mappade publiken som läsare.
3. **Stäm av identiteterna** i läsgruppen för att ansluta till federerade data.

![federated-method-1-1](assets/federated-method-1-1.png)

![federated-method-1-2](assets/federated-method-1-2.png)

Vi kommer att titta på ett annat exempel på hur du använder federerade data för att [stöda personalisering&quot;för ögonblicket&quot;](deliver-in-the-moment-personalization.md)!
