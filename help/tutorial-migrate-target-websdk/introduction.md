---
title: Migrate Target från at.js 2.x till Web SDK
description: Lär dig migrera en Adobe Target-implementering från at.js 2.x till Adobe Experience Platform Web SDK. Exempel på ämnen är att läsa in JavaScript-biblioteket, skicka parametrar, renderingsaktiviteter och andra viktiga bildtexter.
last-substantial-update: 2023-02-23T00:00:00Z
exl-id: c8920fde-ad6b-4f2d-a35f-ce865b35bba0
source-git-commit: d6471c8e383e22fed4ad5870952d0d0470f593db
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 0%

---

# Migrate Target från at.js 2.x till Platform Web SDK

Den här guiden är till för erfarna Adobe Target-utvecklare som vill lära sig hur man migrerar en at.js-implementering till Adobe Experience Platform Web SDK.

Adobe Experience Platform Web SDK är ett JavaScript-bibliotek på klientsidan som gör att Adobe Experience Cloud-kunder kan interagera med Experience Cloud genom Adobe Experience Platform Edge Network. I det nya biblioteket kombineras funktionerna i de olika programbiblioteken i Adobe till ett enda lättviktspaket som fullt ut kan utnyttja de nya funktionerna i Adobe Experience Platform.


>[!NOTE]
>
>Liknande självstudiekurser för migrering finns för:
>
> * [Adobe Analytics](../tutorial-migrate-analytics-websdk/migration-to-websdk-overview.md)
> * [Adobe Audience Manager](https://experienceleague.adobe.com/sv/docs/audience-manager/user-guide/migrate-to-web-sdk/appmeasurement-to-web-sdk)

>[!CAUTION]
>
> Eftersom Platform Web SDK stöder flera Adobe-program bör alla Adobe-bibliotek på en viss sida migreras samtidigt. En blandad implementering av Web SDK for Target och AppMeasurement for Analytics på en enskild sida _stöds till exempel inte_. Det finns dock stöd för en blandad implementering på olika sidor, till exempel Web SDK på sida A och at.js med AppMeasurementet på sida B.



## Viktiga fördelar

Några av fördelarna med Platform Web SDK jämfört med det fristående at.js-biblioteket är:

* Snabbare delning av målgrupper från [Real-time Customer Data Platform](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html)
* Integrera Target med Journey Optimizer för att stödja [leverans av Offer decisioning](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html)
* Möjlighet att använda [ID:n för första part](https://experienceleague.adobe.com/docs/platform-learn/data-collection/edge-network/generate-first-party-device-ids.html) för att generera ECID:t för besöksidentifiering med längre varaktighet
* Mindre utrymme för bättre sidhastighetsmätningar
* Ytterligare implementeringsflexibilitet för utvecklare

Den största fördelen för Target-kunder med migrering är förmodligen integrering med Real-time Customer Data Platform. Real-Time CDP erbjuder enastående målgruppsfunktioner baserat på alla data som inhämtas till Experience Platform och dess kapacitet för kundprofiler i realtid. Ett inbyggt ramverk för datastyrning automatiserar ansvarsfull användning av dessa data. Med Customer AI kan ni enkelt använda maskininlärningsmodeller för att konstruera benägenhets- och bortfallsmodeller vars utdata kan delas tillbaka till Adobe Target. Slutligen kan kunder som har tillvalet Healthcare and Privacy &amp; Security Shield använda funktionen för medgivande för att enkelt tillämpa individuella kunders samtycke. Platform Web SDK är ett krav för att använda dessa Real-Time CDP-funktioner i din webbkanal.

## Utbildningsmål

I slutet av den här självstudiekursen kan du:

* Förstå skillnaderna mellan at.js och Platform Web SDK vid implementering av Target
* Konfigurera den inledande konfigurationen för Target-funktionen
* Uppgradera at.js-biblioteket till Platform Web SDK
* Skapa formulärbaserade och visuella upplevelsedispositioner
* Skicka parametrar till Target
* Spåra konverteringshändelser
* Aktivera stöd för flera domäner
* Uppdatera målgrupper och profilskript
* Validera implementeringen
* Debug Target experience delivery


## Förhandskrav

För att slutföra den här självstudiekursen bör du först:

* Ha en teknisk förståelse för er nuvarande implementering av Target at.js
* Se till att du har en [redigerare- eller utgivarroll](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html#section_8C425E43E5DD4111BBFC734A2B7ABC80) för din Target-instans så att du kan testa exempel själv
* Lär dig hur du ställer in aktiviteter i Adobe Target. Om du behöver en uppdaterare kan du använda följande självstudiekurser och guider för den här lektionen:
   * [Använd Visual Experience Composer](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-visual-experience-composer.html)
   * [Använd den formulärbaserade Experience Composer](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-form-based-experience-composer.html)
   * [Skapa aktiviteter för målinriktning av upplevelser](https://experienceleague.adobe.com/docs/target-learn/tutorials/activities/create-experience-targeting-activities.html)

När du är klar är det första steget mot en lyckad migrering att [lära dig mer om migreringsprocessen](migration-overview.md) och hur at.js och Platform Web SDK skiljer sig åt.

>[!NOTE]
>
>Vi vill hjälpa dig att lyckas med din Target-migrering från at.js till Web SDK. Om du stöter på problem med din migrering eller om du känner att det saknas viktig information i den här guiden kan du meddela oss genom att publicera [den här communitydiskussionen](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
