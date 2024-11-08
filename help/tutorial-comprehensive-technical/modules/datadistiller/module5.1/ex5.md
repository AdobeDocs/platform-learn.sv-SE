---
title: Query Service - Utforska datauppsättningen med Power BI
description: Query Service - Utforska datauppsättningen med Power BI
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---

# 5.1.5 Query Service och Power BI

Öppna Microsoft Power BI Desktop.

![start-power-bi.png](./images/start-power-bi.png)

Klicka på **Hämta data**.

![power-bi-get-data.png](./images/power-bi-get-data.png)

Sök efter **affischer** (1), välj **Postgres** (2) i listan och **Connect** (3).

![power-bi-connect-progress.png](./images/power-bi-connect-progress.png)

Gå till Adobe Experience Platform, till **Frågor** och till **Referenser**.

![query-service-credentials.png](./images/query-service-credentials.png)

Kopiera **Host** från sidan **Credentials** i Adobe Experience Platform och klistra in den i fältet **Server**. Kopiera sedan **Database** och klistra in den i fältet **Database** i PowerBI. Klicka sedan på OK (2).

>[!IMPORTANT]
>
>Se till att du inkluderar porten **:80** i slutet av servervärdet eftersom frågetjänsten för närvarande inte använder PostgreSQL-standardporten 5432.

![power-bi-connect-server.png](./images/power-bi-connect-server.png)

I nästa dialogruta fyller du i användarnamnet och lösenordet med ditt användarnamn och lösenord som finns i **Autentiseringsuppgifter** för frågor i Adobe Experience Platform.

![query-service-credentials.png](./images/query-service-credentials.png)

I dialogrutan Överblick placerar du **LDAP** i sökfältet (1) för att hitta dina CTAS-datauppsättningar och markerar kryssrutan bredvid varje (2). Klicka sedan på Läs in (3).

![power-bi-load-churn-data.png](./images/power-bi-load-churn-data.png)

Kontrollera att fliken **Rapport** (1) är markerad.

![power-bi-report-tab.png](./images/power-bi-report-tab.png)

Markera kartan (1) och förstora kartan (2) när den har lagts till på rapportarbetsytan.

![power-bi-select-map.png](./images/power-bi-select-map.png)

Därefter måste vi definiera mått och mått. Det gör du genom att dra fält från avsnittet **fält** till motsvarande platshållare (som finns under **visualiseringar**) enligt nedan:

![power-bi-drag-lat-lon.png](./images/power-bi-drag-lat-lon.png)

Som mått använder vi antalet **customerId**. Dra fältet **crmid** från avsnittet **fields** till platshållaren **Size**:

![power-bi-drag-crmid.png](./images/power-bi-drag-crmid.png)

Om du vill göra en del **callTopic**-analyser drar vi fältet **callTopic** till platshållaren för **sidnivåfilter** (du kan behöva rulla i avsnittet **visualiseringar** ).

![power-bi-drag-calltopic.png](./images/power-bi-drag-calltopic.png)

Välj/avmarkera **callTopics** för att undersöka:

![power-bi-report-select-calltopic.png](./images/power-bi-report-select-calltopic.png)

Du har nu avslutat den här övningen.

Nästa steg: [5.1.7 API för frågetjänst](./ex7.md)

[Gå tillbaka till modul 5.1](./query-service.md)

[Gå tillbaka till Alla moduler](../../../overview.md)
