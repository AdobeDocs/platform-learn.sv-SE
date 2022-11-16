---
title: Importera och analysera Google Analytics-data i Adobe Experience Platform med BigQuery Source Connector - Läs in data från BigQuery i Adobe Experience Platform
description: Importera och analysera Google Analytics-data i Adobe Experience Platform med BigQuery Source Connector - Läs in data från BigQuery i Adobe Experience Platform
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 150df432-e87a-402a-b821-ca9e33c5fd80
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 2%

---

# 12.4 Läs in data från BigQuery till Adobe Experience Platform

## Mål

- Mappa BigQuery-data till ett XDM-schema
- Läs in BigQuery-data i Adobe Experience Platform
- Bekanta dig med användargränssnittet i BigQuery Source Connector

## Innan du börjar

När du har tränat 12.3 bör du ha den här sidan öppen i Adobe Experience Platform:

![demo](./images/datasets.png)

**Om du har öppnat den, fortsätt med träning 12.4.1.**

**Om du inte har den öppen, gå till [Adobe Experience Platform](https://experience.adobe.com/platform/home).**

Gå till Källor på den vänstra menyn. Då ser du **Källor** hemsida. I **Källor** meny, klicka på **Databaser**.

![demo](./images/sourceshome.png)

Välj **Google BigQuery** Source Connector och klicka på **+ Konfigurera**.

![demo](./images/bq.png)

Då visas urvalsskärmen för Google BigQuery-konto.

![demo](./images/0-c.png)

Välj ditt konto och klicka på **Nästa**.

![demo](./images/ex4/0-d.png)

Då ser du **Lägg till data** vy.

![demo](./images/datasets.png)

## 12.4.1 Val av BigQuery-tabell

I **Lägg till data** väljer du din BigQuery-datauppsättning.

![demo](./images/datasets.png)

Nu kan du se en förhandsvisning av Google Analytics data i BigQuery.

Klicka på **Nästa**.

![demo](./images/ex4/3.png)

## 12.4.2 XDM-mappning

Nu ser du det här:

![demo](./images/xdm4a.png)

Du måste nu antingen skapa en ny datauppsättning eller välja en befintlig datauppsättning att läsa in Google Analytics data i. För den här övningen har en datauppsättning och ett schema redan skapats. Du behöver inte skapa ett nytt schema eller en ny datauppsättning.

Välj **Befintlig datauppsättning**. Öppna listrutan för att välja en datauppsättning. Sök efter datauppsättningen med namnet `Demo System - Event Dataset for BigQuery (Global v1.1)` och markera den. Klicka på **Nästa**.

![demo](./images/xdm6.png)

Bläddra nedåt. Nu måste du mappa var **Källfält** från Google Analytics/BigQuery till en XDM **Målfält**, fält för fält.

![demo](./images/xdm8.png)

Använd mappningstabellen nedan för den här övningen.

| Källfält | Målfält |
| ----------------- |-------------| 
| **_id** | _id |
| **_id** | kanal._id |
| timeStamp | tidsstämpel |
| GA_ID | ``--aepTenantId--``.identity.core.gaid |
| customerID | ``--aepTenantId--``.identity.core.loyaltyId |
| Sida | web.webPageDetails.name |
| Enhet | device.type |
| Webbläsare | environment.browserDetails.vendor |
| MarketingChannel | marketing.trackingCode |
| TrafficSource | channel.typeAtSource |
| TrafficMedium | channel.mediaType |
| TransactionID | commerce.order.payments.transactionID |
| ecommerce_Action_Type | eventType |
| Sidor | web.webPageDetails.pageViews.value |
| Unique_Purchases | commerce.purchases.value |
| product_detail_views | commerce.productViews.value |
| add_to_cart | commerce.productListAdds.value |
| product_removes_from_art | commerce.productListRemovals.value |
| Product_Checkouts | commerce.checkouts.value |

När du har kopierat och klistrat in mappningen ovan i Adobe Experience Platform UI bör du kontrollera om det inte finns några fel på grund av stavfel eller inledande/avslutande blanksteg.

Du har nu en **Mappning** så här:

![demo](./images/xdm34.png)

Källfälten **GA_ID** och **customerID** mappas till en identifierare i det här XDM-schemat. På så sätt kan du förbättra Google Analytics-data (webb-/appbeteendedata) med andra datauppsättningar som Loyalty eller Call Center-data.

Klicka på **Nästa**.

![demo](./images/ex4/38.png)

## 12.4.3 Anslutning och planering av dataöverföring

Nu ser du **Schemaläggning** tab:

![demo](./images/xdm38a.png)

I **Schemaläggning** kan du definiera en frekvens för dataöverföringsprocessen för den här **Mappning** och data.

Eftersom du använder demodata i Google BigQuery som inte kommer att uppdateras finns det inget behov av att ställa in ett schema i den här övningen. Du måste välja något och för att undvika för många onödiga dataöverföringsprocesser måste du ange frekvensen så här:

- Frekvens: **Vecka**
- Intervall: **200**

![demo](./images/ex4/39.png)

**Viktigt**: se till att du aktiverar **Backfill** byt.

![demo](./images/ex4/39a.png)

Sist men inte minst måste du definiera en **delta** fält.

![demo](./images/ex4/36.png)

The **delta** -fältet används för att schemalägga anslutningen och bara överföra nya rader som kommer till din BigQuery-datauppsättning. Ett delta-fält är vanligtvis alltid en tidsstämpelkolumn. Så för framtida schemalagda datainmatningar kommer endast rader med en ny, nyare tidsstämpel att kapslas.

Välj **timeStamp** som deltafält.

![demo](./images/ex4/37.png)

Du har den här nu.

![demo](./images/xdm37a.png)

Klicka på **Nästa**.

![demo](./images/ex4/42.png)

## 12.4.4 Granska och starta anslutningen

I **Flödesdetaljer för datauppsättning** vy. du måste namnge anslutningen, vilket hjälper dig att hitta den senare.

Använd den här namnkonventionen:

| Fält | Namngivning | Exempel |
| ----------------- |-------------| -------------|
| Namn på dataflöde | DataFlow - ldap - BigQuery Web Interaction | DataFlow - vangeluw - BigQuery-webbplatsinteraktion |
| Beskrivning | DataFlow - ldap - BigQuery Web Interaction | DataFlow - vangeluw - BigQuery-webbplatsinteraktion |

![demo](./images/xdm44.png)

Klicka på **Nästa**.

![demo](./images/ex4/45.png)

Nu visas en detaljerad översikt över din anslutning. Kontrollera att allt är korrekt innan du fortsätter, eftersom vissa inställningar inte kan ändras längre efteråt, till exempel XDM-mappningen.

![demo](./images/xdm46.png)

Klicka **Slutför**.

![demo](./images/ex4/finish.png)

Det kan ta ett tag att konfigurera anslutningen, så oroa dig inte om följande visas:

![demo](./images/ex4/47.png)

När anslutningen har skapats ser du följande:

![demo](./images/xdm48.png)

Du är nu redo att fortsätta med nästa övning, där du kommer att använda Customer Journey Analytics för att skapa kraftfulla visualiseringar utöver Google Analytics data.

Nästa steg: [12.5 Analysera Google Analytics-data med Customer Journey Analytics](./ex5.md)

[Gå tillbaka till modul 12](./customer-journey-analytics-bigquery-gcp.md)

[Gå tillbaka till Alla moduler](./../../overview.md)
