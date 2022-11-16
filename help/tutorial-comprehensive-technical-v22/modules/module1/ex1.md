---
title: Foundation - Installation av Adobe Experience Platform Data Collection och Web SDK-tillägget - förklarar Adobe Experience Platform Data Collection
description: Foundation - Installation av Adobe Experience Platform Data Collection och Web SDK-tillägget - förklarar Adobe Experience Platform Data Collection
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: f498bb8c-659c-44b4-bb2e-36ea14640773
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 1%

---

# 1.1 Förstå Adobe Experience Platform datainsamling

## Kontext

Adobe Experience Platform Data Collection används av varumärken för ett antal användningsområden. Det är nästa generation av Tag Management System (TMS) som ger kunderna ett enkelt sätt att driftsätta och hantera alla analyser-, marknadsförings- och annonslösningar som behövs för att driva relevanta kundupplevelser. Adobe Experience Platform Data Collection kostar inget och kan köpas av alla Adobe Experience Cloud-kunder. Ett varumärke kan använda Adobe Experience Platform Data Collection för att

- Implementera både Adobe Experience Cloud och Adobe Experience Platform.
- Hantera de olika kraven för olika delar av organisationen genom att förse dem med sina egna **Egenskap** att hantera.
- Tillåt testning och livscykelhantering.
- Lägg in egna javascript- och tredjepartstaggar, som alla hanteras på ett och samma ställe.

## Utforska användargränssnittet

Gå till [Adobe Experience Platform Data Collection](https://experience.adobe.com/#/data-collection/).

Gå till **Taggar**. Nu ser du **[!UICONTROL Egenskaper]** vy. Egenskaper som anges här är till för självstudiekurshantering. Dessa egenskaper representerar..

- App- och webbegenskaper
- Olika webbplatser ger kunderna olika service på olika sätt. Exempel: Luma Retail skulle ha en egenskap, Luma Travel skulle ha en annan
- Äldre såväl som aktuella webbplatser
- En specifik Adobe Analytics-design som är gemensam för flera olika webbplatser
- Interna intranätsidor bredvid externa platser

![Visa egenskapsvyn](./images/launch1.png)

Ta en titt på den vänstra listen.

![Starta vänster tåg](./images/launch2.png)

- **[!UICONTROL Taggar]** ger en översikt över alla egenskaper på klientsidan
- **[!UICONTROL Appytor]** ger en översikt över alla appkonfigurationer för att aktivera push-meddelanden (som används/aktiveras i kombination med Project Sierra)
- **[!UICONTROL Datastreams]** utforskas i [nästa övning](./ex2.md)
- **[!UICONTROL Vidarebefordran av händelser]** ger en översikt över alla egenskaper på serversidan som utforskas i [Modul 14 - Real-Time CDP Connections: Vidarebefordran av händelser](../module14/aep-data-collection-ssf.md)

## Ytterligare information

Adobe Experience Platform Data Collection är ett mycket avancerat verktyg som omfattar mer än bara Adobe Experience Platform självstudiekurser. Organisationer kanske inte använder Adobe Experience Platform Data Collection för sina tagghanteringsfunktioner, utan använder tagghanteringslösningar som inte är Adobe för att mata in kod och hantera taggar. Det finns stöd för att använda tagghanteringslösningar som inte är Adobe i från Adobe och Adobe Professional Services.
Nedan finns ytterligare information för dem som är intresserade av att förstå Adobe Experience Platform Data Collection ytterligare.

- [Användarhandbok för Adobe Experience Platform Data Collection](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=sv)
- [Implementera Adobe Experience Cloud med Web SDK, genomgång](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html)
- [Konfigurera användarbehörigheter](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html)
- [API-dokumentation](https://developer.adobelaunch.com/api/)

Nästa steg: [1.2 Edge Network, DataStreams och Server Side Data Collection](./ex2.md)

[Gå tillbaka till modul 1](./data-ingestion-launch-web-sdk.md)

[Gå tillbaka till Alla moduler](./../../overview.md)
