---
title: Spåra konverteringshändelser - Migrera Adobe Target-implementeringen i din mobilapp till Adobe Journey Optimizer - Beslutstillägg
description: Lär dig hur du spårar konverteringshändelser för Adobe Target med tillägget Adobe Journey Optimizer - Bestämning av mobilenheter
exl-id: 7b53aab1-0922-4d9f-8bf0-f5cf98ac04c4
source-git-commit: d2da62ed2d36f73af1c8053be5af27feea32cb14
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---

# Spåra konverteringshändelser med mobiltillägget Decisioning

Målet med de flesta Target-aktiviteter är att driva värdefulla användaråtgärder i programmet, som inköp, registrering, klick med mera. Målimplementeringar använder ofta anpassade konverteringshändelser för att spåra dessa åtgärder, som ofta innehåller ytterligare information om konverteringen. Konverteringshändelser för Target kan spåras med Optimize SDK som liknar Target SDK. Specifika API:er måste anropas för att spåra konverteringshändelser enligt tabellen nedan:

| Aktivitetsmål | Måltillägg | Beslutstillägg |
|---|---|---|
| Spåra en visningskonverteringshändelse för en mbox-plats (scope) | Anropa API:t [displayedLocations](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#displayedlocations){target=_blank} när mbox-platsen visas | Anropa API:t [som visas](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#proposition-tracking-using-direct-offer-class-methods){target=_blank} när erbjudandet för mbox-platsen visas. Detta skickar en händelse med händelsetypen decisioning.propositionDisplay till Experience Edge-nätverket. **Detta är nödvändigt för att öka antalet besökare i dina Target-aktiviteter och måste göras när du levererar både vanliga och standarderbjudanden för Target.** |
| Spåra en klickkonverteringshändelse för en mbox-plats (scope) | Anropa API:t [clichedLocations](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#displayedlocations){target=_blank} när användaren klickar på mbox-platsen | Anropa API:t för [appade](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#proposition-tracking-using-direct-offer-class-methods){target=_blank} när användaren klickar på erbjudandet för mbox-platsen. Detta skickar en händelse med händelsetypen decisioning.propositionInteract till Experience Edge-nätverket. |
| Spåra en anpassad konverteringshändelse som även kan innehålla ytterligare data, till exempel parametrar för målprofilen och orderdetaljer | Skicka ytterligare data i fältet TargetParameters som tillhandahålls av API:erna [displayedLocations](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#displayedlocations){target=_blank} och [clickings](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#displayedlocations){target=_blank} | Använd de publika metoderna [generateDisplayInteractionXdm](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#proposition-tracking-using-edge-extension-api){target=_blank} och [generateTapInteractionXdm](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#proposition-tracking-using-edge-extension-api){target=_blank} som är tillgängliga i erbjudandet för mbox-platsen för att generera XDM-formaterade data för visning respektive klicka. Anropa sedan Edge SDK [sendEvent](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#sendevent){target=_blank}-API:t för att skicka XDM-spårningsdata tillsammans med eventuella ytterligare XDM-data och frihandsdata till Experience Edge-nätverket. |


Lär dig sedan [uppdatera målgrupper och profilskript](update-audiences.md) för att säkerställa kompatibilitet med beslutstillägget.

>[!NOTE]
>
>Vi strävar efter att hjälpa dig att lyckas med din migrering av mobilmål från måltillägget till beslutstillägget. Om du stöter på problem med din migrering eller om du känner att det saknas viktig information i den här guiden kan du meddela oss genom att publicera [den här communitydiskussionen](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
