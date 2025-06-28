---
title: Kör frågor
seo-title: Run queries | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Kör frågor
description: I den här lektionen får du lära dig hur du ställer in, skriver och kör frågor för att validera data som du har kapslat.
role: Data Architect, Data Engineer
feature: Queries
jira: KT-4348
thumbnail: 4348-run-queries.jpg
exl-id: a37531cb-96ad-4547-86af-84f7ed65f019
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# Kör frågor

<!-- 15 min-->
I den här lektionen får du lära dig hur du ställer in, skriver och kör frågor för att validera data som du har kapslat.

Adobe Experience Platform Query Service hjälper dig att förstå dina data genom att du kan använda standard-SQL för att fråga efter data i Platform. Med hjälp av frågetjänsten kan du ansluta till valfri datauppsättning i datasjön och samla in frågeresultaten som en ny datauppsättning för användning vid rapportering, maskininlärning eller för förtäring i realtidskundprofil.

**Dataarkitekter** och **Datatekniker** måste använda frågetjänsten utanför den här självstudien.

Innan du börjar övningarna ska du titta på den här korta videon och lära dig mer om Query Service:
>[!VIDEO](https://video.tv.adobe.com/v/3464265?learn=on&enablevpops&captions=swe)

## Behörigheter krävs

I lektionen [Konfigurera behörigheter](configure-permissions.md) ställer du in alla åtkomstkontroller som krävs för att slutföra lektionen.

<!-- Settings > **[!UICONTROL Services]** > **[!UICONTROL Query Service]**
* Permission items Data Management > **[!UICONTROL View Datasets]** and  **[!UICONTROL Manage Datasets]**
* Permission item Sandboxes > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
-->

## Enkla frågor

Låt oss börja med några enkla frågor:

1. Gå till **Frågor** i den vänstra navigeringen i användargränssnittet för plattformen
1. Markera knappen **Skapa fråga** längst upp till höger för att öppna en textruta där frågor kan köras och köras
1. Skriv följande fråga i redigeraren och tryck på Skift+Enter eller Skift+Retur för att köra frågan.

   ```
   SHOW TABLES
   ```

1. Här visas en lista med tillgängliga tabeller

   ![VISA TABLE-fråga](assets/queries-showTables.png)


1. Prova den här frågan och ersätt `_techmarketingdemos` med ditt eget klientnamnutrymme, som visas i dina scheman om du kommer ihåg det.

   ```
   SELECT person.name.lastName,loyalty.tier
   FROM luma_loyalty_dataset
   WHERE loyalty.tier ='gold'
   ```

   ![SELECT-data från lojalitetsdatauppsättningen](assets/queries-loyaltySelect.png)

1. Om något fel uppstår visas detaljerade meddelanden på fliken **[!UICONTROL Console]**, enligt bilden nedan
   ![Fel i frågan](assets/queries-error.png)

1. Med din fråga **[!UICONTROL Name]** `Luma Gold Level Customers`
1. Markera knappen **[!UICONTROL Save]**
   ![Sparar frågan](assets/queries-loyaltySelect-save.png)


<!--SELECT COUNT(DISTINCT (_techmarketingdemos.systemIdentifier.loyaltyId)) FROM luma_loyalty_dataset 


SELECT _techmarketingdemos.systemIdentifier.loyaltyId, COUNT(_techmarketingdemos.systemIdentifier.loyaltyId)
FROM luma_loyalty_dataset 
GROUP BY _techmarketingdemos.systemIdentifier.loyaltyId
HAVING COUNT(_techmarketingdemos.systemIdentifier.loyaltyId) > 1;-->

## Ytterligare övningar

Ytterligare frågetjänstövningar kommer att läggas till i självstudiekursen vid ett senare datum.
<!--
## Join Datasets

In this exercise, we will join two datasets `Luma Loyalty Dataset` and `Luma Offline Purchase` to get list of gold customers who have spend over $500 dollars in one purchase.

1. Create a new query
1. Copy and paste following query in query editor and execute, again replacing `_techmarketingdemos` with your own tenant namespace
    
    ```
    SELECT DISTINCT lopd.commerce.order.purchaseID as PurchaseId ,
        lld.person.name.firstName as LastName ,
        lld.person.name.lastName as LastName ,
        lopd.personalEmail.address as email,
        lopd.commerce.order.priceTotal as Total

    FROM luma_loyalty_dataset lld
    JOIN luma_offline_purchase_event_dataset lopd
    ON lopd._techmarketingdemos.systemIdentifier.loyaltyId = lld._techmarketingdemos.systemIdentifier.loyaltyId

    WHERE lld._techmarketingdemos.loyalty.level ='gold' AND lopd.commerce.order.priceTotal >500;
    ```

1. You should get list of Gold Customers who have spend over $500 in single purchase.

## Output datasets

1. Select on Output Dataset button
1. Provide name and description to the dataset
1. Save.
1. Go to **Datasets** under **Data Management** to find new dataset created.

-->
<!--Add content for Adobe Defined Functions-->

## Ytterligare resurser

* [Dokumentation för frågetjänsten](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=sv)
* [API-referens för frågetjänst](https://www.adobe.io/experience-platform-apis/references/query-service/)

Nu till den sista praktiska lektionen: [skapar segment](build-segments.md)!
