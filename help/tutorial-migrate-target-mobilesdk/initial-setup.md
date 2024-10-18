---
title: Inledande konfiguration - Migrera från Adobe Target till Adobe Journey Optimizer - mobiltillägg för beslut
description: Lär dig mer om och konfigurera viktiga grundläggande element som krävs för implementeringen av Platform Web SDK
source-git-commit: afbc8248ad81a5d9080a4fdba1167e09bbf3b33d
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# Utför den första datainsamlingsinställningen

Migrering från at.js till Platform Web SDK kräver en första konfiguration för att möjliggöra korrekt datainhämtning, funktioner och funktioner för Platform Web SDK. Följande steg från [implementeringsjälvstudiekursen för Web SDK för plattformen](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html) måste slutföras innan några webbplatsimplementeringsändringar görs:

- [Konfigurera lämpliga behörigheter](https://experienceleague.adobe.com/en/docs/platform-learn/implement-web-sdk/overview#prerequisites){target="_blank"} i Adobe Admin Console för datainsamling
- [Konfigurera ett XDM-schema](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-schemas.html){target="_blank"} för att skicka strukturerade data till Edge Network
- [Konfigurera ett identitetsnamnområde](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-identities.html){target="_blank"} för enhetspersonalisering och funktionen mbox3rdPartyId
- [Skapa en datastream](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-datastream.html){target="_blank"} för att aktivera vidarebefordran av data från Edge Network
- [Konfigurera datastream](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html#configure-the-datastream){target="_blank"} för att aktivera vidarebefordran av data till Adobe Target

>[!CAUTION]
>
>Kom ihåg att dessa designaspekter bör samordnas i alla Target-, Analytics- och Audience Manager-migreringar.

När den inledande konfigurationen är klar bör Target-funktionen aktiveras med Adobe Experience Platform Edge Network.

Lär dig sedan [ersätta at.js-biblioteket och konfigurera en grundläggande SDK-implementering för plattformen](replace-library.md).

>[!NOTE]
>
>Vi strävar efter att hjälpa dig att lyckas med din migrering av mobilmål från måltillägget till beslutstillägget. Om du stöter på problem med din migrering eller om du känner att det saknas viktig information i den här guiden kan du meddela oss genom att publicera [den här communitydiskussionen](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
