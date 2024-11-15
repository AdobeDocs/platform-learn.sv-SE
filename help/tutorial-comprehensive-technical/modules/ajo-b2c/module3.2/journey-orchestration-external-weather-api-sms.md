---
title: Adobe Journey Optimizer - External Weather API, SMS Action med mera
description: Adobe Journey Optimizer - External Weather API, SMS Action med mera
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 7f3d6dcb-845d-4ff1-97c3-8e93b8d2c624
source-git-commit: f4b3463ce9464c96378790bf8070504fc90cb2ff
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 0%

---

# 3.2 Adobe Journey Optimizer: Externa datakällor och anpassade åtgärder

**Författare: [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

I den här modulen ska du använda Adobe Journey Optimizer för att lyssna på kundbeteenden, både online och offline, och svara på dem på ett intelligent, sammanhangsberoende sätt och i realtid. Du har redan haft en inledande praktisk erfarenhet av Adobe Journey Optimizer i modul 6. I den här övningen går du lite längre och utforskar ett mer avancerat användningssätt där externa datakällor används som en del av en resa.

## Utbildningsmål

- Lär dig skapa händelser, externa datakällor och resor i Adobe Journey Optimizer
- Lär dig hur du använder väderinformation från Open Weather API
- Lär dig hur du använder anpassade åtgärdsmål som Twilio och Slack från Adobe Journey Optimizer

## Förhandskrav

- Åtkomst till Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Tillgång till Adobe Journey Optimizer
- Åtkomst till Open Weather API

## Affärskontext

Som varumärke har ni investerat mycket i personalisering av onlineupplevelser. Nu vill ni vara lika sammanhangsberoende och relevanta för offlineupplevelser.
I den här modulen kommer ni att använda en kunds närvaro i en offlinebutik för att sedan leverera en personaliserad upplevelse i butiken genom att visa relevant innehåll för kunden på våra butiksskärmar och samtidigt leverera ett personaliserat push- eller SMS-meddelande till samma kund, allt i realtid.
Som varumärke förstår ni också att sammanhanget i hög grad påverkar en kunds intresse, så att ni vill ta med den aktuella väderinformationen om kundens plats och bestämma vilket innehåll eller vilken kampanj som ska visas.

>[!NOTE]
>
>Glöm inte att installera, konfigurera och använda Chrome-tillägget enligt [Installera Chrome-tillägget för Experience League-dokumentationen](../../gettingstarted/gettingstarted/ex1.md)

## Utövningar

[3.2.1 Definiera en händelse](./ex1.md)

Lär dig hur du definierar en anpassad händelse med Adobe Journey Optimizer.

[3.2.2 Definiera en extern datakälla](./ex2.md)

Lär dig hur du konfigurerar en extern datakälla med Adobe Journey Optimizer.

[3.2.3 Definiera en anpassad åtgärd](./ex3.md)

Lär dig hur du definierar en extern åtgärd med Adobe Journey Optimizer.

[3.2.4 Skapa din resa och dina meddelanden](./ex4.md)

Kombinera händelser, datakällor och åtgärder till en intelligent och sammanhangsberoende resa.

[3.2.5 Utlösa din resa](./ex5.md)

Utlös din resa.

[Sammanfattning och fördelar](./summary.md)

Sammanfattning av den här modulen och en översikt över fördelarna.

>[!NOTE]
>
>Tack för att du lägger ned din tid på att lära dig allt om Adobe Experience Platform och dess program. Om du har frågor kan du dela allmän feedback om dina förslag på framtida innehåll. Kontakta Tech Insiders direkt genom att skicka ett e-postmeddelande till **techinsiders@adobe.com**.

[Gå tillbaka till Alla moduler](../../../overview.md)
