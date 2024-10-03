---
title: Planering - Migrera mål från at.js 2.x till Web SDK
description: Lär dig planera Adobe Target-implementeringen från at.js 2.x till Adobe Experience Platform Web SDK.
exl-id: 0e8f9cde-f361-4f69-886d-aad3074cd9b2
source-git-commit: d4308b68d6974fe47eca668dd16555d15a8247c9
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 0%

---

# Planera migreringen från at.js till Platform Web SDK

Innan du uppgraderar till Platform Web SDK på din webbplats bör du utvärdera din nuvarande implementering.

## Utvärdera aktuell at.js-implementering

Det första steget mot en framgångsrik migrering är att ha en god förståelse för den aktuella implementeringen av at.js Target. Det finns funktioner, funktioner och anpassad kod som du kan använda och som behöver uppdateras. Tänk på följande när du utvärderar:

### Vilka funktioner stöds?

Platform Web SDK är under ständig aktiv utveckling och funktioner och förbättringar läggs till regelbundet. När du utvärderar din nuvarande at.js-implementering kan du få den senaste informationen på sidan [Supported use cases](https://github.com/orgs/adobe/projects/18/views/1) .

### Vilka funktioner använder du idag?

Platform Web SDK är ett nytt bibliotek som samlar alla Adobe-lösningar för webbplatserna i en enda SDK. Detta ger bättre integration och möjliggör nya funktioner som är unika för Adobe Experience Platform. Detta innebär dock också att funktionen at.js inte är bakåtkompatibel med Platform Web SDK. Observera följande när du utvärderar den aktuella implementeringen:

- at.js-funktioner som `getOffer()` och `applyOffer()`
- Ändringar av Target-ets globala inställningar
- Integrering med Adobe Analytics
- Användning av ett flimmerande skript
- Användning av svarstoken
- Användning av parametrarna mbox, profile och entity
- Anpassad kod som är unik för din implementering

### Vilken migreringsstrategi tänker du använda?

När du har granskat implementeringen av at.js måste du fastställa en migreringsstrategi. Det finns två alternativ:

- Migrera alla Adobe-program samtidigt på hela webbplatsen
- Migrera sida vid sida

Eftersom Platform Web SDK kombinerar och aktiverar flera Adobe-program måste du koordinera målmigreringen för andra Adobe-program som Analytics och Audience Manager. Alla Adobe-bibliotek på en viss sida bör migreras samtidigt. En blandad implementering av Platform Web SDK för Target och AppMeasurement för Analytics på en viss sida stöds inte. Det finns dock stöd för en blandad implementering på olika sidor, till exempel Platform Web SDK på sida A och at.js med AppMeasurement på sida B.

När du migrerar bör du planera för att följa företagets process för att testa och släppa ny kod och använda saker som utvecklingsmiljöer, qa och staging-miljöer innan du släpper till produktion.

>[!CAUTION]
>
>Omdirigeringserbjudanden stöds inte i sidvis migrering om du omdirigerar från en sida med ett bibliotek till en sida med ett annat bibliotek


Granska sedan den detaljerade [jämförelsen av at.js till Platform Web SDK](detailed-comparison.md) för att få en bättre förståelse för de tekniska skillnaderna och identifiera områden som kräver ytterligare fokus.

>[!NOTE]
>
>Vi vill hjälpa dig att lyckas med målmigreringen från at.js till Web SDK. Om du stöter på problem med din migrering eller om du känner att det saknas viktig information i den här guiden kan du meddela oss genom att publicera [den här communitydiskussionen](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
