---
title: 1. Installation av Adobe Experience Platform Data Collection och Web SDK-tillägget
description: Foundation - konfigurera Adobe Experience Platform Data Collection och Web SDK-tillägget
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 86da7132-cb06-4be3-b6b8-ea3ab937e6dc
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 0%

---

# 1. Foundation - konfigurera Adobe Experience Platform Data Collection och Web SDK-tillägget

**Författare: [Matthew Joseph Woolley](https://www.linkedin.com/in/matthewjwoolley/), [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

I den här grundläggande modulen får du lära dig Adobe datainsamlingsvision och en förklaring av hur du hämtar data från en webbplats och ett mobilprogram till Adobe Experience Platform och andra program via Adobe Experience Platform Data Collection, Adobe Experience Platform SDK:er och Adobe Experience Platform Edge Network. I den här modulen introduceras vissa koncept och tekniker som har en effekt som inte omfattas av en teknisk självstudiekurs från Adobe Experience Platform. Det bör stå klart vilka delar av övningarna som ligger till grund för resten av den omfattande självstudiekursen, som lär dig mer om Experience Edge och dess funktioner, och var du ska gå för mer information och självstudiekurser.

## Utbildningsmål

- Läs om hur ett varumärke använder Adobe Experience Platform Data Collection som sitt Tag Management System (TMS).
- Lär dig de dataflöden som ett varumärke använder för att importera data till sina Adobe-produkter.
- Lär dig hur du skickar data till Adobe Experience Platform och andra produkter via Adobe Experience Platform Edge Network.
- Lär dig hur du skapar dataelement och regler som samlar in data från webben och mobiler.
- Lär dig mer om Web SDK-spårningshändelser och hur du felsöker deras innehåll.
- Lär dig vad ett datalager är och vad Adobe rekommenderar när du implementerar ett lager.
- Lär dig hur du implementerar Web SDK från grunden.
- Lär dig skillnaden mellan webb- och mobilimplementering.

## Förutsättningar

- Tillgång till Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Åtkomst till Adobe Experience Platform Data Collection: [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)
- Tillgång till demowebbplatsen

>[!IMPORTANT]
>
>Den här självstudiekursen har skapats för att underlätta ett visst workshop-format. Den använder specifika system och konton som du kanske inte har tillgång till. Även om ni inte har tillgång till dem tror vi att ni fortfarande kan lära er mycket genom att läsa igenom detta mycket detaljerade innehåll. Om du deltar i något av seminarierna och behöver dina inloggningsuppgifter, kontakta din Adobe-representant som kommer att ge dig den information som krävs.

## Arkitektur - översikt

Titta närmare på arkitekturen nedan, som visar vilka komponenter som kommer att diskuteras och användas i den här modulen.

![Arkitektur - översikt](../../assets/images/architecturem1.png)

## Sandlåda att använda

Använd den här sandlådan för den här modulen: `--aepSandboxId--`.

>[!NOTE]
>
>Glöm inte att installera, konfigurera och använda Chrome-tillägget enligt referensen i [0.1 - Installera Chrome-tillägget för Experience League-dokumentationen](../module0/ex1.md)

## Utövningar

[1.1 Förstå Adobe Experience Platform datainsamling](./ex1.md)

I den här övningen kan du utforska användargränssnittet i Adobe Experience Platform Data Collection och få en förståelse för dess funktioner.

[1.2 Edge Network, DataStreams och Server Side Data Collection](./ex2.md)

I den här övningen får du lära dig att vidarebefordra data till Adobe-produkter i Adobe Experience Platform Data Collection-gränssnittet och undersöka de dataströmmar som används av demowebbplatsen.

[1.3 Introduktion till Adobe Experience Platform Data Collection](./ex3.md)

I den här övningen får du lära dig att konfigurera ett tillägg, skapa dataelement och regler och publicera dem på webben.

[1.4 Webbdatainsamling på klientsidan](./ex4.md)

I den här övningen felsöker du det Web SDK som har installerats för att förstå hur det fungerar och vilka data som kommer att användas i framtida övningar.

[1.5 Implementera Adobe Analytics och Adobe Audience Manager](./ex5.md)

I den här övningen ska du se och använda webbdata som samlats in med Web SDK i Adobe Analytics och Adobe Audience Manager.

[1.6 Implementera Adobe Target](./ex6.md)

I den här övningen kan du skapa en aktivitet i Adobe Target som implementeras via Web SDK.

[1.7 XDM-schemakrav i Adobe Experience Platform](./ex7.md)

För att säkerställa att Web SDK och alloy.js kan importera data till Adobe Experience Platform finns det ett krav på att en specifik XDM-mixin ska ingå i XDM-schemat i Adobe Experience Platform.

[Sammanfattning och fördelar](./summary.md)

Sammanfattning av den här modulen och en översikt över fördelarna.

>[!NOTE]
>
>Tack för att du lade ned din tid på att lära dig allt om Adobe Experience Platform. Om du har frågor kan du dela allmän feedback om dina förslag på framtida innehåll. Kontakta Wouter Van Geluwe direkt genom att skicka ett e-postmeddelande till **vangeluw@adobe.com**.

[Gå tillbaka till Alla moduler](../../overview.md)
