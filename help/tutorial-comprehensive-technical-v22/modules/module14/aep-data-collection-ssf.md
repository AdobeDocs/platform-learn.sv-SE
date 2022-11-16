---
title: Adobe Experience Platform Data Collection & Servervidarebefordran i realtid
description: I den här modulen använder du de tidigare konfigurerade datauppsättningarna, scheman och Adobe Experience Platform Data Collection Server-egenskapen för att samla in data och sedan vidarebefordrar du den till en valfri slutpunkt.
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: c157ca52-c84f-4398-a658-2b6067e41707
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 0%

---

# 14. Real-Time CDP Connections: Vidarebefordran av händelser

**Författare: [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/), [Clement Delalande](https://www.linkedin.com/in/clement-delalande/)**

I den här modulen använder du de tidigare konfigurerade datauppsättningarna, scheman och klientegenskapen för Adobe Experience Platform Data Collection för att samla in data och sedan vidarebefordra den till en valfri slutpunkt.

I den här modulen kommer du att:

- Skapa en Adobe Experience Platform Data Collection Server-egenskap
- Installera och använda tillägget Adobe Cloud Connector i Adobe Experience Platform Data Collection
- Skapa en Google Function-slutpunkt och strömma data till den
- Skapa en AWS-slutpunkt och strömma data till den

Titta på den här videon för att förstå värde, kundresa och konfigurationsprocess:

>[!VIDEO](https://video.tv.adobe.com/v/331987?quality=12&learn=on)

## Utbildningsmål

- Bekanta dig med Adobe Experience Platform Data Collection Server och det nya tillägget Adobe Cloud Connector
- Lär dig återanvända Adobe Experience Platform Web SDK-data i tredjepartslösningar som Google och AWS
- Förstå arkitekturen bakom Adobe Experience Platform Data Collection och Serverside Forwarding.

## Förutsättningar

- Tillgång till Adobe Experience Platform och Adobe Experience Platform Data Collection
- Förståelse för Adobe Experience Platform datamängder och XDM

>[!IMPORTANT]
>
>Den här självstudiekursen har skapats för att underlätta ett visst workshop-format. Den använder specifika system och konton som du kanske inte har tillgång till. Även om ni inte har tillgång till dem tror vi att ni fortfarande kan lära er mycket genom att läsa igenom detta mycket detaljerade innehåll. Om du deltar i något av seminarierna och behöver dina inloggningsuppgifter, kontakta din Adobe-representant som kommer att ge dig den information som krävs.

## Arkitektur - översikt

Titta närmare på arkitekturen nedan, som visar vilka komponenter som kommer att diskuteras och användas i den här modulen.

![Arkitektur - översikt](../../assets/images/architecturem21.png)

## Sandlåda att använda

Använd den här sandlådan för den här modulen: `--aepSandboxId--`.

>[!NOTE]
>
>Glöm inte att installera, konfigurera och använda Chrome-tillägget enligt referensen i [0.1 - Installera Chrome-tillägget för Experience League-dokumentationen](../module0/ex1.md)

## Utövningar

[14.1 Skapa en händelsevidarebefordringsegenskap för datainsamling](./ex1.md)

I den här övningen ska du skapa en händelsevidarebefordringsegenskap för Adobe Experience Platform Data Collection.

[14.2 Uppdatera ditt datastream så att data blir tillgängliga för din Data Collection Event Forwarding-egenskap](./ex2.md)

I den här övningen ska du uppdatera din befintliga datastream så att data som samlas in av din Adobe Experience Platform Data Collection Client-egenskap blir tillgängliga för din Adobe Experience Platform Data Collection Server-egenskap.

[14.3 Skapa och konfigurera en anpassad webkrok](./ex3.md)

I den här övningen skapar och konfigurerar du en anpassad webkrok och du börjar vidarebefordra data som samlas in av Web SDK till den anpassade webkroken.

[14.4 Skapa och konfigurera en Google Cloud-funktion](./ex4.md)

I den här övningen skapar och konfigurerar du en Google Cloud-funktion och du börjar vidarebefordra data som samlas in av Web SDK till Google.

[14.5 Vidarebefordra evenemang till AWS ekosystem](./ex5.md)

I den här övningen konfigurerar du AWS-miljön med AWS API Gateway, AWS Kinesis, AWS Firehose och AWS S3, varefter du börjar vidarebefordra händelsedata som samlas in av Web SDK.

[Sammanfattning och fördelar](./summary.md)

Sammanfattning av den här modulen och en översikt över fördelarna.

>[!NOTE]
>
>Tack för att du lade ned din tid på att lära dig allt om Adobe Experience Platform. Om du har frågor kan du dela allmän feedback om dina förslag på framtida innehåll. Kontakta Wouter Van Geluwe direkt genom att skicka ett e-postmeddelande till **vangeluw@adobe.com**.

[Gå tillbaka till Alla moduler](../../overview.md)
