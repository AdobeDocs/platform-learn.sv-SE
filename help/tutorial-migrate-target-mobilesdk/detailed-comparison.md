---
title: Jämförelse mellan måltillägget och beslutets förlängning
description: Lär dig mer om skillnaderna mellan Target-tillägg till beslutstillägget, inklusive funktioner, funktioner, inställningar och dataflöde.
exl-id: 6c854049-4126-45cf-8b2b-683cf29549f3
source-git-commit: 05b0146256c6f8644e42f851498a0f49ff44bf68
workflow-type: tm+mt
source-wordcount: '829'
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
| Egna parametrar | Stöds | Stöds* |
| Profilparametrar | Stöds | Stöds* |
| Enhetsparametrar | Stöds | Stöds* |
| Målgrupper | Stöds | Stöds |
| Real-Time CDP målgrupper | ?? | Stöds |
| Real-Time CDP-attribut | ?? | Stöds |
| Livscykelstatistik | Stöds | Stöds via datainsamlingsregler |
| thirdPartyId (mbox3rdPartyId) | Stöds | Stöds via konfiguration av identitetskarta och namnutrymme i datastream |
| Meddelanden (visa, klicka) | Stöds | Stöds |
| Svarstoken | Stöds | Stöds |
| Analyser för mål (A4T) | Endast på klientsidan | Klientsida och serversida |
| Förhandsvisning av mobiler (QA-läge) | Stöds | Begränsad support med Assurance |

>[!IMPORTANT]
>
> \* Parametrar som skickas i en begäran gäller alla scope i begäran. Om du behöver ange olika parametrar för olika omfattningar måste du göra ytterligare förfrågningar.



## Anteckningsbara bildtexter

>[!NOTE]
>
>Det finns inte stöd för att migrera Target till Platform Web SDK med bevarad Adobe Analytics-implementering för ett visst AppMeasurement.
>
> Det går att migrera din at.js-implementering (och AppMeasurement.js) till Platform Web SDK en sida i taget. Om du väljer det här sättet är det bäst att ange alternativen [`idMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#id-migration-enabled) och [`targetMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#targetMigrationEnabled) till `true` med kommandot `configure`.

## Tilläggsfunktioner för mål och beslutets tilläggsekvivalenter

Många Target-tilläggsfunktioner har en likvärdig metod med hjälp av det beslutstillägg som beskrivs i tabellen nedan. Mer information om [funktionerna](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/atjs-functions/) finns i Adobe Target Developer Guide.

| Måltillägg | Beslutstillägg | Anteckningar |
| --- | --- | --- | 
| `prefetchContent` | `updatePropositions` |  |
| `retrieveLocationContent` | `getPropositions` | När du använder `getPropositions` API görs inget fjärranrop för att hämta icke-cachelagrade scope i SDK. |
| `displayedLocations` | Erbjudande -> `displayed()` | Dessutom kan erbjudandemetoden `generateDisplayInteractionXdm` användas för att generera XDM för objektvisning. Därefter kan Edge nätverks-SDK:s sendEvent-API användas för att bifoga ytterligare XDM-data, frihandsdata och skicka en Experience Event till fjärrservern. |
| `clickedLocation` | Erbjudande -> `tapped()` | Dessutom kan erbjudandemetoden `generateTapInteractionXdm` användas för att generera XDM för artikelknackning. Därefter kan Edge nätverks-SDK:s sendEvent-API användas för att bifoga ytterligare XDM-data, frihandsdata och skicka en Experience Event till fjärrservern. |
| `clearPrefetchCache` | `clearCachedPropositions` |  |
| `resetExperience` |  | Använd `removeIdentity`-API:t från Identity för Edge Network-tillägget för SDK för att sluta skicka besöksidentifieraren till Edge-nätverket. Mer information finns i [dokumentationen för API:t removeIdentity](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/api-reference/#removeidentity). <br><br>Obs! Mobile Core `resetIdentities` API tar bort alla lagrade identiteter i SDK, inklusive Experience Cloud ID (ECID), och det bör användas sparsamt! |
| `getSessionId` |  | `state:store`-svarsreferensen innehåller sessionsrelaterad information. Edge-nätverkstillägg hjälper till att hantera det genom att koppla tillståndslagringsobjekt som inte har förfallit till efterföljande begäranden. |
| `setSessionId` |  | `state:store`-svarsreferensen innehåller sessionsrelaterad information. Edge-nätverkstillägg hjälper till att hantera det genom att koppla tillståndslagringsobjekt som inte har förfallit till efterföljande begäranden. |
| `getThirdPartyId` | n/a | Använd API:t updateIdentities från Identity för tillägget Edge Network för att ange ID-värdet för tredje part. Konfigurera sedan namnutrymmet för det tredje parts-ID:t i datastream. Mer information finns i [Målets mobildokumentation för tredjeparts-ID](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#target-third-party-id). |
| `setThirdPartyId` | n/a | Använd API:t updateIdentities från Identity för tillägget Edge Network för att ange ID-värdet för tredje part. Konfigurera sedan namnutrymmet för det tredje parts-ID:t i datastream. Mer information finns i [Målets mobildokumentation för tredjeparts-ID](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#target-third-party-id). |
| `getTntId` |  | Svarshandtaget `locationHint:result` innehåller information om målplatstips. Det antas att Target-kanten kommer att samlokaliseras med Experience Edge. <br> <br>Edge-nätverkstillägget använder platsledtråden för EdgeNetwork för att avgöra vilket Edge-nätverkskluster som begäranden ska skickas till. Använd API:erna `getLocationHint` och `setLocationHint` från tillägget Edge Network om du vill dela Edge-nätverksplatstips mellan SDK:er (hybridappar). Mer information finns i [API-dokumentationen för `getLocationHint`](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#getlocationhint). |
| `setTntId` |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |

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
