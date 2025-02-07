---
title: Översikt - Omfattande teknisk självstudiekurs för AEP och appar
description: Utgångspunkt för datatekniker, dataanalytiker, dataarkitekter, datavetenskaper, Orchestration Engineers och Marketers för att få en fullständig förståelse för affärsvärdet hos Adobe Experience Platform och alla dess programtjänster.
doc-type: multipage-overview
exl-id: 88c19383-c185-40f0-b118-6cb82db0ce0e
source-git-commit: 3b3c62499bfed86ab13a657a816424879cab4f42
workflow-type: tm+mt
source-wordcount: '1258'
ht-degree: 0%

---

# Omfattande teknisk självstudiekurs för Adobe Experience Platform

![Tech Insiders](./assets/images/techinsiders.png){width="50px" align="left"}

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

Om du vill använda den här självstudiekursen med din egen Adobe Experience Platform-instans följer du instruktionerna [här](./setup.md) för att förbereda din organisation för självstudiekursen.

- Åtkomst till Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Åtkomst till Adobe Experience Platform Data Collection: [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)
- Åtkomst till demosystemet: [https://dsn.adobe.com/](https://dsn.adobe.com/)

## Videor

Du kan hitta många intressanta videor från vårt Tech Academy-webbseminarium, från bootcamp med mera på vår [Experience Makers Community YouTube-kanal](https://www.youtube.com/channel/UCUKG2dkZ9pYuZUPebQ21jUw).

## Slutförande och certifiering

Den här självstudiekursen är en del av en Adobe-certifieringskurs. Du kan registrera dig för kursen tillsammans med den här självstudiekursen genom att gå till [https://certification.adobe.com/courses/1258](https://certification.adobe.com/courses/1258).

För varje modul som du slutför med hjälp av självstudiekursen nedan måste du skicka in ett bevis på slutförandet enligt [här](./completion.md).

## Innehåll

Gå till [statussidan](./status.md) om du vill kontrollera status för innehållet nedan.

[0. Komma igång](./modules/gettingstarted/gettingstarted/getting-started.md)

I den här grundläggande modulen kommer du att konfigurera allt så att du kan komma åt och använda demomiljön.

**Tidsinvestering:** 30 minuter

### 1. Datainsamling

[1.1 Foundation - installation av Adobe Experience Platform Data Collection &amp; Web SDK](./modules/datacollection/module1.1/data-ingestion-launch-web-sdk.md)

I den här grundläggande modulen får du lära dig mer om Adobe Experience Platform Data Collection och det nya Web SDK-tillägget.

**Tidsinvestering:** 30 minuter

[1.2 Foundation - datainmatning](./modules/datacollection/module1.2/data-ingestion.md)

I den här grundläggande modulen kommer du att importera data från olika källor till Adobe Experience Platform

**Tidsinvestering:** 120 minuter

[1.3 Sammansatt målgrupp](./modules/datacollection/module1.3/fac.md)

I den här modulen får du lära dig att konfigurera en Federated Audiences-modell och generera målgrupper med federerade data.

**Tidsinvestering:** 90 minuter

### 2. Real-Time CDP

[2.1 Foundation - kundprofil i realtid](./modules/rtcdp-b2c/module2.1/real-time-customer-profile.md)

I den här grundläggande modulen kommer du att utforska kundprofilen i realtid i Adobe Experience Platform genom att använda gränssnittet och API:t.

**Tidsinvestering:** 90 minuter

[2.2 Intelligenta tjänster](./modules/rtcdp-b2c/module2.2/intelligent-services.md)

I den här modulen får du lära dig hur du konfigurerar, konfigurerar och använder Adobe Experience Platform Intelligent Services.

**Tidsinvestering:** 60 minuter

[2.3 Real-Time CDP - Bygg en målgrupp och agera](./modules/rtcdp-b2c/module2.3/real-time-cdp-build-a-segment-take-action.md)

I den här modulen ska du konfigurera en målgrupp och aktivera målgruppen för flera destinationer, inklusive Google DV360, Adobe Target och AWS S3.

**Tidsinvestering:** 90 minuter

[2.4 Real-Time CDP: Audience Activation till Microsoft Azure Event Hub](./modules/rtcdp-b2c/module2.4/segment-activation-microsoft-azure-eventhub.md)

I den här modulen konfigurerar du ett Microsoft Azure EventHub-mål som ett realtidsmål för Adobe Experience Platform CDP i realtid. Du kommer också att konfigurera och distribuera en Azure-funktion som aktiveras i realtid när Adobe Experience Platform levererar en målgruppsnyttolast till ditt Azure EventHub-mål. Azure-funktionen som du utlöser visar mekanismen för Adobe Experience Platform CDP:s aktiveringsfunktioner i realtid.
Som en del av den här modulen får du också en förståelse för vad som utlöser CDP i realtid för att faktiskt leverera en nyttolast till en angiven destination. Vi kommer också att diskutera status för en målgruppskvalifikation och hur den hör ihop med aktiveringen.

**Tidsinvestering:** 90 minuter

[2.5 Real-Time CDP Connections: Event Forwarding](./modules/rtcdp-b2c/module2.5/aep-data-collection-ssf.md)

I den här modulen använder du tidigare konfigurerade datauppsättningar, scheman och Adobe Experience Platform Data Collection-egenskapen för att samla in data och sedan vidarebefordra den data på serversidan till flera slutpunkter, som Google Cloud Platform Pub/Sub och AWS Kinesis.

**Tidsinvestering:** 90 minuter

[2.6 Strömma data från Apache Kafka till Real-Time CDP](./modules/rtcdp-b2c/module2.6/aep-apache-kafka.md)

I den här modulen får du lära dig hur du konfigurerar ett eget Apache Kafka-kluster, definierar ämnen, producenter och konsumenter samt strömmar data till Adobe Experience Platform med Adobe Experience Platform Sink Connector for Kafka Connect.

**Tidsinvestering:** 90 minuter

### 3. Adobe Journey Optimizer B2C

[3.1 Adobe Journey Optimizer: Orchestration](./modules/ajo-b2c/module3.1/journey-orchestration-create-account.md)

I den här modulen ska du använda Adobe Journey Optimizer för att skapa en utlösarbaserad resa.

**Tidsinvestering:** 60 minuter

[3.2 Adobe Journey Optimizer: Externa datakällor och anpassade åtgärder](./modules/ajo-b2c/module3.2/journey-orchestration-external-weather-api-sms.md)

I den här modulen använder du Adobe Journey Optimizer för att lyssna på kundbeteenden, både online och offline, och svara på dem i en intelligent, sammanhangsbaserad och realtidsbaserad lösning över olika kanaler.

**Tidsinvestering:** 90 minuter

[3.3 Adobe Journey Optimizer: Offer decisioning](./modules/ajo-b2c/module3.3/offer-decisioning.md)

I den här modulen kommer du att använda Adobe Experience Platform - erbjudanden/beslutsprogram på ett praktiskt sätt för att konfigurera personaliserade erbjudanden och din egen erbjudandeaktivitet.

**Tidsinvestering:** 120 minuter

[3.4 Adobe Journey Optimizer: Händelsebaserade resor](./modules/ajo-b2c/module3.4/journeyoptimizer.md)

I den här modulen får ni lära er allt om Journey Optimizer, som hjälper företag att utforma och leverera sammankopplade, kontextuella och personaliserade upplevelser till sina kunder.

**Tidsinvestering:** 120 minuter

### 4. Adobe Customer Journey Analytics

[4.1 Customer Journey Analytics: Skapa en kontrollpanel med Analysis Workspace ovanpå Adobe Experience Platform](./modules/cja-b2c/module4.1/customer-journey-analytics-build-a-dashboard.md)

I den här modulen får du information online för offlineåtkomst genom att konfigurera en instrumentpanel som innehåller flerkanalsdata som webbplatsinteraktioner, mobilappsinteraktioner, Call Center-interaktioner, interaktioner i butiken och mycket annat.

**Tidsinvestering:** 120 minuter

[4.2 Customer Journey Analytics: Importera och analysera data från Google Analytics i Adobe Experience Platform med BigQuery Source Connector](./modules/cja-b2c/module4.2/customer-journey-analytics-bigquery-gcp.md)

I den här modulen ska du konfigurera en egen instans av Google Cloud Platform, läsa in demodata i Google Cloud Platform och sedan använda BigQuery Source Connector för att importera data från Google Cloud Platform till Adobe Experience Platform. Slutligen använder ni Customer Journey Analytics för att visualisera dessa data.

**Tidsinvestering:** 120 minuter

### 5. Data Distiller

[5.1 Query Service](./modules/datadistiller/module5.1/query-service.md)

I den här modulen får du lära dig hur du använder Adobe Experience Platform Query Service.

**Tidsinvestering:** 90 minuter

![Tech Insiders](./assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>Om du har frågor kan du dela allmän feedback om dina förslag på framtida innehåll. Kontakta Tech Insiders direkt genom att skicka ett e-postmeddelande till **techinsiders@adobe.com**.
