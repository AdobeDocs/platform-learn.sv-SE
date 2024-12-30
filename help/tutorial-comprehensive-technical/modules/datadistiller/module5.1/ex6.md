---
title: Query Service - Utforska datauppsättningen med Power BI
description: Query Service - Utforska datauppsättningen med Power BI
kt: 5342
doc-type: tutorial
exl-id: c27abd0e-e563-4702-a243-1aec84ce6116
source-git-commit: f843c50af04d744a7d769f320b5b55a5e6d25ffd
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---

# 5.1.6 Query Service och Power BI

Öppna Microsoft Power BI Desktop.

![start-power-bi.png](./images/startpowerbi.png)

Klicka på **Hämta data**.

![power-bi-get-data.png](./images/powerbigetdata.png)

Sök efter **affischer** (1), välj **Postgres** (2) i listan och **Connect** (3).

![power-bi-connect-progress.png](./images/powerbiconnectprogress.png)

Gå till Adobe Experience Platform, till **Frågor** och till **Referenser**.

![query-service-credentials.png](./images/queryservicecredentials.png)

Kopiera **Host** från sidan **Credentials** i Adobe Experience Platform och klistra in den i fältet **Server**. Kopiera sedan **Database** och klistra in den i fältet **Database** i PowerBI. Klicka sedan på OK (2).

>[!IMPORTANT]
>
>Se till att du inkluderar porten **:80** i slutet av servervärdet eftersom frågetjänsten för närvarande inte använder PostgreSQL-standardporten 5432.

![power-bi-connect-server.png](./images/powerbiconnectserver.png)

I nästa dialogruta fyller du i användarnamnet och lösenordet med ditt användarnamn och lösenord som finns i **Autentiseringsuppgifter** för frågor i Adobe Experience Platform.

![query-service-credentials.png](./images/queryservicecredentials.png)

I dialogrutan Överblick placerar du **LDAP** i sökfältet (1) för att hitta dina CTAS-datauppsättningar och markerar kryssrutan bredvid varje (2). Klicka sedan på Läs in (3).

![power-bi-load-churn-data.png](./images/powerbiloadchurndata.png)

Kontrollera att fliken **Rapport** (1) är markerad.

![power-bi-report-tab.png](./images/powerbireporttab.png)

Markera kartan (1) och förstora kartan (2) när den har lagts till på rapportarbetsytan.

![power-bi-select-map.png](./images/powerbiselectmap.png)

Därefter måste vi definiera mått och mått. Det gör du genom att dra fält från avsnittet **fält** till motsvarande platshållare (som finns under **visualiseringar**) enligt nedan:

![power-bi-drag-lat-lon.png](./images/powerbidraglatlon.png)

Som mått använder vi antalet **customerId**. Dra fältet **crmid** från avsnittet **fields** till platshållaren **Size**:

![power-bi-drag-crmid.png](./images/powerbidragcrmid.png)

Om du vill göra en del **callTopic**-analyser drar vi fältet **callTopic** till platshållaren för **sidnivåfilter** (du kan behöva rulla i avsnittet **visualiseringar** ).

![power-bi-drag-calltopic.png](./images/powerbidragcalltopic.png)

Välj/avmarkera **callTopics** för att undersöka:

![power-bi-report-select-calltopic.png](./images/powerbireportselectcalltopic.png)

Du har nu avslutat den här övningen.

Nästa steg: [5.1.8 API för frågetjänst](./ex8.md)

[Gå tillbaka till modul 5.1](./query-service.md)

[Gå tillbaka till Alla moduler](../../../overview.md)
