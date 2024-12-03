---
title: Frågetjänst
description: Frågetjänst
kt: 5342
doc-type: tutorial
exl-id: 6eb65de3-d0e8-49d4-a702-5c9d6a1952b7
source-git-commit: b53ee64ae8438b8f48f842ed1f44ee7ef3e813fc
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 1%

---

# 5.1 Query Service

I den här modulen får du en praktisk förhandsgranskning av Adobe Experience Platform Query Service. Med frågetjänsten kan du utföra flerkanalsfrågor i alla Adobe Experience Cloud-programdata, förena och analysera data i Adobe Campaign, Analytics, Audience Manager, Target och Advertising Cloud samt andra kunddata som läses in/infogas i Adobe Experience Platform.

Query Service är ett serverlöst verktyg. Den stöder SQL-frågor och anslutningar från flera klientprogram genom sin PostSQL-kompatibilitet.
Vi kommer att använda data som har injicerats i plattformen med antingen Web Interaction Data, Call Center Interactions i kombination med kundlojalitetsdata som överförts till plattformen.

## Utbildningsmål

- Bekanta dig med Adobe Experience Platform användargränssnitt
- Anslut till frågetjänsten och kör dina SQL-frågor
- Utforska datauppsättningar i Adobe Experience Platform
- Koppla Tableu eller Power BI till Adobe Experience Platform Query Service för att skapa visualiseringar och rapporter

## Förhandskrav

- Viss kunskap om SQL är att föredra, men behövs inte
- Åtkomst till Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Datauppsättningar (datauppsättningar som används under labben, förinlästa åt dig)
- PostgreSQL
- Tableau eller Microsoft Power BI Desktop
- **Hämta de här resurserna**:
   - [JSON - Exempeldata: Webbplatsinteraktioner](./../../../assets/json/ee.json)
   - [JSON - Exempeldata: Interaktioner mellan callcenter](./../../../assets/json/callcenter.json)
   - [JSON - Exempeldata: Lojalitet](./../../../assets/json/loyalty.json)

>[!NOTE]
>
>Glöm inte att installera, konfigurera och använda Chrome-tillägget enligt [Installera Chrome-tillägget för Experience League-dokumentationen](../../gettingstarted/gettingstarted/ex1.md)

## Utövningar

[5.1.1 Krav](./ex1.md)

Du måste installera PSQL för att kunna köra frågorna i den här aktiveringsövningen. Beroende på vilket operativsystem du har måste du installera Microsoft Power BI eller Tableau. Windows-användare kan välja mellan Power BI och Tableau. Mac-användare bör installera Tableau.

[5.1.2 Komma igång](./ex2.md)

I den här övningen ska du utforska Adobe Experience Platform Query Service-användargränssnittet, lära dig mer om datauppsättningar, hitta dina frågor och slutligen konfigurera en anslutning från PSQL.

[5.1.3 Använda frågetjänsten](./ex3.md)

I den här övningen får du lära dig mer om den grundläggande frågetjänstens syntax och du kan identifiera attributen för XDM-schemat i din fråga.

[5.1.4 Frågor, frågor, frågor ... och kundanalys](./ex4.md)

I den här övningen kommer du att göra frågor, medan du gör någon omsättningsanalys, lära dig mer om de Adobe-definierade funktionerna. När du är klar skriver du en fråga för att förbereda en datauppsättning för användning i Microsoft Power BI.

[5.1.5 Generera en datauppsättning från en fråga](./ex5.md)

I den här övningen genererar du en datauppsättning från en fråga som kördes tidigare och du kommer att använda den här datauppsättningen i nästa övning.

[5.1.6 Query Service och Power BI](./ex6.md)

I den här övningen ansluter du Power BI till Adobe Experience Platform och frågetjänsten för att utföra callcenter-interaktionsanalys.

[5.1.7 Query Service och Tableau](./ex7.md)

I den här övningen ansluter du Tableau till Adobe Experience Platform och Query Service för att utföra Callcenter Interaction Analysis.

[5.1.8 Query Service API](./ex8.md)

I den här övningen ska du använda API:t för frågetjänsten för att hantera frågemallar och frågescheman.

[Sammanfattning och fördelar](./summary.md)

Sammanfattning av den här modulen och en översikt över fördelarna.

>[!NOTE]
>
>Tack för att du lägger ned din tid på att lära dig allt om Adobe Experience Platform och dess program. Om du har frågor kan du dela allmän feedback om dina förslag på framtida innehåll. Kontakta Tech Insiders direkt genom att skicka ett e-postmeddelande till **techinsiders@adobe.com**.

[Gå tillbaka till Alla moduler](../../../overview.md)
