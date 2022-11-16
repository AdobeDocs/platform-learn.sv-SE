---
title: Importera och analysera Google Analytics-data i Adobe Experience Platform med BigQuery Source Connector
description: Importera och analysera Google Analytics-data i Adobe Experience Platform med BigQuery Source Connector
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: c9c28b5a-d158-49fa-9533-1a295876f6c4
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 0%

---

# 12. Importera och analysera Google Analytics-data i Adobe Experience Platform med BigQuery Source Connector

**Författare: [Victor de la Iglesia](https://www.linkedin.com/in/victordelaiglesia/), [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

I den här modulen ska du konfigurera en egen instans av Google Cloud Platform, läsa in exempeldata i Google Cloud Platform och sedan använda BigQuery Source Connector för att importera data från Google Cloud Platform till Adobe Experience Platform. Slutligen använder ni Customer Journey Analytics för att visualisera dessa data.

Källkopplingar i Adobe Experience Platform gör det enkelt att hämta data till Adobe Experience Platform. Google BigQuery är en av de redan tillgängliga anslutningarna. Tack vare Adobe Experience Platform och BigQuery Source Connector kan vi nu föra in Google Analytics data i Analysis Workspace i Customer Journey Analytics.

Dessutom kan vi berika Google Analytics data genom att koppla dem till andra datakällor som CRM, Call Center eller Loyalty inom Customer Journey Analytics.

## Utbildningsmål

- Bekanta dig med användargränssnittet i Google Cloud Platform och BigQuery
- Importera data från Google Analytics till Adobe Experience Platform
- Använd Customer Journey Analytics för att analysera data från Google Analytics
- Förbättra Google Analytics data med offlinedata

## Förutsättningar

- Viss kunskap om Customer Journey Analytics är att föredra, men är inte nödvändig
- Tillgång till Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Åtkomst till Customer Journey Analytics
- Tillgång till Google Cloud Platform och Google BigQuery
- **Hämta dessa resurser**:
   - [JSON - Exempeldata: Förmånsdata](./../../assets/json/bqLoyalty.json)

>[!IMPORTANT]
>
>Den här självstudiekursen har skapats för att underlätta ett visst workshop-format. Den använder specifika system och konton som du kanske inte har tillgång till. Även om ni inte har tillgång till dem tror vi att ni fortfarande kan lära er mycket genom att läsa igenom detta mycket detaljerade innehåll. Om du deltar i något av seminarierna och behöver dina inloggningsuppgifter, kontakta din Adobe-representant som kommer att ge dig den information som krävs.

## Arkitektur - översikt

Titta närmare på arkitekturen nedan, som visar vilka komponenter som kommer att diskuteras och användas i den här modulen.

![Arkitektur - översikt](../../assets/images/architecturem16.png)

## Sandlåda att använda

Använd den här sandlådan för den här modulen: `--aepSandboxId--`.

>[!NOTE]
>
>Glöm inte att installera, konfigurera och använda Chrome-tillägget enligt referensen i [0.1 - Installera Chrome-tillägget för Experience League-dokumentationen](../module0/ex1.md)

## Utövningar

[12.1 Skapa ett Google Cloud Platform-konto](./ex1.md)

Skapa ett Google Cloud Platform-konto.

[12.2 Skapa din första fråga i BigQuery](./ex2.md)

Lär dig hur du använder BigQuery för att förbereda data för inläsning till plattformen.

[12.3 Anslut GCP och BigQuery till Adobe Experience Platform](./ex3.md)

Lär dig hur du konfigurerar källkopplingen i Adobe Experience Platform.

[12.4 Läs in data från BigQuery till Adobe Experience Platform](./ex4.md)

Lär dig hur du konfigurerar BigQuery-källkopplingen i Adobe Experience Platform så att dina Google Analytics-data importeras.

[12.5 Analysera Google Analytics-data med Customer Journey Analytics](./ex5.md)

Lär dig hur du analyserar Google Analytics data i Customer Journey Analytics och kombinerar dem med lojalitetsdata.

[Sammanfattning och fördelar](./summary.md)

Sammanfattning av den här modulen och en översikt över fördelarna.

>[!NOTE]
>
>Tack för att du lade ned din tid på att lära dig allt om Adobe Experience Platform. Om du har frågor kan du dela allmän feedback om dina förslag på framtida innehåll. Kontakta Wouter Van Geluwe direkt genom att skicka ett e-postmeddelande till **vangeluw@adobe.com**.

[Gå tillbaka till Alla moduler](../../overview.md)
