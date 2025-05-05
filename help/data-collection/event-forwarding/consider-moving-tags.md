---
title: Överväg att flytta leverantörstaggar till händelsevidarebefordran
description: Lär dig hur du utvärderar en leverantörstagg på klientsidan för datadistribution på serversidan.
feature: Event Forwarding, Tags, Integrations
role: Admin, Developer, Architect, Data Engineer
level: Intermediate, Experienced
jira: KT-9921
exl-id: f8fd351a-435c-4cc1-b987-ed2ead20d4d6
source-git-commit: 7edf8fc46943ae2f1e6e2e20f4d589d7959310c8
workflow-type: tm+mt
source-wordcount: '1279'
ht-degree: 0%

---

# Överväg att flytta leverantörstaggar på klientsidan till händelsevidarebefordran

Det finns flera goda skäl att överväga att flytta leverantörstaggar på klientsidan från webbläsare och enheter och till en server. I den här artikeln diskuterar vi hur du utvärderar en leverantörstagg på klientsidan för att kunna flytta den till en händelsevidarebefordringsegenskap.

Den här utvärderingen är bara nödvändig om du överväger att ta bort en leverantörstagg på klientsidan och ersätta den med datadistribution på serversidan i en händelsevidarebefordringsegenskap. I den här artikeln förutsätts du känna till grunderna för [datainsamling](https://experienceleague.adobe.com/docs/data-collection.html?lang=sv-SE) och [vidarebefordran av händelser](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=sv-SE).

>[!NOTE]
>
>Adobe Experience Platform Launch har omklassificerats som en serie datainsamlingstekniker i Adobe Experience Platform. Som ett resultat av detta har flera terminologiska förändringar införts i produktdokumentationen. I följande [dokument](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=sv-SE) finns en konsoliderad referens till de ändrade terminologin.

Webbläsarleverantörer ändrar hur de hanterar cookies från tredje part. Advertising och marknadsföringsleverantörer och marknadsföringsteknologier kräver ofta användning av många taggar på klientsidan. Dessa utmaningar är bara två övertygande skäl till att våra kunder lägger till datadistribution på serversidan.

>[!NOTE]
>
>`Tag` i den här artikeln betyder klientkod, vanligtvis JavaScript från en leverantör som används för datainsamling i webbläsaren eller enheten medan en besökare interagerar med webbplatsen eller appen. `Website` eller `site` avser här en webbplats, ett webbprogram eller ett program för en mobil enhet. En&quot;tagg&quot; för dessa syften kallas ofta även en pixel.

## Användningsexempel och data {#use-cases-data}

Det första steget är att definiera de användningsfall som implementeras med leverantörstaggen på klientsidan. Ta till exempel pixeln Facebook (Meta). Om du flyttar den från vår webbplats till [Meta Conversions API](https://exchange.adobe.com/apps/ec/109168/meta-conversions-api) med tillägget för händelsevidarebefordran måste du först dokumentera de specifika användningsfallen.

För den aktuella leverantörskoden på klientsidan:

- Vilka specifika händelser och andra datapunkter visas och skickas till klientsidans tagg?
- När och var sker dataöverföringen?

Det kan vara praktiskt att göra en lista, ett kalkylblad, ett diagram eller annan post med data och händelsesekvenser för att dokumentera utvärderingen, även om det bara är till för dig. Se till att du inkluderar etiketter för datakällor - varifrån kommer det? Destinationer - vart går den? Och omvandlingar - vad händer mellan källa och mål?

I vårt exempel spårar vi konverteringar med Facebook pixel när besökarna interagerar med vår webbplats efter att ha tittat på en Facebook-annons. De kan också interagera med vår webbplats efter att ha tittat på relaterade annonser på en annan social plattform. För att kunna se dessa konverteringar i Facebook annonseringsverktyg och rapporter måste de data som behövs hämtas till Facebook. Dessa data kan omfatta konverteringshändelser som nedladdningar, registreringar, gilla-markeringar eller inköp.

### Data {#data}

Vad händer med data för vår användning när den befintliga taggen på klientsidan körs eller körs på vår webbplats? Kan vi samla in de data vi behöver i klienten, utan leverantörstaggen, så att vi kan skicka dem till händelsevidarebefordran? När du använder [taggar](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=sv) eller andra tagghanteringssystem är de flesta besökarinteraktionsdata tillgängliga för insamling och distribution. Men finns de data vi behöver för vår användning tillgängliga när vi behöver dem, där vi behöver dem och i det format vi behöver dem - utan leverantörstaggen på klientsidan? Här är några andra datafrågor att tänka på:

- Krävs det ett användar-ID för varje leverantör för varje händelse?
- Om så är fallet, hur kan de samlas in eller genereras utan klientsidestaggen?
- Kräver leverantören specifikt sin klientkod vid körning?
- Vilka andra data krävs? Var kommer dessa data ifrån?

De flesta leverantörstaggar på klientsidan kräver inte många datapunkter för ett visst användningsfall, men det kan vara bra att notera användningsexempel och obligatoriska data under utvärderingarna.

## Leverantörs-API:er {#vendor-apis}

Nu vet vi vilka specifika användningsfall som ska implementeras, vilka data som krävs och sekvensen av händelser från källa till mål. För att avgöra om användningsexemplet passar bra för vidarebefordran av händelser kan vi nu undersöka leverantörs-API-informationen.

>[!IMPORTANT]
>
>Många leverantörer aktiverar API:er för överföring från server till server, men det finns också många som för närvarande inte har API:er som passar för dessa ändamål.

### Undersöker API:er {#investigate-apis}

Här är några steg vi kan ta för att undersöka leverantörs-API-slutpunkter.

Har leverantören API:er som är utformade för överföring av händelsedata från server till server? Börja med att hitta kraven för dessa specifika API-slutpunkter:

- Finns API-slutpunkterna för att skicka nödvändiga data? Om du vill hitta slutpunkter som stöder dina användningsfall kan du titta i leverantörens dokumentation för utvecklare eller API.
- Tillåter de strömmande händelsedata eller endast batchdata?
- Vilka autentiseringsmetoder stöder de? Token, HTTP, OAuth client credentials version eller annan? Se [här](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html?lang=sv-SE) för metoder som stöds av händelsevidarebefordran.
- Vad är uppdateringsförskjutningen för deras API? Är den begränsningen kompatibel med minimumen för händelsespridning? Information [här](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html?lang=sv-SE#:~:text=you%20can%20configure%20the%20Refresh%20Offset%20value%20for%20the%20secret).
- Vilka data kräver de för de relevanta slutpunkterna?
- Kräver de en leverantörsspecifik användaridentifierare för varje anrop till slutpunkten?
- Om de behöver den identifieraren, var och hur kan den genereras eller hämtas, utan kod på klientsidan?

Med andra ord:

- Tillhandahåller leverantören de API-slutpunkter som krävs för våra användningsfall?
- Har de någon kompatibel autentiseringsmetod för vidarebefordran av händelser?
- Kan vi komma åt alla data som krävs för en implementering av vidarebefordran av händelser (antingen från klienten eller från andra API-anrop)?

Taggen är antagligen en bra kandidat för att gå från klienten till våra servrar i en händelsevidarebefordringsegenskap om vi kan svara ja på dessa frågor.

Om leverantören inte har API-slutpunkterna som stöd för våra användningsfall är det uppenbart att leverantörstaggen inte är en bra kandidat för att använda händelsevidarebefordran i stället för leverantörstaggen på klientsidan.

Vad händer om de har API:er, men också behöver ett unikt besökar- eller användar-ID för varje API-anrop? Hur kommer vi åt det ID:t om vi inte har leverantörens klientkod (tagg) på webbplatsen?

Vissa leverantörer förändrar sina system för den nya världen utan cookies från tredje part. Dessa ändringar inkluderar användning av alternativa unika identifierare, som ett [UID](https://developer.mozilla.org/en-US/docs/Glossary/UUID) eller annat [kundgenererat ID](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/first-party-device-ids.html?lang=sv-SE). Om leverantören tillåter ett kundgenererat ID kan vi antingen skicka det från klienten till Platform Edge Network med Web eller Mobile SDK, eller eventuellt hämta det från ett API-anrop vid händelsevidarebefordran. När vi skickar data till den leverantören i en regel för vidarebefordran av händelser, tar vi bara med den identifieraren vid behov.

Om leverantören kräver data (t.ex. ett leverantörsspecifikt unikt ID) som bara kan genereras eller kommas åt av deras egen tagg på klientsidan, är det troligt att den leverantörstaggen inte är en bra kandidat att flytta. _Försök att bakåtkompilera en klientsidestagg med tanken att flytta den datainsamlingen till händelsevidarebefordran utan lämpliga API:er rekommenderas inte._

Tillägget [Adobe Experience Platform Cloud Connector](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/cloud-connector/overview.html?lang=sv-SE) kan göra HTTP-begäranden vid behov med leverantörer som har rätt API:er för överföring av händelsedata från server till server. Även om leverantörsspecifika tillägg är bra att ha och fler tillägg håller på att utvecklas just nu, kan vi implementera regler för vidarebefordran av händelser i dag med Cloud Connector-tillägget, utan att vänta på ytterligare leverantörstillägg.

## Verktyg {#tools}

Det är enklare att undersöka och testa leverantörs-API-slutpunkter med verktyg som [Postman](https://www.postman.com/) eller textredigeringstillägg som Visual Studio Code [Thunder Client](https://marketplace.visualstudio.com/items?itemName=rangav.vscode-thunder-client) eller [HTTP Client](https://marketplace.visualstudio.com/items?itemName=mkloubert.vscode-http-client).

## Nästa steg {#next-steps}

I den här artikeln finns en serie steg för att utvärdera en leverantörs klientsidestagg och eventuellt flytta den på serversidan i en egenskap för vidarebefordring av händelser. Mer information om relaterade ämnen finns i följande länkar:

- [Tagghantering](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=sv) i Adobe Experience Platform
- [Vidarebefordran av händelser](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=sv-SE) för bearbetning på serversidan
- [Terminologiska uppdateringar](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=sv-SE) i datainsamling
