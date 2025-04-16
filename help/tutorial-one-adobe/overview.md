---
title: Översikt - Omfattande teknisk handledning - En Adobe
description: Omfattande teknisk självstudiekurs - En Adobe
doc-type: multipage-overview
exl-id: 5bc0d621-0662-4d94-80a0-b6c173c0ac9e
source-git-commit: 603e48e0453911177823fe7ceb340f8ca801c5e1
workflow-type: tm+mt
source-wordcount: '978'
ht-degree: 1%

---

# Omfattande teknisk självstudiekurs - En Adobe

![Tech Insiders](./assets/images/techinsiders.png){width="50px" align="left"}

## Översikt

Självstudiekursen är mycket varierad och ger tydliga insikter i följande program:

- Adobe Firefly Services, Adobe Photoshop, Adobe Frame I/O, Adobe Substance 3D Staging
- Adobe Workfront &amp; Adobe Workfront Fusion
- Adobe Experience Manager Cloud Service, Sites, Assets och Edge Delivery Services
- Adobe Experience Platform
- Adobe Real-Time CDP
- Adobe Journey Optimizer

Den här självstudiekursen fokuserar inte bara på Adobe-program utan tar hänsyn till det större ekosystem som varumärkena använder. I vissa lektioner fokuserar vi på hur andra program än Adobe kan integreras med Adobe-program. Därför får du en djupgående förståelse för hur följande program kommer att fungera tillsammans med Adobe Experience Platform:

- Amazon AWS
- Google Cloud-plattform
- Microsoft Azure
- Postman
- Snowflake
- ...

## Förhandskrav

Om du vill använda den här självstudiekursen med din egen Adobe Experience Cloud-instans måste följande program etableras i din instans och du måste ha tillgång till dem:

- Adobe Firefly
- Adobe Photoshop, Adobe Frame I/O, Adobe Substance 3D-iscensättning
- Adobe Workfront
- Adobe Workfront Fusion
- Adobe Experience Platform, Adobe Experience Platform Data Collection
- Åtkomst till demosystemet nästa: [https://dsn.adobe.com/](https://dsn.adobe.com/){target="_blank"}

## Slutförande och certifiering

Den här självstudiekursen ingår i en Adobe Certification-kurs. Du kan registrera dig för kursen tillsammans med den här självstudiekursen genom att gå till [https://certification.adobe.com](https://certification.adobe.com).

För varje modul som du slutför med hjälp av självstudiekursen nedan måste du skicka in ett bevis på slutförandet enligt [här](./completion.md).

## Innehållsstatus

Gå till [statussidan](./status.md){target="_blank"} om du vill kontrollera status för innehållet nedan.

### Komma igång

[Komma igång](./modules/getting-started/gettingstarted/getting-started.md){target="_blank"}

I den här grundläggande modulen kommer du att förbereda allt så att du kan komma åt och använda demomiljön.

### 1. Arbetsflöde och planering

### 2. Skapa och producera

[1.1 Adobe Firefly Services](./modules/creation-production/module1.1/firefly-services.md){target="_blank"}

I den här modulen använder du Adobe Firefly Services API:er, Photoshop API:er och Microsoft Azure Storage Services för att generera bilder och lagra dem programmatiskt.

[1.2 Automatisering av Creative-arbetsflöden med Workfront Fusion](./modules/creation-production/module1.2/automation.md){target="_blank"}

I den här grundläggande modulen använder du Adobe Workfront Fusion för att automatisera och skala arbetsflödena för att skapa innehåll.

[1.3 Adobe Express och Adobe Experience Cloud](./modules/creation-production/module1.3/express.md){target="_blank"}

I den här grundläggande modulen kommer ni att använda Adobe Express för att skapa bilder och videor, och ni kommer att dela dessa resurser med det bredare Adobe Experience Cloud-ekosystemet.

### 3. Förvaltning av tillgångar

[1.1 Adobe Experience Manager molntjänst och leveranstjänster för Edge](./modules/asset-mgmt/module2.1/aemcs.md){target="_blank"}

I den här grundläggande modulen kommer du att konfigurera Adobe Experience Manager Cloud Service Program, Site och Assets.

[1.2 Arbetsflödeshantering med Adobe Workfront](./modules/asset-mgmt/module2.2/workfront.md){target="_blank"}

I den här grundläggande modulen kommer du att konfigurera och använda Adobe Workfront för att hantera godkännandeflöden och du kommer att använda integreringar med Adobe Experience Manager Assets, Universal Editor, Photoshop med flera.

### 4. Leverans och aktivering

#### Datainsamling

[1.1 Foundation - installation av Adobe Experience Platform Data Collection &amp; Web SDK](./modules/delivery-activation/datacollection/dc1.1/data-ingestion-launch-web-sdk.md)

I den här grundläggarmodulen får du lära dig mer om Adobe Experience Platform Data Collection och det nya Web SDK-tillägget.

[1.2 Foundation - Datainmatning](./modules/delivery-activation/datacollection/dc1.2/data-ingestion.md)

I den här grundläggande modulen kommer du att importera data från olika källor till Adobe Experience Platform

[1.3 Sammansatt målgrupp](./modules/delivery-activation/datacollection/dc1.3/fac.md)

I den här modulen får du lära dig att konfigurera en Federated Audiences-modell och generera målgrupper med federerade data.

#### Real-Time CDP B2C

[2.1 Foundation - kundprofil i realtid](./modules/delivery-activation/rtcdp-b2c/rtcdpb2c-1/real-time-customer-profile.md)

I den här grundläggande modulen kommer du att utforska kundprofilen i realtid i Adobe Experience Platform med hjälp av användargränssnittet och API:t.

[2.2 Intelligenta tjänster](./modules/delivery-activation/rtcdp-b2c/rtcdpb2c-2/intelligent-services.md)

I den här modulen får du lära dig hur du konfigurerar, konfigurerar och använder Adobe Experience Platform Intelligent Services.

[2.3 CDP i realtid - Bygg upp en publik och vidta åtgärder](./modules/delivery-activation/rtcdp-b2c/rtcdpb2c-3/real-time-cdp-build-a-segment-take-action.md)

I den här modulen ska du konfigurera en målgrupp och aktivera målgruppen för flera destinationer, inklusive Google DV360, Adobe Target och AWS S3.

[2.4 Real-Time CDP: Audience Activation till Microsoft Azure Event Hub](./modules/delivery-activation/rtcdp-b2c/rtcdpb2c-4/segment-activation-microsoft-azure-eventhub.md)

I den här modulen konfigurerar du ett Microsoft Azure EventHub-mål som ett realtidsmål för Adobe Experience Platform CDP i realtid.

[2.5 Real-Time CDP Connections: Event Forwarding](./modules/delivery-activation/rtcdp-b2c/rtcdpb2c-5/aep-data-collection-ssf.md)

I den här modulen vidarebefordrar du data på serversidan till flera slutpunkter, till exempel Google Cloud Platform Pub/Sub och AWS Kinesis.

[2.6 Strömma data från Apache Kafka till Real-Time CDP](./modules/delivery-activation/rtcdp-b2c/rtcdpb2c-6/aep-apache-kafka.md)

I den här modulen får du lära dig hur du konfigurerar ett eget Apache Kafka-kluster och strömmar data till Adobe Experience Platform.

#### Adobe Journey Optimizer B2C

[3.1 Adobe Journey Optimizer: Orchestration](./modules/delivery-activation/ajo-b2c/ajob2c-1/journey-orchestration-create-account.md)

I den här modulen ska du använda Adobe Journey Optimizer för att skapa en utlösarbaserad resa.

[3.2 Adobe Journey Optimizer: Externa datakällor och anpassade åtgärder](./modules/delivery-activation/ajo-b2c/ajob2c-2/journey-orchestration-external-weather-api-sms.md)

I den här modulen använder ni Adobe Journey Optimizer för att lyssna på kundernas beteende, både online och offline, och svara på det på ett intelligent, kontextuellt sätt i realtid via olika kanaler.

[3.3 Adobe Journey Optimizer: Offer Decisioning](./modules/delivery-activation/ajo-b2c/ajob2c-3/offer-decisioning.md)

I den här modulen använder du Adobe Journey Optimizer för att konfigurera anpassade erbjudanden och ditt eget beslut om erbjudanden.

[3.4 Adobe Journey Optimizer: Händelsebaserade resor](./modules/delivery-activation/ajo-b2c/ajob2c-4/journeyoptimizer.md)

I den här modulen får ni lära er allt om Journey Optimizer, som hjälper företag att utforma och leverera sammankopplade, kontextuella och personaliserade upplevelser till sina kunder.

[3.5 Adobe Journey Optimizer: Översättningstjänster](./modules/delivery-activation/ajo-b2c/ajob2c-5/ajotranslationsvcs.md)

I den här modulen får du lära dig hur du konfigurerar och använder översättningstjänster i Adobe Journey Optimizer för att lokalisera dina meddelanden till dina kunder.

### 5. Rapportering och insikter

#### Analys av kundresan från Adobe

[1.1 Customer Journey Analytics: Bygg en kontrollpanel med Analysis Workspace ovanpå Adobe Experience Platform](./modules/reporting-insights/cja-b2c/cjab2c-1/customer-journey-analytics-build-a-dashboard.md)

I den här modulen får du insikter från online till offline genom att konfigurera en instrumentpanel som innehåller flerkanalsdata.

[1.2 Customer Journey Analytics: Importera och analysera Google Analytics-data i Adobe Experience Platform med BigQuery Source Connector](./modules/reporting-insights/cja-b2c/cjab2c-2/customer-journey-analytics-bigquery-gcp.md)

I den här modulen ska du konfigurera en egen instans av Google Cloud Platform, läsa in demodata i Google Cloud Platform och sedan använda BigQuery Source Connector för att importera data från Google Cloud Platform till Adobe Experience Platform.

#### Data Distiller

[2.1 Frågetjänst](./modules/reporting-insights/datadistiller/dd-1/query-service.md)

I den här modulen får du lära dig hur du använder Adobe Experience Platform Query Service.

![Tech Insiders](./assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>Om du har frågor kan du dela allmän feedback om dina förslag på framtida innehåll. Kontakta Tech Insiders direkt genom att skicka ett e-postmeddelande till **techinsiders@adobe.com**.
