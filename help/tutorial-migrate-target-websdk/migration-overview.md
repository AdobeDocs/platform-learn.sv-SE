---
title: Migreringsöversikt - Migrera mål från at.js 2.x till Web SDK
description: Lär dig mer om skillnaderna mellan at.js och Platform Web SDK och hur du planerar din migreringssatsning.
exl-id: a8ed78e4-c8c2-4505-b4b5-e5d508f5ed87
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 0%

---

# Target at.js to Platform Web SDK migration overview

Hur mycket du ska göra för att migrera från at.js till Platform Web SDK beror på hur komplex din nuvarande implementering och de produktfunktioner som används är.

Oavsett hur enkel eller komplex implementeringen är är det viktigt att du förstår ditt nuvarande läge fullständigt innan du migrerar. Den här guiden hjälper dig att bryta ned komponenterna i den aktuella implementeringen och utveckla en hanterbar plan för att migrera varje del.

Migreringsprocessen omfattar följande viktiga steg:

1. Utvärdera er nuvarande implementering och fastställa en migreringsstrategi
1. Konfigurera de inledande komponenterna för anslutning till Adobe Experience Platform Edge Network
1. Uppdatera den grundläggande implementeringen för att ersätta at.js med Platform Web SDK
1. Förbättra implementeringen av Platform Web SDK för dina specifika användningsfall. Detta kan innebära att ytterligare parametrar skickas, att SPA-vy (single page app) används, att svarstoken används och mycket annat.
1. Uppdatera objekt i Target-gränssnittet, till exempel profilskript, aktiviteter och målgruppsdefinitioner
1. Validera den slutliga implementeringen innan du byter i produktionsmiljön

## Viktiga skillnader mellan at.js och Platform Web SDK

Innan du startar migreringsprocessen är det viktigt att förstå skillnaderna mellan at.js och Platform Web SDK.

### Operativa skillnader

Platform Web SDK kombinerar funktionaliteten i flera Adobe-program i ett enda bibliotek. Detta enhetliga tillvägagångssätt innebär att ni bör överväga ansvar och processer mellan team för att säkerställa en bra implementering.

| | Mål at.js 2.x | Platform Web SDK |
|---|---|---|
| Ägarskap | at.js-biblioteket är oberoende av andra programbibliotek. Anpassningar och ägarskap av dessa olika bibliotek kan anpassas efter olika team i organisationen. | SDK-biblioteket Platform Web och de data som skickas är enhetliga för alla Adobe-program. Ägarskapet för implementeringen av Platform Web SDK bör representera intressenter för alla program i senare led. |
| Underhåll | Separata team kan arbeta med implementeringsförbättringar för varje Adobe-program, som Target och Analytics. | Helst ska ett team ansvara för förbättringar som påverkar plattformens SDK-implementering. |
| Process | Ändringar i en Target-implementering kan följa en process som har en annan inriktning eller QA-krav än andra program som Analytics. | Ändringar av en implementering av Platform Web SDK bör omfatta alla program längre fram i kedjan, och QA- och publiceringsprocessen bör anpassas därefter. |
| Collaboration | Data som är specifika för Target kan skickas direkt i Target-anropen. Beroende på implementeringen kan det finnas ytterligare Target-anrop. Detta har ingen direkt inverkan på Adobe Analytics data och samordningen med analysteamet är inte så viktig. | Data som skickas i SDK-anrop för plattformar kan vidarebefordras till både Target och Analytics. Samordning mellan grupper krävs för att säkerställa att ändringar inte påverkar en viss tillämpning negativt. |

### Tekniska skillnader

Platform Web SDK är inte en utveckling av Target at.js-biblioteket. Det är ett nytt och enhetligt sätt att implementera alla Adobe-program för webbkanalen. Det finns flera tekniska skillnader att vara medveten om.

| | Mål at.js 2.x | Platform Web SDK |
|---|---|---|
| Biblioteksfunktioner | Målfunktioner från at.js. Integrering med andra program från Visitor.js och AppMeasurement.js | Funktioner för alla Adobe-program från ett enda plattformsbibliotek för SDK: alloy.js |
| Prestanda | at.js är ett av flera bibliotek som måste läsas in för korrekt integrering mellan program. Detta resulterar i mindre än optimal inläsningstid. | Platform Web SDK är ett enda lättviktsbibliotek som eliminerar behovet av flera programspecifika bibliotek, vilket ger bättre sidladdningsprestanda. |
| Begäranden | Olika samtal för varje Adobe-program. Målsamtal är i stort sett oberoende av andra nätverksanrop. | Samtal för alla Adobe-program. Ändringar av data som skickas i dessa anrop kan påverka flera program längre fram i kedjan. |
| Läs in ordning | För en korrekt integrering med andra Adobe-program krävs en särskild inläsningsordning för bibliotek och nätverksanrop. | Korrekt integrering kräver inte att du sammanfogar data från olika programspecifika nätverksanrop, och därför behöver du inte bekymra dig om inläsningsordningen. |
| Edge Network | Använder Adobe Experience Cloud Edge Network (tt.omtrdc.net), eventuellt med en CNAME som är specifik för Target. | Använder Adobe Experience Platform Edge Network (edge.adobedc.net), eventuellt tillsammans med en enda CNAME. |
| Grundläggande terminologi | at.js-namngivning: <br> - `mbox` <br> - `pageLoad` händelse (global mbox) <br> - `offer` | SDK-motsvarighet för plattformar: <br> - `decisionScope` <br> - `__view__` DecisionScope <br> - `proposition` |

### Videoöversikt

I följande videofilm visas en översikt över Adobe Experience Platform Web SDK och Adobe Experience Platform Edge Network.

>[!VIDEO](https://video.tv.adobe.com/v/34141/?learn=on&enablevpops)

Nu när du förstår skillnaderna på hög nivå mellan at.js och Platform Web SDK kan du [planera migreringen](plan-migration.md).

>[!NOTE]
>
>Vi vill hjälpa dig att lyckas med din Target-migrering från at.js till Web SDK. Om du stöter på problem med din migrering eller om du känner att det saknas viktig information i den här guiden kan du meddela oss genom att publicera [den här communitydiskussionen](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
