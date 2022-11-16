---
title: Översikt
description: Utgångspunkt för datatekniker, dataanalytiker, dataarkitekter, datavetenskaper, Orchestration Engineers och Marketers för att få en fullständig förståelse för affärsvärdet hos Adobe Experience Platform och alla dess programtjänster.
doc-type: multipage-overview
hide: false
exl-id: 88c19383-c185-40f0-b118-6cb82db0ce0e
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1869'
ht-degree: 0%

---

# Omfattande teknisk självstudiekurs för Adobe Experience Platform

## Översikt

Den här självstudiekursen är den perfekta utgångspunkten för datatekniker, dataanalytiker, dataarkitekter, datavetare, Orchestration-tekniker och marknadsförare för att få en fullständig förståelse för Adobe Experience Platform affärsvärde och alla dess programtjänster. Varje lektion fokuserar på en verklig utmaning som företag står inför i dagens komplexa ekosystem av personalisering och bryter ned hur Experience Platform löser den utmaningen i olika praktiska övningar. Titta på den här videon för att förstå vilka problem Adobe Experience Platform kan hjälpa dig att lösa.

>[!VIDEO](https://video.tv.adobe.com/v/344237?quality=12&enable=on)

Självstudiekursen är mycket varierad och ger tydliga insikter i följande program:

- Adobe Experience Platform
- Adobe Experience Platform Data Collection
- CDP i realtid
- Adobe Journey Optimizer
- Customer Journey Analytics
- offer decisioning

Den här självstudiekursen fokuserar inte bara på Adobe-program utan tar hänsyn till det större ekosystem som varumärkena använder. I vissa lektioner fokuserar vi på hur _ej Adobe_ -program integreras med Adobe Experience Platform. Därför får du en djupgående förståelse för hur följande program fungerar tillsammans med Adobe Experience Platform:

- Amazon: AWS Lambda, AWS S3, AWS Kinesis
- Google: Google Cloud Platform, Google BigQuery, Google Display&amp;Video 360, Google AdWords
- Microsoft: Power BI, Azure EventHub, Azure Blob Storage
- Salesforce: Tableau
- Apache Kafka
- Postman
- ...

När du är klar med den här självstudiekursen kan du:

- Konfigurera scheman, mixar, datauppsättningar och identiteter
- Konfigurera en Adobe Experience Platform Data Collection-egenskap och konfigurera det nya Web SDK-tillägget i Adobe Experience Platform Data Collection
- Strömma data till Adobe Experience Platform i realtid med Adobe Experience Platform Data Collection, Google Tag Manager eller Amazon Alexa
- Batchimportera data till Adobe Experience Platform med ett arbetsflöde eller med ett ETL-program (extract, transform, load)
- Visualisera och använda kundprofilen i realtid i Adobe Experience Platform
- Skapa segment
- Förbruka flera Adobe Experience Platform API:er
- Använd SQL för att fråga dina data i Adobe Experience Platform
- Konfigurera, utbilda och poängsätta maskininlärningsmodeller i Adobe Experience Platform
- Använd Journey Orchestration för att konfigurera resorna i realtid, utlösarbaserade
- Använd CDP i realtid för att agera genom att aktivera ett segment till olika destinationer
- Använd Customer Journey Analytics för att rapportera flerkanaliga kunddata från olika källor, inklusive Google BigQuery

## Förutsättningar

- Tillgång till Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Åtkomst till Adobe Experience Platform Data Collection: [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)
- Åtkomst till Demo System: [https://dashboard.adobedemo.com/](https://dashboard.adobedemo.com/)

>[!IMPORTANT]
>
>Den här självstudiekursen har skapats för att underlätta ett visst workshop-format. Den använder specifika system och konton som du kanske inte har tillgång till. Även om ni inte har tillgång till dem tror vi att ni fortfarande kan lära er mycket genom att läsa igenom detta mycket detaljerade innehåll. Om du deltar i något av seminarierna och behöver dina inloggningsuppgifter, kontakta din Adobe-representant som kommer att ge dig den information som krävs.

## Om den här självstudiekursen

I den här lektionen kommer du att implementera Adobe Experience Platform och Application Services med en demowebbplats som stöder flera branscher. Demonens webbplats och mobilapp har ett omfattande datalager och funktioner som gör att du kan skapa en realistisk implementering. Den ger tillgång till demovarumärken som **Luma**, **Citi Signal**, **EXP News**, **MUTUAL365**, **Carvelo** och flera andra. Du skapar en egen Adobe Experience Platform Data Collection Client-egenskap i din egen Experience Cloud-organisation och mappar den till din demowebbplats. Då genereras data som skickas till din egen Adobe Experience Platform-instans.

## Arkitektur

Innan du börjar med övningarna bör du titta på arkitekturen bakom den här självstudiekursen. Som du kan se i ovanstående översikt kommer den här självstudiekursen att fördjupa sig i ett antal funktioner och funktioner i Adobe Experience Platform, men den kommer även att innehålla en rad integreringar mellan olika källor och mål. För att du ska förstå arkitekturen bakom den här självstudiekursen och den övergripande placeringen av Adobe Experience Platform i ditt Enterprise-ekosystem börjar du med att titta på arkitekturvideon och diagrammet.

Gå till [Arkitektur](./architecture.md).


## Videor

![Videor](./assets/images/yt.jpeg)

Du kan hitta många intressanta videor från våra Tech Academy-event, från Bootcamp med mera på vår [Experience Makers Community YouTube channel](https://www.youtube.com/channel/UCUKG2dkZ9pYuZUPebQ21jUw).

Flera videofilmer har skapats som visar olika delar av aktiveringen och kraftfulla integreringar mellan Adobe Experience Platform och andra program än Adobe. Klicka på länken nedan om du vill visa en översikt över dessa videofilmer.

Gå till [Videor](./videos.md).



## Hur mäts slutförandet av den omfattande tekniska självstudiekursen för Adobe Experience Platform?

Om du deltar i den här självstudiekursen som partner eller anställd i Adobe måste du skicka in dina framsteg när du har slutfört alla aktiveringsmoduler.

Här finns information om krav och process för att skicka in en ansökan: [Mäta slutförande](./completion.md)

## Innehåll

[0. Komma igång](./modules/module0/getting-started.md)

- **Målgrupp:** Alla som deltar i den omfattande tekniska självstudiekursen för Adobe Experience Platform
- **Förutsättningar:** Åtkomst till Demo System Next, Adobe Experience Platform och Adobe Experience Platform Data Collection. Åtkomst till standardkonfigurations-ID:t för din Adobe Experience Platform-miljö.
- **Beskrivning:** I den här grundläggande modulen kommer du att konfigurera allt så att du kan komma åt och använda demomiljön.
- **Tidsinvestering:** 30 minuter

[1. Foundation - konfigurera Adobe Experience Platform Data Collection &amp; Web SDK](./modules/module1/data-ingestion-launch-web-sdk.md)

- **Målgrupp:** Datatekniker, dataarkitekt
- **Förutsättningar:** Tillgång till Adobe Experience Platform och Adobe Experience Platform Data Collection.
- **Beskrivning:** I den här grundläggande modulen får du lära dig mer om Adobe Experience Platform Data Collection och det nya SDK-tillägget för webben.
- **Tidsinvestering:** 30 minuter

[2. Foundation - datainmatning](./modules/module2/data-ingestion.md)

- **Målgrupp:** Datatekniker, dataarkitekt
- **Förutsättningar:** Tillgång till Adobe Experience Platform och Adobe Experience Platform Data Collection.
- **Beskrivning:** I den här grundläggande modulen kommer du att importera data från webbplatsen till Platform
- **Tidsinvestering:** 120 minuter

[3. Foundation - kundprofil i realtid](./modules/module3/real-time-customer-profile.md)

- **Målgrupp:** Datatekniker, dataarkitekt, marknadsförare
- **Förutsättningar:** Tillgång till Adobe Experience Platform och Postman
- **Beskrivning:** I den här grundläggande modulen kommer du att utforska kundprofilen i realtid i Adobe Experience Platform genom att använda gränssnittet och API:t.
- **Tidsinvestering:** 90 minuter
- **Hämta dessa resurser**:
   - [Postman-samlingar](./assets/postman/postman_profile.zip)

[4. Frågetjänst](./modules/module4/query-service.md)

- **Målgrupp:** Datatekniker, dataarkitekt, dataanalytiker, BI Expert
- **Förutsättningar:** Tillgång till Adobe Experience Platform, Query Service, Power BI eller Tableau
- **Beskrivning:** I den här modulen får du lära dig hur du använder Adobe Experience Platform Query Service.
- **Tidsinvestering:** 90 minuter
- **Hämta dessa resurser**:
   - [JSON - Exempeldata: Demo System - händelsedatauppsättning för webbplats](./assets/json/ee.json)
   - [JSON - Exempeldata: Demo System - händelsedatauppsättning för callcenter](./assets/json/callcenter.json)
   - [JSON - Exempeldata: Demo System - profildatauppsättning för lojalitet](./assets/json/loyalty.json)

[5. Intelligenta tjänster](./modules/module5/intelligent-services.md)

- **Målgrupp:** Datatekniker, dataarkitekt, datatekniker
- **Förutsättningar:** Tillgång till Adobe Experience Platform, intelligenta tjänster
- **Beskrivning:** I den här modulen får du lära dig hur du konfigurerar, konfigurerar och använder Adobe Experience Platform Intelligent Services.
- **Tidsinvestering:** 60 minuter

[6. Real-Time CDP - Bygg ett segment och agera](./modules/module6/real-time-cdp-build-a-segment-take-action.md)

- **Målgrupp:** Dataarkitekt, Orchestration Engineer, Marketer
- **Förutsättningar:** Tillgång till Adobe Experience Platform, CDP, Adobe Audience Manager, Adobe Target, AWS S3 i realtid
- **Beskrivning:** I den här modulen ska du konfigurera ett segment, aktivera det för direktuppspelningssegmentering och aktivera det för flera destinationer, inklusive Google DV360, Google AdWords, Adobe Audience Manager, Adobe Target och S3-destinationer som Salesforce Marketing Cloud.
- **Tidsinvestering:** 90 minuter

[7. Adobe Journey Optimizer: Orchestration](./modules/module7/journey-orchestration-create-account.md)

- **Målgrupp:** Datatekniker, dataarkitekt, Orchestration Engineer
- **Förutsättningar:** Tillgång till Adobe Experience Platform och Adobe Journey Optimizer
- **Beskrivning:** I den här modulen ska du använda Adobe Journey Optimizer för att skapa en utlösarbaserad resa.
- **Tidsinvestering:** 60 minuter

[8. Adobe Journey Optimizer: Externa datakällor och anpassade åtgärder](./modules/module8/journey-orchestration-external-weather-api-sms.md)

- **Målgrupp:** Datatekniker, dataarkitekt, Orchestration Engineer, Marketer
- **Förutsättningar:** Tillgång till Adobe Experience Platform, Adobe Journey Optimizer, Open Weather API, Twilio
- **Beskrivning:** I den här modulen använder du Adobe Journey Optimizer för att lyssna på kundbeteenden, både online och offline, och svara på dem i en intelligent, sammanhangsbaserad och realtidsbaserad väg över olika kanaler.
- **Tidsinvestering:** 90 minuter

[9. Adobe Journey Optimizer: offer decisioning](./modules/module9/offer-decisioning.md)

- **Målgrupp:** Datatekniker, dataarkitekt, Orchestration Engineer, Marketer
- **Förutsättningar:** Tillgång till Adobe Experience Platform och Offer decisioning
- **Beskrivning:** I den här modulen kommer du att använda Adobe Experience Platform - erbjudanden/beslutsprogram på ett praktiskt sätt för att konfigurera personaliserade erbjudanden och din egen erbjudandeaktivitet.
- **Tidsinvestering:** 120 minuter

[10. Adobe Journey Optimizer: Händelsebaserade resor](./modules/module10/journeyoptimizer.md)

- **Målgrupp:** Email Marketer, Orchestration Specialist, Data Engineer, Data Architect, Data Analyst
- **Förutsättningar:** Tillgång till Adobe Experience Platform och Journey Optimizer
- **Beskrivning:** I den här modulen får ni lära er allt om Journey Optimizer, som hjälper företag att utforma och leverera sammankopplade, kontextuella och personaliserade upplevelser till sina kunder.
- **Tidsinvestering:** 120 minuter

[11. Customer Journey Analytics: Skapa en kontrollpanel med Analysis Workspace ovanpå Adobe Experience Platform](./modules/module11/customer-journey-analytics-build-a-dashboard.md)

- **Målgrupp:** Datatekniker, dataarkitekt, dataanalytiker
- **Förutsättningar:** Tillgång till Adobe Experience Platform och Customer Journey Analytics
- **Beskrivning:** I den här modulen får du information online för offlineåtkomst genom att konfigurera en instrumentpanel som innehåller flerkanalsdata som webbplatsinteraktioner, mobilappsinteraktioner, Call Center-interaktioner, interaktioner i butiken och mycket annat.
- **Tidsinvestering:** 120 minuter

[12. Customer Journey Analytics: Importera och analysera Google Analytics-data i Adobe Experience Platform med BigQuery Source Connector](./modules/module12/customer-journey-analytics-bigquery-gcp.md)

- **Målgrupp:** Datatekniker, dataarkitekt, dataanalytiker
- **Förutsättningar:** Tillgång till Adobe Experience Platform, Customer Journey Analytics, Google Cloud Platform, Google BigQuery
- **Beskrivning:** I den här modulen ska du konfigurera en egen instans av Google Cloud Platform, läsa in demodata i Google Cloud Platform och sedan använda BigQuery Source Connector för att importera data från Google Cloud Platform till Adobe Experience Platform. Slutligen använder ni Customer Journey Analytics för att visualisera dessa data.
- **Tidsinvestering:** 120 minuter
- **Hämta dessa resurser**:
   - [JSON - Exempeldata: Demo - lojalitetsdata](./assets/json/bqLoyalty.json)

[13. Real-Time CDP: Segmentaktivering till Microsoft Azure Event Hub](./modules/module13/segment-activation-microsoft-azure-eventhub.md)

- **Målgrupp:** Datatekniker, dataarkitekt, dataanalytiker
- **Förutsättningar:** Tillgång till Adobe Experience Platform, CDP och Microsoft Azure i realtid
- **Beskrivning:** I den här modulen konfigurerar du ett Microsoft Azure EventHub-mål som ett realtidsmål för Adobe Experience Platform CDP i realtid. Du kommer också att konfigurera och distribuera en Azure-funktion som aktiveras i realtid när Adobe Experience Platform levererar en segmentnyttolast till Azure EventHub-målet. Azure-funktionen som du utlöser visar mekanismen för Adobe Experience Platform CDP:s aktiveringsfunktioner i realtid.
Som en del av den här modulen får du också en förståelse för vad som utlöser CDP i realtid för att faktiskt leverera en nyttolast till en angiven destination. Vi kommer också att diskutera statusen för en segmentkvalificering och hur den hör ihop med aktiveringen.
- **Tidsinvestering:** 90 minuter

[14. Real-Time CDP Connections: Vidarebefordran av händelser](./modules/module14/aep-data-collection-ssf.md)

- **Målgrupp:** Datatekniker, dataarkitekt, dataanalytiker
- **Förutsättningar:** Åtkomst till egenskaper för Real-Time CDP-anslutningar, taggar och händelsevidarebefordran
- **Beskrivning:** I den här modulen använder du tidigare konfigurerade datauppsättningar, scheman och Adobe Experience Platform Data Collection-egenskapen för att samla in data och sedan vidarebefordra den data på serversidan till en valfri slutpunkt.
- **Tidsinvestering:** 90 minuter

[15. Strömma data från Apache Kafka till Real-Time CDP](./modules/module15/aep-apache-kafka.md)

- **Målgrupp:** Dataanalytiker, datatekniker, dataarkitekt
- **Förutsättningar:** Tillgång till Adobe Experience Platform
- **Beskrivning:** I den här modulen får du lära dig hur du konfigurerar ett eget Apache Kafka-kluster, definierar ämnen, producenter och konsumenter samt strömmar data till Adobe Experience Platform med Adobe Experience Platform Sink Connector for Kafka Connect.
- **Tidsinvestering:** 90 minuter

>[!NOTE]
>
>Tack för att du lade ned din tid på att lära dig allt om Adobe Experience Platform. Om du har frågor kan du dela allmän feedback om dina förslag på framtida innehåll. Kontakta Wouter Van Geluwe direkt genom att skicka ett e-postmeddelande till **vangeluw@adobe.com**.
