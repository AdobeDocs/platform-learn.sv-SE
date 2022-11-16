---
title: CDP i realtid - Bygg ett segment och vidta åtgärder
description: CDP i realtid - Bygg ett segment och vidta åtgärder
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 147d9153-5742-4857-aae1-0ec434a1e626
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---

# 6. CDP i realtid - Bygg ett segment och vidta åtgärder

**Författare: [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/), [Alberto De Caro](https://www.linkedin.com/in/albertodecaro/), [Benedikt Wedenik](https://www.linkedin.com/in/benedikt-wedenik/)**

I den här modulen ska du konfigurera ett direktuppspelningssegment och aktivera segmentet för flera mål.

## Utbildningsmål

- Lär dig hur du skapar ett segment och aktiverar det för direktuppspelning.
- Lär dig hur du konfigurerar ett annonsmål med hjälp av Adobe Experience Platform användargränssnitt.
- Lär dig hur du ansluter ett segment till ett mål och aktiverar det.
- Lär dig hur du använder Adobe Experience Platform-segment i Adobe Audience Manager och hur du använder Adobe Audience Manager-segment i Adobe Experience Platform, tack vare dubbelriktad segmentdelning.

## Förutsättningar

- Tillgång till Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Tillgång till Adobe Target
- Tillgång till AWS S3

>[!IMPORTANT]
>
>Den här självstudiekursen har skapats för att underlätta ett visst workshop-format. Den använder specifika system och konton som du kanske inte har tillgång till. Även om ni inte har tillgång till dem tror vi att ni fortfarande kan lära er mycket genom att läsa igenom detta mycket detaljerade innehåll. Om du deltar i något av seminarierna och behöver dina inloggningsuppgifter, kontakta din Adobe-representant som kommer att ge dig den information som krävs.

## Arkitektur - översikt

Titta närmare på arkitekturen nedan, som visar vilka komponenter som kommer att diskuteras och användas i den här modulen.

![Arkitektur - översikt](../../assets/images/architecturem11.png)

## Sandlåda att använda

Använd den här sandlådan för den här modulen: `--module11sandbox--`.

>[!NOTE]
>
>Glöm inte att installera, konfigurera och använda Chrome-tillägget enligt referensen i [0.1 - Installera Chrome-tillägget för Experience League-dokumentationen](../module0/ex1.md)

## Utövningar

[6.1 Skapa ett segment](./ex1.md)

Lär dig hur du skapar ett segment.

[6.2 Granska hur du konfigurerar DV360-mål med hjälp av destinationer](./ex2.md)

Lär dig hur du konfigurerar ett annonsmål med hjälp av Real-Time CDP användargränssnitt.

[6.3 Vidta åtgärder: skicka segmentet till DV360](./ex3.md)

Anslut segmentet som du skapade i övning 6.1 till mål-DV360.

[6.4 Vidta åtgärder: skicka segmentet till en S3-destination](./ex4.md)

Använd segmentet som du skapade i övning 6.1 och skicka det till en S3-destination, som vanligtvis används för e-postmarknadsföring.

[6.5 Vidta åtgärder: skicka segmentet till Adobe Target](./ex5.md)

Använd det segment du skapat i övning 6.1 för att konfigurera en Experience Targeting Activity i Adobe Target.

[6.6 Externa målgrupper](./ex6.md)

Importera målgrupper från ett externt källsystem till Adobe Experience Platform.

[6.7 Destinations-SDK](./ex7.md)

Konfigurera ditt eget mål med Destinations SDK.

[Sammanfattning och fördelar](./summary.md)

Sammanfattning av den här modulen och en översikt över fördelarna.

>[!NOTE]
>
>Tack för att du lade ned din tid på att lära dig allt om Adobe Experience Platform. Om du har frågor kan du dela allmän feedback om dina förslag på framtida innehåll. Kontakta Wouter Van Geluwe direkt genom att skicka ett e-postmeddelande till **vangeluw@adobe.com**.

[Gå tillbaka till Alla moduler](../../overview.md)
