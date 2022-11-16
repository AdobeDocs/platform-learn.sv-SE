---
title: Segmentaktivering till Microsoft Azure Event Hub
description: Segmentaktivering till Microsoft Azure Event Hub
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 73c2576d-0a69-4d56-a671-9ae1f75580b9
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---

# 13. Real-Time CDP: Segmentaktivering till Microsoft Azure Event Hub

**Författare: [Marc Meewis](https://www.linkedin.com/in/marcmeewis/), [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

I den här modulen konfigurerar du ett Microsoft Azure EventHub-mål som ett realtidsmål för Adobe Experience Platform CDP i realtid. Du kommer också att konfigurera och distribuera en Azure-funktion som aktiveras i realtid när Adobe Experience Platform levererar en segmentnyttolast till Azure EventHub-målet. Azure-funktionen som du utlöser visar mekanismen för Adobe Experience Platform CDP:s aktiveringsfunktioner i realtid.

Som en del av den här modulen får du också en förståelse för vad som utlöser CDP i realtid för att faktiskt leverera en nyttolast till en angiven destination. Vi kommer också att diskutera statusen för en segmentkvalificering och hur den hör ihop med aktiveringen.

Adobe Experience Platform CDP i realtid har stöd för dataaktivering till direktuppspelade molnlagringsdestinationer, vilket gör att du kan exportera målgruppsdata och händelser i realtid till dessa destinationer i JSON-format. Du kan sedan beskriva affärslogiken ovanpå dessa händelser på dina destinationer

Microsoft Azure Event Hubs är en helt hanterad datainjektionstjänst i realtid som är enkel, tillförlitlig och skalbar. Strömma miljontals händelser per sekund från valfri källa för att bygga dynamiska dataredningar och reagera direkt på affärsutmaningar.

## Utbildningsmål

- Bekanta dig med Microsoft Azure Event Hubs
- Konfigurera ett RTCDP-mål för din Microsoft Azure Event Hub
- Förstå när CDP aktiveras i realtid och hur aktiveringsnyttolasten ser ut
- Konfigurera Visual Studio-kod för att utveckla, testa och distribuera ditt Azure-projekt
- Skapa och distribuera en Azure-funktion som konsumerar segmentkvalifikationer som levereras i realtid av RTCDP

## Förutsättningar

- Åtkomst till [Adobe Experience Platform](https://experience.adobe.com/platform)
- Välbekant med webbplatsmiljön för AEP-demo
- Förstå hur man definierar, använder och aktiverar strömningssegment i Adobe Experience Platform

>[!IMPORTANT]
>
>Den här självstudiekursen har skapats för att underlätta ett visst workshop-format. Den använder specifika system och konton som du kanske inte har tillgång till. Även om ni inte har tillgång till dem tror vi att ni fortfarande kan lära er mycket genom att läsa igenom detta mycket detaljerade innehåll. Om du deltar i något av seminarierna och behöver dina inloggningsuppgifter, kontakta din Adobe-representant som kommer att ge dig den information som krävs.

## Arkitektur - översikt

Titta närmare på arkitekturen nedan, som visar vilka komponenter som kommer att diskuteras och användas i den här modulen.

![Arkitektur - översikt](../../assets/images/architecturem18.png)

## Sandlåda att använda

Använd den här sandlådan för den här modulen: `--module18sandbox--`.

>[!NOTE]
>
>Glöm inte att installera, konfigurera och använda Chrome-tillägget enligt referensen i [0.1 - Installera Chrome-tillägget för Experience League-dokumentationen](../module0/ex1.md)

## Utövningar

[13.0 Konfigurera miljön](./ex0.md)

I den här övningen ska du konfigurera din Microsoft Azure-miljö.

[13.1 Konfigurera din Microsoft Azure EventHub-miljö](./ex1.md)

I den här övningen ska du konfigurera din Microsoft Azure EventHub-miljö.

[13.2 Konfigurera Azure Event Hub-målet i Adobe Experience Platform](./ex2.md)

I den här övningen konfigurerar du din CDP-målanslutning i realtid som levererar segment i realtid till den EventHub som du konfigurerade i den föregående övningen.

[13.3 Skapa ett segment](./ex3.md)

I den här övningen ska du skapa ett direktuppspelningssegment i Adobe Experience Platform

[13.4 Aktivera segment](./ex4.md)

I den här övningen ska du aktivera ditt direktuppspelningssegment till din CDP EventHub-destination i realtid.

[13.5 Skapa ditt Microsoft Azure-projekt](./ex5.md)

I den här övningen skapar du en Azure-funktion som aktiveras i realtid när Adobe Experience-plattformen aktiverar segmentkvalifikationer för motsvarande Azure Event Hub-mål.

[13.6 Heltäckande scenario](./ex6.md)

Nu är allting klart. Nu kan du surfa lite på din AEP Demo-webbplats och få segmentkvalifikationer levererade till din Microsoft Azure EventHub Trigger-funktion.

[Sammanfattning och fördelar](./summary.md)

Sammanfattning av den här modulen och en översikt över fördelarna.

>[!NOTE]
>
>Tack för att du lade ned din tid på att lära dig allt om Adobe Experience Platform. Om du har frågor kan du dela allmän feedback om dina förslag på framtida innehåll. Kontakta Wouter Van Geluwe direkt genom att skicka ett e-postmeddelande till **vangeluw@adobe.com**.

[Gå tillbaka till Alla moduler](../../overview.md)
