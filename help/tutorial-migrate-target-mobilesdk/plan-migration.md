---
title: Planera migreringen - Migrera Adobe Target-implementeringen i din mobilapp till Adobe Journey Optimizer - Beslutstillägg
description: Lär dig mer om skillnaderna mellan at.js och Platform Web SDK och hur du planerar din migreringssatsning.
exl-id: 86849319-d2ad-4338-aa1a-d307d8807d4a
source-git-commit: b8baa6d48b9a99d2d32fad2221413b7c10937191
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---

# Planera migreringen

Hur stor insats du ska göra för att migrera från måltillägget till beslutstillägget beror på hur komplex din nuvarande implementering och vilka målfunktioner som används är.

Oavsett hur enkel eller komplex implementeringen är är det viktigt att du förstår ditt nuvarande läge fullständigt innan du migrerar. Den här guiden hjälper dig att bryta ned komponenterna i den aktuella implementeringen och utveckla en hanterbar plan för att migrera varje del.

Migreringsprocessen omfattar följande viktiga steg:

1. Utvärdera er nuvarande implementering och fastställa en migreringsstrategi
1. Konfigurera de inledande komponenterna för anslutning till Adobe Experience Platform Edge Network
1. Uppdatera den grundläggande implementeringen för att ersätta måltillägget med beslutstillägget
1. Förbättra SDK-implementeringen för dina specifika användningsfall. Detta kan innebära att ytterligare parametrar skickas, att svarstoken används med mera.
1. Uppdatera objekt i Target-gränssnittet, till exempel profilskript, aktiviteter och målgruppsdefinitioner
1. Validera den slutliga implementeringen innan du byter till produktionsappen

>[!INFO]
>
>I Adobe Experience Platform Mobile SDK-ekosystemet implementeras tillägg av SDK:er som importeras till dina program och som kan ha olika namn:
>
> * **Mål-SDK** implementerar **Adobe Target-tillägget**
> * **Optimera SDK** implementerar tillägget **Adobe Journey Optimizer - Bestämning**


Granska sedan den detaljerade [jämförelsen av måltillägget och beslutstillägget](detailed-comparison.md) för att få en bättre förståelse för de tekniska skillnaderna och identifiera områden som kräver ytterligare fokus.

>[!NOTE]
>
>Vi strävar efter att hjälpa dig att lyckas med din migrering av mobilmål från måltillägget till beslutstillägget. Om du stöter på problem med din migrering eller om du känner att det saknas viktig information i den här guiden kan du meddela oss genom att publicera [den här communitydiskussionen](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
