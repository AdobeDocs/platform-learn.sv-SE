---
title: Migrera från Adobe Target till Adobe Journey Optimizer - mobiltillägg för beslut
description: Lär dig hur du migrerar din mobilappsimplementering från Adobe Target till Adobe Journey Optimizer - Beslutstillägg
last-substantial-update: 2023-02-23T00:00:00Z
exl-id: 32363b95-b6ad-44af-a3b0-e1fbbbf5a8f1
source-git-commit: f3fd5f45412900dcb871bc0b346ce89108fa8913
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---

# Migrera från Adobe Target till Adobe Journey Optimizer - mobiltillägg för beslut

Den här guiden är till för erfarna Adobe Target-implementerare som vill lära sig att migrera befintliga Adobe Experience Platfrom Mobile SDK-implementeringar från Adobe Target-tillägget till Adobe Journey Optimizer - Beslutstillägg.

Adobe Experience Platform Mobile SDK ger total interaktion i era mobilapplikationer. Target-tillägget bygger på Mobile SDK för att hjälpa er att personalisera appupplevelser med Adobe Target. Beslutstillägget är ett nyare tillvägagångssätt för att implementera Adobe Target i mobilappar som använder Adobe Experience Platform Edge Network-funktioner som hjälper till att integrera Target med plattformsbaserade appar som Real-Time CDP och Journey Optimizer.

## Viktiga fördelar

Några av fördelarna med Adobe Journey Optimizer Decision Extension jämfört med Target-tillägget är:

* Snabbare delning av målgrupper från [Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html)
* Integrera Target med Journey Optimizer för att stödja [leverans av Offer decisioning](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html)
* Bättre integrering med Adobe Analytics som inte förlitar sig på att sammanfoga information från separata nätverksanrop
* Ytterligare implementeringsflexibilitet för utvecklare

Den största fördelen för Target-kunder med migrering är förmodligen integrering med Real-time Customer Data Platform. Real-Time CDP erbjuder enastående målgruppsfunktioner baserat på alla data som inhämtas till Experience Platform och dess kapacitet för kundprofiler i realtid. Ett inbyggt ramverk för datastyrning automatiserar ansvarsfull användning av dessa data. Med Customer AI kan ni enkelt använda maskininlärningsmodeller för att konstruera benägenhets- och bortfallsmodeller vars utdata kan delas tillbaka till Adobe Target. Slutligen kan kunder som har tillvalet Healthcare and Privacy &amp; Security Shield använda funktionen för medgivande för att enkelt tillämpa individuella kunders samtycke. Platform Mobile SDK och Decisioning är ett krav för att du ska kunna använda dessa Real-Time CDP-funktioner i din mobilkanal.


>[!NOTE]
>
>Vi strävar efter att hjälpa dig att lyckas med din migrering av mobilmål från måltillägget till beslutstillägget. Om du stöter på problem med din migrering eller om du känner att det saknas viktig information i den här guiden kan du meddela oss genom att publicera [den här communitydiskussionen](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
