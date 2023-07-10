---
title: Använd era kunddata för att leverera strömmande upplevelser
description: Lär dig hur du minskar påverkan av data av låg kvalitet, minskar time to value och multiplicerar avkastningen genom att använda samma data för många olika användningsområden.
feature: Queries
role: Data Engineer, Data Architect, Developer
jira: KT-10323
thumbnail: 342533.jpeg
exl-id: 30574cc5-66fa-4ab8-83ed-7af710294dbf
source-git-commit: adbe8f4476340abddebbf9231e3dde44ba328063
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 3%

---

# Använd era kunddata för att leverera strömmande upplevelser

Flerkanalsdata är en viktig ingrediens för att driva kundprofiler som kan användas av marknadsförare för att samordna aktivering och mäta kundresorna. Men företag står inför utmaningar när det gäller att hantera kvaliteten, skalan och variationen av dessa data. De behöver effektiva lösningar för att minska verkningarna av data av låg kvalitet, minska time to value och öka avkastningen genom att använda samma data för många olika användningsområden.

Den här videon utforskar:

* Utnyttja Adobe Experience Platform funktioner för dataförberedelser
* Ökad avkastning från Adobe Real-Time CDP, Adobe Journey Optimizer och Customer Journey Analytics

>[!VIDEO](https://video.tv.adobe.com/v/342533?quality=12&learn=on)

## SQL-exempel

```sql
INSERT INTO summit_adv_data_prep_dataset
SELECT STRUCT(
customerId AS crmCustomerId, struct(sku AS sku, price AS sku_price, abandonTS AS abandonTS) AS abandonBrowse) AS _pfreportingonprod
FROM
(SELECT
B.personKey.sourceID AS customerId,
A.productListItems[0].SKU AS sku,
max(A.timestamp) AS abandonTS,
max(C._pfreportingonprod.price) AS price
FROM summit_adobe_analytics_dataset A,profile_attribute_14adf268_2a20_4dee_bee6_a6b0e34616a9 B,summit_product_dataset C
WHERE A._experience.analytics.customDimensions.eVars.eVar1 = B.personKey.sourceID
AND A.productListItems[0].sku = C._pfreportingonprod.sku
AND A.web.webpagedetails.URL NOT LIKE '%orderconfirmation%'
AND timestamp > current_date - interval '4 day'
GROUP BY customerId,sku
order by price desc)D;
```

Mer information finns på [Dokumentation för frågetjänsten](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=sv).

>[!NOTE]
>
>Den här videon är ett utdrag från sessionen Adobe Summit 2020 *[Återvinning av data över flera kanaler för att skapa upplevelser](https://business.adobe.com/summit/2022/sessions/recharging-omnichannel-data-for-electrifying-exper-s409.html)*.
