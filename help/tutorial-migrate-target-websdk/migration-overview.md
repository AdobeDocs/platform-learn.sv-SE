---
title: Migreringsöversikt | Migrera mål från at.js 2.x till Web SDK
description: Lär dig mer om de viktigaste skillnaderna mellan at.js och Platform Web SDK och hur du planerar din migrering.=
source-git-commit: 287ebcb275c4fca574dbd6cdf7e07ba4268bddb5
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 0%

---

# Target at.js to Platform Web SDK migration overview

Hur mycket du ska göra för att migrera från at.js till Platform Web SDK beror på hur komplex din nuvarande implementering och de produktfunktioner som används är.

Oavsett hur enkel eller komplex implementeringen är är det viktigt att du förstår ditt nuvarande läge fullständigt innan du migrerar. Den här guiden hjälper dig att bryta ned komponenterna i den aktuella implementeringen och utveckla en hanterbar plan för att migrera varje del.

Migreringsprocessen omfattar följande viktiga steg:

1. Utvärdera er nuvarande implementering och fastställa en migreringsstrategi
1. Konfigurera de initiala komponenterna för att ansluta till Adobe Experience Platform Edge Network
1. Uppdatera den grundläggande implementeringen för att ersätta at.js med Platform Web SDK
1. Förbättra implementeringen av Platform Web SDK för dina specifika användningsfall. Detta kan innebära att ytterligare parametrar skickas, att enstaka SPA (app) visas, att svarstoken används och mycket annat.
1. Uppdatera objekt i Target-gränssnittet, till exempel profilskript, aktiviteter och målgruppsdefinitioner
1. Validera den slutliga implementeringen innan du byter i produktionsmiljön

## Viktiga skillnader mellan at.js och Platform Web SDK

Innan du startar migreringsprocessen är det viktigt att förstå skillnaderna mellan at.js och Platform Web SDK.

### Operativa skillnader

Platform Web SDK kombinerar funktionaliteten hos flera Adobe-program i ett enda bibliotek. Detta enhetliga tillvägagångssätt innebär att ni bör överväga ansvar och processer mellan team för att säkerställa en bra implementering.

|  | Mål at.js 2.x | Platform Web SDK |
|---|---|---|
| Ägarskap | at.js-biblioteket är oberoende av andra programbibliotek. Anpassningar och ägarskap av dessa olika bibliotek kan anpassas efter olika team i organisationen. | Plattformsbiblioteket Web SDK och de data som skickas är enhetliga för alla Adobe-program. Ägarskapet för implementeringen av Platform Web SDK bör representera intressenter för alla program längre fram i kedjan. |
| Underhåll | Separata team kan arbeta med implementeringsförbättringar för varje Adobe-program, som Target och Analytics. | Helst ska ett team ansvara för förbättringar som påverkar implementeringen av Platform Web SDK. |
| Process | Ändringar i en Target-implementering kan följa en process som har en annan inriktning eller QA-krav än andra program som Analytics. | Ändringar av en plattformsbaserad Web SDK-implementering bör omfatta alla program längre fram i kedjan, och QA- och publiceringsprocessen bör anpassas därefter. |
| Samarbete | Data som är specifika för Target kan skickas direkt i Target-anropen. Beroende på implementeringen kan det finnas ytterligare Target-anrop. Detta har ingen direkt inverkan på Adobe Analytics data och samordningen med analysteamet är inte så viktig. | Data som skickas i Platform Web SDK-anrop kan vidarebefordras till både Target och Analytics. Samordning mellan grupper krävs för att säkerställa att ändringar inte påverkar en viss tillämpning negativt. |

### Tekniska skillnader

Platform Web SDK är inte en utveckling av Target at.js-biblioteket. Det är en ny och enhetlig metod för att implementera alla Adobe-program för webbkanalen. Det finns flera tekniska skillnader att vara medveten om.

|  | Mål at.js 2.x | Platform Web SDK |
|---|---|---|
| Biblioteksfunktioner | Målfunktioner från at.js. Integrering med andra program från Visitor.js och AppMeasurement.js | Funktioner för alla Adobe-program som tillhandahålls av ett enda plattformsbibliotek för Web SDK: alloy.js |
| Prestanda | at.js är ett av flera bibliotek som måste läsas in för korrekt integrering mellan program. Detta resulterar i mindre än den optimala inläsningstiden. | Platform Web SDK är ett enda lättviktsbibliotek som eliminerar behovet av flera programspecifika bibliotek, vilket ger bättre sidladdningsprestanda. |
| Begäranden | Separata anrop för varje Adobe-program. Målsamtal är i stort sett oberoende av andra nätverksanrop. | Samtal för alla Adobe-program. Ändringar av data som skickas i dessa anrop kan påverka flera program längre fram i kedjan. |
| Läs in ordning | För en korrekt integrering med andra Adobe-program krävs en särskild inläsningsordning för bibliotek och nätverksanrop. | Korrekt integrering kräver inte att du sammanfogar data från olika programspecifika nätverksanrop, och därför behöver du inte bekymra dig om inläsningsordningen. |
| Edge Network | Använder Adobe Experience Cloud Edge Network (tt.omtrdc.net), eventuellt med en CNAME som är specifik för Target. | Använder Adobe Experience Platform Edge-nätverket (edge.adobedc.net), eventuellt tillsammans med en enda CNAME. |
| Grundläggande terminologi | at.js-namngivning: <br> - `mbox` <br> - `pageLoad` event (global mbox) <br> - `offer` | SDK-motsvarighet för plattform: <br> - `decisionScope` <br> - `__view__` DecisionScope <br> - `proposition` |

### Videoöversikt

I följande video visas en översikt över Adobe Experience Platform Web SDK och Adobe Experience Platform Edge Network.

>[!VIDEO](https://video.tv.adobe.com/v/34141/?quality=12&learn=on)

Nu när du förstår skillnaderna på hög nivå mellan at.js och Platform Web SDK kan du [planera migreringen](plan-migration.md).

>[!NOTE]
>
>Vi vill hjälpa dig att lyckas med målmigreringen från at.js till Web SDK. Om du stöter på problem med din migrering eller känner att det saknas viktig information i den här guiden ber vi dig att meddela oss genom att publicera i [den här communitydiskussionen](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).