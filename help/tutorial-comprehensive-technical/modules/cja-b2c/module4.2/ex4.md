---
title: Importera och analysera data från Google Analytics i Adobe Experience Platform med BigQuery Source Connector - Läs in data från BigQuery i Adobe Experience Platform
description: Importera och analysera data från Google Analytics i Adobe Experience Platform med BigQuery Source Connector - Läs in data från BigQuery i Adobe Experience Platform
kt: 5342
doc-type: tutorial
exl-id: 793b35c6-761f-4b0a-b0bc-3eab93c82162
source-git-commit: d6f6423adbc8f0ce8e20e686ea9ffd9e80ebb147
workflow-type: tm+mt
source-wordcount: '710'
ht-degree: 0%

---

# 4.2.4 Läs in data från BigQuery till Adobe Experience Platform

## Mål

- Mappa BigQuery-data till ett XDM-schema
- Läs in BigQuery-data i Adobe Experience Platform
- Bekanta dig med användargränssnittet i BigQuery Source Connector

## Innan du börjar

Efter föregående övning bör du ha den här sidan öppen i Adobe Experience Platform:

![demo](./images/datasets.png)

**Om du har den öppen fortsätter du med nästa övning.**

**Om du inte har den öppen går du till [Adobe Experience Platform](https://experience.adobe.com/platform/home).**

Gå till Källor på den vänstra menyn. Du kommer då att se hemsidan **Källor**. Gå till **Google BigQuery**-källkopplingen på menyn **Källor** och klicka på **Konfigurera**.

![demo](./images/sourceshome.png)

Då visas urvalsskärmen för Google BigQuery-konto. Välj ditt konto och klicka på **Nästa**.

![demo](./images/0c.png)

Sedan visas skärmen **Markera data**.

![demo](./images/datasets.png)

## 4.2.4.1 Val av BigQuery-tabell

På skärmen **Välj data** väljer du din BigQuery-datamängd. Nu kan du se en förhandsvisning av Google Analytics data i BigQuery.

Klicka på **Nästa**.

![demo](./images/datasets1.png)

## 4.2.4.2 XDM-mappning

Nu ser du det här:

![demo](./images/xdm4a.png)

Du måste nu antingen skapa en ny datauppsättning eller välja en befintlig datauppsättning att läsa in Google Analytics data i. För den här övningen har en datauppsättning och ett schema redan skapats. Du behöver inte skapa ett nytt schema eller en ny datauppsättning.

Välj **Befintlig datauppsättning**. Öppna listrutan för att välja en datauppsättning. Sök efter datauppsättningen `Demo System - Event Dataset for BigQuery (Global v1.1)` och markera den. Klicka på **Nästa**.

![demo](./images/xdm6.png)

Rulla ned. Du måste nu mappa varje **Source Field** från Google Analytics/BigQuery till ett XDM **målfält**, fält för fält. Du kan se ett antal fel som kommer att åtgärdas i mappningsövningen nedan.

![demo](./images/xdm8.png)

Använd mappningstabellen nedan för den här övningen.

| Source Field | Målfält |
| ----------------- |-------------| 
| `_id` | `_id` |
| `_id` | kanal._id |
| `timeStamp` | tidsstämpel |
| `GA_ID` | ``--aepTenantId--``.identity.core.gaid |
| `customerID` | ``--aepTenantId--``. identification.core.crmId |
| `Page` | web.webPageDetails.name |
| `Device` | device.type |
| `Browser` | environment.browserDetails.vendor |
| `MarketingChannel` | marketing.trackingCode |
| `TrafficSource` | channel.typeAtSource |
| `TrafficMedium` | channel.mediaType |
| `TransactionID` | commerce.order.payments.transactionID |
| `Ecommerce_Action_Type` | eventType |
| `Pageviews` | web.webPageDetails.pageViews.value |


För vissa fält måste du ta bort den ursprungliga mappningen och skapa en ny för ett **beräknat fält**.

| Beräknat fält | Målfält |
| ----------------- |-------------| 
| `iif("Ecommerce_Action_Type".equalsIgnoreCase("Product_Refunds"), 1, 0)` | commerce.purchases.value |
| `iif("Ecommerce_Action_Type".equalsIgnoreCase("Product_Detail_Views"), 1, 0)` | commerce.productViews.value |
| `iif("Adds_To_Cart".equalsIgnoreCase("Adds_To_Cart"), 1, 0)` | commerce.productListAdds.value |
| `iif("Ecommerce_Action_Type".equalsIgnoreCase("Product_Removes_From_Cart"), 1, 0)` | commerce.productListRemovals.value |
| `iif("Ecommerce_Action_Type".equalsIgnoreCase("Product_Checkouts"), 1, 0)` | commerce.checkouts.value |

Om du vill skapa ett **beräknat fält** klickar du på **+ Ny fälttyp** och sedan på **Beräknat fält**.

![demo](./images/xdm8a.png)

Klistra in regeln ovan och klicka på **Spara** för vart och ett av fälten i tabellen ovan.

![demo](./images/xdm8b.png)

Du har nu en **mappning** som den här.

Källfälten **GA_ID** och **customerID** mappas till en identifierare i det här XDM-schemat. På så sätt kan du förbättra Google Analytics-data (webb-/appbeteendedata) med andra datauppsättningar som Loyalty eller Call Center-data.

Klicka på **Nästa**.

![demo](./images/xdm34.png)

## 4.2.4.3 Anslutning och planering av dataöverföring

Fliken **Schemaläggning** visas nu:

På fliken **Schemaläggning** kan du definiera en frekvens för datainmatningsprocessen för den här **mappningen** och data.

Eftersom du använder demodata i Google BigQuery som inte kommer att uppdateras finns det inget behov av att ställa in ett schema i den här övningen. Du måste välja något och för att undvika för många onödiga dataöverföringsprocesser måste du ange frekvensen så här:

- Frekvens: **Vecka**
- Intervall: **200**
- Starttid: **när som helst under nästa timme**

**Viktigt**: Kontrollera att du aktiverar växeln **Backfill**.

Sist men inte minst måste du definiera ett **delta**-fält.

Fältet **delta** används för att schemalägga anslutningen och bara överföra nya rader som kommer till din BigQuery-datamängd. Ett delta-fält är vanligtvis alltid en tidsstämpelkolumn. Så för framtida schemalagda datainmatningar kommer endast rader med en ny, nyare tidsstämpel att kapslas.

Välj **timeStamp** som deltafält.
Klicka på **Nästa**.

![demo](./images/ex437.png)

## 4.2.4.4 Granska och starta anslutning

Nu visas en detaljerad översikt över din anslutning. Kontrollera att allt är korrekt innan du fortsätter, eftersom vissa inställningar inte kan ändras längre efteråt, till exempel XDM-mappningen.

Klicka på **Slutför**.

![demo](./images/xdm46.png)

När anslutningen har skapats ser du följande:

![demo](./images/xdm48.png)

Du är nu redo att fortsätta med nästa övning, där du kommer att använda Customer Journey Analytics för att skapa kraftfulla visualiseringar utöver Google Analytics data.

Nästa steg: [4.2.5 Analysera Google Analytics-data med Customer Journey Analytics](./ex5.md)

[Gå tillbaka till modul 4.2](./customer-journey-analytics-bigquery-gcp.md)

[Gå tillbaka till Alla moduler](./../../../overview.md)
