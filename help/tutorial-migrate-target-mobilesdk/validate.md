---
title: Validera och felsöka implementeringen av beslutstillägg
description: Lär dig hur du validerar och felsöker en mobilimplementering från Adobe Target med hjälp av beslutstillägget.
exl-id: edc6e25a-58d7-4145-97c3-bf48e980914f
source-git-commit: a4fe85580776e5d84f6deaf3c0224f0513ba8415
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# Validera och felsöka implementeringen av beslutstillägg

När du har migrerat målinsimplementeringen från måltillägget till beslutandetillägget är det viktigt att du validerar att allt fungerar som det ska innan du publicerar några ändringar i produktionsappen. Adobe rekommenderar följande, som beskrivs utförligt på denna sida:

* Genomför en teknisk validering för att säkerställa att den grundläggande implementeringen och förfrågningar och svar från SDK på Platform Mobile ser korrekta ut
* Se till att Target-aktiviteter levereras och återges korrekt
* Kontrollera att rapportering fungerar som den ska
* Besök målgrupper och profilskript för att kontrollera att de är kompatibla med Platform Mobile SDK och Optimie-tillägget
* Säkerställ att integreringen med Adobe eller tredjepartsprogram fungerar som den ska

Alla Target-implementeringar skiljer sig åt beroende på webbplatsens arkitektur och vilka funktioner som används. Du kan använda tabellerna nedan som utgångspunkt och lägga till objekt som är unika för implementeringen.

## Teknisk validering och felsökning

Teknisk validering och felsökning med Platform Mobile SDK och beslutstillägget har förbättrats avsevärt med Assurance. Läs följande dokumentationssidor om du vill veta mer om det här viktiga verktyget:

* [Konfigurera beslutsplugin-program i Assurance](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/assurance-setup/){target=_blank}

* [Validerar SDK-inställningar](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/optimize-configuration-view/){target=_blank}

* [Granska begäranden och simulera olika upplevelser](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/review-simulate/){target=_blank}

När du har utfört valideringsstegen ovan kan du vara säker på att implementeringen av Platform Mobile SDK med beslutstillägget är klar att gå över till produktion.

Grattis, du har kommit till slutet av självstudiekursen! Lycka till med att migrera din Adobe Target-implementering till beslutstillägget!

>[!NOTE]
>
>Vi strävar efter att hjälpa dig att lyckas med din migrering av mobilmål från måltillägget till beslutstillägget. Om du stöter på problem med din migrering eller om du känner att det saknas viktig information i den här guiden kan du meddela oss genom att publicera [den här communitydiskussionen](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
