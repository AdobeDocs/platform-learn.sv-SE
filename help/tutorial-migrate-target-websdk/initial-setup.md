---
title: Inledande konfiguration | Migrera mål från at.js 2.x till Web SDK
description: Lär dig mer om och konfigurera viktiga grundläggande element som krävs för implementeringen av Platform Web SDK
source-git-commit: dad7a1b01c4313d6409ce07d01a6520ed83f5e89
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 0%

---

# Utför den första datainsamlingsinställningen

Migrering från at.js till Platform Web SDK kräver en första konfiguration för att möjliggöra korrekt datainhämtning, funktioner och funktioner för Platform Web SDK. Följande steg från [Implementering av SDK för plattform](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html) måste fyllas i innan några ändringar av webbplatsens implementering görs:

- [Konfigurera lämpliga behörigheter](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-permissions.html){target=&quot;_blank&quot;} i Adobe Admin Console för datainsamling
- [Konfigurera ett XDM-schema](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-schemas.html){target=&quot;_blank&quot;} för att skicka strukturerade data till Edge Network
- [Konfigurera ett identitetsnamnutrymme](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-identities.html){target=&quot;_blank&quot;} för enhetspersonalisering och funktionen mbox3rdPartyId
- [Skapa ett datastream](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/initial-configuration/configure-datastream.html){target=&quot;_blank&quot;} för att aktivera vidarebefordran av data från Edge Network
- [Konfigurera datastream](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html#configure-the-datastream){target=&quot;_blank&quot;} om du vill aktivera vidarebefordran av data till Adobe Target

>[!CAUTION]
>
>Kom ihåg att dessa designaspekter av Web SDK måste samordnas mellan Target-, Analytics- och Audience Manager-migreringar.

När den första konfigurationen är klar bör Target-funktionen aktiveras med Adobe Experience Platform Edge Network.

Lär dig sedan hur du [ersätta at.js-biblioteket och konfigurera en grundläggande SDK-implementering för plattformen](replace-library.md).

>[!NOTE]
>
>Vi vill hjälpa dig att lyckas med målmigreringen från at.js till Web SDK. Om du stöter på problem med din migrering eller känner att det saknas viktig information i den här guiden ber vi dig att meddela oss genom att publicera i [den här communitydiskussionen](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).
