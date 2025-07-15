---
title: Inledande konfiguration - Migrera Adobe Target-implementeringen i din mobilapp till Offer Decisioning- och Target-tillägget
description: Läs mer om och konfigurera de grundläggande element som krävs för implementeringen av SDK på webben på din plattform
exl-id: dfc5abc8-0e79-454a-b1bb-6a42b1219771
source-git-commit: 876e664a213aec954105bf2d5547baab5d8a84ea
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 0%

---

# Utför den första datainsamlingsinställningen

Att migrera från Target SDK till Optimize SDK kräver en första konfiguration för att möjliggöra korrekt datainhämtning, funktioner och funktioner i Optimize SDK. Följande steg måste slutföras innan implementeringen av mobilappar kan ändras:

- [Konfigurera lämpliga behörigheter](https://experienceleague.adobe.com/sv/docs/platform-learn/implement-web-sdk/overview#permissions){target="_blank"} i Adobe Admin Console för datainsamling
- [Konfigurera ett XDM-schema](https://experienceleague.adobe.com/sv/docs/platform-learn/implement-mobile-sdk/initial-configuration/create-schema){target="_blank"} för att skicka strukturerade data till Edge Network
- [Konfigurera schemat](https://experienceleague.adobe.com/sv/docs/platform-learn/implement-mobile-sdk/experience-cloud/target#update-your-schema){target="_blank"} för att ta emot Adobe Target-data
- [Konfigurera ett ID-namnområde](https://experienceleague.adobe.com/sv/docs/platform-learn/implement-mobile-sdk/app-implementation/identity#set-up-a-custom-identity-namespace){target="_blank"} för anpassning av olika enheter och mbox3rdPartyId-funktioner
- [Skapa en datastream](https://experienceleague.adobe.com/sv/docs/platform-learn/implement-mobile-sdk/initial-configuration/create-datastream){target="_blank"} för att aktivera vidarebefordran av data från Edge Network
- [Konfigurera datastream](https://experienceleague.adobe.com/sv/docs/platform-learn/implement-mobile-sdk/experience-cloud/target#update-datastream-configuration){target="_blank"} för att aktivera vidarebefordran av data till Adobe Target
- [Konfigurera taggegenskapen](https://experienceleague.adobe.com/sv/docs/platform-learn/implement-mobile-sdk/experience-cloud/target#install-adobe-journey-optimizer---decisioning-tags-extension){target="_blank"} för tilläggen Offer Decisioning och Target

## Tilläggskonfiguration

>[!BEGINTABS]

>[!TAB Offer Decisioning- och Target-tillägg]

Märkordstillägg som installeras när tillägget Offer Decisioning och Target används:

1. Offer Decisioning och Target
1. Adobe Experience Platform Edge Network
1. Mobile Core
1. Profil
1. Godkännande
1. Identitet
1. AEP Assurance (tillval, krävs för felsökning)

![Märkordstillägg som installeras när tillägget Offer Decisioning och Target används](assets/tag-extensions-decisioning.png)

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

| Måltillägg | Offer Decisioning och Target | Anteckningar |
| --- | --- | --- | 
| Klientkod | n/a | Ange automatiskt efter kanten med hjälp av IMS-organisationsinformationen |
| Miljö-ID | Målmiljö-ID | Konfigurerad i datastream |
| Ange Workspace-egenskap | Egenskapstoken | Konfigurerad i datastream |
| Timeout | Timeout | Kan konfigureras i Offer Decisioning- och Target-tilläggen och i Optimera SDK. Standardtidsgränsen är 10 sekunder. |
| Serverdomän | Edge Network | Ange i Adobe Experience Platform Edge Network-tillägget |

Läs sedan om hur du [ersätter SDK](replace-sdk.md).

>[!NOTE]
>
>Vi vill hjälpa dig att lyckas med din migrering av mobilmål från Target-tillägget till Offer Decisioning- och Target-tillägget. Om du stöter på problem med din migrering eller om du känner att det saknas viktig information i den här guiden kan du meddela oss genom att publicera [den här communitydiskussionen](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-adobe-target-to-mobile-sdk-on-edge/m-p/747484#M625).
