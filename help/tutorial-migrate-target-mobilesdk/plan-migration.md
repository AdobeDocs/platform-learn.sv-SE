---
title: Planera migreringen - Migrera från Adobe Target till Adobe Journey Optimizer - Bestämning av mobiltillägg
description: Lär dig mer om skillnaderna mellan at.js och Platform Web SDK och hur du planerar din migreringssatsning.
exl-id: 86849319-d2ad-4338-aa1a-d307d8807d4a
source-git-commit: f3fd5f45412900dcb871bc0b346ce89108fa8913
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 0%

---

# Planera migreringen

Hur stor insats du ska göra för att migrera från måltillägget till beslutstillägget beror på hur komplex din nuvarande implementering och vilka produktfunktioner som används är.

Oavsett hur enkel eller komplex implementeringen är är det viktigt att du förstår ditt nuvarande läge fullständigt innan du migrerar. Den här guiden hjälper dig att bryta ned komponenterna i den aktuella implementeringen och utveckla en hanterbar plan för att migrera varje del.

Migreringsprocessen omfattar följande viktiga steg:

1. Utvärdera er nuvarande implementering och fastställa en migreringsstrategi
1. Konfigurera de initiala komponenterna för anslutning till Adobe Experience Platform Edge Network
1. Uppdatera den grundläggande implementeringen för att ersätta måltillägget och beslutstillägget
1. Förbättra SDK-implementeringen för dina specifika användningsfall. Detta kan innebära att ytterligare parametrar skickas, att svarstoken används med mera.
1. Uppdatera objekt i Target-gränssnittet, till exempel profilskript, aktiviteter och målgruppsdefinitioner
1. Validera den slutliga implementeringen innan du byter i produktionsmiljön

## Viktiga skillnader mellan Target-tillägget och Decisioneringstillägget

Innan du startar migreringsprocessen är det viktigt att förstå skillnaderna mellan måltillägget och beslutstillägget.

### Operativa skillnader

| | Mål at.js 2.x | Platform Web SDK |
|---|---|---|
| Process | Ändringar i en Target-implementering kan följa en process som har en annan inriktning eller QA-krav än andra program som Analytics. | Ändringar av en implementering av ett beslutstillägg bör omfatta alla program i senare led och QA- och publiceringsprocessen bör anpassas i enlighet med detta. |
| Collaboration | Data som är specifika för Target kan skickas direkt i Target-anropen. Om rapportkällan för Target är Adobe Analytics kan data som är specifika för Target också skickas till Adobe Analytics när lämpliga spårningsmetoder i tillägget Target anropas för visning av målinnehåll och interaktion. | Data som skickas i anrop till beslutstillägg kan vidarebefordras till både Target och Analytics om Target-rapportkällan är Adobe Analytics, Adobe Analytics är aktiverat i dataströmmen och lämpliga spårningsmetoder i Beslutstillägg anropas när Target-innehåll visas och interagerar med det. |

### Tekniska skillnader

| | Måltillägg | Beslutstillägg |
|---|---|---|
| Beroenden | Endast SDK med Mobile Core | Använder Mobile Core och Edge Network SDK |
| Biblioteksfunktioner | Stöder endast hämtning av innehåll från Adobe Target | Stöd för hämtning av innehåll från Adobe Target och Offer decisioning |
| Begäranden | Målsamtal är i stort sett oberoende av andra nätverksanrop | Målnätverksanrop köas tillsammans med nätverksanrop för andra Edge-baserade lösningar som Messaging i Edge SDK och utförs seriellt. |
| Edge Network | Använder målservervärdet eller Adobe Experience Cloud Edge Network med klientkoden (clientcode.tt.omtrdc.net), som båda anges i [målkonfigurationen](https://developer.adobe.com/client-sdks/solution/adobe-target/#configure-the-target-extension-in-the-data-collection-ui) i användargränssnittet för datainsamling | Använder den Edge-nätverksdomän som anges i Adobe Experience Platform [Edge Network-konfiguration](https://developer.adobe.com/client-sdks/edge/edge-network/#configure-the-edge-network-extension-in-data-collection-ui) i användargränssnittet för datainsamling. |
| Grundläggande terminologi | mbox, TargetParameters | DecisionScope, Map (Android)/Dictionary (iOS) för målparametrar |
| Standardinnehåll | Tillåter att klientsidans standardinnehåll skickas i TargetRequest, som returneras om nätverksanropet misslyckas eller resulterar i fel. | Det går inte att skicka standardinnehåll på klientsidan. Returnerar inte något innehåll om nätverksanropet misslyckas eller resulterar i fel. |
| Målparametrar | Tillåter att globala TargetParameters skickas per begäran och olika TargetParameters per mbox | Tillåter att globala TargetParameters skickas endast per begäran |

Granska sedan den detaljerade [jämförelsen av måltillägget och beslutstillägget](detailed-comparison.md) för att få en bättre förståelse för de tekniska skillnaderna och identifiera områden som kräver ytterligare fokus.

>[!NOTE]
>
>Vi strävar efter att hjälpa dig att lyckas med din migrering av mobilmål från måltillägget till beslutstillägget. Om du stöter på problem med din migrering eller om du känner att det saknas viktig information i den här guiden kan du meddela oss genom att publicera [den här communitydiskussionen](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
