---
title: Felsök - Migrera mål från
description: Lär dig felsöka en Adobe Target-implementering med Adobe Experience Platform Mobile SDK.
source-git-commit: 009548969b88d1bfa6eac23f65b1ca2144f27c34
workflow-type: tm+mt
source-wordcount: '1224'
ht-degree: 0%

---

# Debug Target with the Platform Mobile SDK

Verifiera målaktiviteter och felsöka Mobile SDK för att felsöka problem med implementering, innehållsleverans och målgruppskvalifikation. På den här sidan i migreringsguiden förklaras skillnaderna mellan felsökning med at.js och Platform Web SDK.

Tabellen nedan sammanfattar funktioner och stöd för testning och felsökning.

| Funktion eller verktyg | support för at.js | Stöd för Platform Web SDK |
| --- | --- | --- |
| URL för aktivitets-QA | Ja | Ja |
| URL-parametern `mboxDisable` | Ja | Se informationen nedan för att [inaktivera Target-funktionen](#disable-target-functionality) |
| URL-parametern `mboxDebug` | Ja | Använd parametern `alloy_debug` för liknande felsökningsinformation |
| URL-parametern `mboxTrace` | Ja | Använda webbläsartillägget Experience Platform Debugger |
| Adobe Experience Platform Debugger | Ja | Ja |
| URL-parametern `alloy_debug` | Ej tillämpligt | Ja |
| Adobe Experience Platform Assurance | Ej tillämpligt | Ja |

## Webbläsartillägget Adobe Experience Platform Debugger

Tillägget Adobe Experience Platform Debugger för Chrome och Firefox undersöker dina webbsidor och hjälper dig att validera dina Adobe Experience Cloud-implementeringar.

Du kan köra Platform Debugger på valfri webbsida och tillägget har tillgång till publika data. Om du vill få åtkomst till icke-offentliga data med tillägget, till exempel målspårningsinformation, måste du autentisera till Experience Cloud via länken **[!UICONTROL Sign in]**.


## Förhandsgranska målaktiviteter med QA-URL:er

I både at.js och Platform Web SDK kan du förhandsgranska Target-aktiviteter med hjälp av Target QA-URL:er, och båda implementeringsmetoderna har stöd för samma QA-funktioner.

Ange QA-URL:er som mål genom att instruera at.js eller Platform Web SDK att skriva en specifik cookie till din webbläsare med namnet `at_qa_mode`. Denna cookie används för att framtvinga kvalificering för en viss aktivitet och upplevelse.

>[!CAUTION]
>
>Funktionen för mål-QA-läge stöds av Platform Web SDK version 2.13.0 eller senare. Mål-QA-läget är aktiverat baserat på det `xdm.web.webPageDetails.URL`-värde som skickades i `sendEvent`-anropet. Om du ändrar det här värdet, till exempel tar bort alla tecken, kan det medföra att mål-QA-läget inte fungerar som det ska.

Mer information om [Målaktivitet QA](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html) finns i den dedikerade guiden.

## Implementering av felsökningsmål

Tabellen nedan visar skillnaderna mellan felsökningsmetoderna at.js och Platform Web SDK:

| at.js, funktion | SDK-motsvarighet för plattform |
| --- | --- |
| **Mbox Inaktivera** - Inaktivera mål från hämtning och återgivning för att kontrollera om sidan har brutits utan målinteraktioner<br><br>Läs in sida med URL-parameter: `mboxDisable=true` | Ingen direkt motsvarighet. Du kan blockera alla Platform Web SDK-begäranden med webbläsarens utvecklarverktyg. |
| **Mbox Debug** - loggar alla at.js-åtgärder i webbläsarens konsol för att felsöka återgivningsproblem<br><br>Läs in sida med URL-parameter: `mboxDebug=true` | **Allokera felsökning** - loggar detaljerade åtgärder för SDK, inklusive men inte begränsat till målpersonaliseringsåtgärder.<br><br>Läs in sida med URL-parameter: `alloy_debug=true` <br /><br />Eller kör `alloy("setDebug", { "enabled": true });` i utvecklarkonsolen |
| **Målspårning** - med en mbox-spårningstoken genererad i målgränssnittet, är ett trace-objekt med information som har deltagit i beslutsprocessen tillgängligt under objektet `window.___target_trace`.<br><br>Läs in sida med URL-parameter: `mboxTrace=window&authorization={TOKEN}` | Använd Adobe Experience Platform felsökningstillägg eller Platform Assurance. |

>[!NOTE]
>
>Alla felsökningsfunktionerna i at.js ovan är tillgängliga med förbättrade funktioner i Adobe Experience Platform Debugger.

### Inaktivera Target-funktioner

Platform Web SDK har för närvarande ingen funktion för att selektivt undertrycka målsvar. Det är dock möjligt att inaktivera begäran om Platform Web SDK med webbläsarens utvecklarverktyg, olika webbläsartillägg eller tredjepartsprogram. Så här blockerar du till exempel Platform Web SDK med Google Chrome:

1. Högerklicka någonstans på sidan och välj **Inspect**
1. Välj fliken **Nätverk**
1. Filtrera efter strängen `//ee//` så att endast platsens Web SDK-anrop visas
1. Läs in sidan igen
1. Högerklicka på en av de filtrerade nätverksförfrågningarna och välj **Blockera begärandedomän**
1. Läs in sidan igen och observera att nätverksbegäran har blockerats
1. När du är klar med felsökningen högerklickar du på den blockerade nätverksbegäran och väljer **Ta bort blockering** eller stänger panelen Utvecklingsverktyg

### Visa felsökningsloggning

Felsökningsloggning för at.js med URL-parametern `mboxDebug=true` visar detaljerad information om varje Target-begäran, svar och försök att återge innehållet på sidan. Platform Web SDK har liknande felsökningsloggning med URL-parametern `alloy_debug=true`.

| Loggad information | at.js (`mboxDebug=true`) | Plattforms-SDK (`alloy_debug=true`) |
| --- | --- | --- |
| Loggningsprefix för filtrering | `AT:` | `[alloy]` |
| Information om sidinläsningsbegäran | Ja | Ja |
| Mbox eller scope request details | Ja | Ja |
| Status för förfrågan | Ja | Ja |
| Svarsinformation | Ja | Ja |
| Återgivningsstatus | Slutförda och fel | Endast fel |
| Återgivningsinformation | Ja | Ja |

>[!NOTE]
>
>Felsökningsloggar för at.js och Platform Web SDK ger en liknande detaljnivå med det anmärkningsvärda undantaget att Web SDK bara meddelar om återgivningsfel på grund av ogiltiga väljare. Felsökningsloggningen bekräftar för närvarande inte att återgivningen lyckades.

### Visa målspår

Målspår innehåller detaljerad information om aktivitetskvalifikationer och besökarens Target-profil. Eftersom Target-spårningar innehåller information som inte är allmänt tillgänglig, krävs en verifieringstoken för att kunna visas och autentiseras i webbläsartilläggsfönstret i Adobe Experience Platform Debugger.

| Målspårningsmetod | at.js | Platform Web SDK |
| --- | --- | --- |
| URL-parametern `mboxTrace` | Ja | Nej |
| Webbläsartillägget Adobe Experience Platform Debugger | Ja | Ja |
| Adobe Experience Platform Assurance | Nej | Ja |



<!--![How to view Target traces with Adobe Experience Platform Debugger](assets/target-trace-debugger.png){zoomable="yes"}-->

När du har valt **[!UICONTROL View]** visas en övertäckning som gör att du kan se följande information om begäran:

- Matchade aktiviteter
- Oöverträffade aktiviteter
- Information om förfrågan
- Ögonblicksbild av profil

Mer information om målspår finns i den dedikerade guiden om [felsökning av leverans av målinnehåll](https://experienceleague.adobe.com/docs/target/using/activities/troubleshoot-activities/content-trouble.html).

### Felsök med Assurance

Målspårningsinformation kan visas både i webbläsartillägget Adobe Experience Platform Debugger och i Assurance-programmet (tidigare kallat Project Griffon). Så här visar du målspår i Assurance:

1. Öppna webbläsartillägget Adobe Experience Platform Debugger och anslut en fjärrfelsökningssession enligt ovan
1. Markera länken med ditt sessionsnamn ovanför felsökningsloggen
1. Platform Assurance läser in och visar detaljerad loggning för alla Adobe-program som konfigurerats i dataströmmen för din implementering
1. Filtrera loggen efter `adobe.target`
1. Välj en loggpost med typen `com.adobe.target.trace`
1. Expandera informationen om nyttolasten och visa informationen under `context > targetTrace`

<!--![How to view Target traces with Assurance](assets/target-trace-assurance.png){zoomable="yes"}-->

## Undersök nätverksbegäran och svar

Nyttolasten och svaret för plattformens Web SDK `sendEvent`-anrop skiljer sig från at.js. Med hjälp av konturen nedan kan du förstå hur begäran och svaret är upplagda samtidigt som du undersöker nätverksanropen med webbläsarens utvecklingsverktyg.

### Nyttolast för innehållsbegäran

<!--![Target specific elements of the Platform Web SDK payload](assets/target-payload.png){zoomable="yes"}-->

- Profil, entitet och andra icke-mbox-parametrar skickas i händelsearrayen under `data.__adobe.target`
- Beslutsomfattningarna finns i händelsearrayen under `query.personalization.decisionScopes`
- XDM-data som mappas till mbox-parametrar längre ned finns i händelsearrayen under `xdm`

### Innehållssvarets brödtext

<!--![Target specific elements of the Platform Web SDK response body](assets/target-response.png){zoomable="yes"}-->

- Platform Web SDK returnerar åtgärder för alla Adobe-program under objektet `handle`
- Åtgärden `personalization:decisions` innebär ett svar från mål eller offer decisioning
- Målförslag presenteras som en matris, där vart och ett har ett unikt förslags-ID med prefixet `AT:`
- Beslutsomfattandet och aktivitetsinformationen finns i förslagsarrayen
- Erbjudandeinformationen finns i arrayen `items` under `data`
- Svarstoken finns i `items`-matrisen under `meta`

### Sprid händelsens nyttolast

<!--![Target proposition event example](assets/target-proposition-event.png){zoomable="yes"}-->

- Målspecifika SDK-händelser är antingen `decisioning.propositionDisplay` för ett intryck eller `decisioning.propositionInteract` för en interaktion, till exempel ett klick
- Information om händelsen proposition finns i arrayen events under `xdm._experience.decisioning`
- Förslags-ID för visnings- eller interaktionshändelsen ska matcha förslags-ID för innehållet som returneras från Target


Grattis, du har kommit till slutet av självstudiekursen! Lycka till med att migrera din Adobe Target-implementering till Web SDK!

>[!NOTE]
>
>Vi vill hjälpa dig att lyckas med din migrering av mobilmål från måltillägget till optimeringstillägget. Om du stöter på problem med din migrering eller om du känner att det saknas viktig information i den här guiden kan du meddela oss genom att publicera [den här communitydiskussionen](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
