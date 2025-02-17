---
title: Importera och analysera Google Analytics-data i Adobe Experience Platform med BigQuery Source Connector
description: Importera och analysera Google Analytics-data i Adobe Experience Platform med BigQuery Source Connector
kt: 5342
doc-type: tutorial
exl-id: 19266ac3-7c93-4cdb-8b65-75ce5c38649c
source-git-commit: 1e3a8d585503eddad4c642a3b13d2b5f7ddc9943
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# 1.2 Infoga och analysera Google Analytics-data i Adobe Experience Platform med BigQuery Source Connector

I den här modulen ska du konfigurera en egen instans av Google Cloud Platform, läsa in exempeldata i Google Cloud Platform och sedan använda BigQuery Source Connector för att importera data från Google Cloud Platform till Adobe Experience Platform. Slutligen använder ni Customer Journey Analytics för att visualisera dessa data.

Source-kontakter i Adobe Experience Platform gör det enkelt att hämta data till Adobe Experience Platform. Google BigQuery är en av de redan tillgängliga anslutningarna. Tack vare Adobe Experience Platform och BigQuery Source Connector kan vi nu överföra Google Analytics-data till Analysis Workspace i Customer Journey Analytics.

Dessutom kan vi berika Google Analytics-data genom att koppla dem till andra datakällor som CRM, Call Center eller Loyalty inom Customer Journey Analytics.

## Utbildningsmål

- Bekanta dig med användargränssnittet i Google Cloud Platform och BigQuery
- Infoga Google Analytics-data i Adobe Experience Platform
- Använd Customer Journey Analytics för att analysera Google Analytics-data
- Förbättra Google Analytics-data med offlinedata

## Förhandskrav

- Viss kunskap om Customer Journey Analytics är att föredra, men är inte nödvändig
- Åtkomst till Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Tillgång till Customer Journey Analytics
- Tillgång till Google Cloud Platform och Google BigQuery
- **Hämta de här resurserna**:
   - [JSON - Exempeldata: Förmånsdata](./../../../../assets/json/bqLoyalty.json)

>[!NOTE]
>
>Glöm inte att installera, konfigurera och använda Chrome-tillägget enligt [Installera Chrome-tillägget för Experience League-dokumentationen](../../../getting-started/gettingstarted/ex1.md)

## Utövningar

[1.2.1 Börja använda Google Cloud Platform](./ex1.md)

Börja använda Google Cloud Platform-miljön.

[1.2.2 Skapa din första fråga i BigQuery](./ex2.md)

Lär dig hur du använder BigQuery för att förbereda data för inläsning till plattformen.

[1.2.3 Anslut GCP och BigQuery till Adobe Experience Platform](./ex3.md)

Lär dig hur du konfigurerar källkopplingen i Adobe Experience Platform.

[1.2.4 Läs in data från BigQuery till Adobe Experience Platform](./ex4.md)

Lär dig hur du konfigurerar BigQuery-källkopplingen i Adobe Experience Platform för att importera dina Google Analytics-data.

[1.2.5 Analysera Google Analytics-data med Customer Journey Analytics](./ex5.md)

Lär dig hur du analyserar Google Analytics-data i Customer Journey Analytics och kombinerar dem med lojalitetsdata.

[Sammanfattning och fördelar](./summary.md)

Sammanfattning av den här modulen och en översikt över fördelarna.

![Tech Insiders](./../../../../assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>Tack för att du lägger ned din tid på att lära dig allt om Adobe Experience Platform och dess program. Om du har frågor kan du dela allmän feedback om dina förslag på framtida innehåll. Kontakta Tech Insiders direkt genom att skicka ett e-postmeddelande till **techinsiders@adobe.com**.

[Gå tillbaka till Alla moduler](./../../../../overview.md)
