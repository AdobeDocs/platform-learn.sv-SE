---
title: Foundation - Installation av Adobe Experience Platform Data Collection och Web SDK-tillägget - förklarar Adobe Experience Platform Data Collection
description: Foundation - Installation av Adobe Experience Platform Data Collection och Web SDK-tillägget - förklarar Adobe Experience Platform Data Collection
kt: 5342
doc-type: tutorial
source-git-commit: 7d2f5f842559b2d6d9f115f3993268a4b36a0fe0
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---

# 1.1.1 Förstå Adobe Experience Platform datainsamling

## Kontext

Adobe Experience Platform Data Collection används av varumärken för ett antal användningsområden. Det är nästa generation av Tag Management System (TMS) som ger kunderna ett enkelt sätt att driftsätta och hantera alla analyser-, marknadsförings- och annonslösningar som behövs för att driva relevanta kundupplevelser. Adobe Experience Platform Data Collection kostar inget och kan köpas av alla Adobe Experience Cloud-kunder. Ett varumärke kan använda Adobe Experience Platform Data Collection för att

- Implementera både Adobe Experience Cloud och Adobe Experience Platform.
- Hantera de olika kraven för olika delar av organisationen genom att ge var och en en en egen **Property** att hantera.
- Tillåt testning och livscykelhantering.
- Lägg in egna javascript- och tredjepartstaggar, som alla hanteras på ett och samma ställe.

## Utforska användargränssnittet

Gå till [Adobe Experience Platform datainsamling](https://experience.adobe.com/#/data-collection/).

Gå till **Taggar**. Du ser nu vyn **[!UICONTROL Properties]**. Egenskaper som anges här är till för självstudiekurshantering. Dessa egenskaper representerar..

- App- och webbegenskaper
- Olika webbplatser ger kunderna olika service på olika sätt. Exempel: Luma Retail har en egenskap, Luma Travel har en annan
- Äldre såväl som aktuella webbplatser
- En specifik Adobe Analytics-design som är gemensam för flera olika webbplatser
- Interna intranätsidor bredvid externa platser

![Starta egenskapsvyn](./images/launch1.png)

Ta en titt på den vänstra listen.

![Starta vänster järnväg](./images/launch2.png)

- **[!UICONTROL Tags]** ger en översikt över alla egenskaper på klientsidan
- **[!UICONTROL App Surfaces]** ger en översikt över alla appkonfigurationer för att aktivera push-meddelanden (som används/aktiveras i kombination med Project Sierra)
- **[!UICONTROL Datastreams]** utforskas i [nästa övning](./ex2.md)
- **[!UICONTROL Event Forwarding]** ger en översikt över alla egenskaper på serversidan som utforskas i [Modul 14 - Real-Time CDP-anslutningar: Händelsevidarebefordran](./../../../modules/rtcdp-b2c/module2.5/aep-data-collection-ssf.md)

## Ytterligare information

Adobe Experience Platform Data Collection är ett mycket avancerat verktyg som omfattar mer än bara en självstudiekurs från Adobe Experience Platform. Organisationer kanske inte använder Adobe Experience Platform Data Collection för sina tagghanteringsfunktioner, utan använder tagghanteringslösningar som inte är Adobe för att mata in kod och hantera taggar. Det finns stöd för att använda tagghanteringslösningar som inte är Adobe i från Adobe och Adobe Professional Services.
Nedan finns ytterligare information för dem som är intresserade av att förstå Adobe Experience Platform Data Collection.

- [Användarhandbok för Adobe Experience Platform Data Collection](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=sv)
- [Implementera Adobe Experience Cloud med Web SDK, genomgång](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html)
- [Konfigurera användarbehörigheter](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html)
- [API-dokumentation](https://developer.adobelaunch.com/api/)

Nästa steg: [1.1.2 Edge Network, datastreams och datainsamling på serversidan](./ex2.md)

[Gå tillbaka till modul 1.1](./data-ingestion-launch-web-sdk.md)

[Gå tillbaka till Alla moduler](./../../../overview.md)
