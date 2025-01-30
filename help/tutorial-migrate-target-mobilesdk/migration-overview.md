---
title: Migreringsöversikt - Migrera från Adobe Target till Adobe Journey Optimizer - mobiltillägg för beslut
description: Lär dig mer om skillnaderna mellan at.js och Platform Web SDK och hur du planerar din migreringssatsning.
exl-id: 86849319-d2ad-4338-aa1a-d307d8807d4a
source-git-commit: 6e442413c178e76183f88454d97d3896f8efa8bc
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 0%

---

# Target at.js to Platform Web SDK migration overview

Hur stor insats du ska göra för att migrera från måltillägget till beslutstillägget beror på hur komplex din nuvarande implementering och vilka produktfunktioner som används är.

Oavsett hur enkel eller komplex implementeringen är är det viktigt att du förstår ditt nuvarande läge fullständigt innan du migrerar. Den här guiden hjälper dig att bryta ned komponenterna i den aktuella implementeringen och utveckla en hanterbar plan för att migrera varje del.

Migreringsprocessen omfattar följande viktiga steg:

1. Utvärdera er nuvarande implementering och fastställa en migreringsstrategi
1. Konfigurera de initiala komponenterna för anslutning till Adobe Experience Platform Edge Network
1. Uppdatera implementeringen för att ersätta SDK Target med XYZ
1. Förbättra implementeringen av Platform Mobile SDK för dina specifika användningsfall. Detta kan innebära att ytterligare parametrar skickas, XYZ.
1. Vill du uppdatera objekt i Target-gränssnittet, till exempel profilskript, aktiviteter och målgruppsdefinitioner??
1. Validera den slutliga implementeringen innan du publicerar den uppdaterade appen

## Viktiga skillnader mellan at.js och Platform Web SDK

Innan du startar migreringsprocessen är det viktigt att förstå skillnaderna mellan at.js och Platform Web SDK.

### Operativa skillnader

Platform Web SDK kombinerar funktionaliteten hos olika Adobe-program i ett enda bibliotek. Detta enhetliga tillvägagångssätt innebär att ni bör överväga ansvar och processer mellan team för att säkerställa en bra implementering.

| | Mål at.js 2.x | Platform Web SDK |
|---|---|---|
| Ägarskap | Måltillägget är oberoende av andra program-SDK:er (TROR INTE ATT DETTA ÄR TRUE FÖR MOBILE). Anpassningar och ägarskap av dessa olika bibliotek kan anpassas efter olika team i organisationen. | SDK-biblioteket Platform Web och de data som skickas är enhetliga för alla Adobe-program. Ägarskapet för implementeringen av Platform Web SDK bör representera intressenter för alla program i senare led. |
| Underhåll | Separata team kan arbeta med implementeringsförbättringar för varje Adobe-program, som Target och Analytics. | Helst ska ett team ansvara för förbättringar som påverkar plattformens SDK-implementering. |
| Process | Ändringar i en Target-implementering kan följa en process som har en annan inriktning eller QA-krav än andra program som Analytics. | Ändringar av en implementering av Platform Web SDK bör omfatta alla program längre fram i kedjan, och QA- och publiceringsprocessen bör anpassas därefter. |
| Collaboration | Data som är specifika för Target kan skickas direkt i Target-anropen. Beroende på implementeringen kan det finnas ytterligare Target-anrop. Detta har ingen direkt inverkan på Adobe Analytics data och samordningen med analysteamet är inte så viktig. | Data som skickas i SDK-anrop för plattformar kan vidarebefordras till både Target och Analytics. Samordning mellan grupper krävs för att säkerställa att ändringar inte påverkar en viss tillämpning negativt. |

### Tekniska skillnader

Platform Web SDK är inte en utveckling av Target at.js-biblioteket. Det är en ny och enhetlig metod för att implementera alla Adobe-program för webbkanalen. Det finns flera tekniska skillnader att vara medveten om.

| | Mål at.js 2.x | Platform Web SDK |
|---|---|---|
| Biblioteksfunktioner | Målfunktioner från at.js. Integrering med andra program från Visitor.js och AppMeasurement.js | Funktioner för alla Adobe-program från ett enda SDK-bibliotek för plattformen: alloy.js |
| Prestanda | at.js är ett av flera bibliotek som måste läsas in för korrekt integrering mellan program. Detta resulterar i mindre än optimal inläsningstid. | Platform Web SDK är ett enda lättviktsbibliotek som eliminerar behovet av flera programspecifika bibliotek, vilket ger bättre sidladdningsprestanda. |
| Begäranden | Separata anrop för varje Adobe-program. Målsamtal är i stort sett oberoende av andra nätverksanrop. | Samtal för alla Adobe-program. Ändringar av data som skickas i dessa anrop kan påverka flera program längre fram i kedjan. |
| Läs in ordning | För en korrekt integrering med andra Adobe-program krävs en särskild inläsningsordning för bibliotek och nätverksanrop. | Korrekt integrering kräver inte att du sammanfogar data från olika programspecifika nätverksanrop, och därför behöver du inte bekymra dig om inläsningsordningen. |
| Edge Network | Använder Adobe Experience Cloud Edge Network (tt.omtrdc.net), eventuellt med en CNAME som är specifik för Target. | Använder Adobe Experience Platform Edge Network (edge.adobedc.net), eventuellt tillsammans med en enda CNAME. |
| Grundläggande terminologi | at.js-namngivning: <br> - `mbox` <br> - `pageLoad` händelse (global mbox) <br> - `offer` | SDK-motsvarighet för plattformar: <br> - `decisionScope` <br> - `__view__` DecisionScope <br> - `proposition` |

### Videoöversikt

I följande videofilm visas Adobe Experience Platform Web SDK och Adobe Experience Platform Edge Network.


Nu när du förstår skillnaderna på hög nivå mellan at.js och Platform Web SDK kan du [planera migreringen](plan-migration.md).

>[!NOTE]
>
>Vi strävar efter att hjälpa dig att lyckas med din migrering av mobilmål från måltillägget till beslutstillägget. Om du stöter på problem med din migrering eller om du känner att det saknas viktig information i den här guiden kan du meddela oss genom att publicera [den här communitydiskussionen](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
