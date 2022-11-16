---
title: Intelligenta tjänster
description: Intelligenta tjänster
kt: 5342
audience: Data Engineer, Data Architect, Data Scientist
doc-type: tutorial
activity: develop
exl-id: 99b56722-95bf-4c51-b4d6-8b5a8e5fd936
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---

# 5. Intelligenta tjänster

**Författare: [Diptiman Badajena](https://www.linkedin.com/in/diptiman-badajena-1b178019/), [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

I den här modulen får du lära dig hur du konfigurerar, konfigurerar och använder Adobe Experience Platform Intelligent Services.

## Utbildningsmål

- Bekanta dig med Adobe Experience Platform
- Konfigurera schema/datauppsättning för användning med intelligenta tjänster
- Skapa en ny AI-instans för kunder
- Kontrollpanel och segmentering

## Förutsättningar

- Tillgång till Adobe Experience Platform: [https://experience.adobe.com/platform](https://experience.adobe.com/platform)

>[!IMPORTANT]
>
>Den här självstudiekursen har skapats för att underlätta ett visst workshop-format. Den använder specifika system och konton som du kanske inte har tillgång till. Även om ni inte har tillgång till dem tror vi att ni fortfarande kan lära er mycket genom att läsa igenom detta mycket detaljerade innehåll. Om du deltar i något av seminarierna och behöver dina inloggningsuppgifter, kontakta din Adobe-representant som kommer att ge dig den information som krävs.

## Arkitektur - översikt

Titta närmare på arkitekturen nedan, som visar vilka komponenter som kommer att diskuteras och användas i den här modulen.

![Arkitektur - översikt](../../assets/images/architecturem5.png)

## Sandlåda att använda

Använd den här sandlådan för den här modulen: `--module10sandbox--`.

>[!NOTE]
>
>Glöm inte att installera, konfigurera och använda Chrome-tillägget enligt referensen i [0.1 - Installera Chrome-tillägget för Experience League-dokumentationen](../module0/ex1.md)

## Utövningar

[5.1 Customer AI - Data Preparation (Ingest)](./ex1.md)

Kunddata importeras och omvandlas med Experience Data Model (XDM) på Adobe Experience Platform. I synnerhet måste alla datauppsättningar som används i Intelligent Services överensstämma med CEE-XDM-schemat (Consumer Experience Event).

[5.2 Customer AI - Create a New Instance (Konfigurera)](./ex2.md)

Marknadsföringsanalytikern konfigurerar önskade prognoser genom att specificera affärsregler och identifiera relevanta data. När du har konfigurerat modellen schemalägger du körningar och granskningspoäng.

[5.3 Customer AI - Scoring Dashboard and Segmentation (Predict &amp; Take Action)](./ex3.md)

När modellerna har avslutat utbildningen och poängsättningen skrivs poängen tillbaka till Platform. Du kan bestämma vilka åtgärder som ska vidtas med prognoserna, som att definiera segment, bygga anpassade kontrollpaneler osv.

>[!NOTE]
>
>Tack för att du lade ned din tid på att lära dig allt om Adobe Experience Platform. Om du har frågor kan du dela allmän feedback om dina förslag på framtida innehåll. Kontakta Wouter Van Geluwe direkt genom att skicka ett e-postmeddelande till **vangeluw@adobe.com**.

[Gå tillbaka till Alla moduler](../../overview.md)
