---
title: Foundation - Installation av Adobe Experience Platform Data Collection och Web SDK-tillägget - Förklaring av Adobe Experience Platform Data Collection
description: Foundation - Installation av Adobe Experience Platform Data Collection och Web SDK-tillägget - Förklaring av Adobe Experience Platform Data Collection
kt: 5342
doc-type: tutorial
exl-id: 1f5dd730-d84a-4d3a-b5ef-2be3e089c7fd
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 0%

---

# 1.1.1 Förstå Adobe Experience Platform datainsamling

## Kontext

Adobe Experience Platform Data Collection används av varumärken för ett antal användningsområden. Det är nästa generation av Tag Management System (TMS) som ger kunderna ett enkelt sätt att driftsätta och hantera alla analyser-, marknadsförings- och annonslösningar som behövs för att driva relevanta kundupplevelser. Adobe Experience Platform Data Collection kostar inget och kan köpas av alla Adobe Experience Cloud-kunder. Ett varumärke kan använda Adobe Experience Platform Data Collection för att

- Implementera både Adobe Experience Cloud och Adobe Experience Platform.
- Hantera de olika kraven för olika delar av organisationen genom att ge var och en en en egen **Property** att hantera.
- Tillåt testning och livscykelhantering.
- Lägg in egna JavaScript- och tredjepartstaggar, som alla hanteras på ett och samma ställe.

## Utforska användargränssnittet

Gå till [Adobe Experience Platform datainsamling](https://experience.adobe.com/#/data-collection/).

Gå till **Taggar**. Du ser nu vyn **[!UICONTROL Properties]**. Egenskaper som anges här är till för självstudiekurshantering. Dessa egenskaper representerar:

- App- och webbegenskaper
- Olika webbplatser ger kunderna olika service på olika sätt. Luma Retail skulle till exempel ha en egenskap, Luma Travel skulle ha en annan.
- Äldre såväl som aktuella webbplatser
- En specifik Adobe Analytics-design som är gemensam för flera olika webbplatser
- Interna intranätsidor bredvid externa platser

![Starta egenskapsvyn](./images/launch1.png)

Ta en titt på den vänstra listen.

![Starta vänster järnväg](./images/launch2.png)

- **[!UICONTROL Tags]** ger en översikt över alla egenskaper på klientsidan
- **[!UICONTROL App Surfaces]** ger en översikt över alla appkonfigurationer för att aktivera push-meddelanden (som används/aktiveras i kombination med Project Sierra)
- **[!UICONTROL Datastreams]** utforskas i [nästa övning](./ex2.md)
- **[!UICONTROL Event Forwarding]** ger en översikt över alla egenskaper på serversidan som utforskas i [Modul 2.5 - Real-Time CDP-anslutningar: Händelsevidarebefordran](./../../../../modules/delivery-activation/rtcdp-b2c/rtcdpb2c-5/aep-data-collection-ssf.md)
- **[!UICONTROL Monitoring]** ger en översikt över inkommande och utgående händelsetrafik via händelsevidarebefordran
- **[!UICONTROL Assurance]** ger åtkomst till felsökning och implementering med Adobe Debugger
- **[!UICONTROL Places]** ger åtkomst till hantering av POI:n som blir tillgängliga för platsbaserad personalisering i mobilprogram
- **[!UICONTROL Schemas]** ger åtkomst till Adobe Experience Platform schemaredigerare
- **[!UICONTROL Identities]** ger åtkomst till inställningarna för Adobe Experience Platform Identity Graph

## Ytterligare information

Adobe Experience Platform Data Collection är ett mycket avancerat verktyg som omfattar mer än bara en självstudiekurs från Adobe Experience Platform. Organisationer kanske inte använder Adobe Experience Platform Data Collection för sina tagghanteringsfunktioner, utan använder tagghanteringslösningar som inte är från Adobe för att mata in kod och hantera taggar. Adobe och Adobe Professional Services har stöd för att använda tagghanteringslösningar som inte är Adobe.
Nedan finns ytterligare information för dem som är intresserade av att förstå Adobe Experience Platform Data Collection.

- [Användarhandbok för Adobe Experience Platform Data Collection](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=sv)
- [Implementera Adobe Experience Cloud med Web SDK, självstudiekurs](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html)
- [Konfigurera användarbehörigheter](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html)
- [API-dokumentation](https://developer.adobelaunch.com/api/)

## Nästa steg

Gå till [1.1.2 Edge Network, datastreams och datainsamling på serversidan](./ex2.md){target="_blank"}

Gå tillbaka till [Konfigurera Adobe Experience Platform Data Collection och taggtillägget Web SDK](./data-ingestion-launch-web-sdk.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../../overview.md){target="_blank"}
