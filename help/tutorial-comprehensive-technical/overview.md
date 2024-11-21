---
title: Översikt
description: Utgångspunkt för datatekniker, dataanalytiker, dataarkitekter, datavetenskaper, Orchestration Engineers och Marketers för att få en fullständig förståelse för affärsvärdet hos Adobe Experience Platform och alla dess programtjänster.
doc-type: multipage-overview
hide: false
exl-id: 88c19383-c185-40f0-b118-6cb82db0ce0e
source-git-commit: b6c98ca773ba46205c467321a7796c29b614e75c
workflow-type: tm+mt
source-wordcount: '1511'
ht-degree: 0%

---

# Omfattande teknisk självstudiekurs för Adobe Experience Platform

## Översikt

Den här självstudiekursen är den perfekta utgångspunkten för datatekniker, dataanalytiker, dataarkitekter, datavetare, Orchestration-tekniker och marknadsförare för att få en fullständig förståelse för Adobe Experience Platform affärsvärde och alla dess programtjänster. Varje lektion fokuserar på en verklig utmaning som företag står inför i dagens komplexa ekosystem av personalisering och bryter ned hur Experience Platform löser den utmaningen i olika praktiska övningar.

Självstudiekursen är mycket varierad och ger tydliga insikter i följande program:

- Adobe Experience Platform
- Adobe Experience Platform Data Collection
- CDP i realtid
- Adobe Journey Optimizer
- Customer Journey Analytics

Den här självstudiekursen fokuserar inte bara på Adobe-program utan tar hänsyn till det större ekosystem som varumärkena använder. I vissa lektioner fokuserar vi på hur _program som inte är Adobe_ kan integreras med Adobe Experience Platform. Därför får du en djupgående förståelse för hur följande program kommer att fungera tillsammans med Adobe Experience Platform:

- Amazon: AWS Lambda, AWS S3, AWS Kinesis
- Google: Google Cloud Platform, Google BigQuery, Google Display&amp;Video 360, Google AdWords
- Microsoft: Power BI, Azure EventHub, Azure Blob Storage
- Salesforce: Tableau
- Apache Kafka
- Postman
- ...

När du är klar med övningarna i den här självstudien kan du:

- Konfigurera scheman, fältgrupper, datauppsättningar och identiteter
- Konfigurera en Adobe Experience Platform Data Collection-egenskap och konfigurera det nya Web SDK-tillägget i Adobe Experience Platform Data Collection
- Strömma data i Adobe Experience Platform i realtid med Adobe Experience Platform Data Collection
- Batchimportera data till Adobe Experience Platform med ett arbetsflöde eller med ett ETL-program (extract, transform, load)
- Visualisera och använda kundprofilen i realtid i Adobe Experience Platform
- Skapa målgrupper
- Förbruka flera Adobe Experience Platform API:er
- Använd SQL för att fråga dina data i Adobe Experience Platform
- Konfigurera och kör utlösarbaserade resor i realtid
- Använd CDP i realtid för att agera genom att aktivera en målgrupp till olika destinationer
- Använd Customer Journey Analytics för att rapportera flerkanaliga kunddata från olika källor, inklusive Google BigQuery

## Förhandskrav

- Åtkomst till Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Åtkomst till Adobe Experience Platform Data Collection: [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)
- Åtkomst till demosystemet: [https://dsn.adobe.com/](https://dsn.adobe.com/)

## Videor

Du kan hitta många intressanta videor från vårt Tech Academy-webbseminarium, från bootcamp med mera på vår [Experience Makers Community YouTube-kanal](https://www.youtube.com/channel/UCUKG2dkZ9pYuZUPebQ21jUw).

## Innehåll

[0. Komma igång](./modules/gettingstarted/gettingstarted/getting-started.md)

- **Målgrupp:** Alla deltagare i den omfattande tekniska självstudiekursen för Adobe Experience Platform
- **Krav:** Åtkomst till Demo System Next, Adobe Experience Platform och Adobe Experience Platform Data Collection.
- **Beskrivning:** I den här grundläggande modulen konfigurerar du allt så att du kan komma åt och använda demomiljön.
- **Tidsinvestering:** 30 minuter

### 1. Datainsamling

[1.1 Foundation - konfiguration av Adobe Experience Platform Data Collection &amp; Web SDK](./modules/datacollection/module1.1/data-ingestion-launch-web-sdk.md)

- **Målgrupp:** Datatekniker, dataarkitekt
- **Krav:** Åtkomst till Adobe Experience Platform och Adobe Experience Platform datainsamling.
- **Beskrivning:** I den här grundläggande modulen får du lära dig mer om Adobe Experience Platform Data Collection och det nya Web SDK-tillägget.
- **Tidsinvestering:** 30 minuter

[1.2 Foundation - datainmatning](./modules/datacollection/module1.2/data-ingestion.md)

- **Målgrupp:** Datatekniker, dataarkitekt
- **Krav:** Åtkomst till Adobe Experience Platform och Adobe Experience Platform datainsamling.
- **Beskrivning:** I den här grundläggande modulen importerar du data från webbplatsen till plattformen
- **Tidsinvestering:** 120 minuter

[1.3 Sammansatt målgrupp](./modules/datacollection/module1.3/fac.md)

- **Målgrupp:** Dataanalytiker, datatekniker, dataarkitekt
- **Krav:** Åtkomst till Adobe Experience Platform
- **Beskrivning:** I den här modulen får du lära dig att konfigurera ett eget Apache Kafka-kluster, definiera ämnen, producenter och konsumenter samt strömma data till Adobe Experience Platform med Adobe Experience Platform Sink Connector för Kafka Connect.
- **Tidsinvestering:** 90 minuter

### 2. Real-Time CDP

[2.1 Foundation - kundprofil i realtid](./modules/rtcdp-b2c/module2.1/real-time-customer-profile.md)

- **Målgrupp:** Datatekniker, dataarkitekt, marknadsförare
- **Krav:** Åtkomst till Adobe Experience Platform och Postman
- **Beskrivning:** I den här grundläggande modulen utforskar du kundprofilen i realtid i Adobe Experience Platform genom att använda gränssnittet och API:t.
- **Tidsinvestering:** 90 minuter
- **Hämta de här resurserna**:
   - [Postman-samlingar](./assets/postman/postman_profile.zip)

[2.2 Intelligenta tjänster](./modules/rtcdp-b2c/module2.2/intelligent-services.md)

- **Målgrupp:** Datatekniker, dataarkitekt, datavetare
- **Krav:** Åtkomst till Adobe Experience Platform, Intelligenta tjänster
- **Beskrivning:** I den här modulen får du lära dig hur du konfigurerar, konfigurerar och använder Adobe Experience Platform Intelligent Services.
- **Tidsinvestering:** 60 minuter

[2.3 Real-Time CDP - Bygg en målgrupp och agera](./modules/rtcdp-b2c/module2.3/real-time-cdp-build-a-segment-take-action.md)

- **Målgrupp:** Dataarkitektur, Orchestration-tekniker, Marketer
- **Krav:** Åtkomst till Adobe Experience Platform, CDP, Adobe Audience Manager, Adobe Target, AWS S3 i realtid
- **Beskrivning:** I den här modulen konfigurerar du en målgrupp och aktiverar målgruppen till flera mål, inklusive Google DV360, Adobe Target och AWS S3.
- **Tidsinvestering:** 90 minuter

[2.4 Real-Time CDP: Audience Activation till Microsoft Azure Event Hub](./modules/rtcdp-b2c/module2.4/segment-activation-microsoft-azure-eventhub.md)

- **Målgrupp:** Datatekniker, dataarkitekt, dataanalytiker
- **Krav:** Åtkomst till Adobe Experience Platform, CDP i realtid och Microsoft Azure
- **Beskrivning:** I den här modulen konfigurerar du ett Microsoft Azure EventHub-mål som realtidsmål för Adobe Experience Platform CDP i realtid. Du kommer också att konfigurera och distribuera en Azure-funktion som aktiveras i realtid när Adobe Experience Platform levererar en målgruppsnyttolast till ditt Azure EventHub-mål. Azure-funktionen som du utlöser visar mekanismen för Adobe Experience Platform CDP:s aktiveringsfunktioner i realtid.
Som en del av den här modulen får du också en förståelse för vad som utlöser CDP i realtid för att faktiskt leverera en nyttolast till en angiven destination. Vi kommer också att diskutera status för en målgruppskvalifikation och hur den hör ihop med aktiveringen.
- **Tidsinvestering:** 90 minuter

[2.5 Real-Time CDP Connections: Event Forwarding](./modules/rtcdp-b2c/module2.5/aep-data-collection-ssf.md)

- **Målgrupp:** Datatekniker, dataarkitekt, dataanalytiker
- **Förutsättningar:** Åtkomst till egenskaper för Real-Time CDP-anslutningar, taggar och händelsevidarebefordran
- **Beskrivning:** I den här modulen använder du de tidigare konfigurerade datauppsättningarna, scheman och Adobe Experience Platform Data Collection-egenskapen för att samla in data och vidarebefordrar sedan den till en valfri slutpunkt.
- **Tidsinvestering:** 90 minuter

[2.6 Strömma data från Apache Kafka till Real-Time CDP](./modules/rtcdp-b2c/module2.6/aep-apache-kafka.md)

- **Målgrupp:** Dataanalytiker, datatekniker, dataarkitekt
- **Krav:** Åtkomst till Adobe Experience Platform
- **Beskrivning:** I den här modulen får du lära dig att konfigurera ett eget Apache Kafka-kluster, definiera ämnen, producenter och konsumenter samt strömma data till Adobe Experience Platform med Adobe Experience Platform Sink Connector för Kafka Connect.
- **Tidsinvestering:** 90 minuter

### 3. Adobe Journey Optimizer B2C

[3.1 Adobe Journey Optimizer: Orchestration](./modules/ajo-b2c/module3.1/journey-orchestration-create-account.md)

- **Målgrupp:** Datatekniker, dataarkitekt, Orchestration-tekniker
- **Krav:** Åtkomst till Adobe Experience Platform och Adobe Journey Optimizer
- **Beskrivning:** I den här modulen använder du Adobe Journey Optimizer för att skapa en utlösarbaserad resa.
- **Tidsinvestering:** 60 minuter

[3.2 Adobe Journey Optimizer: Externa datakällor och anpassade åtgärder](./modules/ajo-b2c/module3.2/journey-orchestration-external-weather-api-sms.md)

- **Målgrupp:** Datatekniker, dataarkitekt, Orchestration-tekniker, marknadsförare
- **Förutsättningar:** Åtkomst till Adobe Experience Platform, Adobe Journey Optimizer, Open Weather API, Twilio
- **Beskrivning:** I den här modulen använder du Adobe Journey Optimizer för att lyssna på kundbeteende, både online och offline, och svara på det på ett intelligent, sammanhangsberoende och i realtid via olika kanaler.
- **Tidsinvestering:** 90 minuter

[3.3 Adobe Journey Optimizer: Offer decisioning](./modules/ajo-b2c/module3.3/offer-decisioning.md)

- **Målgrupp:** Datatekniker, dataarkitekt, Orchestration-tekniker, marknadsförare
- **Krav:** Åtkomst till Adobe Experience Platform och Offer decisioning
- **Beskrivning:** I den här modulen använder du programtjänsten Adobe Experience Platform - erbjudanden/beslut på ett praktiskt sätt för att konfigurera anpassade erbjudanden och din egen erbjudandeaktivitet.
- **Tidsinvestering:** 120 minuter

[3.4 Adobe Journey Optimizer: Händelsebaserade resor](./modules/ajo-b2c/module3.4/journeyoptimizer.md)

- **Målgrupp:** E-postmarknadsförare, Orchestration-specialist, datatekniker, dataarkitekt, dataanalytiker
- **Krav:** Åtkomst till Adobe Experience Platform och Journey Optimizer
- **Beskrivning:** I den här modulen får du lära dig allt om Journey Optimizer, som hjälper företag att utforma och leverera sammankopplade, kontextuella och personaliserade upplevelser till sina kunder.
- **Tidsinvestering:** 120 minuter

### 4. Adobe Customer Journey Analytics

[4.1 Customer Journey Analytics: Skapa en kontrollpanel med Analysis Workspace ovanpå Adobe Experience Platform](./modules/cja-b2c/module4.1/customer-journey-analytics-build-a-dashboard.md)

- **Målgrupp:** Datatekniker, dataarkitekt, dataanalytiker
- **Krav:** Åtkomst till Adobe Experience Platform och Customer Journey Analytics
- **Beskrivning:** I den här modulen kan du komma åt offlineinsikter genom att konfigurera en instrumentpanel som innehåller flerkanalsdata som webbplatsinteraktioner, mobilappsinteraktioner, Call Center-interaktioner, interaktioner i butiken och mycket annat.
- **Tidsinvestering:** 120 minuter

[4.2 Customer Journey Analytics: Importera och analysera data från Google Analytics i Adobe Experience Platform med BigQuery Source Connector](./modules/cja-b2c/module4.2/customer-journey-analytics-bigquery-gcp.md)

- **Målgrupp:** Datatekniker, dataarkitekt, dataanalytiker
- **Krav:** Åtkomst till Adobe Experience Platform, Customer Journey Analytics, Google Cloud Platform, Google BigQuery
- **Beskrivning:** I den här modulen skapar du en egen instans av Google Cloud Platform, läser in demodata i Google Cloud Platform och använder sedan BigQuery Source Connector för att importera data från Google Cloud Platform till Adobe Experience Platform. Slutligen använder ni Customer Journey Analytics för att visualisera dessa data.
- **Tidsinvestering:** 120 minuter
- **Hämta de här resurserna**:
   - [JSON - Exempeldata: Demo - lojalitetsdata](./assets/json/bqLoyalty.json)

### 5. Data Distiller

[5.1 Query Service](./modules/datadistiller/module5.1/query-service.md)

- **Målgrupp:** Datatekniker, dataarkitekt, dataanalytiker, BI Expert
- **Krav:** Åtkomst till Adobe Experience Platform, frågetjänst, Power BI eller Tableau
- **Beskrivning:** I den här modulen får du lära dig hur du använder Adobe Experience Platform Query Service.
- **Tidsinvestering:** 90 minuter
- **Hämta de här resurserna**:
   - [JSON - Exempeldata: Demo System - händelsedatauppsättning för webbplats](./assets/json/ee.json)
   - [JSON - Exempeldata: Demonstrationssystem - händelsedatauppsättning för callcenter](./assets/json/callcenter.json)
   - [JSON - Exempeldata: Demo System - profildatauppsättning för lojalitet](./assets/json/loyalty.json)





