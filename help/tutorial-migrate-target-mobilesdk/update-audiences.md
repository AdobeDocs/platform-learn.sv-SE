---
title: Uppdatera målgrupper och profilskript - Migrera Target från at.js 2.x till Web SDK
description: Lär dig hur du uppdaterar Adobe Target målgrupper och profilskript för kompatibilitet med Experience Platform Web SDK.
source-git-commit: 009548969b88d1bfa6eac23f65b1ca2144f27c34
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# Uppdatera målgrupper och profilskript för kompatibilitet med Platform Web SDK


## Justera målgrupper


Mer information och bästa praxis finns i den dedikerade dokumentationen om [profilskript](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html).

## Uppdatera parametertoken för dynamiskt innehåll



Om du väljer att göra justeringar efter migreringen för att ta hänsyn till de nya parameternamnen för XDM-mbox ska du se till att pausa alla aktiviteter som påverkas under migreringshändelsen för att förhindra aktivitetsvisningsfel för besökarna.

Läs sedan om hur du [validerar målimplementeringen](validate.md).

>[!NOTE]
>
>Vi vill hjälpa dig att lyckas med din migrering av mobilmål från måltillägget till optimeringstillägget. Om du stöter på problem med din migrering eller om du känner att det saknas viktig information i den här guiden kan du meddela oss genom att publicera [den här communitydiskussionen](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
