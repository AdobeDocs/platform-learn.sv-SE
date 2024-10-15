---
title: Planering - Migrera mål i mobilappar från måltillägget till optimeringstillägget
description: Lär dig planera Adobe Target-implementeringen från at.js 2.x till Adobe Experience Platform Web SDK.
source-git-commit: 009548969b88d1bfa6eac23f65b1ca2144f27c34
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 0%

---

# Planera målmigreringen till tillägget Optimera

Innan du uppgraderar Target från Target-tillägget till Optimera-tillägget i din mobilapp bör du utvärdera den aktuella implementeringen.

## Utvärdera aktuell implementering av måltillägg

Det första steget mot en framgångsrik migrering är att ha en god förståelse för den aktuella implementeringen av måltillägget. Det finns funktioner, funktioner och anpassad kod som du kan använda och som behöver uppdateras. Tänk på följande när du utvärderar:

### Vilka funktioner stöds?

<!--Platform Web SDK is under continuous active development and features and enhancements are added regularly. As you evaluate your current at.js implementation, refer to the [supported use cases](https://github.com/orgs/adobe/projects/18/views/1) page for the latest information.-->

### Vilka funktioner använder du idag?

<!--Platform Web SDK is a new library that consolidates all Adobe solutions for the websites into a single SDK. This enables tighter integration and enables new capabilities unique to Adobe Experience Platform. However, this also means at.js functions are not backwards compatible with Platform Web SDK. As you evaluate your current implementation, make note of the following:

- at.js functions such as `getOffer()` and `applyOffer()`
- Modifications to Target's global settings
- Integration with Adobe Analytics
- Use of a flicker mitigation script
- Use of response tokens
- Use of mbox, profile, and entity parameters
- Custom code unique to your implementation-->

### Vilken migreringsstrategi tänker du använda?

<!--Once you have revisited your at.js implementation, you need to determine a migration approach. There are two options:

- Migrate all Adobe applications at once across the entire site
- Migrate on a page-by-page basis

Because Platform Web SDK combines and enables multiple Adobe applications, you must coordinate the Target migration of other Adobe applications like Analytics and Audience Manager. All Adobe libraries on a given page should be migrated at the same time. A mixed implementation of Platform Web SDK for Target and AppMeasurement for Analytics on a particular page is not supported. However, a mixed implementation across different pages is supported, for example Platform Web SDK on page A, and at.js with AppMeasurement on page B.

As you migrate, you should plan on following your company's process for testing and releasing new code and use things like development, qa, and staging environments before you release to production.-->

<!--
>[!CAUTION]
>
>Redirect offers are not supported in page-by-page migrations if redirecting from a page with one library to a page with a different library
-->


Granska sedan den detaljerade [jämförelsen av måltillägget och Optimera-tillägget](detailed-comparison.md) för att få en bättre förståelse för de tekniska skillnaderna och identifiera områden som kräver ytterligare fokus.

>[!NOTE]
>
>Vi vill hjälpa dig att lyckas med din migrering av mobilmål från måltillägget till optimeringstillägget. Om du stöter på problem med din migrering eller om du känner att det saknas viktig information i den här guiden kan du meddela oss genom att publicera [den här communitydiskussionen](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
