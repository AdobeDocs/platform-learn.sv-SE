---
title: Översikt
description: Översikt
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 8ffa258b-6ff7-4413-aead-21b106668c65
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 1%

---

# Översikt

Att samla in data om händelser i en användares webbläsare är en grundläggande del av en marknadsföringsstrategi. Adobe har tillhandahållit flera verktyg som hjälper dig att hantera dessa data. Även om du kan bekanta dig med vart och ett av dessa verktyg var för sig, försöker den här självstudiekursen ge en mer heltäckande bild av vad varje verktyg gör och hur de fungerar tillsammans för att uppnå ett gemensamt mål.

I den här självstudiekursen diskuterar vi en strategi för (1) att strukturera och lagra data i Adobe Experience Platform, (2) att hantera data i webbläsaren och att meddela att vissa händelser har inträffat och (3) att reagera på sådana händelser genom att skicka relevanta data till Adobe Experience Platform.

I den här självstudiekursen används Adobe Client Data Layer, Adobe Experience Platform Web SDK och taggningsfunktionen för en mer prediktiv, sömlös implementering, men du kan också blanda och matcha dessa verktyg med tredjeparts- eller interna verktyg för optimal flexibilitet.

## Exempelscenario

I den här självstudiekursen antar vi att du implementerar datainsamling för en enkel produktsida på en e-handelsplats. Produktsidan läses in i webbläsaren. Här ser du att användaren har tittat på produkten. Användaren bestämmer sig för att köpa produkten, så att han/hon klickar på en knapp för att lägga produkten i kundvagnen. Här ser du att användaren har öppnat en ny kundvagn och lagt till produkten i kundvagnen genom att skicka upplevelsehändelser till Adobe Experience Platform. Slutligen klickar användaren på en _Ladda ned appen_ eftersom de är intresserade av din mobilapp. Du spårar att användaren har klickat på länken.
