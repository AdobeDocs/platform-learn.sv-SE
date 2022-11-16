---
title: Foundation - datainmatning
description: Foundation - datainmatning
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: dbbc0539-ae1b-488d-b312-76a74d4d361f
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%

---

# 2. Foundation - datainmatning

**Författare: [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

I den här modulen är målet att lära sig allt om datainmatning. Du får lära dig mer om datainmatning i Streaming och Batch. Du implementerar Streaming Data Ingmit med Launch, så att kundbeteendet på Hands-On Lab-webbplatsen strömmas till Adobe Experience Platform i realtid. Du får lära dig mer om inmatning av batchdata genom att använda ett Adobe Experience Platform-arbetsflöde för att ta en CSV-fil, mappa den mot ett XDM-schema och sedan importera den till Adobe Experience Platform.

## Utbildningsmål

- Lär dig hur du skapar ett XDM-schema i Adobe Experience Platform
- Lär dig hur du skapar datauppsättningar i Adobe Experience Platform
- Lär dig hur du skapar en slutpunkt för direktuppspelning och konfigurerar Adobe Experience Platform-tillägget i Launch
- Lär dig hur du skapar regler i Launch för att strömma data till Adobe Experience Platform
- Lär dig integrera Adobe Experience Platform Launch på en webbsida
- Lär dig hur du använder ett Adobe Experience Platform Workflow för att importera en CSV-fil till Adobe Experience Platform

## Förutsättningar

- Tillgång till Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Tillgång till Adobe Experience Platform Launch: [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)
- Åtkomst till [https://public.aepdemo.net](https://public.aepdemo.net)
- Tillgång till Postman

>[!IMPORTANT]
>
>Den här självstudiekursen har skapats för att underlätta ett visst workshop-format. Den använder specifika system och konton som du kanske inte har tillgång till. Även om ni inte har tillgång till dem tror vi att ni fortfarande kan lära er mycket genom att läsa igenom detta mycket detaljerade innehåll. Om du deltar i något av seminarierna och behöver dina inloggningsuppgifter, kontakta din Adobe-representant som kommer att ge dig den information som krävs.

## Arkitektur - översikt

Titta närmare på arkitekturen nedan, som visar vilka komponenter som kommer att diskuteras och användas i den här modulen.

![Arkitektur - översikt](../../assets/images/architecturem2.png)

## Sandlåda att använda

Använd den här sandlådan för den här modulen: `--module2sandbox--`.

>[!NOTE]
>
>Glöm inte att installera, konfigurera och använda Chrome-tillägget enligt referensen i [0.1 - Installera Chrome-tillägget för Experience League-dokumentationen](../module0/ex1.md)

## Utövningar

[2.1 Utforska webbplatsen](./ex1.md)

I den här övningen ska du utforska den webbplats som du kommer att använda som en del av den här funktionen.

[2.2 Konfigurera scheman och ange identifierare](./ex2.md)

I den här övningen konfigurerar du de XDM-scheman som krävs för att hämta profilinformation och kundbeteende. I varje XDM-schema måste du också konfigurera en primär identifierare för att länka all information till.

[2.3 Konfigurera datauppsättningar](./ex3.md)

I den här övningen hämtar du de nödvändiga datauppsättningarna för att hämta in och lagra profilinformation och kundbeteende.

[2.4 Datainmatning från offlinekällor](./ex4.md)

I den här övningen ska du besöka webbplatsen och mobilappen och uppträda som en kund, som strömmar data till Platform.

[2.5 Data Landing Zone](./ex5.md)

Konfigurera din källanslutning till Data Landing Zone med Azure Blob Storage.

[Sammanfattning och fördelar](./summary.md)

Sammanfattning av den här modulen och en översikt över fördelarna.

>[!NOTE]
>
>Tack för att du lade ned din tid på att lära dig allt om Adobe Experience Platform. Om du har frågor kan du dela allmän feedback om dina förslag på framtida innehåll. Kontakta Wouter Van Geluwe direkt genom att skicka ett e-postmeddelande till **vangeluw@adobe.com**.

[Gå tillbaka till Alla moduler](../../overview.md)
