---
title: Inledande konfiguration - Migrera mål från at.js 2.x till Web SDK
description: Lär dig mer om och konfigurera viktiga grundläggande element som krävs för implementeringen av Platform Web SDK
exl-id: dbf9683b-1cfc-474a-9c38-432cad4d1533
source-git-commit: d4308b68d6974fe47eca668dd16555d15a8247c9
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---

# Utför den första datainsamlingsinställningen

Migrering från at.js till Platform Web SDK kräver en första konfiguration för att möjliggöra korrekt datainhämtning, funktioner och funktioner för Platform Web SDK. Följande steg från [implementeringsjälvstudiekursen för Web SDK för plattformen](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=sv-SE) måste slutföras innan några webbplatsimplementeringsändringar görs:

- [Konfigurera lämpliga behörigheter](https://experienceleague.adobe.com/sv/docs/platform-learn/implement-web-sdk/overview#prerequisites){target="_blank"} i Adobe Admin Console för datainsamling
- [Konfigurera ett XDM-schema](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-schemas.html?lang=sv-SE){target="_blank"} för att skicka strukturerade data till Edge Network
- [Konfigurera ett identitetsnamnområde](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-identities.html?lang=sv-SE){target="_blank"} för enhetspersonalisering och funktionen mbox3rdPartyId
- [Skapa en datastream](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-datastream.html?lang=sv-SE){target="_blank"} för att aktivera vidarebefordran av data från Edge Network
- [Konfigurera datastream](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html?lang=sv-SE#configure-the-datastream){target="_blank"} för att aktivera vidarebefordran av data till Adobe Target

>[!CAUTION]
>
>Kom ihåg att dessa designaspekter bör samordnas i alla Target-, Analytics- och Audience Manager-migreringar.

När den inledande konfigurationen är klar bör Target-funktionen aktiveras med Adobe Experience Platform Edge Network.

Lär dig sedan [ersätta at.js-biblioteket och konfigurera en grundläggande SDK-implementering för plattformen](replace-library.md).

>[!NOTE]
>
>Vi vill hjälpa dig att lyckas med målmigreringen från at.js till Web SDK. Om du stöter på problem med din migrering eller om du känner att det saknas viktig information i den här guiden kan du meddela oss genom att publicera [den här communitydiskussionen](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587?profile.language=sv#M463).
