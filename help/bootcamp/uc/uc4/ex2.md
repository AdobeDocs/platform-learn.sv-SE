---
title: Bootcamp - Customer Journey Analytics - Connect Adobe Experience Platform Datasets in Customer Journey Analytics
description: Bootcamp - Customer Journey Analytics - Connect Adobe Experience Platform Datasets in Customer Journey Analytics
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Connections
exl-id: 47e02021-019c-4ea4-a7a8-003deef7c9e5
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 0%

---

# 4.2 Ansluta Adobe Experience Platform-datauppsättningar i Customer Journey Analytics

## Mål

- Förstå användargränssnittet för dataanslutning
- Använd Adobe Experience Platform-data i CJA
- Förstå person-ID och datasammanfogning
- Lär dig mer om dataströmning i Customer Journey Analytics

## 4.2.1 Anslutning

Gå till [analytics.adobe.com](https://analytics.adobe.com) om du vill komma åt Customer Journey Analytics.

Gå till **Anslutningar** på Customer Journey Analytics-hemsidan.

![demo](./images/cja2.png)

Här ser du alla olika anslutningar mellan CJA och Platform. Dessa anslutningar har samma mål som rapporteringsprogram i Adobe Analytics. Insamlingen av data är dock helt annorlunda. Alla data kommer från Adobe Experience Platform datamängder.

Låt oss skapa din första anslutning. Klicka på **Skapa ny anslutning**.

![demo](./images/cja4.png)

Därefter visas gränssnittet **Skapa anslutning**.

![demo](./images/cja5.png)

Nu kan du ge anslutningen ett namn.

Använd den här namnkonventionen: `yourLastName – Omnichannel Data Connection`.

Exempel: `vangeluw - Omnichannel Data Connection`

Du måste också välja rätt sandlåda att använda. Välj din sandlåda på sandlådemenyn, som ska vara `Bootcamp`. I det här exemplet är sandlådan som ska användas **Bootcamp**. Du måste också ange **Genomsnittligt antal dagliga händelser** till **mindre än 1 miljon**.

![demo](./images/cjasb.png)

När du har valt sandlådan kan du börja lägga till datauppsättningar i den här anslutningen. Klicka på **Lägg till datauppsättningar**.

![demo](./images/cjasb1.png)

## 4.2.2 Välj Adobe Experience Platform-datauppsättningar

Sök efter datauppsättningen `Demo System - Event Dataset for Website (Global v1.1)`. Klicka på **+** för att lägga till datauppsättningen i den här anslutningen.

![demo](./images/cja7.png)

Sök och markera kryssrutorna för `Demo System - Profile Dataset for Loyalty (Global v1.1)` och `Demo System - Event Dataset for Call Center (Global v1.1)`.

Du får den här då. Klicka på **Nästa**.

![demo](./images/cja9.png)

## 4.2.3 Person-ID och datatitlar

### Person-ID

Målet är nu att gå med i dessa datauppsättningar. För varje datamängd som du har valt visas ett fält med namnet **Person-ID**. Varje datauppsättning har ett eget fält för person-ID.

![demo](./images/cja11.png)

Som du ser har de flesta automatiskt valt person-ID. Detta beror på att en primär identifierare har valts i alla scheman i Adobe Experience Platform. Här är till exempel schemat för `Demo System - Event Schema for Call Center (Global v1.1)`, där du kan se att primär identifierare är inställd på `phoneNumber`.

![demo](./images/cja13.png)

Du kan dock fortfarande påverka vilken identifierare som ska användas för att sammanfoga datauppsättningar för din anslutning. Du kan använda valfri identifierare som är konfigurerad i det schema som är länkat till din datauppsättning. Klicka på listrutan för att utforska de ID:n som finns på varje datauppsättning.

![demo](./images/cja14.png)

Som vi nämnt kan du ange olika person-ID:n för varje datauppsättning. På så sätt kan du samla olika datauppsättningar från flera ursprung i CJA. Tänk dig att ta in NPS-data eller enkätdata som skulle vara mycket intressant och till hjälp för att förstå sammanhanget och varför något har hänt.

Namnet på fältet för person-ID är inte viktigt, så länge som värdet i fälten för person-ID motsvarar det. Om till exempel person-ID:t är `email` i en datauppsättning och `emailAddress` i en annan, och `dnb-bootcamp@adobe.com` är samma värde för person-ID-fältet i båda datauppsättningarna, kan CJA sätta ihop data.

För närvarande finns det några andra begränsningar som att knyta det anonyma beteendet till kända. Granska de vanliga frågorna här: [Vanliga frågor](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-faq.html?lang=sv-SE).

### Ställa in data med användar-ID

Nu när du förstår konceptet med att sy ihop datauppsättningar med person-ID:t, ska vi välja `email` som ditt person-ID för varje datauppsättning.

![demo](./images/cja15.png)

Gå till varje datauppsättning för att uppdatera person-ID:t.

![demo](./images/cja12a.png)

Fyll nu i fältet Person-ID och välj `email` i listrutan.

![demo](./images/cja17.png)

När du har sytt ihop de tre datauppsättningarna är vi redo att fortsätta.

| datauppsättning | Person-ID |
| ----------------- |-------------| 
| Demo System - händelsedatauppsättning för webbplats (Global v1.1) | e-post |
| Demo System - profildatauppsättning för lojalitet (Global v1.1) | e-post |
| Demo System - händelsedatauppsättning för callcenter (Global v1.1) | e-post |

Du måste också se till att följande alternativ är aktiverade för varje datauppsättning:

- Importera alla nya data
- Fyll i alla befintliga data

Klicka på **Lägg till datauppsättningar**.

![demo](./images/cja16.png)

Klicka på **Spara** och gå till nästa övning.
När du har skapat din **anslutning** kan det ta några timmar innan dina data är tillgängliga i CJA.

![demo](./images/cja20.png)

Nästa steg: [4.3 Skapa en datavy](./ex3.md)

[Gå tillbaka till användarflöde 4](./uc4.md)

[Gå tillbaka till Alla moduler](./../../overview.md)
