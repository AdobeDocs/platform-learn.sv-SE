---
title: Mappa en federerad publik till S3
seo-title: Map a federated audience to S3 | Unlock cross-channel insights with Federated Audience Composition
breadcrumb-title: Mappa en federerad publik till S3
description: I den här lektionen ska vi kartlägga en federerad målgrupp till en Real-Time CDP-målgrupp längre fram i kedjan för att stödja en personaliserad offlineupplevelse.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-create-an-audience.jpg
hide: true
source-git-commit: a5ae2695763bc3d6dce786861dcbc15f3422c035
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---


# Mappa federerad publik till S3 för att utnyttja målgruppsattribut för berikning

I den här övningen får du lära dig att utnyttja målgruppsattribut i ert datalager för att berika er målgrupps upplevelse av aktiveringsarbetsflöden längre fram i kedjan med hjälp av RTCDP-destinationer. För SecurFinancial kan dessa federerade attribut användas för att förbättra kundens personaliseringsupplevelse offline. I det här exemplet mappar vi den federerade publiken till ett förkonfigurerat Amazon S3-mål.

## Steg

1. Navigera till **målportalen**.

2. Klicka på knappen **3-punktmeny** bredvid det förkonfigurerade Amazon S3-målet och klicka sedan på **Aktivera målgrupper**.

   ![activate-audiences](assets/activate-audiences.png)

3. Välj **S3-målet** och klicka sedan på **Nästa**.

   ![select-s3-destination](assets/select-s3-destination.png)

4. Välj målgruppen **SecureFinancial Customers - No Loans, Good Credit**.

   ![select-s3-audience](assets/select-s3-audience.png)

5. Lämna alla standardinställningar i avsnittet **Schemaläggning** och klicka på **Nästa**.

6. I steget **Mappning** kontrollerar du att följande är inkluderat och markerat som **dedupliceringsnyckel**. Klicka sedan på **Nästa**:
   - `xdm: personalEmail.address`

   ![dedupliceringsnyckel](assets/deduplication-key.png)

7. I följande mappningssteg kan du välja anrikningsattribut baserat på målgruppsfältsmappningar i den federerade målgruppskompositionen. Klicka på ikonen **Penna (redigera)** för att visa de förmarkerade attributen.

   ![edit-attributes](assets/edit-attributes.png)

   ![final-attributes](assets/final-attribution.png)

8. Granska målgruppsmappningen och tryck på **Slutför**.

Vi är redo att gå vidare till [skapa en resa](build-journey-federated-audience.md).
