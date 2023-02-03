---
title: Jämförelse mellan at.js 2.x och Web SDK | Migrera mål från at.js 2.x till Web SDK
description: Läs om skillnaderna mellan at.js 2.x och Platform Web SDK, inklusive funktioner, inställningar och dataflöde.
source-git-commit: 8209b13b745dbea418003b133a6834825947950e
workflow-type: tm+mt
source-wordcount: '2154'
ht-degree: 3%

---

# Jämförelse mellan at.js och Platform Web SDK

Det fristående Adobe Target at.js-biblioteket skiljer sig avsevärt från Platform Web SDK. Följande tabeller är en referens som hjälper dig att utvärdera områden av implementeringen som du kan behöva fokusera på under migreringsprocessen.

När du har granskat informationen nedan och utvärderat din nuvarande tekniska at.js-implementering bör du förstå följande:

- Vilka målfunktioner som stöds av Platform Web SDK
- Funktionerna at at.js har motsvarigheter för Platform Web SDK
- Hur målinställningar används med Platform Web SDK
- Hur dataflödet för at.js och Platform Web SDK skiljer sig åt

Om du inte har använt Platform Web SDK tidigare behöver du inte bekymra dig. Objekten nedan beskrivs mer ingående i den här självstudiekursen.

## Jämförelse av funktioner

|  | Mål at.js 2.x | Platform Web SDK |
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
| Förhämta kartor | Stöds | Aktiveras som standard i alla nya migreringar som påbörjas efter 1 oktober 2022 |
| Anpassade händelser | Stöds | Stöds inte. Se [allmän färdplan](https://github.com/orgs/adobe/projects/18/views/1?pane=item&amp;itemId=17372355{target="_blank"}) för aktuell status. |
| Svarstoken | Stöds | Stöds. Se [dokumentation för dedikerad svarstoken](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html) för kodexempel och skillnader mellan at.js och Platform Web SDK |
| Dataleverantörer | Stöds | Stöds inte. Anpassad kod kan användas för att utlösa en Platform Web SDK `sendEvent` efter att data har hämtats från en annan provider. |


## Anteckningsbara bildtexter

|  | Mål at.js 2.x | Platform Web SDK |
|---|---|---|
| Flimmerreducering | I det föregående dolda fragmentet för asynkrona implementeringar används ett format-ID på `at-body-style`. at.js söker efter detta element-ID för att ta bort formatet när ett svar tas emot. | Standardfragmentet för fördöljning använder ett format-ID på `alloy-prehiding`. Web SDK är inte kompatibelt med fragmentet at.js så det måste ändras som en del av migreringsprocessen. |
| Återge innehåll automatiskt vid sidinläsning | Kontrolleras med en global målinställning. Aktiverad när `pageLoadEnabled` är inställd på `true`. | Anges i Platform Web SDK `sendEvent` -kommando. Aktiverat genom att ställa in `renderDecisions` alternativ till `true`. |
| Återge innehåll manuellt | The `applyOffer()` och `applyOffers()` funktioner som endast stöder inställning HTML | The `applyPropositions` kan ange, ersätta och lägga till HTML för ökad flexibilitet |
| Spåra anpassade händelser | Stöds med `trackEvent()` och `sendNotifications()` funktioner. Dessa funktioner är specifika för Target och påverkar inte Adobe Analytics-statistik. | Alla data från Platform Web SDK `sendEvent` samtal vidarebefordras till Target. Ytterligare data som behövs specifikt för Target ska inkluderas i `sendEvent` kommando med eventType för `decisioning.propositionDisplay` eller `decisioning.propositionInteract` för att säkerställa att Adobe Analytics-statistik inte påverkas. |
| Mål-CNAME | Stöds. Detta skiljer sig från CNAME som används för Analytics och Experience Cloud ID Service. | Inte längre relevant. En enda CNAME kan användas för alla Platform Web SDK-anrop. |
| Felsökning | The `mboxDisable`, `mboxDebug`och `mboxTrace` URL-parametrar kan användas för felsökning med webbläsarens utvecklarverktyg.<br><br>Adobe Experience Platform Debugger är också ett felsökningsverktyg som stöds. | The `mboxDisable`, `mboxDebug`och `mboxTrace` URL-parametrar stöds inte.<br><br>Du kan aktivera Web SDK-felsökning genom att lägga till `alloy_debug=true` till frågesträngen eller köra `alloy("setDebug", { "enabled": true });` i utvecklarkonsolen.<br><br>Webbläsartillägget Adobe Experience Platform Debugger kan användas för att initiera en kantspårning för felsökning.<br><br>Se [felsöka Platform Web SDK](debugging.md) mer information. |
| Analyser för mål (A4T) | Använder SDID-värden för sammanfogning av Target- och Analytics-anrop | Inbyggt stöd utan behov av sammanfogning |

>[!NOTE]
>
>Det går inte att migrera Target till Platform Web SDK med bibehållen befintlig AppMeasurement Adobe Analytics-implementering för en viss sida.
>
> Det går att migrera din at.js-implementering (och AppMeasurement.js) till Platform Web SDK en sida i taget. Om du väljer det här sättet är det bäst att ange [`idMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#id-migration-enabled) och [`targetMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#targetMigrationEnabled) alternativ till `true` med `configure` -kommando.

## at.js-funktioner och motsvarigheter till Platform Web SDK

Många at.js-funktioner har en likvärdig metod med Platform Web SDK som beskrivs i tabellen nedan. Mer information om [Funktionerna at.js](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/atjs-functions/)finns i Adobe Target Developer Guide.

| funktionen at.js 2.x | SDK-motsvarighet för plattform |
| --- | --- | 
| `getOffer()` och `getOffers()` | För att begära och [rendera automatiskt](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#automatically-rendering-content) Rikta in er mot VEC-baserade upplevelser med `sendEvent` och ange `renderDecisions` till true.<br><br>Begär formulärbaserade upplevelser eller [rendera manuellt](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#manually-rendering-content) innehåll, ange en array med `decisionScopes` (mboxes) med `sendEvent` -kommando. |
| `applyOffer()` och `applyOffers()` | Använd [`applyPropositions`](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html#applypropositions) för att använda innehåll. Du kan välja att ställa in, ersätta eller lägga till HTML i en viss väljare. |
| `triggerView()` | Platform Web SDK utlöser automatiskt en [visa ändring](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/web-sdk-atjs-comparison.html#how-to-trigger-a-view-change-in-a-single-page-application) vid tillämpning av SPA VEC om `web.webPageDetails.viewName` egenskapen anges under `xdm` alternativ för `sendEvent` -kommando. |
| `trackEvent()` och `sendNotifications()` | Använd `sendEvent` kommando med [specifik `eventType`](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/web-sdk-atjs-comparison.html#how-to-track-events) set:<br><br>`decisioning.propositionDisplay` signalerar återgivning av en aktivitet<br><br>`decisioning.propositionInteract` signalerar en användarinteraktion med en aktivitet, som ett musklick. |
| `targetGlobalSettings()` | Ingen direkt motsvarighet. Se [Jämförelse av målinställningar](detailed-comparison.md) om du vill ha mer information. |
| `targetPageParams()` och `targetPageParamsAll()` | Alla data som skickas i `xdm` alternativ för `sendEvent` kommandot är mappat till Target-parametrar för mbox. Eftersom mbox-parametrar namnges med serialiserad punktnotation kan du behöva uppdatera befintliga målgrupper och aktiviteter för att kunna använda de nya mbox-parameternamnen när du migrerar till Platform Web SDK. <br><br>Data som skickas som en del av `data.__adobe.target` i `sendEvent` kommandot är mappat till [Målprofil och Recommendations-specifika parametrar](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/target-overview.html#single-profile-update). |
| at.js, anpassade händelser | Stöds inte. Se [allmän färdplan](https://github.com/orgs/adobe/projects/18/views/1?pane=item&amp;itemId=17372355{target="_blank"}) för aktuell status. [Svarstoken](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/accessing-response-tokens.html) exponeras som en del av `propositions` som svar på `sendEvent` ring. |

## at.js-inställningar och motsvarigheter till Platform Web SDK

At.js-biblioteket kan konfigureras och laddas ned med olika inställningar i målgränssnittet. Dessa inställningar kan även uppdateras med [`targetGlobalSettings()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/targetglobalsettings/) funktion. I tabellen nedan jämförs dessa inställningar med de som är tillgängliga med Platform Web SDK.

| at.js, inställning | SDK-motsvarighet för plattform |
| --- | --- |
| `bodyHiddenStyle` | Ange [`prehidingStyle`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#prehidingStyle) med `configure` kommando |
| `bodyHidingEnabled` | Om en `prehidingStyle` är definierad med `configure` och den här funktionen är aktiverad. Om inget format definieras försöker inte Platform Web SDK att dölja något innehåll. |
| `clientCode` | Automatiskt konfigurerad |
| `cookieDomain` | Ej tillämpligt |
| `crossDomain` | Ange `thirdPartyCookiesEnabled` alternativ till `true` med `configure` för att aktivera cookies från första och tredje part för användning över domäner |
| `cspScriptNonce` och `cspStyleNonce` | Läs dokumentationen för [konfigurera en CSP](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-a-csp.html) |
| `dataProviders` | Stöds inte |
| `decisioningMethod` | All Platform Web SDK `sendEvent` -kommandon använder beslut på serversidan. Hybrid- och enhetsbeslut stöds inte. |
| `defaultContentHiddenStyle` och `defaultContentVisibleStyle` | Gäller endast med at.js 1.x. Precis som i at.js 2.x kan du använda anpassad kod för att reducera eventuella flimmer för formulärbaserade upplevelser. |
| `deviceIdLifetime` | Stöds inte. If `targetMigrationEnabled` är inställd på `true` med `configure` kommandot, `mbox` cookie anges med enhetens livstid inställd på 2 år. Detta värde kan inte konfigureras. |
| `enabled` | Målfunktionen är aktiverad eller inaktiverad med dataströmskonfigurationen |
| `globalMboxAutoCreate` | Ange `renderDecisions` alternativ till `true` med `sendEvent` för att automatiskt hämta och återge VEC-baserade upplevelser.<br><br>Begär en `decisionScope` for `__view__` om du föredrar att manuellt återge VEC-baserade upplevelser. |
| `imsOrgId` | Ange `orgId` med `configure` kommando |
| `optinEnabled` och `optoutEnabled` | Se Platform Web SDK [sekretessalternativ](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html). The `defaultConsent` gäller för alla Adobe-lösningar som Platform Web SDK stöder. |
| `overrideMboxEdgeServer` och `overrideMboxEdgeServerTimeout` | Ej tillämpligt. Alla SDK-begäranden för plattformar använder Adobe Experience Platform Edge-nätverket. |
| `pageLoadEnabled` | Ange `renderDecisions` alternativ till `true` med `sendEvent` kommando |
| `secureOnly` | Stöds inte. Platform Web SDK anger alla cookies med `secure` och `sameSite="none"` attribut. |
| `selectorsPollingTimeout` | Stöds inte. Värdet 5 sekunder används för Platform Web SDK. Anpassad kod kan användas för att manuellt återge innehåll om det behövs. |
| `serverDomain` | Använd `edgeDomain` med `configure` kommando |
| `telemetryEnabled` | Ej tillämpligt |
| `timeout` | Stöds inte. Vi rekommenderar att du ser till att en lämplig tidsgräns anges för all kod som reducerar flimret. |
| `viewsEnabled` | Stöds inte. Innehåll för målvyer hämtas alltid på den första `sendEvent()` ring om `renderDecisions` är inställd på `true` eller `__view__` DecisionScope ingår i begäran. |
| `visitorApiTimeout` | Ej tillämpligt |


## Systemdiagramsjämförelse

Följande diagram bör hjälpa dig att förstå skillnaderna i dataflöde mellan en Target-implementering med at.js och en implementering med hjälp av Platform Web SDK.

### at.js 2.x systemdiagram

![at.js 2.0-beteende vid sidinläsning](assets/target-at-js-2x-diagram.png)

| Utlysning | Information |
| --- | --- |
| 1 | Anropet returnerar Experience Cloud-ID (ECID). Om användaren är autentiserad synkroniseras kundens ID med ett annat samtal. |
| 2 | at.js-biblioteket läses in synkront och döljer dokumentets brödtext (at.js kan också läsas in asynkront med ett valfritt predhide-fragment implementerat på sidan). |
| 3 | Begäran om sidinläsning omfattar alla konfigurerade parametrar, ECID, SDID och kund-ID. |
| 4 | Profilskript körs och matas in i profilarkivet. Store begär kvalificerade målgrupper från målgruppsbiblioteket (till exempel målgrupper som delas från Analytics, Audience Manager och så vidare). Kundattribut skickas till profilarkivet i en gruppbearbetning. |
| 5 | Baserat på URL, begärandeparametrar och profildata avgör Target vilka aktiviteter och upplevelser som ska returneras till besökaren för den aktuella sidan och framtida vyer. |
| 6 | Målinriktat innehåll som skickas tillbaka till sidan, eventuellt med profilvärden för ytterligare personalisering.<br><br>Målinriktat innehåll på den aktuella sidan visas så snabbt som möjligt utan att du behöver flimra standardinnehållet.<br><br>Målanpassat innehåll för framtida vyer av ett enkelsidigt program cachelagras i webbläsaren så att det kan tillämpas direkt utan ett extra serveranrop när vyerna aktiveras. (Se nästa diagram för triggerView()-beteende). |
| 7 | Analysdata som skickas från sidan till datainsamlingsservrarna. |
| 8 | Måldata matchas mot Analytics-data via SDID och bearbetas till lagringsplatsen för analysrapporter. Analysdata kan sedan visas både i Analytics och Target via A4T-rapporter. |

Se utvecklarhandboken för mer information om hur du [implementera Target med at.js för enkelsidiga program](https://developer.adobe.com/target/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application/).

### Systemdiagram för Platform Web SDK

![Diagram över Adobe Target edge-beslut med Platform Web SDK](assets/target-platform-web-sdk.png)

| Utlysning | Information |
| --- | --- |
| 1 | Enheten läser in Platform Web SDK. Platform Web SDK skickar en begäran till edge-nätverket med XDM-data, DataStreams Environment ID, inskickade parametrar och kundens ID (valfritt). Sidan (eller behållarna) är fördold. |
| 2 | edge-nätverket skickar begäran till edge-tjänsterna för att berika den med besökar-ID, samtycke och annan kontextinformation för besökare, som geopositionering och enhetsvänliga namn. |
| 3 | Edge-nätverket skickar den berikade personaliseringsbegäran till Target-kanten med besökar-ID och skickade parametrar. |
| 4 | Profilskript körs och matas sedan in i målprofilens lagring. Profillagring hämtar segment från målgruppsbiblioteket (till exempel segment som delas från Adobe Analytics, Adobe Audience Manager, Adobe Experience Platform). |
| 5 | Baserat på parametrar för URL-begäran och profildata avgör Target vilka aktiviteter och upplevelser som ska visas för besökaren för den aktuella sidvyn och för framtida förhämtade vyer. Target skickar sedan tillbaka den här till gränsnätverket. |
| 6 | a. Kantnätverket skickar personaliseringssvaret tillbaka till sidan, eventuellt inklusive profilvärden för ytterligare personalisering. Personaliserat innehåll på den aktuella sidan visas så snabbt som möjligt utan att man behöver flimra standardinnehållet.<br><br>b. Personaliserat innehåll för vyer som visas som ett resultat av användaråtgärder i ett Single Page-program (SPA) cachas för direktåtergivning utan ytterligare serveranrop.<br><br>c. Edge-nätverket skickar besökar-ID och andra värden i cookies (till exempel samtycke, sessions-ID, identitet, cookie-kontroll, personalisering och så vidare). |
| 7 | Edge Network Forwards Analytics for Target (A4T)-information (aktivitet, upplevelse och konverteringsmetadata) till Analytics-kanten. |

Se utvecklarhandboken för mer information om hur du [implementera Target med Platform Web SDK för Single-page-program](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/spa-implementation.html).

När du har en god teknisk förståelse för den aktuella Target-implementeringen och de funktioner du använder är nästa steg att utföra [inledande konfiguration](initial-setup.md).

>[!NOTE]
>
>Vi vill hjälpa dig att lyckas med målmigreringen från at.js till Web SDK. Om du stöter på problem med din migrering eller känner att det saknas viktig information i den här guiden ber vi dig att meddela oss genom att publicera i [den här communitydiskussionen](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).
