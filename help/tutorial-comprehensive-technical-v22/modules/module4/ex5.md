---
title: Frågetjänst - Utforska datauppsättningen med Power BI
description: Frågetjänst - Utforska datauppsättningen med Power BI
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst, BI Expert
doc-type: tutorial
activity: develop
exl-id: 0f9e6719-056b-4858-8c86-04b3beaa950e
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# 4.5 Query Service och Power BI

Öppna Microsoft Power BI Desktop.

![start-power-bi.png](./images/start-power-bi.png)

Klicka **Hämta data**.

![power-bi-get-data.png](./images/power-bi-get-data.png)

Sök efter **affischer** (1), välja **Postgres** (2) från förteckningen och **Anslut** (3).

![power-bi-connect-progress.png](./images/power-bi-connect-progress.png)

Gå till Adobe Experience Platform **Frågor** och till **Autentiseringsuppgifter**.

![query-service-credentials.png](./images/query-service-credentials.png)

Från **Autentiseringsuppgifter** i Adobe Experience Platform, kopiera **Värd** och klistra in den i **Server** och kopiera **Databas** och klistra in den i **Databas** i PowerBI och klicka sedan på OK (2).

>[!IMPORTANT]
>
>Se till att inkludera port **:80** i slutet av servervärdet eftersom frågetjänsten för närvarande inte använder PostgreSQL-standardporten 5432.

![power-bi-connect-server.png](./images/power-bi-connect-server.png)

I nästa dialogruta fyller du i användarnamnet och lösenordet med ditt användarnamn och lösenord som finns i dialogrutan **Autentiseringsuppgifter** för frågor i Adobe Experience Platform.

![query-service-credentials.png](./images/query-service-credentials.png)

I dialogrutan Överblick placerar du **LDAP** i sökfältet (1) för att hitta dina CTAS-datauppsättningar och markera kryssrutan bredvid varje (2). Klicka sedan på Läs in (3).

![power-bi-load-churn-data.png](./images/power-bi-load-churn-data.png)

Se till att **Rapport** -fliken (1) är markerad.

![power-bi-report-tab.png](./images/power-bi-report-tab.png)

Markera kartan (1) och förstora kartan (2) när den har lagts till på rapportarbetsytan.

![power-bi-select-map.png](./images/power-bi-select-map.png)

Därefter måste vi definiera mått och mått. Det gör du genom att dra fält från **fält** till motsvarande platshållare (finns under **visualiseringar**) enligt nedan:

![power-bi-drag-lat-lon.png](./images/power-bi-drag-lat-lon.png)

Som mått kommer vi att använda ett antal **customerId**. Dra **krut** fält från **fält** till **Storlek** platshållare:

![power-bi-drag-crmid.png](./images/power-bi-drag-crmid.png)

Till sist: **callTopic** analys, vi drar **callTopic** till **Sidnivåfilter** platshållare (du kan behöva rulla i **visualiseringar** avsnitt),

![power-bi-drag-calltopic.png](./images/power-bi-drag-calltopic.png)

Markera/avmarkera **callTopics** undersöka

![power-bi-report-select-calltopic.png](./images/power-bi-report-select-calltopic.png)

Du har nu avslutat den här övningen.

Nästa steg: [4.7 Query Service API](./ex7.md)

[Gå tillbaka till modul 4](./query-service.md)

[Gå tillbaka till Alla moduler](../../overview.md)
