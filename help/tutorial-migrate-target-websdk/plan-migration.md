---
title: Planering | Migrera mål från at.js 2.x till Web SDK
description: Lär dig planera Adobe Target-implementeringen från at.js 2.x till Adobe Experience Platform Web SDK.
source-git-commit: dad7a1b01c4313d6409ce07d01a6520ed83f5e89
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 0%

---

# Planera migreringen från at.js till Platform Web SDK

Innan du uppgraderar till Platform Web SDK på din webbplats bör du utvärdera din nuvarande implementering.

## Utvärdera aktuell at.js-implementering

Det första steget mot en framgångsrik migrering är att ha en god förståelse för den aktuella implementeringen av at.js Target. Det finns funktioner, funktioner och anpassad kod som du kan använda och som behöver uppdateras. Tänk på följande när du utvärderar:

### Vilka funktioner stöds?

Platform Web SDK är under ständig aktiv utveckling och funktioner och förbättringar läggs till regelbundet. När du utvärderar din nuvarande at.js-implementering kan du läsa [användningsfall som stöds](https://github.com/orgs/adobe/projects/18/views/1) sida för den senaste informationen.

### Vilka funktioner använder du idag?

Platform Web SDK är ett nytt bibliotek som samlar alla Adobe-lösningar för webbplatserna i en enda SDK. Detta ger bättre integration och möjliggör nya funktioner som är unika för Adobe Experience Platform. Detta innebär dock också att funktionen at.js inte är bakåtkompatibel med Platform Web SDK. Observera följande när du utvärderar den aktuella implementeringen:

- at.js funktioner som `getOffer()` och `applyOffer()`
- Ändringar av Target-ets globala inställningar
- Integrering med Adobe Analytics
- Användning av ett flimmerande skript
- Användning av svarstoken
- Användning av mbox-, profile- och enhetsparametrar
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


Granska sedan detaljerna [jämförelse av at.js med Platform Web SDK](detailed-comparison.md) för att få en bättre förståelse för de tekniska skillnaderna och identifiera områden som kräver extra fokus.

>[!NOTE]
>
>Vi vill hjälpa dig att lyckas med målmigreringen från at.js till Web SDK. Om du stöter på problem med din migrering eller känner att det saknas viktig information i den här guiden ber vi dig att meddela oss genom att publicera i [den här communitydiskussionen](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).
