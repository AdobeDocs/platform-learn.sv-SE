---
title: Migrera din mobilapp från Adobe Target till Adobe Journey Optimizer - Beslutstillägg
description: Lär dig hur du migrerar din mobilappsimplementering från Adobe Target till Adobe Journey Optimizer - Beslutstillägg
last-substantial-update: 2023-02-23T00:00:00Z
exl-id: 32363b95-b6ad-44af-a3b0-e1fbbbf5a8f1
source-git-commit: e0359d1bade01f79d0f7aff6a6e69f3e4d0c3b62
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 0%

---

# Migrera din mobilapp från Adobe Target till Adobe Journey Optimizer - Beslutstillägg

Den här guiden är till för erfarna Adobe Target-implementerare som vill lära sig hur man migrerar befintliga Adobe Experience Platfrom Mobile SDK-implementeringar från Adobe Target-tillägget till Adobe Journey Optimizer - Beslutstillägg.

Adobe Experience Platform Mobile SDK ger total interaktion i era mobilapplikationer. Target-tillägget bygger på Mobile SDK för att hjälpa er att personalisera appupplevelser med Adobe Target. Beslutstillägget är ett nyare tillvägagångssätt för att implementera Adobe Target i mobilappar som använder Adobe Experience Platform Edge Network-funktioner som hjälper till att integrera Target med plattformsbaserade appar som Real-Time CDP och Journey Optimizer.

![Bild som visar Mobile SDK som ansluter till Target via Edge Network med beslutstillägget](assets/datacollection.png)

## Viktiga fördelar

Några av fördelarna med Adobe Journey Optimizer Decision Extension jämfört med Target-tillägget är:

* Snabbare delning av målgrupper från [Real-Time Customer Data Platform](https://experienceleague.adobe.com/sv/docs/platform-learn/tutorials/destinations/target/next-hit-personalization)
* Integrera Target med Journey Optimizer för att stödja [Offer Decisioning-leverans](https://experienceleague.adobe.com/sv/docs/target/using/integrate/ajo/offer-decision)
* Bättre integrering med Adobe Analytics som inte förlitar sig på att sammanfoga information från separata nätverksanrop
* Ytterligare implementeringsflexibilitet för utvecklare

Den största fördelen för Target-kunder med migrering är förmodligen integrering med Real-Time Customer Data Platform. Real-Time CDP erbjuder enastående målgruppsfunktioner baserat på alla data som hämtas in till Experience Platform och dess kapacitet för kundprofiler i realtid. Ett inbyggt ramverk för datastyrning automatiserar ansvarsfull användning av dessa data. Med Customer AI kan ni enkelt använda maskininlärningsmodeller för att konstruera benägenhets- och bortfallsmodeller vars utdata kan delas tillbaka till Adobe Target. Slutligen kan kunder som har tillvalet Healthcare and Privacy &amp; Security Shield lägga in medgivandefunktionen för att få individuella kunders samtycke. Platform Mobile SDK och Decisioning är ett krav för att du ska kunna använda dessa Real-Time CDP-funktioner i din mobilkanal.

## Migreringssteg

Hur stor insats du ska göra för att migrera från måltillägget till beslutstillägget beror på hur komplex din nuvarande implementering och vilka målfunktioner som används är.

Oavsett hur enkel eller komplex implementeringen är är det viktigt att du förstår ditt nuvarande läge fullständigt innan du migrerar. Den här guiden hjälper dig att bryta ned komponenterna i den aktuella implementeringen och utveckla en hanterbar plan för att migrera varje del.

Migreringsprocessen omfattar följande viktiga steg:

1. Utvärdera er nuvarande implementering, inklusive:
   1. Alla Target-API:er som används
   1. Ändringar av Target-ets globala inställningar
   1. Integrering med Adobe Analytics
   1. Användning av parametrarna mbox, profile och entity
   1. Användning av profilskript och målgrupper
   1. Anpassad kod som är unik för din implementering
1. Konfigurera de inledande komponenterna för anslutning till Adobe Experience Platform Edge Network
1. Uppdatera den grundläggande implementeringen för att ersätta måltillägget med beslutstillägget
1. Förbättra SDK-implementeringen för dina specifika användningsfall. Detta kan innebära att ytterligare parametrar skickas, att svarstoken används med mera.
1. Uppdatera objekt i Target-gränssnittet, till exempel profilskript, aktiviteter och målgruppsdefinitioner
1. Validera den slutliga implementeringen innan du byter till produktionsappen


>[!INFO]
>
>I Adobe Experience Platform Mobile SDK-ekosystemet implementeras tillägg av SDK:er som importeras till dina program och som kan ha olika namn:
>
> * **Mål-SDK** implementerar **Adobe Target-tillägget**
> * **Optimera SDK** implementerar tillägget **Adobe Journey Optimizer - Bestämning**

Granska sedan den detaljerade [jämförelsen av måltillägget och beslutstillägget](comparison.md) för att få en bättre förståelse för de tekniska skillnaderna och identifiera områden som kräver ytterligare fokus.

>[!NOTE]
>
>Vi strävar efter att hjälpa dig att lyckas med din migrering av mobilmål från måltillägget till beslutstillägget. Om du stöter på problem med din migrering eller om du känner att det saknas viktig information i den här guiden kan du meddela oss genom att publicera [den här communitydiskussionen](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-adobe-target-to-mobile-sdk-on-edge/m-p/747484#M625).
