---
title: Skapa datauppsättningar
seo-title: Create datasets | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Skapa datauppsättningar
description: I den här lektionen ska du skapa datauppsättningar som tar emot dina data.
role: Data Architect, Data Engineer
feature: Data Management
jira: KT-4348
thumbnail: 4348-create-datasets.jpg
exl-id: 80227af7-4976-4fd2-b1d4-b26bc4626fa0
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 0%

---

# Skapa datauppsättningar

<!--15min-->

I den här lektionen ska du skapa datauppsättningar som tar emot dina data. Det här är den kortaste lektionen i självstudiekursen!

Alla data som har inhämtats till Adobe Experience Platform lagras i datasjön som datauppsättningar. En datauppsättning är en lagrings- och hanteringskonstruktion för en datamängd, vanligtvis en tabell, som innehåller ett schema (kolumner) och fält (rader). Datauppsättningar innehåller också metadata som beskriver olika aspekter av de data som lagras.

**Dataarkitekturer** måste skapa datauppsättningar utanför den här självstudien.

Innan du börjar övningarna ska du titta på den här korta videon och lära dig mer om datauppsättningar:
>[!VIDEO](https://video.tv.adobe.com/v/27269?learn=on&enablevpops)

## Behörigheter krävs

I lektionen [Konfigurera behörigheter](configure-permissions.md) ställer du in alla åtkomstkontroller som krävs för att slutföra lektionen.

<!--
* Permission items **[!UICONTROL Data Management]** > **[!UICONTROL View Datasets]** and **[!UICONTROL Manage Datasets]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

## Skapa datauppsättningar i användargränssnittet

I den här övningen kommer vi att skapa datauppsättningar i användargränssnittet. Låt oss börja med lojalitetsdata:

1. Gå till **[!UICONTROL Datasets]** i vänster navigering i plattformsanvändargränssnittet
1. Markera knappen **[!UICONTROL Create dataset]**
   ![Skapa en datauppsättning](assets/datasets-createDataset.png)

1. På nästa skärm väljer du **Skapa datauppsättning från schema**
1. Markera `Luma Loyalty Schema` på nästa skärm och välj sedan knappen **[!UICONTROL Next]**
   ![Markera datauppsättningen](assets/datasets-selectSchema.png)

1. Namnge datauppsättningen `Luma Loyalty Dataset` och välj knappen **[!UICONTROL Finish]**
   ![Namnge datauppsättningen](assets/datasets-nameDataset.png)
1. När datauppsättningen har sparats visas en skärm som den här:
   ![Datauppsättningen har skapats](assets/datasets-created.png)

Så ja! Jag sa ju att det här skulle gå fort. Skapa dessa andra datauppsättningar med samma steg:

1. `Luma Offline Purchase Events Dataset` för din `Luma Offline Purchase Events Schema`
1. `Luma Web Events Dataset` för din `Luma Web Events Schema`
1. `Luma Product Catalog Dataset` för din `Luma Product Catalog Schema`


## Skapa en datauppsättning med API

Skapa nu `Luma CRM Dataset` med API:t.

>[!NOTE]
>
>Om du vill hoppa över API-övningen och skapa `Luma CRM Dataset` i det användargränssnitt som är bra. Ge den namnet `Luma CRM Dataset` och använd `Luma CRM Schema`.

### Hämta ID:t för schemat som ska användas i datauppsättningen

Först måste vi hämta `$id` för `Luma CRM Schema`:

1. Öppna [!DNL Postman]
1. Om du inte har någon åtkomsttoken öppnar du begäran **[!DNL OAuth: Request Access Token]** och väljer **Skicka** för att begära en ny åtkomsttoken, precis som i lektionen [!DNL Postman].
1. Öppna begäran **[!DNL Schema Registry API > Schemas > Retrieve a list of schemas within the specified container.]**
1. Välj knappen **Skicka**
1. Du borde få 200 svar
1. Leta i svaret för objektet `Luma CRM Schema` och kopiera värdet `$id`
   ![Kopiera $id](assets/dataset-crm-getSchemaId.png)

### Skapa datauppsättningen

Nu kan du skapa datauppsättningen:

1. Hämta [katalogtjänstens API.postman_collection.json](https://raw.githubusercontent.com/adobe/experience-platform-postman-samples/master/apis/experience-platform/Catalog%20Service%20API.postman_collection.json) till din `Luma Tutorial Assets`-mapp.
1. Importera samlingen till [!DNL Postman]
1. Välj begäran **[!DNL Catalog Service API > Datasets > Create a new dataset.]**
1. Klistra in följande som **brödtext** i begäran och ***ersätt id-värdet med ditt eget***:

   ```json
   {
       "name": "Luma CRM Dataset",
   
       "schemaRef": {
           "id": "REPLACE_WITH_YOUR_OWN_ID",
           "contentType": "application/vnd.adobe.xed-full+json;version=1"
       },
       "fileDescription": {
           "persisted": true,
           "containerFormat": "parquet",
           "format": "parquet"
       }
   }
   ```

1. Välj knappen **Skicka**
1. Du bör få ett svar från 2011 Created som innehåller ID:t för din nya datauppsättning!
   ![Datauppsättningen har skapats med API, ditt anpassade $id som används i brödtexten](assets/datasets-crm-created.png)

>[!TIP]
>
> Vanliga fel som gör denna begäran och troliga korrigeringar:
>
> * `400: There was a problem retrieving xdm schema`. Kontrollera att du har ersatt ID:t i exemplet ovan med ID:t för din `Luma CRM Schema`
> * Ingen autentiseringstoken: Kör **OAuth: Begär åtkomsttoken**-begäran för att generera en ny token
> * `401: Not Authorized to PUT/POST/PATCH/DELETE for this path : /global/schemas/`: Uppdatera miljövariabeln **CONTAINER_ID** från `global` till `tenant`
> * `403: PALM Access Denied. POST access is denied for this resource from access control`: Verifiera dina användarbehörigheter i Admin Console


Du kan gå tillbaka till skärmen **[!UICONTROL Datasets]** i användargränssnittet för plattformen. Du kan verifiera att alla fem datauppsättningarna har skapats!
![Fem datauppsättningar har slutförts](assets/datasets-allComplete.png)


## Ytterligare resurser

* [Dokumentation för datauppsättningar](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html?lang=sv-SE)
* [API för datauppsättningar (ingår i katalogtjänsten), referens](https://www.adobe.io/experience-platform-apis/references/catalog/#tag/Datasets)

Nu när alla våra scheman, identiteter och datauppsättningar finns på plats kan vi [aktivera dem för kundprofil i realtid](enable-profiles.md).
