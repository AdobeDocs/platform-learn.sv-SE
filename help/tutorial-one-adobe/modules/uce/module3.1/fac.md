---
title: Datainsamling - sammanställning av externa målgrupper
description: Datainsamling - sammanställning av externa målgrupper
kt: 5342
doc-type: tutorial
source-git-commit: dc86e52b659d7b428aca03fdb041e7410901e1fd
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 0%

---

# 3.1 Sammansatt målgrupp

I den här modulen är målet att lära sig allt om att skapa målgrupper med Federated Audience Composition.

Med Federated Audience Composition (FAC) i Experience Platform kan ni få åtkomst till och skapa målgrupper med motsvarande värdefulla attribut från datalager i företagsklass, som berikar och kompletterar kundprofilen och målgrupperna i realtid i Experience Platform för förbättrad segmentering, målgruppsanpassning, aktivering och leverans av slagkraftiga kundupplevelser. Med Federated Audience Composition skapas en virtuell databas genom att fjärrdatabaser länkas via metadata. Den här metoden förenklar åtkomst, minskar dubbletter och förbättrar slutanvändarens upplevelse. Teamen får flexibilitet att importera datauppsättningar direkt till Experience Platform eller få tillgång till datauppsättningar som finns i datalager när de samlar målgrupper för engagemangsarbetsflöden. Den här metoden utnyttjar datalagerinvesteringar och -resurser för att komplettera Real-Time CDP och Journey Optimizer. Med Federated Audience Composition kan kunderna använda och kombinera batch- och realtidsfunktioner i kritiska nya användningsmönster:

- Samlad målgruppssegmentering: Ett team kan skapa en målgrupp med hjälp av ett marknadsvänligt dra och släpp-gränssnitt för målgruppsdisposition i Real-Time CDP och Journey Optimizer, men med en fråga som skickas till datalagret, lämna känsliga underliggande data i lagerstället utan att behöva duplicera och ge flexibel tillgång till viktiga datauppsättningar.
- Målgruppsutveckling: De målgrupper som byggts i Real-Time CDP och Journey Optimizer kan berikas med ytterligare företagsdata för att förbättra målgruppsanpassning och personalisering med ytterligare profilbaserade och icke-profilbaserade datauppsättningar som inte finns kvar i Adobe Experience Platform. Ett detaljhandelsmärke kan t.ex. komplettera en publik av nyligen köpare på nätet med en lista över de främsta tegelstenarna och de största platserna för att skapa en målgrupp för en flerkanalsmarknadsföring online och i butik.
- Profilberikning: Teamen kan välja profilattribut från datalagret som är avgörande för att de upplevelser som är aktuella i ögonblicket ska kunna behållas i användbara kundprofiler som finns i Real-Time CDP och nås via Journey Optimizer. Dessa ytterligare datapunkter är sedan tillgängliga för segmentering längre fram i kedjan och personalisering som triggas av händelsebeteenden beroende på användaråtgärd och kundanvändning. Detta gör att attribut som följer med federerade målgrupper kan vara tillgängliga för segmentering och personalisering i ögonblicket, tillsammans med andra attribut och beteendesignaler som finns kvar i en kundprofil.

Federated Audience Composition ger kunder i Real-Time CDP och Journey Optimizer flexibilitet att bestämma vilka data de vill använda när och hjälper till att undvika onödiga dubbletter av datauppsättningar eller integreringsmönster. Detta är en unik kombination av en federerad strategi för att använda företagsdata för att strukturera målgrupper och värdefulla attribut, kombinerat med ett system som är optimerat för interaktion i alla kanaler. Detta resulterar i mindre datarörelser men också nya möjligheter att utnyttja värdefulla målgrupper och attribut för konsekvent aktivering med låg fördröjning i alla kanaler.

## Utbildningsmål

- Lär dig ansluta Snowflake med Adobe Experience Platform
- Lär dig hur du skapar en datamodell för dina federerade data i Adobe Experience Platform
- Lär dig skapa sammansatta målgruppsbilder i Adobe Experience Platform

## Förhandskrav

- Åtkomst till Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Åtkomst till ett datalager i Snowflake

## Utövningar

[3.1.1 Konfigurera Snowflake-miljön](./ex1.md)

I den här övningen ska du konfigurera ditt testkonto för Snowflake och ansluta det till Adobe Experience Platform

[3.1.2 Skapa scheman, datamodell och länkar](./ex2.md)

I den här övningen konfigurerar du din datamodell i AEP för federerade data.

[3.1.3 Skapa en federerad komposition](./ex3.md)

I den här övningen konfigurerar du din datamodell i AEP för federerade data.

[Sammanfattning och fördelar](./summary.md)

Sammanfattning av den här modulen och en översikt över fördelarna.

>[!NOTE]
>
>Tack för att du lägger ned din tid på att lära dig allt om Adobe Experience Platform och dess program. Om du har frågor kan du dela allmän feedback om dina förslag på framtida innehåll. Kontakta Tech Insiders direkt genom att skicka ett e-postmeddelande till **techinsiders@adobe.com**.

[Gå tillbaka till Alla moduler](../../../overview.md)
