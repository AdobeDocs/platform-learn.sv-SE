---
title: Migrera från Adobe Target till Adobe Journey Optimizer - mobiltillägg för beslut
description: Lär dig hur du migrerar din mobilappsimplementering från Adobe Target till Adobe Journey Optimizer - Beslutstillägg
last-substantial-update: 2023-02-23T00:00:00Z
exl-id: 32363b95-b6ad-44af-a3b0-e1fbbbf5a8f1
source-git-commit: 485e79e3569052184475fbc49ab5f43cebcac9a6
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 0%

---

# Migrera från Adobe Target till Adobe Journey Optimizer - mobiltillägg för beslut

Den här guiden är till för erfarna Adobe Target-implementerare som vill lära sig att migrera befintliga Adobe Experience Platfrom Mobile SDK-implementeringar från Adobe Target-tillägget till Adobe Journey Optimizer - Beslutstillägg.

Adobe Experience Platform Mobile SDK ger ett lyft för hela engagemanget i era mobilapplikationer. Target-tillägget bygger på Mobile SDK för att hjälpa er att personalisera appupplevelser med Adobe Target. Beslutstillägget är ett nyare tillvägagångssätt för att implementera Adobe Target i mobilappar som använder Adobe Experience Platform Edge Network-funktioner som hjälper till att integrera Target med plattformsbaserade appar som Real-Time CDP och Journey Optimizer.

## Viktiga fördelar

Några av fördelarna med förlängningen av beslutet är:

* Snabbare delning av målgrupper från [Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html)
* Integrera Target med Journey Optimizer för att stödja [leverans av Offer decisioning](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html)
* Bättre integrering med Adobe Analytics som inte förlitar sig på att sammanfoga information från separata nätverksanrop
* Ytterligare implementeringsflexibilitet för utvecklare

Den största fördelen för Target-kunder med migrering är förmodligen integrering med Real-time Customer Data Platform. Real-Time CDP erbjuder enastående målgruppsfunktioner baserat på alla data som inhämtas till Experience Platform och dess kapacitet för kundprofiler i realtid. Ett inbyggt ramverk för datastyrning automatiserar ansvarsfull användning av dessa data. Med Customer AI kan ni enkelt använda maskininlärningsmodeller för att konstruera benägenhets- och bortfallsmodeller vars utdata kan delas tillbaka till Adobe Target. Slutligen kan kunder som har tillvalet Healthcare and Privacy &amp; Security Shield använda funktionen för medgivande för att enkelt tillämpa individuella kunders samtycke. Platform Web SDK är ett krav för att använda dessa Real-Time CDP-funktioner i din webbkanal.

## Utbildningsmål

I slutet av den här självstudiekursen kan du:

* Punkt 1
* Punkt 2


## Förhandskrav

För att slutföra den här självstudiekursen bör du först:

* Punkt 1
* Punkt 2


>[!NOTE]
>
>Vi strävar efter att hjälpa dig att lyckas med din migrering av mobilmål från måltillägget till beslutstillägget. Om du stöter på problem med din migrering eller om du känner att det saknas viktig information i den här guiden kan du meddela oss genom att publicera [den här communitydiskussionen](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
