---
title: Adobe Experience Platform Data Collection & Servervidarebefordran i realtid
description: I den här modulen använder du de tidigare konfigurerade datauppsättningarna, scheman och Adobe Experience Platform Data Collection Server-egenskapen för att samla in data och sedan vidarebefordrar du den till en valfri slutpunkt.
kt: 5342
doc-type: tutorial
exl-id: dbf5e995-9c2e-4f72-b336-e942cb22cde5
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 0%

---

# 2.5 Real-Time CDP Connections: Event Forwarding

I den här modulen använder du de tidigare konfigurerade datauppsättningarna, scheman och klientegenskapen för Adobe Experience Platform Data Collection för att samla in data och sedan vidarebefordra den till en valfri slutpunkt.

I den här modulen kommer du att:

- Skapa en Adobe Experience Platform Data Collection Server-egenskap
- Installera och använda tillägget Adobe Cloud Connector i Adobe Experience Platform Data Collection
- Skapa en Google Function-slutpunkt och strömma data till den
- Skapa en AWS-slutpunkt och strömma data till den

## Utbildningsmål

- Bekanta dig med Adobe Experience Platform Data Collection Server och det nya tillägget Adobe Cloud Connector
- Lär dig återanvända Adobe Experience Platform Web SDK-data i tredjepartslösningar som Google och AWS
- Förstå arkitekturen bakom Adobe Experience Platform Data Collection och Serverside Forwarding.

## Förhandskrav

- Tillgång till Adobe Experience Platform och Adobe Experience Platform Data Collection
- Förståelse för Adobe Experience Platform datasets och XDM

>[!NOTE]
>
>Glöm inte att installera, konfigurera och använda Chrome-tillägget enligt [Installera Chrome-tillägget för Experience League-dokumentationen](../../../getting-started/gettingstarted/ex1.md)

## Utövningar

[2.5.1 Skapa en händelsevidarebefordringsegenskap för datainsamling](./ex1.md)

I den här övningen ska du skapa en händelsevidarebefordringsegenskap för Adobe Experience Platform Data Collection.

[2.5.2 Uppdatera din datastream så att data blir tillgängliga för din Data Collection Event Forwarding-egenskap](./ex2.md)

I den här övningen ska du uppdatera din befintliga datastream så att data som samlas in av din Adobe Experience Platform Data Collection Client-egenskap blir tillgängliga för din Adobe Experience Platform Data Collection Server-egenskap.

[2.5.3 Skapa och konfigurera en anpassad webkrok](./ex3.md)

I den här övningen skapar och konfigurerar du en anpassad webkrok och du börjar vidarebefordra data som samlas in av Web SDK till den anpassade webkroken.

[2.5.4 Vidarebefordra händelser till GCP Pub/Sub](./ex4.md)

I den här övningen skapar och konfigurerar du en Google Cloud-funktion och du börjar vidarebefordra data som samlas in av Web SDK till Google.

[2.5.5 Vidarebefordra event till AWS Kinesis &amp; AWS S3](./ex5.md)

I den här övningen konfigurerar du AWS-miljön med AWS IAM, AWS Kinesis, AWS Firehose och AWS S3, varefter du börjar vidarebefordra händelsedata som samlas in av Web SDK.

[Sammanfattning och fördelar](./summary.md)

Sammanfattning av den här modulen och en översikt över fördelarna.

![Tech Insiders](./../../../../assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>Tack för att du lägger ned din tid på att lära dig allt om Adobe Experience Platform och dess program. Om du har frågor kan du dela allmän feedback om dina förslag på framtida innehåll. Kontakta Tech Insiders direkt genom att skicka ett e-postmeddelande till **techinsiders@adobe.com**.

[Gå tillbaka till Alla moduler](./../../../../overview.md)
