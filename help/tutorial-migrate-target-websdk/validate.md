---
title: Validera målimplementeringar med Web SDK - migrera mål från at.js 2.x till Web SDK
description: Lär dig validera aktiviteter och felsöka en Adobe Target-implementering med Adobe Experience Platform Web SDK.
exl-id: 09b4ebeb-fae9-470d-8ea9-f6e3c7d7da5e
source-git-commit: d4308b68d6974fe47eca668dd16555d15a8247c9
workflow-type: tm+mt
source-wordcount: '1093'
ht-degree: 0%

---

# Validera implementeringen av Platform Web SDK

När du har migrerat din Target-implementering från at.js till Platform Web SDK är det viktigt att validera att allt fungerar som det ska innan du publicerar några ändringar på produktionsplatsen. Adobe rekommenderar följande, som beskrivs utförligt på denna sida:

* Genomför en teknisk validering för att säkerställa att den grundläggande implementeringen och Platform Web SDK-begäranden och -svar ser korrekta ut
* Se till att Target-aktiviteter levereras och återges korrekt
* Kontrollera att rapportering fungerar som den ska
* Besök målgrupper och profilskript för att kontrollera att de är kompatibla med Platform Web SDK
* Säkerställ att integreringen med Adobe eller program från tredje part fungerar korrekt

Alla Target-implementeringar skiljer sig åt beroende på webbplatsens arkitektur och vilka funktioner som används. Du kan använda tabellerna nedan som utgångspunkt och lägga till objekt som är unika för implementeringen. På sidan [Felsökning](debugging.md) i den här självstudiekursen visas verktyg som du kan använda för att utföra den här valideringen.

## Teknisk validering

| Valideringsobjekt | Anteckningar |
|---|---|
| At.js-fragmentet som döljer koden finns inte längre på sidan | SDK för plattformswebben tar inte automatiskt bort formatet med ID `at-body-style`. Om du lämnar det här gamla fragmentet på sidan kommer dolt innehåll att visas tills fragmentets timeout nås. |
| At.js-biblioteket finns inte längre på sidan | Kontrollera att det inte finns något adobe.target-objekt i webbläsarens verktygskonsol för utvecklare. Om du inkluderar både Platform Web SDK och at.js resulterar det i oönskat återgivningsbeteende |
| Förväntade parametrar finns i XDM och dataobjekt i `sendEvent`-begäran | |
| Recommendations-katalogen uppdateras som förväntat om sidbegäranden används för att fylla i katalogen | |
| Profilparametrar har skickats till Target | Visa Edge-spår i Felsökning |
| Parametrar som är mappade till XDM i datastream-mapparen skickas korrekt till Target | Validera med Edge Trace-funktionen i Felsökning och/eller Assurance |
| Målinnehållet returneras i tillämpliga `sendEvent` svar | Förväntades när alternativet `renderDecisions` har angetts till `true` eller omfattningar har begärts och användaren kvalificerar sig för en viss målaktivitet |
| En `decisioning.propositionDisplay`-händelse utlöses efter att VEC-baserade aktiviteter återger | Aktiviteter som återges automatiskt och on demand förväntas ha separata händelseanrop |
| En `decisioning.propositionDisplay`-händelse utlöses efter att formulärbaserade aktiviteter återger | Gäller endast vissa implementeringar. Kräver anpassad kod för att köra det här anropet. |
| En `decisioning.propositionDisplay`-händelse utlöses när ett erbjudande tillämpas på en SPA | Gäller endast för SPA implementeringar |
| En `decisioning.propositionDisplay`-händelse utlöses INTE när en SPA återger för en viss vy | Gäller endast för SPA implementeringar |
| En `decisioning.propsitionInteract`-händelse utlöses efter en aktivitetskonvertering | De&quot;klickade på ett element&quot; och anpassade konverteringar som migrerats från at.js `trackEvent` eller `sendNotifications` förväntas ha separata händelseanrop |
| Svarstoken returneras i svaret `sendEvent` och har förväntade värden | Svarstoken ska fungera normalt med Web SDK |
| ECID:n är konsekventa på alla sidor med Web SDK och at.js | Gäller för sidvis migrering. Omdirigeringserbjudanden förväntas inte fungera i den här typen av migreringar |


## Leverans och rendering av aktivitet

| Valideringsobjekt | Anteckningar |
|---|---|
| VEC-baserade aktiviteter återges korrekt vid sidinläsning | Det är bäst att validera både anpassade kodändringar och grundläggande ändringar som att ordna om element eller ersätta text |
| VEC-baserade aktiviteter återges korrekt SPA visningsändringar | Gäller endast för SPA implementeringar |
| Formulärbaserade aktiviteter återges korrekt | Gäller endast vissa implementeringar. Återgivning av formulärbaserade aktiviteter kräver en anpassad kod som liknar at.js. |
| Aktiviteter som använder omdirigeringar fungerar korrekt | Omdirigeringar stöds om både käll- och målsidan använder Platform Web SDK. En Target-omdirigering från en at.js-sida till en Platform Web SDK-sida eller tvärtom stöds inte. |
| Aktiviteter som använder fjärrerbjudanden fungerar korrekt | Inte vanligt, kontrollera ert Target-erbjudande för fjärrerbjudanden |
| Flimmer har reducerats på rätt sätt | Flimmerhantering är valfri, men se till att eventuella begränsningsåtgärder som du har gjort fungerar som förväntat för optimala sidprestanda och användarupplevelser |
| QA-länkar fungerar som förväntat | Om den inte fungerar kontrollerar du att web.webPageDetails.URL:en exakt matchar URL:en i webbläsaren |
| Alla de vanligaste erbjudandetyperna återges som förväntat |  |

## Rapportering

| Valideringsobjekt | Anteckningar |
|---|---|
| Besökarna kan hänföras till VEC-baserad verksamhet | Det är bäst att validera rapporteringsfunktionen som förväntat för både sidladdningsändringar och SPA |
| Besökare kan hänföras till formulärbaserade aktiviteter | Beroende på vilken återgivningsmetod som används kan din implementering kräva anpassad kod för att köra en `decisioning.propositionDisplay`-händelse |
| Målen för standardkonverteringen hämtas korrekt | Gäller antingen Target eller Analytics som rapportkälla |
| Orderkonverteringar och detaljer registreras korrekt | Kontrollera revideringsrapporten |
| Klickspårningskonverteringar spelas in korrekt |  |
| Anpassade konverteringsmål hämtas korrekt | Konverteringsmål har till exempel migrerats från at.js `trackEvent` eller `sendNotifications` som ofta används med målet &quot;visade en mbox&quot; |

## Publiker och profilskript

| Valideringsobjekt | Anteckningar |
|---|---|
| Målgrupper som används i live-aktiviteter är kompatibla med Platform Web SDK | Målgrupper som använder komponenten &quot;Custom&quot; (parametern mbox) måste uppdateras för att inkludera XDM-attribut |
| Alla profilskript är kompatibla med Platform Web SDK | Alla profilskript som använder mbox-parametrar måste uppdateras för att inkludera XDM-attribut |
| Verksamheter som returneras för målgrupper | Det är bäst att utföra en komplett validering på de målgrupper du ändrar för att bli kompatibel med Platform Web SDK |
| Profilskript utvärderas som förväntat | Visa Edge-spår i Felsökning |

## Integrering med Adobe-program

| Valideringsobjekt | Anteckningar |
|---|---|
| Avkastning av aktiviteter för Experience Cloud-målgrupper | Ett segment som publicerats från Adobe Analytics |
| Avkastning av aktiviteter för Experience Platform-målgrupper | Gäller endast om du har en licens för ett Experience Platform-baserat program som RTCDP |
| Avkastning av aktiviteter för Audience Manager-målgrupper | Ett segment som t.ex. bygger på besök på en viss sida |
| Målaktivitetsdata visas i Analysis Workspace | Gäller aktiviteter som använder Adobe Analytics som rapportkälla |

## Integrering med tredjepartsprogram

| Valideringsobjekt | Anteckningar |
|---|---|
| Svarstokendata skickas korrekt till tredjepartsprogram | Integreringsmetoderna kan variera, men en vanlig metod är att använda Target-svarstoken för att skicka aktivitets- och upplevelseinformation till andra analysverktyg som Google Analytics |
| Information från tredje part skickas som antingen XDM eller profildata | All relevant information från tredje part ska skickas i `sendEvent` anrop till Target |

När du har utfört valideringsstegen ovan kan du vara säker på att implementeringen av Platform Web SDK är klar att gå över till produktion.

Läs sedan om hur du [felsöker en målistimplementering med hjälp av Platform Web SDK](debugging.md).

>[!NOTE]
>
>Vi vill hjälpa dig att lyckas med målmigreringen från at.js till Web SDK. Om du stöter på problem med din migrering eller om du känner att det saknas viktig information i den här guiden kan du meddela oss genom att publicera [den här communitydiskussionen](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
