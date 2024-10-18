---
title: Jämförelse mellan måltillägget och beslutets förlängning
description: Läs om skillnaderna mellan at.js 2.x och Platform Web SDK, inklusive funktioner, inställningar och dataflöde.
source-git-commit: afbc8248ad81a5d9080a4fdba1167e09bbf3b33d
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---

# Jämförelse mellan måltillägget och beslutets förlängning

Det fristående Adobe Target at.js-biblioteket skiljer sig avsevärt från Platform Web SDK. Följande tabeller är en referens som hjälper dig att utvärdera områden av implementeringen som du kan behöva fokusera på under migreringsprocessen.

När du har granskat informationen nedan och utvärderat din nuvarande tekniska at.js-implementering bör du förstå följande:

- Vilka målfunktioner som stöds av Platform Web SDK
- Funktionerna at at.js har motsvarigheter för Platform Web SDK
- Hur målinställningarna tillämpas med Platform Web SDK
- Hur dataflödet för at.js och Platform Web SDK skiljer sig åt

Om du inte har använt Platform Web SDK tidigare behöver du inte bekymra dig. Objekten nedan beskrivs mer ingående i den här självstudiekursen.

## Jämförelse av funktioner

| | Måltillägg | Beslutstillägg (mål via Edge) | AJO Code-based Experiences (Messaging SDK) |
|---|---|---|---|
| Förhämtningsläge | Stöds | Stöds | Stöds |
| Körningsläge | Stöds | Stöds inte | Stöds inte |
| Egna parametrar | Stöds | Parametrar per ruta stöds inte | Stöds inte |
| Deltagande målgrupper | Stöds | Stöds | Stöds via Campaigns målgrupp och experimentets utelämnandeinställning |
| Målgruppssegmentering med mobil Lifecycle-statistik | Stöds | Stöds via datainsamlingsregler | Upplevelseanpassning stöds för närvarande inte |
| thirdPartyId (mbox3rdPartyId) | Stöds via konfiguration av identitetskarta och namnutrymme i datastream | Stöds inte |
| Meddelanden (visa, klicka) | Stöds | Stöds | Stöds |
| Svarstoken | Stöds | Stöds | Ingen motsvarighet för att returnera Campaign-specifika metadata utanför innehållet |
| Dynamiska erbjudanden | Stöds | Stöds | Profil- och beslutsartikelrelaterad tokenåtergivning i innehåll stöds |
| Analyser för mål (A4T) | Endast på klientsidan | Klientsida och serversida | Stöds inte |
| Förhandsvisning av mobiler (QA-läge) | Stöds | Begränsad support | Pågår |



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

Följande diagram bör hjälpa dig att förstå skillnaderna i dataflöde mellan en Target-implementering med at.js och en implementering med hjälp av Platform Web SDK.

### Diagram över måltilläggssystem



### Avgör tilläggssystemsdiagram




>[!NOTE]
>
>Vi strävar efter att hjälpa dig att lyckas med din migrering av mobilmål från måltillägget till beslutstillägget. Om du stöter på problem med din migrering eller om du känner att det saknas viktig information i den här guiden kan du meddela oss genom att publicera [den här communitydiskussionen](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
