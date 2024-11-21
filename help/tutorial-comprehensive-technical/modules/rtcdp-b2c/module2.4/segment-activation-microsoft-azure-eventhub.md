---
title: Audience Activation till Microsoft Azure Event Hub
description: Audience Activation till Microsoft Azure Event Hub
kt: 5342
doc-type: tutorial
exl-id: 23713cb4-2055-43e8-9380-0ca8845a75e8
source-git-commit: 216914c9d97827afaef90e21ed7d4f35eaef0cd3
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 0%

---

# 2.4 Real-Time CDP: Audience Activation till Microsoft Azure Event Hub

I den här modulen konfigurerar du ett Microsoft Azure EventHub-mål som ett realtidsmål för Adobe Experience Platform CDP i realtid. Du kommer också att konfigurera och distribuera en Azure-funktion som aktiveras i realtid när Adobe Experience Platform levererar en målgruppsnyttolast till ditt Azure EventHub-mål. Azure-funktionen som du utlöser visar mekanismen för Adobe Experience Platform CDP:s aktiveringsfunktioner i realtid.

Som en del av den här modulen får du också en förståelse för vad som utlöser CDP i realtid för att faktiskt leverera en nyttolast till en angiven destination. Vi kommer också att diskutera status för en målgruppskvalifikation och hur den hör ihop med aktiveringen.

Adobe Experience Platform CDP i realtid har stöd för dataaktivering till direktuppspelade molnlagringsdestinationer, vilket gör att du kan exportera målgruppsdata och händelser i realtid till dessa destinationer i JSON-format. Du kan sedan beskriva affärslogiken ovanpå dessa händelser på dina destinationer

Microsoft Azure Event Hubs är en helt hanterad datainjektionstjänst i realtid som är enkel, tillförlitlig och skalbar. Strömma miljontals händelser per sekund från valfri källa för att bygga dynamiska dataredningar och reagera direkt på affärsutmaningar.

## Utbildningsmål

- Bekanta dig med Microsoft Azure Event Hubs
- Konfigurera ett RTCDP-mål för din Microsoft Azure Event Hub
- Förstå när CDP aktiveras i realtid och hur aktiveringsnyttolasten ser ut
- Konfigurera Visual Studio-kod för att utveckla, testa och distribuera ditt Azure-projekt
- Skapa och distribuera en Azure-funktion som konsumerar målgruppskvalifikationer som levereras i realtid av RTCDP

## Förhandskrav

- Åtkomst till [Adobe Experience Platform](https://experience.adobe.com/platform)
- Förstå hur man definierar, använder och aktiverar målgrupper i Adobe Experience Platform

>[!NOTE]
>
>Glöm inte att installera, konfigurera och använda Chrome-tillägget enligt [Installera Chrome-tillägget för Experience League-dokumentationen](../../gettingstarted/gettingstarted/ex1.md)

## Utövningar

[2.4.1 Konfigurera miljön](./ex1.md)

I den här övningen ska du konfigurera din Microsoft Azure-miljö.

[2.4.2 Konfigurera din Microsoft Azure EventHub-miljö](./ex2.md)

I den här övningen ska du konfigurera din Microsoft Azure EventHub-miljö.

[2.4.3 Konfigurera Azure Event Hub-målet i Adobe Experience Platform](./ex3.md)

I den här övningen ska du konfigurera en CDP-målanslutning i realtid som levererar målgrupper i realtid till Event Hub-instansen som du har konfigurerat i föregående övning.

[2.4.4 Skapa en målgrupp](./ex4.md)

I den här övningen kommer du att skapa en publik i Adobe Experience Platform

[2.4.5 Aktivera er målgrupp](./ex5.md)

I den här övningen aktiverar du målgruppen till ditt EventHub-mål.

[2.4.6 Skapa ditt Microsoft Azure-projekt](./ex6.md)

I den här övningen skapar du en Azure-funktion som aktiveras i realtid när Adobe Experience-plattformen levererar målgruppskvalifikationer till motsvarande Azure Event Hub-mål.

[2.4.7 Heltäckande scenario](./ex7.md)

I det här skedet är allting klart. Nu kan du surfa lite på demowebbplatsen och få målgruppskvalifikationer levererade till din Microsoft Azure Event Hub Trigger-funktion.

[Sammanfattning och fördelar](./summary.md)

Sammanfattning av den här modulen och en översikt över fördelarna.

>[!NOTE]
>
>Tack för att du lägger ned din tid på att lära dig allt om Adobe Experience Platform och dess program. Om du har frågor kan du dela allmän feedback om dina förslag på framtida innehåll. Kontakta Tech Insiders direkt genom att skicka ett e-postmeddelande till **techinsiders@adobe.com**.

[Gå tillbaka till Alla moduler](../../../overview.md)
