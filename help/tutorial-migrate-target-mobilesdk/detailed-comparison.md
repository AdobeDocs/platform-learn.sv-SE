---
title: Jämförelse mellan måltillägget och beslutets förlängning
description: Lär dig mer om skillnaderna mellan Target-tillägg till beslutstillägget, inklusive funktioner, funktioner, inställningar och dataflöde.
source-git-commit: 78d04d625aa55ce5eb76615c220b49aefd958431
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# Jämförelse mellan måltillägget och beslutets förlängning

Tillägget Adobe Journey Optimizer - Decisioning skiljer sig från Adobe Target-tillägget för mobilappar. Följande tabeller är en referens som hjälper dig att utvärdera områden av implementeringen som du kan behöva fokusera på under migreringsprocessen.

När du har granskat informationen nedan och utvärderat din nuvarande implementering av det tekniska måltillägget bör du förstå följande:

- Vilka Target-funktioner som stöds av Adobe Journey Optimizer - Decisioning
- Vilka Adobe Target-tilläggsfunktioner som har Adobe Journey Optimizer - Beslutsmotsvarigheter
- Hur målinställningar används med Adobe Journey Optimizer - beslut
- Hur dataflödet för Adobe Target-tillägget och Adobe Journey Optimizer - Beslutstillägg skiljer sig åt

Om du inte har använt Platform Web SDK tidigare behöver du inte bekymra dig. Objekten nedan beskrivs mer ingående i den här självstudiekursen.

## Jämförelse av funktioner

| Funktion | Måltillägg | Beslutstillägg (mål via Edge) |
|---|---|---|
| Förhämtningsläge | Stöds | Stöds |
| Körningsläge | Stöds | Stöds inte |
| Egna parametrar | Stöds | Parametrar per ruta stöds inte |
| Deltagande målgrupper | Stöds | Stöds |
| Målgruppssegmentering med mobil Lifecycle-statistik | Stöds | Stöds via datainsamlingsregler |
| thirdPartyId (mbox3rdPartyId) | Stöds via konfiguration av identitetskarta och namnutrymme i datastream |
| Meddelanden (visa, klicka) | Stöds | Stöds |
| Svarstoken | Stöds | Stöds |
| Dynamiska erbjudanden | Stöds | Stöds |
| Analyser för mål (A4T) | Endast på klientsidan | Klientsida och serversida |
| Förhandsvisning av mobiler (QA-läge) | Stöds | Begränsad support |



## Anteckningsbara bildtexter

>[!NOTE]
>
>Det finns inte stöd för att migrera Target till Platform Web SDK med bevarad Adobe Analytics-implementering för ett visst AppMeasurement.
>
> Det går att migrera din at.js-implementering (och AppMeasurement.js) till Platform Web SDK en sida i taget. Om du väljer det här sättet är det bäst att ange alternativen [`idMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#id-migration-enabled) och [`targetMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#targetMigrationEnabled) till `true` med kommandot `configure`.

## Tilläggsfunktioner för mål och beslutets tilläggsekvivalenter

Många Target-tilläggsfunktioner har en likvärdig metod med hjälp av det beslutstillägg som beskrivs i tabellen nedan. Mer information om [funktionerna](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/atjs-functions/) finns i Adobe Target Developer Guide.

| Måltillägg | Beslutstillägg |
| --- | --- | 
| |  |

## Målinställningar för tillägg och Avgörande av tilläggsekvivalenter

Måltillägget kan konfigureras och laddas ned med olika inställningar i ...

| Måltillägg | Beslutstillägg |
| --- | --- | 
| |  |


## Systemdiagramsjämförelse

Följande diagram bör hjälpa dig att förstå skillnaderna i dataflöde mellan en Target-implementering med tillägget Adobe Journey Optimizer - Decisioning och en implementering med tillägget Adobe Target.

### Diagram över måltilläggssystem



### Fastställer tilläggssystemsdiagram




>[!NOTE]
>
>Vi strävar efter att hjälpa dig att lyckas med din migrering av mobilmål från måltillägget till beslutstillägget. Om du stöter på problem med din migrering eller om du känner att det saknas viktig information i den här guiden kan du meddela oss genom att publicera [den här communitydiskussionen](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
