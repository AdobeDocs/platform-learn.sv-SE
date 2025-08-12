---
title: Data Warehouse
seo-title: Configure a Data Warehouse connection | Unlock cross-channel insights with Federated Audience Composition
breadcrumb-title: Data Warehouse
description: I den här lektionen konfigurerar vi en anslutning mellan Adobe Experience Platform och ditt företag Data Warehouse för att aktivera Federated Audience Composition.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-configure-a-data-warehouse-connection.jpg
hide: true
source-git-commit: fcfadca95c12d0123cfb221e44909f7e0fa8abab
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---


# Data Warehouse

I den här lektionen konfigurerar vi en anslutning mellan Adobe Experience Platform och ditt företag Data Warehouse för att aktivera Federated Audience Composition. Detta gör att du kan fråga data direkt från de lagerställen som stöds utan replikering. Dessutom skapar vi scheman och datamodeller baserade på Data Warehouse-tabellerna.

För detta labb ansluter vi till ett Snowflake-konto. Federated Audience Composition har stöd för en växande lista över anslutningar i molnlagerplatser. Se den [uppdaterade listan över integreringar](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/access-prerequisites){target="_blank"}.


## Steg

1. Bläddra till avsnittet **FEDERATED DATA** i den vänstra listen.
2. Klicka på knappen **Lägg till federerad databas** i länken **Federerade databaser**.
3. Lägg till ett namn och välj **Snowflake**.
4. Fyll i informationen, klicka på knappen **Testa anslutning** och sedan på knappen **Distribuera funktioner** .

   ![snowflake-connection-setup](assets/snowflake-connection-setup.png)

   ![snowflake-connection-setup-step2](assets/snowflake-connection-setup-step2.png)

   ![snowflake-connection-setup-step3](assets/snowflake-connection-setup-step3.png)

## Skapa ett schema

Så här skapar du scheman i Federated Audience Composition:

1. Klicka på **Modeller** i avsnittet **FEDERATED DATA**.
2. Bläddra på fliken **Schema** och klicka på knappen **Skapa schema** .
3. Markera källdatabasen i listan och klicka på fliken **Lägg till tabeller**.
4. Markera följande tabeller:
   - FSI_CRM
   - FSI_CRM_CONSENT_PREFERENCE

   ![create-schema](assets/create-schema.png)

   ![select-table](assets/select-table.png)

När du har markerat tabellerna granskar du kolumnerna i varje tabell och väljer primärnyckel. För den här övningen väljer vi **EMAIL** som primärnyckel i båda tabellerna.

![create-schema](assets/create-schema.png)

![create-schema-step2](assets/create-schema-step2.png)

## Förhandsgranska data i ett schema

Om du vill förhandsgranska data i tabellen som representeras av ditt schema går du till fliken **Data**.

Klicka på länken **Beräkna** om du vill förhandsgranska det totala antalet poster.

![preview-data-in-schema](assets/preview-data-in-schema.png)

## Skapa en datamodell

Med datamodeller kan du skapa en länk mellan tabeller. Länken kan skapas mellan tabeller i samma databas, t.ex. tabeller i Snowflake, eller mellan tabeller i olika databaser, t.ex. en länk mellan en tabell i Snowflake och en tabell i Amazon Redshift.

Så här skapar du en datamodell i Federated Audience Composition:

1. I avsnittet **FEDERATED DATA** klickar du på **Models** och sedan på **Data Model**.
2. Klicka på knappen **Skapa datamodell** .
3. Ange ett namn för datamodellen.
4. Klicka på **Lägg till scheman** och välj **FSI_CRM** och **FSI_CRM_CONSENT_PREFERENCE** scheman.
5. Skapa en länk mellan de här tabellerna genom att klicka på **Skapa länkar**.

När du skapar en länk väljer du önskad kardinalitet:

- **1-N**: En förekomst av källtabellen kan ha flera motsvarande förekomster av måltabellen, men en förekomst av måltabellen kan ha högst en motsvarande förekomst av källtabellen.
- **N-1**: En förekomst av måltabellen kan ha flera motsvarande förekomster av källtabellen, men en förekomst av källtabellen kan ha högst en motsvarande förekomst av måltabellen.
- **1-1**: En förekomst av källtabellen kan ha högst en motsvarande förekomst av måltabellen.

Nedan visas en förhandsgranskning av länken som skapats för labbövningarna. Länken aktiverar en koppling mellan CRM- och medgivandetabellerna, och använder primärnyckeln för **EMAIL** för att utföra en koppling.

![preview-data-model](assets/preview-data-model.png)

Nu är vi redo att [skapa och målgrupp](audience-creation-exercise.md).
