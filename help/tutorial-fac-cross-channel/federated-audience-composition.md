---
title: Berika Experience Platform-målgrupper med federerade data
seo-title: Enrich Experience Platform audiences with federated data | Unlock cross-channel insights with Federated Audience Composition
breadcrumb-title: Berika Experience Platform-målgrupper med federerade data
description: I den här visuella övningen berikas en Experience Platform-publik med federerade data.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-enrich-audience-with-federated-data.jpg
exl-id: 3f6aa121-0dbd-4ad9-b136-d1455eed03ca
source-git-commit: 3de9721332379f9fd3dd45768ba2ca2308e09357
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 0%

---

# Berika Experience Platform-målgrupper med federerade data

Med Federated Audience Composition kan ni berika befintliga målgrupper i Adobe Experience Platform (AEP) genom att utnyttja sammansatta målgruppsdata som har federerats från företagets datalager. Dessa data bevaras inte i Adobe Experience Platform kundprofiler.

## Läsa en AEP-publik i en federerad komposition

I den här visuella övningen använder vi målgruppen **SecurFinancial Loan Application Page Visitor** som lagras i AEP Profile Service för att starta vår federerade komposition. Företaget använder federerade data i Snowflake för att fastställa förhandsgodkännande baserat på kreditpoäng och låneaktivitet.

![federated-composition-example](assets/snowflake-preapproval.png)

### Steg

1. **Mappa AEP-målgrupp** till sammansättningsmålet för den externa målgruppen.
2. **Bygg din komposition** med den mappade publiken som läsare.
3. **Stäm av identiteterna** i läsgruppen för att ansluta till federerade data.

![federated-method-1-1](assets/federated-method-1-1.png)

![federated-method-1-2](assets/federated-method-1-2.png)

Vi kommer att titta på ett annat exempel på hur du använder federerade data för att [stöda personalisering&quot;för ögonblicket&quot;](drive-in-the-moment-personalization.md)!
