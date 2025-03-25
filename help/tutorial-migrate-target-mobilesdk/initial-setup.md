---
title: Inledande konfiguration - Migrera Adobe Target-implementeringen i din mobilapp till Adobe Journey Optimizer - Beslutstillägg
description: Läs mer om och konfigurera de grundläggande element som krävs för implementeringen av SDK på webben på din plattform
exl-id: dfc5abc8-0e79-454a-b1bb-6a42b1219771
source-git-commit: 45a47cde8bb5ac3baba24d7527fc4029ca3d6596
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 1%

---

# Utför den första datainsamlingsinställningen

Att migrera från Target SDK till Optimize SDK kräver en första konfiguration för att möjliggöra korrekt datainhämtning, funktioner och funktioner i Optimize SDK. Följande steg måste slutföras innan implementeringen av webbplatsen kan ändras:

- [Konfigurera lämpliga behörigheter](https://experienceleague.adobe.com/en/docs/platform-learn/implement-web-sdk/overview#permissions){target="_blank"} i Adobe Admin Console för datainsamling
- [Konfigurera ett XDM-schema](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/initial-configuration/create-schema){target="_blank"} för att skicka strukturerade data till Edge Network
- [Konfigurera schemat](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/experience-cloud/target#update-your-schema){target="_blank"} för att ta emot Adobe Target-data
- [Konfigurera ett identitetsnamnområde](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/app-implementation/identity#set-up-a-custom-identity-namespace){target="_blank"} för enhetspersonalisering och funktionen mbox3rdPartyId
- [Skapa en datastream](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/initial-configuration/create-datastream){target="_blank"} för att aktivera vidarebefordran av data från Edge Network
- [Konfigurera datastream](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/experience-cloud/target#update-datastream-configuration){target="_blank"} för att aktivera vidarebefordran av data till Adobe Target
- [Konfigurera taggegenskapen ](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/experience-cloud/target#install-adobe-journey-optimizer---decisioning-tags-extension){target="_blank"} för beslutstillägg

## Tilläggskonfiguration

>[!BEGINTABS]

>[!TAB Bestämmer tillägg]

Märkordstillägg som installeras när du använder tillägget Beslutsfattning:

1. Adobe Journey Optimizer - beslut
1. Adobe Experience Platform Edge Network
1. Mobile Core
1. Profil
1. Godkännande
1. Identitet
1. AEP Assurance (valfritt, krävs för felsökning)

![Tagga tillägg som installeras när du använder beslutstillägget](assets/tag-extensions-decisioning.png)

>[!TAB Måltillägg]

Märkordstillägg som installeras när du använder Target-tillägget:

1. Adobe Target
1. Mobile Core
1. Profil
1. Adobe Analytics (valfritt, krävs om Adobe Analytics används som rapportkälla för Adobe Target-aktiviteter)

![Märkordstillägg installeras när måltillägget används](assets/tag-extensions-target.png)

>[!ENDTABS]

## Datastream-konfiguration

Måltillägget har [konfigurerbara inställningar](https://developer.adobe.com/client-sdks/solution/adobe-target/#configure-the-target-extension-in-the-data-collection-ui) som med beslutstillägget är [konfigurerade i datastream](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#adobe-experience-platform-data-collection-setup).

| Måltillägg | Beslutstillägg | Anteckningar |
| --- | --- | --- | 
| Klientkod | n/a | Ange automatiskt efter kanten med hjälp av IMS-organisationsinformationen |
| Miljö-ID | Målmiljö-ID | Konfigurerad i datastream |
| Ange Workspace-egenskap | Egenskapstoken | Konfigurerad i datastream |
| Timeout | Timeout | Kan konfigureras i beslutstillägget och i Optimera SDK. Standardtidsgränsen är 10 sekunder. |
| Serverdomän | Edge Network | Ange i Adobe Experience Platform Edge Network-tillägget |

Läs sedan om hur du [ersätter SDK](replace-sdk.md).

>[!NOTE]
>
>Vi strävar efter att hjälpa dig att lyckas med din migrering av mobilmål från måltillägget till beslutstillägget. Om du stöter på problem med din migrering eller om du känner att det saknas viktig information i den här guiden kan du meddela oss genom att publicera [den här communitydiskussionen](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
