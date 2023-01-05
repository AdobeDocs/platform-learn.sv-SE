---
title: Introduktion | Migrera mål från at.js 2.x till Web SDK
description: Lär dig hur du migrerar en Adobe Target-implementering från at.js 2.x till Adobe Experience Platform Web SDK. Du kan läsa in JavaScript-biblioteket, skicka parametrar, återge aktiviteter och andra viktiga bildtexter.
recommendations: catalog,noDisplay
source-git-commit: dad7a1b01c4313d6409ce07d01a6520ed83f5e89
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---

# Migrera mål från at.js 2.x till Platform Web SDK

Den här guiden är till för erfarna Adobe Target-utvecklare som vill lära sig hur man migrerar en at.js-implementering till Adobe Experience Platform Web SDK.

Adobe Experience Platform Web SDK är ett JavaScript-bibliotek på klientsidan som gör att Adobe Experience Cloud-kunder kan interagera med Experience Cloud-tjänster via Adobe Experience Platform Edge Network. I det nya biblioteket kombineras funktionerna i de olika programbiblioteken i Adobe till ett enda lättviktspaket som fullt ut kan utnyttja de nya funktionerna i Adobe Experience Platform.

## Viktiga fördelar

Några av fördelarna med Platform Web SDK jämfört med det fristående at.js-biblioteket är:

* Snabbare delning av målgrupper från [Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html)
* Integrera Target med Journey Optimizer som stöd [offer decisioning](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html)
* Möjlighet att använda [ID för första part](https://experienceleague.adobe.com/docs/platform-learn/data-collection/edge-network/generate-first-party-device-ids.html) för att generera ECID för besöksidentifiering med längre varaktighet
* Konsolidering av nätverksanrop mellan olika Adobe-program
* Mindre utrymme för bättre sidhastighetsmätningar
* En tätare integrering med Adobe Analytics som inte förlitar sig på att sammanfoga information från separata nätverksanrop
* Ytterligare implementeringsflexibilitet för utvecklare

Den största fördelen med migrering är förmodligen Real-time Customer Data Platform kunder. Real-Time CDP erbjuder enastående målgruppsfunktioner baserat på alla data som inhämtas till Experience Platform och dess kapacitet för kundprofiler i realtid. Ett inbyggt ramverk för datastyrning automatiserar ansvarsfull användning av dessa data. Med Customer AI kan ni enkelt använda maskininlärningsmodeller för att konstruera benägenhets- och bortfallsmodeller vars utdata kan delas tillbaka till Adobe Target. Slutligen kan kunder som har tillvalet Healthcare and Privacy &amp; Security Shield använda funktionen för medgivande för att enkelt tillämpa individuella kunders samtycke. Platform Web SDK är ett krav för att du ska kunna använda dessa RTCDP-funktioner i din webbkanal.

## Utbildningsmål

I slutet av den här självstudiekursen kan du:

* Förstå skillnaderna mellan at.js och Platform Web SDK för målitimplementering
* Konfigurera den inledande konfigurationen för Target-funktionen
* Uppgradera at.js-biblioteket till Platform Web SDK
* Skapa formulärbaserade och visuella upplevelsedispositioner
* Skicka parametrar till Target
* Spåra konverteringshändelser
* Aktivera stöd för flera domäner
* Uppdatera målgrupper och profilskript
* Validera implementeringen
* Debug Target experience delivery


## Förutsättningar

För att slutföra den här självstudiekursen bör du först:

* Ha en teknisk förståelse för er nuvarande implementering av Target at.js
* Kontrollera att du har en [Redigerare eller utgivarroll](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html#section_8C425E43E5DD4111BBFC734A2B7ABC80) för Target-instansen så att du kan testa exempel själv
* Installera [Webbläsartillägg för Adobe Experience Cloud Visual Editing](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension.html) för Google Chrome
* Lär dig hur du ställer in aktiviteter i Adobe Target. Om du behöver en uppdaterare kan du använda följande självstudiekurser och guider för den här lektionen:
   * [Använda Visual Experience Composer](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-visual-experience-composer.html)
   * [Använda den formulärbaserade Experience Composer](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-form-based-experience-composer.html)
   * [Skapa aktiviteter för målinriktad upplevelse](https://experienceleague.adobe.com/docs/target-learn/tutorials/activities/create-experience-targeting-activities.html)

När du är klar är det första steget mot en lyckad migrering att [lära sig mer om migreringsprocessen](migration-overview.md) och hur at.js och Platform Web SDK skiljer sig åt.

>[!NOTE]
>
>Vi vill hjälpa dig att lyckas med målmigreringen från at.js till Web SDK. Om du stöter på problem med din migrering eller känner att det saknas viktig information i den här guiden ber vi dig att meddela oss genom att publicera i [den här communitydiskussionen](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).