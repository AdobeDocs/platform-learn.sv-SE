---
title: Mappa en federerad publik till S3
seo-title: Map a federated audience to S3 | Engage with Audiences from your Data Warehouse using Federated Audience Composition
breadcrumb-title: Mappa en federerad publik till S3
description: I den här övningen ska vi kartlägga en federerad målgrupp till en Real-Time CDP-målgrupp längre fram i kedjan för att stödja en personaliserad offlineupplevelse.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-create-an-audience.jpg
exl-id: a47b8f7b-7bd0-43a0-bc58-8b57d331b444
source-git-commit: dd5f594a54a9cab8ef78d36d2cf15a9b5f2b682a
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# Mappa federerad publik till S3 för att utnyttja målgruppsattribut för berikning

Ni kan utnyttja målgruppsattributen i ert datalager för att berika er målgrupps upplevelse av aktiveringsarbetsflöden längre fram i kedjan med hjälp av RTCDP-destinationer. För SecurFinancial kan dessa federerade attribut användas för att förbättra kundens personaliseringsupplevelse offline. Nedan mappas den federerade målgruppen till ett förkonfigurerat Amazon S3-mål.

## Steg

1. Navigera till **målportalen**.

2. Klicka på knappen **3-punktmeny** bredvid det förkonfigurerade Amazon S3-målet och klicka sedan på **Aktivera målgrupper**.

   ![activate-audiences](assets/activate-audiences.png)

3. Välj **S3-målet** och klicka sedan på **Nästa**.

   ![select-s3-destination](assets/select-s3-destination.png)

4. Välj rätt målgrupp. I vårt exempel: **SecureFinancial Customers - No Loans, Good Credit** målgrupp.

   ![select-s3-audience](assets/select-s3-audience.png)

5. Använd standardinställningarna i avsnittet **Schemaläggning** och klicka på **Nästa**.

6. Välj avdupliceringsnyckeln i steget **Mappning**. I vårt exempel inkluderas `xdm: personalEmail.address` och väljs som **Transparens för borttagning av dubbletter**. Klicka sedan på **Nästa**:

   ![dedupliceringsnyckel](assets/deduplication-key.png)

7. I mappningssteget väljer du anrikningsattribut baserat på målgruppsfältsmappningar i den federerade målgruppskompositionen. Klicka på ikonen **Penna (redigera)** för att visa de förmarkerade attributen.

   ![edit-attributes](assets/edit-attributes.png)

   ![final-attributes](assets/final-attribution.png)

8. Granska målgruppsmappningen och tryck på **Slutför**.

>[**!SUMMARY**]
>
> Vi har skapat en publik och aktiverat den på en S3-destination med lätthet. Tack vare det användarvänliga gränssnittet kan marknadsföringsteamen snabbt skapa och aktivera målgrupper utan att flytta underliggande data.

Nu ska vi [skapa en resa](build-journey-federated-audience.md).
