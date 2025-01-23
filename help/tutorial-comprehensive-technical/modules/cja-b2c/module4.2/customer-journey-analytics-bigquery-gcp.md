---
title: Importera och analysera data från Google Analytics i Adobe Experience Platform med BigQuery Source Connector
description: Importera och analysera data från Google Analytics i Adobe Experience Platform med BigQuery Source Connector
kt: 5342
doc-type: tutorial
exl-id: b078d003-da25-44c5-b000-77e3b3188fb6
source-git-commit: bd46be455f88007174f7e6be9a1ce5f508edc09b
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# 4.2 Importera och analysera data från Google Analytics i Adobe Experience Platform med BigQuery Source Connector

I den här modulen ska du konfigurera en egen instans av Google Cloud Platform, läsa in exempeldata i Google Cloud Platform och sedan använda BigQuery Source Connector för att importera data från Google Cloud Platform till Adobe Experience Platform. Slutligen använder ni Customer Journey Analytics för att visualisera dessa data.

Source-kontakter i Adobe Experience Platform gör det enkelt att hämta data till Adobe Experience Platform. Google BigQuery är en av de redan tillgängliga anslutningarna. Tack vare Adobe Experience Platform och BigQuery Source Connector kan vi nu överföra Google Analytics-data till Analysis Workspace i Customer Journey Analytics.

Dessutom kan vi berika Google Analytics data genom att koppla dem till andra datakällor som CRM, Call Center eller Loyalty inom Customer Journey Analytics.

## Utbildningsmål

- Bekanta dig med användargränssnittet i Google Cloud Platform och BigQuery
- Importera data från Google Analytics till Adobe Experience Platform
- Använd Customer Journey Analytics för att analysera data från Google Analytics
- Förbättra Google Analytics data med offlinedata

## Förhandskrav

- Viss kunskap om Customer Journey Analytics är att föredra, men är inte nödvändig
- Åtkomst till Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Åtkomst till Customer Journey Analytics
- Tillgång till Google Cloud Platform och Google BigQuery
- **Hämta de här resurserna**:
   - [JSON - Exempeldata: Förmånsdata](./../../../assets/json/bqLoyalty.json)

>[!NOTE]
>
>Glöm inte att installera, konfigurera och använda Chrome-tillägget enligt [Installera Chrome-tillägget för Experience League-dokumentationen](../../gettingstarted/gettingstarted/ex1.md)

## Utövningar

[4.2.1 Börja använda Google Cloud Platform](./ex1.md)

Börja använda Google Cloud Platform-miljön.

[4.2.2 Skapa din första fråga i BigQuery](./ex2.md)

Lär dig hur du använder BigQuery för att förbereda data för inläsning till plattformen.

[4.2.3 Anslut GCP och BigQuery till Adobe Experience Platform](./ex3.md)

Lär dig hur du konfigurerar källkopplingen i Adobe Experience Platform.

[4.2.4 Läs in data från BigQuery till Adobe Experience Platform](./ex4.md)

Lär dig hur du konfigurerar BigQuery-källkopplingen i Adobe Experience Platform så att dina Google Analytics-data importeras.

[4.2.5 Analysera Google Analytics-data med Customer Journey Analytics](./ex5.md)

Lär dig hur du analyserar Google Analytics data i Customer Journey Analytics och kombinerar dem med lojalitetsdata.

[Sammanfattning och fördelar](./summary.md)

Sammanfattning av den här modulen och en översikt över fördelarna.

![Tech Insiders](./../../../assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>Tack för att du lägger ned din tid på att lära dig allt om Adobe Experience Platform och dess program. Om du har frågor kan du dela allmän feedback om dina förslag på framtida innehåll. Kontakta Tech Insiders direkt genom att skicka ett e-postmeddelande till **techinsiders@adobe.com**.

[Gå tillbaka till Alla moduler](../../../overview.md)
