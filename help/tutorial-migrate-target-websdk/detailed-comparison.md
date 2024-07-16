---
title: Jämförelse mellan at.js 2.x och Web SDK | Migrera mål från at.js 2.x till Web SDK
description: Läs om skillnaderna mellan at.js 2.x och Platform Web SDK, inklusive funktioner, inställningar och dataflöde.
exl-id: b6f0ac2b-0d8e-46ce-8e9f-7bbc61eb20ec
source-git-commit: 299b9586fb5c8e9c9ef3427e08035806af1d9a6b
workflow-type: tm+mt
source-wordcount: '2007'
ht-degree: 1%

---

# Jämförelse mellan at.js och Platform Web SDK

Det fristående Adobe Target at.js-biblioteket skiljer sig avsevärt från Platform Web SDK. Följande tabeller är en referens som hjälper dig att utvärdera områden av implementeringen som du kan behöva fokusera på under migreringsprocessen.

När du har granskat informationen nedan och utvärderat din nuvarande tekniska at.js-implementering bör du förstå följande:

- Vilka målfunktioner som stöds av Platform Web SDK
- Funktionerna at at.js har motsvarigheter för Platform Web SDK
- Hur målinställningarna tillämpas med Platform Web SDK
- Hur dataflödet för at.js och Platform Web SDK skiljer sig åt

Om du inte har använt Platform Web SDK tidigare behöver du inte bekymra dig. Objekten nedan beskrivs mer ingående i den här självstudiekursen.

## Jämförelse av funktioner

| | Mål at.js 2.x | Platform Web SDK |
|---|---|---|
| Uppdatera målprofil | Stöds | Stöds |
| Utlösarvy för SPA | Stöds | Stöds |
| Recommendations | Stöds | Stöds |
| Hämta blankettbaserade erbjudanden | Stöds | Stöds |
| Spåra händelser | Stöds | Stöds |
| A4T: Single page application | Stöds | Stöds |
| A4T: Klickspårning | Stöds | Stöds |
| A4T: Loggning på klientsidan | Stöds | Stöds |
| A4T: Loggning på serversidan | Stöds | Stöds |
| Tillämpa erbjudanden | Stöds | Stöds |
| Återge vyn i SPA utan meddelanden | Stöds | Stöds |
| Hybridtillämpningar | Stöds | Stöds |
| QA-URL:er | Stöds | Stöds |
| Mbox-ID för tredje part | Stöds | Stöds |
| Kundattribut | Stöds | Stöds |
| Fjärrerbjudanden | Stöds | Stöds |
| Omdirigeringserbjudanden | Stöds | Stöds. Omdirigering från en sida med Platform Web SDK till en sida med at.js (och i motsatt riktning) stöds emellertid inte. |
| Beslut på enheten | Stöds | Stöds inte för närvarande |
| Förhämta kartonger | Stöds för anpassade omfattningar och SPA VEC | Förhämtning är standardläge för Web SDK |
| Anpassade händelser | Stöds | Stöds inte. Aktuell status finns i den [offentliga färdplanen](https://github.com/orgs/adobe/projects/18/views/1?pane=item&amp;itemId=17372355{target="_blank"}). |
| Svarstoken | Stöds | Stöds. Se [dokumentationen för dedikerade svarstoken](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html) för kodexempel och skillnader mellan at.js och Platform Web SDK |
| Dataleverantörer | Stöds | Stöds inte. Anpassad kod kan användas för att utlösa ett Platform Web SDK `sendEvent`-kommando när data har hämtats från en annan provider. |


## Anteckningsbara bildtexter

| | Mål at.js 2.x | Platform Web SDK |
|---|---|---|
| Flimmerreducering | I det föregående dolda fragmentet för asynkrona implementeringar används ett format-ID på `at-body-style`. at.js söker efter detta element-ID för att ta bort formatet när ett svar tas emot. | Standardfragmentet för fördöljning använder ett format-ID på `alloy-prehiding`. Web SDK är inte kompatibelt med fragmentet at.js så det måste ändras under migreringsprocessen. |
| Återge innehåll automatiskt vid sidinläsning | Kontrolleras med en global målinställning. Aktiveras när `pageLoadEnabled` är inställd på `true`. | Anges i Platform Web SDK `sendEvent`-kommandot. Aktiveras genom att alternativet `renderDecisions` anges till `true`. |
| Återge innehåll manuellt | Funktionerna `applyOffer()` och `applyOffers()` har endast stöd för inställningen HTML | Kommandot `applyPropositions` stöder inställning, ersättning eller tillägg av HTML för ökad flexibilitet |
| Spåra anpassade händelser | Stöds med funktionerna `trackEvent()` och `sendNotifications()`. Dessa funktioner är specifika för Target och påverkar inte Adobe Analytics-statistik. | Alla data från plattformens Web SDK `sendEvent`-anrop vidarebefordras till Target. Ytterligare data som behövs specifikt för Target ska inkluderas med kommandot `sendEvent` med händelsetypen `decisioning.propositionDisplay` eller `decisioning.propositionInteract` för att säkerställa att Adobe Analytics-mått inte påverkas. |
| Mål-CNAME | Stöds. Detta skiljer sig från CNAME som används för Analytics och Experience Cloud ID Service. | Inte längre relevant. En enda CNAME kan användas för alla Platform Web SDK-anrop. |
| Felsökning | URL-parametrarna `mboxDisable`, `mboxDebug` och `mboxTrace` kan användas för felsökning med webbläsarens utvecklingsverktyg.<br><br>Adobe Experience Platform Debugger är också ett felsökningsverktyg som stöds. | URL-parametrarna `mboxDisable`, `mboxDebug` och `mboxTrace` stöds inte.<br><br>Du kan aktivera Web SDK-felsökning genom att lägga till `alloy_debug=true` i frågesträngen eller köra `alloy("setDebug", { "enabled": true });` i utvecklarkonsolen.<br><br>Webbläsartillägget Adobe Experience Platform Debugger kan användas för att initiera en kantspårning för felsökning.<br><br>Mer information finns i [felsökningsdokumentationen för Platform Web SDK](debugging.md). |
| Analyser för mål (A4T) | Använder SDID-värden för sammanfogning av mål- och analysanrop | Inbyggt stöd utan behov av sys |

>[!NOTE]
>
>Det finns inte stöd för att migrera Target till Platform Web SDK med bevarad Adobe Analytics-implementering för ett visst AppMeasurement.
>
> Det går att migrera din at.js-implementering (och AppMeasurement.js) till Platform Web SDK en sida i taget. Om du väljer det här sättet är det bäst att ange alternativen [`idMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#id-migration-enabled) och [`targetMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#targetMigrationEnabled) till `true` med kommandot `configure`.

## at.js-funktioner och motsvarigheter till Platform Web SDK

Många at.js-funktioner har en likvärdig metod med Platform Web SDK som beskrivs i tabellen nedan. Mer information om funktionerna [ at.js](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/atjs-functions/) finns i Adobe Target Developer Guide.

| funktionen at.js 2.x | SDK-motsvarighet för plattform |
| --- | --- | 
| `getOffer()` och `getOffers()` | Om du vill begära och [automatiskt återge](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#automatically-rendering-content) VEC-baserade målupplevelser använder du kommandot `sendEvent` och anger alternativet `renderDecisions` till true.<br><br>Om du vill begära formulärbaserade upplevelser eller [återge](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#manually-rendering-content) innehåll manuellt anger du en array med `decisionScopes` (rutor) med kommandot `sendEvent`. |
| `applyOffer()` och `applyOffers()` | Använd kommandot [`applyPropositions`](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#applypropositions) för att tillämpa innehåll. Du kan välja att ställa in, ersätta eller lägga till HTML i en viss väljare. |
| `triggerView()` | Platform Web SDK utlöser automatiskt en [visningsändring](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/web-sdk-atjs-comparison.html#how-to-trigger-a-view-change-in-a-single-page-application) för SPA VEC om egenskapen `web.webPageDetails.viewName` anges under alternativet `xdm` för kommandot `sendEvent` . |
| `trackEvent()` och `sendNotifications()` | Använd kommandot `sendEvent` med en [specifik `eventType`](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/web-sdk-atjs-comparison.html#how-to-track-events) uppsättning:<br><br>`decisioning.propositionDisplay` signalerar återgivningen av en aktivitet <br><br>`decisioning.propositionInteract` som signalerar en användarinteraktion med en aktivitet, till exempel ett musklick. |
| `targetGlobalSettings()` | Ingen direkt motsvarighet. Mer information finns i [målinställningsjämförelsen](detailed-comparison.md). |
| `targetPageParams()` och `targetPageParamsAll()` | Alla data som skickas i alternativet `xdm` för kommandot `sendEvent` mappas till Target-parametrar för mbox. Eftersom mbox-parametrar namnges med serialiserad punktnotation kan du behöva uppdatera befintliga målgrupper och aktiviteter för att kunna använda de nya mbox-parameternamnen när du migrerar till Platform Web SDK. <br><br>Data som skickas som en del av `data.__adobe.target` av kommandot `sendEvent` mappas till [Målprofil och Recommendations-specifika parametrar](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/target-overview.html#single-profile-update). |
| at.js, anpassade händelser | Stöds inte. Aktuell status finns i den [offentliga färdplanen](https://github.com/orgs/adobe/projects/18/views/1?pane=item&amp;itemId=17372355{target="_blank"}). [Svarstoken](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/accessing-response-tokens.html) visas som en del av `propositions` i svaret från anropet `sendEvent`. |

## at.js-inställningar och motsvarigheter till Platform Web SDK

At.js-biblioteket kan konfigureras och laddas ned med olika inställningar i målgränssnittet. Dessa inställningar kan även uppdateras med funktionen [`targetGlobalSettings()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/targetglobalsettings/). I tabellen nedan jämförs dessa inställningar med de som är tillgängliga med Platform Web SDK.

| at.js, inställning | SDK-motsvarighet för plattform |
| --- | --- |
| `bodyHiddenStyle` | Ange [`prehidingStyle`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#prehidingStyle) med kommandot `configure` |
| `bodyHidingEnabled` | Om `prehidingStyle` definieras med kommandot `configure` aktiveras den här funktionen. Om inget format definieras försöker inte Platform Web SDK att dölja något innehåll. |
| `clientCode` | Automatiskt konfigurerad |
| `cookieDomain` | Ej tillämpligt |
| `crossDomain` | Ange alternativet `thirdPartyCookiesEnabled` till `true` med kommandot `configure` för att aktivera cookies från första och tredje part för korsdomänsanvändning |
| `cspScriptNonce` och `cspStyleNonce` | Läs dokumentationen om hur du konfigurerar en CSP](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-a-csp.html) i [konfigurationen. |
| `dataProviders` | Stöds inte |
| `decisioningMethod` | Alla Platform Web SDK `sendEvent`-kommandon använder beslut på serversidan. Hybrid- och enhetsbeslut stöds inte. |
| `defaultContentHiddenStyle` och `defaultContentVisibleStyle` | Gäller endast med at.js 1.x. Precis som i at.js 2.x kan du använda anpassad kod för att reducera eventuella flimmer för formulärbaserade upplevelser. |
| `deviceIdLifetime` | Stöds inte. Om `targetMigrationEnabled` är inställt på `true` med kommandot `configure` ställs cookien `mbox` in med enhetens livstid inställd på 2 år. Detta värde kan inte konfigureras. |
| `enabled` | Målfunktionen är aktiverad eller inaktiverad med dataströmskonfigurationen |
| `globalMboxAutoCreate` | Ange alternativet `renderDecisions` till `true` med kommandot `sendEvent` för att automatiskt hämta och återge VEC-baserade upplevelser.<br><br>Begär en `decisionScope` för `__view__` om du föredrar att manuellt återge VEC-baserade upplevelser. |
| `imsOrgId` | Ange `orgId` med kommandot `configure` |
| `optinEnabled` och `optoutEnabled` | Se [sekretessalternativen](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html) för Platform Web SDK. Alternativet `defaultConsent` gäller för alla Adobe-lösningar som Platform Web SDK stöder. |
| `overrideMboxEdgeServer` och `overrideMboxEdgeServerTimeout` | Ej tillämpligt. Alla SDK-begäranden för plattformar använder Adobe Experience Platform Edge-nätverket. |
| `pageLoadEnabled` | Ange alternativet `renderDecisions` till `true` med kommandot `sendEvent` |
| `secureOnly` | Stöds inte. Platform Web SDK anger alla cookies med attributen `secure` och `sameSite="none"`. |
| `selectorsPollingTimeout` | Stöds inte. Värdet 5 sekunder används för Platform Web SDK. Anpassad kod kan användas för att manuellt återge innehåll om det behövs. |
| `serverDomain` | Använd inställningen `edgeDomain` med kommandot `configure` |
| `telemetryEnabled` | Ej tillämpligt |
| `timeout` | Stöds inte. Vi rekommenderar att du ser till att en lämplig tidsgräns anges för all kod som reducerar flimret. |
| `viewsEnabled` | Stöds inte. Innehåll för målvyer hämtas alltid vid det första `sendEvent()`-anropet om `renderDecisions` är inställt på `true` eller om `__view__` DecisionScope är inkluderat i begäran. |
| `visitorApiTimeout` | Ej tillämpligt |


## Systemdiagramsjämförelse

Följande diagram bör hjälpa dig att förstå skillnaderna i dataflöde mellan en Target-implementering med at.js och en implementering med hjälp av Platform Web SDK.

### at.js 2.x systemdiagram

Beteendet ![at.js 2.0 vid sidinläsning](assets/target-at-js-2x-diagram.png){zoomable="yes"}

| Utlysning | Information |
| --- | --- |
| 1 | Anropet returnerar Experience Cloud-ID (ECID). Om användaren är autentiserad synkroniseras kundens ID med ett annat samtal. |
| 2 | at.js-biblioteket läses in synkront och döljer dokumentets brödtext (at.js kan också läsas in asynkront med ett valfritt predhide-fragment implementerat på sidan). |
| 3 | Begäran om sidinläsning omfattar alla konfigurerade parametrar, ECID, SDID och kund-ID. |
| 4 | Profilskript körs och matas in i profilarkivet. Store begär kvalificerade målgrupper från målgruppsbiblioteket (till exempel målgrupper som delas från Analytics, Audience Manager och så vidare). Kundattribut skickas till profilarkivet i en gruppbearbetning. |
| 5 | Baserat på URL, begärandeparametrar och profildata avgör Target vilka aktiviteter och upplevelser som ska returneras till besökaren för den aktuella sidan och framtida vyer. |
| 6 | Målinriktat innehåll som skickas tillbaka till sidan, eventuellt med profilvärden för ytterligare personalisering.<br><br>Målinnehåll på den aktuella sidan visas så snabbt som möjligt utan att standardinnehållet flimrar.<br><br>Målanpassat innehåll för framtida vyer av ett enkelsidigt program cachelagras i webbläsaren, så att det kan tillämpas direkt utan ett extra serveranrop när vyerna aktiveras. |
| 7 | Analysdata som skickas från sidan till datainsamlingsservrarna. |
| 8 | Måldata matchas mot Analytics-data via SDID och bearbetas till lagringsplatsen för analysrapporter. Analysdata kan sedan visas både i Analytics och Target via A4T-rapporter. |

Mer information om hur du [implementerar Target med at.js för enkelsidiga program](https://developer.adobe.com/target/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application/) finns i utvecklarhandboken.

### Systemdiagram för Platform Web SDK

![Diagram över Adobe Target edge-beslut med Platform Web SDK](assets/target-platform-web-sdk.png)

| Utlysning | Information |
| --- | --- |
| 1 | Enheten läser in Platform Web SDK. Platform Web SDK skickar en begäran till edge-nätverket med XDM-data, DataStreams Environment ID, inskickade parametrar och kundens ID (valfritt). Sidan (eller behållarna) är fördold. |
| 2 | edge-nätverket skickar begäran till edge-tjänsterna för att berika den med besökar-ID, samtycke och annan kontextinformation för besökare, som geopositionering och enhetsvänliga namn. |
| 3 | Edge-nätverket skickar den berikade personaliseringsbegäran till Target-kanten med besökar-ID och skickade parametrar. |
| 4 | Profilskript körs och matas sedan in i målprofilens lagring. Profillagring hämtar segment från målgruppsbiblioteket (till exempel segment som delas från Adobe Analytics, Adobe Audience Manager, Adobe Experience Platform). |
| 5 | Baserat på parametrar för URL-begäran och profildata avgör Target vilka aktiviteter och upplevelser som ska visas för besökaren för den aktuella sidvyn och för framtida förhämtade vyer. Target skickar sedan tillbaka den här till gränsnätverket. |
| 6 | a. Edge-nätverket skickar personaliseringssvaret tillbaka till sidan, eventuellt inklusive profilvärden för ytterligare personalisering. Personaliserat innehåll på den aktuella sidan visas så snabbt som möjligt utan att man behöver flimra standardinnehållet.<br><br>b. Personaliserat innehåll för vyer som visas som ett resultat av användaråtgärder i ett Single Page-program (SPA) cachas för direktåtergivning utan ytterligare serveranrop.<br><br>c. Edge-nätverket skickar besökar-ID och andra värden i cookies (till exempel samtycke, sessions-ID, identitet, cookie-kontroll, personalisering och så vidare). |
| 7 | Edge Network Forwards Analytics for Target (A4T)-information (aktivitet, upplevelse och konverteringsmetadata) till Analytics-kanten. |

Mer information om hur du [implementerar Target med Platform Web SDK för enkelsidiga program finns i utvecklarhandboken ](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/spa-implementation.html).

När du har en god teknisk förståelse för den aktuella målinstallationen och de funktioner du använder är nästa steg att utföra den [inledande konfigurationen](initial-setup.md).

>[!NOTE]
>
>Vi vill hjälpa dig att lyckas med målmigreringen från at.js till Web SDK. Om du stöter på problem med din migrering eller om du känner att det saknas viktig information i den här guiden kan du meddela oss genom att publicera [den här communitydiskussionen](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
