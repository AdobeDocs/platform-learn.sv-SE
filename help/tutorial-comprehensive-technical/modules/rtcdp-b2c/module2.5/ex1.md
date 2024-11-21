---
title: Adobe Experience Platform Data Collection & Event Forwarding Side Forwarding - Skapa en händelsevidarebefordringsegenskap för Adobe Experience Platform datainsamling i realtid
description: Skapa en händelsevidarebefordringsegenskap för Adobe Experience Platform Data Collection
kt: 5342
doc-type: tutorial
exl-id: 9c64e57d-c91c-4d4c-923f-91a02edeb2ac
source-git-commit: b4a7144217a68bc0b1bc70b19afcbc52e226500f
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 0%

---

# 2.5.1 Skapa en händelsevidarebefordringsegenskap för Adobe Experience Platform Data Collection

## Vad är en Adobe Experience Platform Data Collection Event Forwarding-egenskap?

När data samlas in med Adobe Experience Platform Data Collection samlas de vanligtvis in på **klientsidan**. **Klientsidan** är en miljö som en webbplats eller ett mobilprogram. I Getting Started and Data Collection diskuterades konfigurationen av en klientegenskap i Adobe Experience Platform Data Collection i detalj och du implementerade egenskapen Adobe Experience Platform Data Collection Client på din webbplats och i ditt mobilprogram, så att data kunde samlas in där när kunden interagerade med webbplatsen och mobilappen.

När interaktionsdata samlas in av egenskapen Adobe Experience Platform Data Collection Client skickas en begäran från webbplatsen eller mobilappen till Adobe Edge. Edge är Adobe Data Collection-miljö och är utgångspunkten för clickstream-data i Adobe ekosystem. Från Edge skickas sedan insamlade data till program som Adobe Experience Platform, Adobe Analytics, Adobe Audience Manager eller Adobe Target.

Med en ny händelsevidarebefordringsegenskap för Adobe Experience Platform Data Collection är det nu möjligt att konfigurera en Adobe Experience Platform Data Collection-egenskap som lyssnar på inkommande data på Edge. När händelsevidarebefordringsegenskapen för Adobe Experience Platform Data Collection som körs på Edge ser inkommande data kan den använda dessa data och vidarebefordra dem till någon annan plats. Det kan nu också vara en extern webkrok som inte är Adobe, vilket gör det möjligt att skicka data till exempelvis valfri datarö, ett beslutsprogram eller något annat program som kan öppna en webkrok.

Konfigurationen av en händelsevidarebefordringsegenskap för Adobe Experience Platform Data Collection ser bekant ut med en klientsidesegenskap, med möjlighet att konfigurera dataelement och regler precis som tidigare med egenskaper för Adobe Experience Platform Data Collection Client. Hur data kommer att användas och kommas emellertid att se lite annorlunda ut, beroende på hur de används.

Låt oss börja med att skapa egenskapen Händelsevidarebefordran för Adobe Experience Platform Data Collection.

## Skapa en händelsevidarebefordringsegenskap för Adobe Experience Platform Data Collection

Gå till [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/). Klicka på **Händelsevidarebefordran** på den vänstra menyn. Därefter visas en översikt över alla tillgängliga egenskaper för händelsevidarebefordran i Adobe Experience Platform Data Collection. Klicka på knappen **Skapa egenskap** .

![Adobe Experience Platform Data Collection SSF](./images/launchhome.png)

Om andra egenskaper för händelsevidarebefordran redan har skapats ser gränssnittet lite annorlunda ut. Klicka i så fall på **Ny egenskap**.

![Adobe Experience Platform Data Collection SSF](./images/launchhomea.png)

Nu måste du ange ett namn för egenskapen för händelsevidarebefordran i Adobe Experience Platform Data Collection. Använd `--aepUserLdap-- - Demo System (DD/MM/YYYY) (Edge)` som namnkonvention. I det här exemplet är namnet **vangeluw - Demo System (22/02/2022) (Edge)**. Klicka på **Spara**.

![Adobe Experience Platform Data Collection SSF](./images/ssf1.png)

Du kommer sedan tillbaka till listan över egenskaper för vidarebefordran av händelser för Adobe Experience Platform Data Collection. Klicka för att öppna den egenskap du nyss skapade.

![Adobe Experience Platform Data Collection SSF](./images/ssf2.png)

## Konfigurera tillägget Adobe Cloud Connector

Gå till **Tillägg** på den vänstra menyn. Tillägget **Core** är redan konfigurerat.

![Adobe Experience Platform Data Collection SSF](./images/ssf3.png)

Gå till **katalog**. Tillägget **Adobe Cloud Connector** visas tillsammans med många andra. Klicka på **Installera** för att installera det.

![Adobe Experience Platform Data Collection SSF](./images/ssf4.png)

Tillägget läggs sedan till. Det finns ingen konfiguration att göra i det här steget. Du kommer tillbaka till översikten över installerade tillägg.

![Adobe Experience Platform Data Collection SSF](./images/ssf5.png)

## 2.5.1.3 Distribuera din egenskap för händelsevidarebefordran i Adobe Experience Platform Data Collection

Gå till **Publiceringsflöde** på den vänstra menyn. Klicka på **Lägg till bibliotek**.

![Adobe Experience Platform Data Collection SSF](./images/ssf6.png)

Ange namnet **Main**, markera miljön **Development (development)** och klicka på **+ Add All Changed Resources**.

![Adobe Experience Platform Data Collection SSF](./images/ssf7.png)

Då ser du det här. Klicka på **Spara och skapa för utveckling**.

![Adobe Experience Platform Data Collection SSF](./images/ssf8.png)

Ditt bibliotek kommer sedan att byggas, vilket kan ta 1-2 minuter.

![Adobe Experience Platform Data Collection SSF](./images/ssf10.png)

Nästa steg: [2.5.2 Uppdatera ditt dataflöde så att data blir tillgängliga för händelsevidarebefordringsegenskapen för datainsamling](./ex2.md)

[Gå tillbaka till modul 2.5](./aep-data-collection-ssf.md)

[Gå tillbaka till Alla moduler](./../../../overview.md)
