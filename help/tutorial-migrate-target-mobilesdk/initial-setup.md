---
title: Inledande konfiguration - Migrera från Adobe Target till Adobe Journey Optimizer - mobiltillägg för beslut
description: Läs mer om och konfigurera de grundläggande element som krävs för implementeringen av SDK på webben på din plattform
exl-id: dfc5abc8-0e79-454a-b1bb-6a42b1219771
source-git-commit: f3fd5f45412900dcb871bc0b346ce89108fa8913
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 1%

---

# Utför den första datainsamlingsinställningen

Att migrera från Target SDK till Optimize SDK kräver en första konfiguration för att möjliggöra korrekt datainhämtning, funktioner och funktioner i Optimize SDK. Följande steg måste slutföras innan implementeringen av webbplatsen kan ändras:

- [Konfigurera lämpliga behörigheter](https://experienceleague.adobe.com/en/docs/platform-learn/implement-web-sdk/overview#prerequisites){target="_blank"} i Adobe Admin Console för datainsamling
- [Konfigurera ett XDM-schema](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/initial-configuration/create-schema){target="_blank"} för att skicka strukturerade data till Edge Network
- [Konfigurera schemat](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/experience-cloud/target#update-your-schema) för att ta emot Adobe Target-data
- [Konfigurera ett identitetsnamnområde](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/app-implementation/identity#set-up-a-custom-identity-namespace){target="_blank"} för enhetspersonalisering och funktionen mbox3rdPartyId
- [Skapa en datastream](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/initial-configuration/create-datastream){target="_blank"} för att aktivera vidarebefordran av data från Edge Network
- [Konfigurera datastream](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/experience-cloud/target#update-datastream-configuration){target="_blank"} för att aktivera vidarebefordran av data till Adobe Target
- [Konfigurera taggegenskapen](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/experience-cloud/target#install-adobe-journey-optimizer---decisioning-tags-extension) för beslutstillägg

>[!BEGINTABS]

>[!TAB Måltillägg]

Märkordstillägg som installeras när du använder Target-tillägget:

1. Mobile Core
1. Profil
1. Adobe Target
1. Adobe Analytics (valfritt, krävs om Adobe Analytics används som rapportkälla för Adobe Target-aktiviteter)

![Märkordstillägg installeras när måltillägget används](assets/tag-extensions-target.png)


>[!TAB Bestämmer tillägg]

Märkordstillägg som installeras när du använder tillägget Beslutsfattning:

1. Mobile Core
1. Profil
1. Godkännande
1. Identitet
1. Adobe Experience Platform Edge Network
1. Adobe Journey Optimizer - beslut
1. AEP Assurance (valfritt, krävs för felsökning)

![Tagga tillägg som installeras när du använder beslutstillägget](assets/tag-extensions-decisioning.png)


>[!ENDTABS]

Lär dig sedan [ersätta at.js-biblioteket och konfigurera en grundläggande SDK-implementering för plattformen](replace-library.md).

>[!NOTE]
>
>Vi strävar efter att hjälpa dig att lyckas med din migrering av mobilmål från måltillägget till beslutstillägget. Om du stöter på problem med din migrering eller om du känner att det saknas viktig information i den här guiden kan du meddela oss genom att publicera [den här communitydiskussionen](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
