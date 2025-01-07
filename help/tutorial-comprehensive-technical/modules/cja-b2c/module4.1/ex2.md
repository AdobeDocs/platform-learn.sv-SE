---
title: Customer Journey Analytics - Ansluta Adobe Experience Platform-datauppsättningar i Customer Journey Analytics
description: Customer Journey Analytics - Ansluta Adobe Experience Platform-datauppsättningar i Customer Journey Analytics
kt: 5342
doc-type: tutorial
exl-id: 96e7a5b2-9833-430a-8eab-27651a113675
source-git-commit: d6f6423adbc8f0ce8e20e686ea9ffd9e80ebb147
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 0%

---

# 4.1.2 Ansluta Adobe Experience Platform-datauppsättningar i Customer Journey Analytics

## Mål

- Förstå användargränssnittet för dataanslutning
- Använd Adobe Experience Platform-data i CJA
- Förstå person-ID och datasammanfogning
- Lär dig mer om dataströmning i Customer Journey Analytics

## 4.1.2.1 Anslutning

Gå till [analytics.adobe.com](https://analytics.adobe.com) om du vill komma åt Customer Journey Analytics.

Gå till **Anslutningar** på Customer Journey Analytics-hemsidan.

![demo](./images/cja2.png)

Här ser du alla olika anslutningar mellan CJA och Platform. Dessa anslutningar har samma mål som rapporteringsprogram i Adobe Analytics. Insamlingen av data är dock helt annorlunda. Alla data kommer från Adobe Experience Platform datamängder.

Låt oss skapa din första anslutning. Klicka på **Skapa ny anslutning**.

![demo](./images/cja4.png)

Därefter visas gränssnittet **Skapa anslutning**.

![demo](./images/cja5.png)

Nu kan du ge anslutningen ett namn.

Använd den här namnkonventionen: `--aepUserLdap-- – Omnichannel Data Connection`.

Du måste också välja rätt sandlåda att använda. Välj din sandlåda på sandlådemenyn, som ska vara `--aepSandboxName--`. I det här exemplet är sandlådan **Tech Insiders**. Du måste också ange **Genomsnittligt antal dagliga händelser** till **mindre än 1 miljon**.

![demo](./images/cjasb.png)

När du har valt sandlådan kan du börja lägga till datauppsättningar. Klicka på **Lägg till datauppsättningar**.

![demo](./images/cjasb1.png)

## 4.1.2.2 Markera Adobe Experience Platform-datauppsättningar

Sök efter datauppsättningen `Demo System - Event Dataset for Website (Global v1.1)`. Aktivera rutan för den här datauppsättningen för att lägga till den i anslutningen.

![demo](./images/cja7.png)

Stanna på samma skärm och sök efter och markera kryssrutan för `Demo System - Event Dataset for Call Center (Global v1.1)`.

Du får den här då. Klicka på **Nästa**.

![demo](./images/cja9.png)

## 4.1.2.3 Person-ID och datatitlar

### Person-ID

Målet är nu att gå med i dessa datauppsättningar. För varje datamängd som du har valt visas ett fält med namnet **Person-ID**. Varje datauppsättning har ett eget fält för person-ID.

![demo](./images/cja11.png)

Som du ser har de flesta automatiskt valt person-ID. Detta beror på att en primär identitet har valts i alla scheman i Adobe Experience Platform. Här är till exempel schemat för `Demo System - Event Schema for Website (Global v1.1)`, där du kan se att den primära identiteten är inställd på `ecid`.

![demo](./images/cja13.png)

Du kan dock fortfarande påverka vilken identifierare som ska användas för att sammanfoga datauppsättningar för din anslutning. Du kan använda valfri identifierare som är konfigurerad i det schema som är länkat till din datauppsättning. Klicka på listrutan för att utforska de ID:n som finns på varje datauppsättning.

![demo](./images/cja14.png)

Som vi nämnt kan du ange olika person-ID:n för varje datauppsättning. På så sätt kan du samla olika datauppsättningar från flera ursprung i CJA. Tänk dig att ta in NPS-data eller enkätdata som skulle vara mycket intressant och till hjälp för att förstå sammanhanget och varför något har hänt.

Namnet på fältet för person-ID är inte viktigt, så länge som värdet i fälten för person-ID motsvarar det. Säg att vi har `email` i en datauppsättning och `emailAddress` i en annan datauppsättning definierad som person-ID. Om `delaigle@adobe.com` är samma värde för person-ID-fältet på båda datauppsättningarna kan CJA sammanfoga data.

Granska de vanliga frågorna för CJA här för att förstå nyanserna med identitetssammanfogning: [Vanliga frågor](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-faq.html).

### Ställa in data med användar-ID

Nu när du förstår konceptet med att sy ihop datauppsättningar med person-ID:t, ska vi välja `email` som ditt person-ID för varje datauppsättning.

![demo](./images/cja15.png)

Gå till varje datauppsättning för att uppdatera person-ID:t. Fyll nu i fältet Person-ID och välj `email` i listrutan.

![demo](./images/cja12a.png)

När du har sammanfogat de två datauppsättningarna är du redo att fortsätta.

| datauppsättning | Person-ID |
| ----------------- |-------------| 
| Demo System - händelsedatauppsättning för webbplats (Global v1.1) | e-post |
| Demo System - händelsedatauppsättning för callcenter (Global v1.1) | e-post |

Du måste också se till att dessa alternativ är aktiverade för båda datauppsättningarna:

- Importera alla nya data
- Fyll i alla befintliga data

(Glöm inte att aktivera båda dessa alternativ för den andra datauppsättningen)

Du måste också välja en **datakälltyp** för varje datamängd.

Detta är inställningarna för datauppsättningen **Demo System - händelsedatauppsättning för webbplats (Global v1.1)**.

![demo](./images/cja16a.png)

Detta är inställningarna för datauppsättningen **Demo System - händelsedatauppsättning för webbplats (Global v1.1)**.

Klicka på **Lägg till datauppsättningar**.

![demo](./images/cja16.png)

Klicka på **Spara** och gå till nästa övning.

När du har skapat din **anslutning** kan det ta några timmar innan dina data är tillgängliga i CJA.

![demo](./images/cja20.png)

Nästa steg: [4.1.3 Skapa en datavy](./ex3.md)

[Gå tillbaka till modul 4.1](./customer-journey-analytics-build-a-dashboard.md)

[Gå tillbaka till Alla moduler](./../../../overview.md)
