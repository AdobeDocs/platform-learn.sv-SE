---
title: Frågetjänst - förutsättningar
description: Frågetjänst - förutsättningar
kt: 5342
doc-type: tutorial
exl-id: e9e4d478-cb8d-42a9-87a3-319e5a8b8522
source-git-commit: 1e3a8d585503eddad4c642a3b13d2b5f7ddc9943
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# 2.1.1 Krav

## Installera PSQL Command Line Utility

Följ instruktionerna i Adobe Experience Platform-dokumentationen för att installera psql-klienten:
[PSQL - installationshandbok](https://experienceleague.adobe.com/docs/experience-platform/query/clients/psql.html?lang=sv-SE)

När du har installerat PSQL kan du behöva uppdatera din **PATH** genom att köra nedanstående kommando i ett terminalfönster:

För macOS (ersätt XX i nedanstående kommando med det PSQL-versionsnummer som du har installerat):

`export PATH=/Library/PostgreSQL/XX/bin:$PATH`

## Installera Power BI

Endast för Windows-användare

[Installera Microsoft Power BI](https://experienceleague.adobe.com/docs/experience-platform/query/clients/power-bi.html?lang=sv-SE)

Kontrollera att du har installerat den exakta versionen av **npgsql** som anges i dokumentet, annars kan du inte ansluta Power BI till Adobe Experience Platform Query Service.

## Installera Tableau

För Windows- och Mac-användare

[Installera skrivbordet &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/query/clients/tableau.html?lang=sv-SE) enligt dokumentationen.

En 14-dagars testperiod automatiskt.

Om du vill använda Tableau mer än dessa 14 dagar behöver du en licensnyckel.

## Nästa steg

Gå till [2.1.2 Komma igång](./ex2.md){target="_blank"}

Gå tillbaka till [frågetjänsten](./query-service.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../../overview.md){target="_blank"}
