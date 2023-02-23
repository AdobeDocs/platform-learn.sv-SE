---
title: Inledande konfiguration | Migrera mål från at.js 2.x till Web SDK
description: Lär dig mer om och konfigurera viktiga grundläggande element som krävs för implementeringen av Platform Web SDK
source-git-commit: 287ebcb275c4fca574dbd6cdf7e07ba4268bddb5
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# Utför den första datainsamlingsinställningen

Migrering från at.js till Platform Web SDK kräver en första konfiguration för att möjliggöra korrekt datainhämtning, funktioner och funktioner för Platform Web SDK. Följande steg från [Implementering av SDK för plattform](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html) måste fyllas i innan några ändringar av webbplatsens implementering görs:

- [Konfigurera lämpliga behörigheter](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-permissions.html){target="_blank"} i Adobe Admin Console for Data Collection
- [Konfigurera ett XDM-schema](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-schemas.html){target="_blank"} för att skicka strukturerade data till Edge Network
- [Konfigurera ett identitetsnamnutrymme](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-identities.html){target="_blank"} för personalisering på olika enheter och funktionen mbox3rdPartyId
- [Skapa ett datastream](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-datastream.html){target="_blank"} för att möjliggöra vidarebefordran av data från Edge Network
- [Konfigurera datastream](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html#configure-the-datastream){target="_blank"} för att möjliggöra överföring av data till Adobe Target

>[!CAUTION]
>
>Kom ihåg att dessa designaspekter bör samordnas i alla Target-, Analytics- och Audience Manager-migreringar.

När den första konfigurationen är klar bör Target-funktionen aktiveras med Adobe Experience Platform Edge Network.

Lär dig sedan hur du [ersätta at.js-biblioteket och konfigurera en grundläggande SDK-implementering för plattformen](replace-library.md).

>[!NOTE]
>
>Vi vill hjälpa dig att lyckas med målmigreringen från at.js till Web SDK. Om du stöter på problem med din migrering eller känner att det saknas viktig information i den här guiden ber vi dig att meddela oss genom att publicera i [den här communitydiskussionen](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
