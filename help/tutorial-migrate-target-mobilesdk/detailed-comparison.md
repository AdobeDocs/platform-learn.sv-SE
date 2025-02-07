---
title: Jämförelse mellan måltillägget och beslutets förlängning
description: Lär dig mer om skillnaderna mellan Target-tillägg till beslutstillägget, inklusive funktioner, funktioner, inställningar och dataflöde.
exl-id: 6c854049-4126-45cf-8b2b-683cf29549f3
source-git-commit: cb08ad8a1ffd687d7748ca02643b11b2243cd1a7
workflow-type: tm+mt
source-wordcount: '1329'
ht-degree: 0%

---

# Jämförelse mellan måltillägget och beslutets förlängning

Tillägget Adobe Journey Optimizer - Decisioning skiljer sig från Adobe Target-tillägget för mobilappar. Följande tabeller är en referens som hjälper dig att utvärdera områden av implementeringen som du kan behöva fokusera på under migreringsprocessen.

När du har granskat informationen nedan och utvärderat din nuvarande implementering av det tekniska måltillägget bör du förstå följande:

- Vilka Target-funktioner som stöds av Adobe Journey Optimizer - Decisioning
- Vilka Adobe Target-tilläggsfunktioner som har Adobe Journey Optimizer - Beslutsmotsvarigheter
- Hur målinställningar används med Adobe Journey Optimizer - beslut
- Hur data flödar med Adobe Journey Optimizer - Beslutstillägg

## Operativa skillnader

| | Måltillägg | Beslutstillägg |
|---|---|---|
| Process | Ändringar i en Target-implementering kan följa en process som har en annan inriktning eller QA-krav än andra program som Analytics. | Ändringar av en implementering av ett beslutstillägg bör omfatta alla program i senare led och QA- och publiceringsprocessen bör anpassas i enlighet med detta. |
| Collaboration | Data som är specifika för Target kan skickas direkt i Target-anropen. Om rapportkällan för Target är Adobe Analytics (A4T) kan data som är specifika för Target också skickas till Adobe Analytics när lämpliga spårningsmetoder i tillägget Target anropas för visning av målinnehåll och interaktion. | Data som skickas i anrop till beslutstillägg kan vidarebefordras till både Target och Analytics om Target-rapportkällan är Adobe Analytics (A4T), Adobe Analytics är aktiverat i dataströmmen och lämpliga spårningsmetoder i beslutningstillägget anropas när Target-innehåll visas och interagerar med det. |

## Grundläggande skillnader

| | Måltillägg | Beslutstillägg |
|---|---|---|
| Beroenden | Endast SDK med Mobile Core | Använder Mobile Core och Edge Network SDK |
| Biblioteksfunktioner | Stöder endast hämtning av innehåll från Adobe Target | Stöd för hämtning av innehåll från Adobe Target och Offer decisioning |
| Begäranden | Målsamtal är i stort sett oberoende av andra nätverksanrop | Målnätverksanrop köas tillsammans med nätverksanrop för andra Edge-baserade lösningar som Messaging i Edge SDK och utförs seriellt. |
| Edge Network | Använder målservervärdet eller Adobe Experience Cloud Edge Network med klientkoden (clientcode.tt.omtrdc.net), som båda anges i [målkonfigurationen](https://developer.adobe.com/client-sdks/solution/adobe-target/#configure-the-target-extension-in-the-data-collection-ui) i användargränssnittet för datainsamling | Använder den Edge-nätverksdomän som anges i Adobe Experience Platform [Edge Network-konfiguration](https://developer.adobe.com/client-sdks/edge/edge-network/#configure-the-edge-network-extension-in-data-collection-ui) i användargränssnittet för datainsamling. |
| Grundläggande terminologi | mbox, TargetParameters | DecisionScope, Map (Android)/Dictionary (iOS) för Target-parametrar |
| Standardinnehåll | Tillåter att klientsidans standardinnehåll skickas i TargetRequest, som returneras om nätverksanropet misslyckas eller resulterar i fel. | Det går inte att skicka standardinnehåll på klientsidan. Returnerar inte något innehåll om nätverksanropet misslyckas eller resulterar i fel. |
| Målparametrar | Tillåter att globala TargetParameters skickas per begäran och olika TargetParameters per mbox | Tillåter att globala TargetParameters skickas endast per begäran |



## Jämförelse av funktioner

| Funktion | Måltillägg | Beslutstillägg (mål via Edge) |
|---|---|---|
| Förhämtningsläge | Stöds | Stöds |
| Körningsläge | Stöds | Stöds inte |
| Egna parametrar | Stöds | Stöds* |
| Profilparametrar | Stöds | Stöds* |
| Enhetsparametrar | Stöds | Stöds* |
| Målgrupper | Stöds | Stöds |
| Real-Time CDP målgrupper | Stöds inte | Stöds |
| Real-Time CDP-attribut | Stöds inte | Stöds |
| Livscykelstatistik | Stöds | Stöds via datainsamlingsregler |
| thirdPartyId (mbox3rdPartyId) | Stöds | Stöds via Identity Map och Target Third Party ID Namespace i datastream |
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
>Ha konfigurationen och inställningarna för måltilläggets taggar på plats även efter att du har migrerat programkoden till beslutstillägget. Detta gör att Target fortsätter att fungera för kunder som ännu inte har uppdaterat appen till den nya versionen.
>
>Om du använder Analytics for Target-integrering (A4T) måste du också migrera din Analytics-implementering med Edge Bridge-tillägget samtidigt som du migrerar din Target-implementering till beslutstillägget.

## Tilläggsfunktioner för mål och beslutets tilläggsekvivalenter

Många Target-tilläggsfunktioner har en likvärdig metod med hjälp av det beslutstillägg som beskrivs i tabellen nedan. Mer information om [funktionerna](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/atjs-functions/) finns i Adobe Target Developer Guide.

| Måltillägg | Beslutstillägg | Anteckningar |
| --- | --- | --- | 
| `prefetchContent` | `updatePropositions` |  |
| `retrieveLocationContent` | `getPropositions` | När du använder `getPropositions` API görs inget fjärranrop för att hämta icke-cachelagrade scope i SDK. |
| `displayedLocations` | Erbjudande -> `displayed()` | Dessutom kan erbjudandemetoden `generateDisplayInteractionXdm` användas för att generera XDM för objektvisning. Därefter kan Edge-nätverkets SDK-API för sendEvent användas för att bifoga ytterligare XDM-data, frihandsdata och skicka en Experience Event till fjärrservern. |
| `clickedLocation` | Erbjudande -> `tapped()` | Dessutom kan erbjudandemetoden `generateTapInteractionXdm` användas för att generera XDM för artikelknackning. Därefter kan Edge-nätverkets SDK-API för sendEvent användas för att bifoga ytterligare XDM-data, frihandsdata och skicka en Experience Event till fjärrservern. |
| `clearPrefetchCache` | `clearCachedPropositions` |  |
| `resetExperience` | n/a | Använd `removeIdentity`-API:t från Identity for Edge Network-tillägget för SDK för att sluta skicka besöksidentifieraren till Edge-nätverket. Mer information finns i [dokumentationen för API:t removeIdentity](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/api-reference/#removeidentity). <br><br>Obs! Mobile Core `resetIdentities`-API:t rensar alla lagrade identiteter i SDK, inklusive Experience Cloud ID (ECID), och det bör användas sparsamt! |
| `getSessionId` | n/a | `state:store`-svarsreferensen innehåller sessionsrelaterad information. Edge-nätverkstillägg hjälper till att hantera det genom att koppla tillståndslagringsobjekt som inte har förfallit till efterföljande begäranden. |
| `setSessionId` | n/a | `state:store`-svarsreferensen innehåller sessionsrelaterad information. Edge-nätverkstillägg hjälper till att hantera det genom att koppla tillståndslagringsobjekt som inte har förfallit till efterföljande begäranden. |
| `getThirdPartyId` | n/a | Använd API:t updateIdentities från Identity för tillägget Edge Network för att ange ID-värdet för tredje part. Konfigurera sedan namnutrymmet för det tredje parts-ID:t i datastream. Mer information finns i [Målets mobildokumentation för tredjeparts-ID](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#target-third-party-id). |
| `setThirdPartyId` | n/a | Använd API:t updateIdentities från Identity för tillägget Edge Network för att ange ID-värdet för tredje part. Konfigurera sedan namnutrymmet för det tredje parts-ID:t i datastream. Mer information finns i [Målets mobildokumentation för tredjeparts-ID](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#target-third-party-id). |
| `getTntId` | n/a | Svarshandtaget `locationHint:result` innehåller information om målplatstips. Det antas att Target-kanten kommer att samlokaliseras med Experience Edge. <br> <br>Edge-nätverkstillägget använder platsledtråden för EdgeNetwork för att avgöra vilket Edge-nätverkskluster som begäranden ska skickas till. Använd API:erna `getLocationHint` och `setLocationHint` från tillägget Edge Network om du vill dela Edge-nätverksplatstips mellan SDK:er (hybridappar). Mer information finns i [API-dokumentationen för `getLocationHint`](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#getlocationhint). |
| `setTntId` | n/a | Svarshandtaget `locationHint:result` innehåller information om målplatstips. Det antas att Target-kanten kommer att samlokaliseras med Experience Edge. <br> <br>Edge-nätverkstillägget använder platsledtråden för EdgeNetwork för att avgöra vilket Edge-nätverkskluster som begäranden ska skickas till. Använd API:erna `getLocationHint` och `setLocationHint` från tillägget Edge Network om du vill dela Edge-nätverksplatstips mellan SDK:er (hybridappar). Mer information finns i [API-dokumentationen för `getLocationHint`](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#getlocationhint). |

## Målinställningar för tillägg och Avgörande av tilläggsekvivalenter

Måltillägget har [konfigurerbara inställningar](https://developer.adobe.com/client-sdks/solution/adobe-target/#configure-the-target-extension-in-the-data-collection-ui) som är [ konfigurerade i datastream](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#adobe-experience-platform-data-collection-setup) med beslutstillägget.

| Måltillägg | Beslutstillägg | Anteckningar |
| --- | --- | --- | 
| Klientkod | n/a | Ange automatiskt efter kanten med hjälp av IMS-organisationsinformationen |
| Miljö-ID | Målmiljö-ID | Konfigurerad i datastream |
| Ange Workspace-egenskap | Egenskapstoken | Konfigurerad i datastream |
| Timeout | Kan inte konfigureras | Tidsgränsen för beslutandetillägget är 10 sekunder |
| Serverdomän | Edge Network domain | Ange i tillägget Adobe Experience Platform Edge Network |

>[!IMPORTANT]
>
> Låt inställningarna för måltillägget vara på plats även efter att du har migrerat programkoden till beslutstillägget. Detta gör att Target fortsätter att fungera för användare som ännu inte har uppdaterat sin app.

## Fastställer tilläggssystemsdiagram

Följande diagram bör hjälpa dig att förstå dataflödet med tillägget Adobe Journey Optimizer - Decisioning.

![Adobe Target Edge Decisioning with client-side Mobile SDK](assets/diagram.png)


>[!NOTE]
>
>Vi strävar efter att hjälpa dig att lyckas med din migrering av mobilmål från måltillägget till beslutstillägget. Om du stöter på problem med din migrering eller om du känner att det saknas viktig information i den här guiden kan du meddela oss genom att publicera [den här communitydiskussionen](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
