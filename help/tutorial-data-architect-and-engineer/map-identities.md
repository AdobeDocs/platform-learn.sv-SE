---
title: Mappa identiteter
seo-title: Map identities | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Mappa identiteter
description: I den här lektionen ska vi skapa identitetsnamnutrymmen och lägga till identitetsfält i våra scheman.
role: Data Architect
feature: Profiles
kt: 4348
thumbnail: 4348-map-identities.jpg
exl-id: e17ffabc-049c-42ff-bf0a-8cc31d665dfa
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '954'
ht-degree: 1%

---

# Mappa identiteter

<!-- 30 min-->

I den här lektionen ska vi skapa identitetsnamnutrymmen och lägga till identitetsfält i våra scheman. När vi gjort det kan vi också slutföra schemarelationerna från föregående lektion.

Adobe Experience Platform identitetstjänst hjälper er att få en bättre bild av era kunder och deras beteenden genom att överbrygga identiteter mellan olika enheter och system, så att ni kan leverera slagkraftiga, personliga digitala upplevelser i realtid. Identitetsfält och namnutrymmen är den kombination som förenar olika datakällor för att skapa en 360-graders kundprofil i realtid.

**Dataarkitekturer** måste kartlägga identiteter utanför den här självstudiekursen.

Titta på den här korta videon om du vill veta mer om din identitet i Adobe Experience Platform innan du börjar övningarna:
>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

>[!NOTE]
>
>Identitetsfält krävs bara om du skapar kundprofiler i realtid. De behövs inte om du bara matar in data i sjön.

<!--explain identity maps-->
<!--explain the strategy behind the identity selection, how these identities will join all the data together-->

## Behörigheter krävs

I [Konfigurera behörigheter](configure-permissions.md) lektionen anger du alla åtkomstkontroller som krävs för att slutföra lektionen.

<!--
* Permission items **[!UICONTROL Identity Management]** > **[!UICONTROL View Identity Namespaces]** and **[!UICONTROL Manage Identity Namespaces]**
* Permission item **[!UICONTROL Data Modeling]** > **[!UICONTROL View Schemas]** and **[!UICONTROL Manage Schemas]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

## Skapa namnområde för identitet

I den här övningen ska vi skapa identitetsnamnutrymmen för Lumas anpassade identitetsfält, `loyaltyId`, `crmId`och `productSku`. Identitetsnamnutrymmen spelar en viktig roll när det gäller att skapa kundprofiler i realtid, eftersom två matchande värden i samma namnutrymme gör att två datakällor kan bilda ett identitetsdiagram.


### Skapa namnutrymmen i användargränssnittet

Vi börjar med att skapa ett namnutrymme för Luma Loyalty Schema:

1. Gå till **[!UICONTROL Identiteter]** i den vänstra navigeringen
1. Du kommer att märka att det finns flera färdiga ID-namnutrymmen. Välj **[!UICONTROL Skapa namnutrymme för identitet]** knapp
1. Ange följande information

   | Fält | Värde |
   |---------------|-----------|
   | Visningsnamn | Lojalitets-ID för Luma |
   | Identitetssymbol | lumaLoyaltyId |
   | Typ | Flera enheter |

1. Välj **[!UICONTROL Skapa]**

   ![Skapa namnutrymmen](assets/identity-createNamespace.png)

Konfigurera nu ett annat namnutrymme för Luma-produktkatalogschemat med följande information:

| Fält | Värde |
|---------------|-----------|
| Visningsnamn | Luma Product SKU |
| Identitetssymbol | lumaProductSKU |
| Typ | Identifierare för icke-personer |



## Skapa namnområde för identitet med API

Vi skapar CRM-namnområdet via API.

>[!NOTE]
>
>Om du föredrar att hoppa över API-övningarna kan du skapa CRM-namnutrymmet via den gränssnittsmetod du använde med följande information:
>
> 1. Som **[!UICONTROL Visningsnamn]**, använda `Luma CRM Id`
> 1. Som **[!UICONTROL Identitetssymbol]**, använda `lumaCrmId`
> 1. Som **[!UICONTROL Typ]**, använd olika enheter


Låt oss skapa identitetsnamnutrymmet `Luma CRM Id`:

1. Hämta [Identitetstjänst.postman_collection.json](https://raw.githubusercontent.com/adobe/experience-platform-postman-samples/master/apis/experience-platform/Identity%20Service.postman_collection.json) till `Luma Tutorial Assets` mapp
1. Importera samlingen till [!DNL Postman]
1. Om du inte har gjort någon begäran de senaste 24 timmarna har din auktoriseringstoken antagligen gått ut. Öppna förfrågan **[!DNL Adobe I/O Access Token Generation > Local Signing (Non-production use-only) > IMS: JWT Generate + Auth via User Token]** och markera **Skicka** för att begära nya JWT- och Access-token.
1. Välj begäran **[!UICONTROL Identitetstjänst] > [!UICONTROL Identitetsnamnutrymme] > [!UICONTROL Skapa ett nytt identitetsnamnutrymme].**
1. Klistra in följande som [!DNL Body] av begäran:

   ```json
   {
       "name": "Luma CRM Id",
       "code": "lumaCrmId",
       "idType": "Cross_device"
   }
   ```

1. Tryck på **Skicka** så får du en **200 OK** svar:

   ![Identitetsnamnutrymme](assets/identity-createUsingApi.png)

Om du återgår till användargränssnittet bör du nu se dina tre nya anpassade namnutrymmen:
![Identitetsnamnutrymme ](assets/identity-newIdentities.png)


## Etikettera identitetsfält i scheman

Nu när vi har våra namnutrymmen är nästa steg att uppdatera våra scheman för att märka våra identitetsfält.


### Etikettera XDM-fält för primär identitet

Varje schema som används med kundprofil i realtid måste ha en primär identitet angiven. Och varje inskickad post måste ha ett värde för det fältet.

Låt oss lägga till en primär identitet i `Luma Loyalty Schema`:

1. Öppna `Luma Loyalty Schema`
1. Markera `Luma Identity profile field group`
1. Välj `loyaltyId` fält
1. Kontrollera **[!UICONTROL Identitet]** box
1. Kontrollera **[!UICONTROL Primär identitet]** även
1. Välj `Luma Loyalty Id` namnutrymme från **[!UICONTROL Identitetsnamnutrymmen]** listruta
1. Välj **[!UICONTROL Använd]**
1. Välj **[!UICONTROL Spara]**

   ![Primär identitet ](assets/identity-loyalty-primary.png)

Upprepa processen för ett annat schema:

1. I `Luma CRM Schema`, etikettera `crmId` fältet som primär identitet med `Luma CRM Id` namespace
1. I `Luma Offline Purchase Events Schema`, etikettera `loyaltyId` fältet som primär identitet med `Luma Loyalty Id` namespace
1. I `Luma Product Catalog Schema`, etikettera `productSku` fältet som primär identitet med `Luma Product SKU` namespace

>[!NOTE]
>
>Data som samlas in med Web SDK är ett undantag från den vanliga metoden att etikettera identitetsfält i schemat. Web SDK använder identitetskartan för att etikettera identiteter *på implementeringssidan* och vi bestämmer därmed identiteterna för `Luma Web Events Schema` när vi implementerar Web SDK på Lumas webbplats. I den lektionen samlar vi in Experience Cloud Visitor-ID (ECID) som primärt id och crmId som ett sekundärt id.

Med vårt urval av primära identiteter är det tydligt att se hur `Luma CRM Schema` kan ansluta till `Luma Offline Purchase Events Schema` eftersom båda använder `loyaltyId` som en identifierare. Men hur kan vi koppla våra offlineköp till onlinebeteende? Hur kan vi klassificera de produkter som köpts med vår produktkatalog? Ytterligare identitetsfält och schemarelationer kommer att användas.

<!--use a visual-->

### Etikettera XDM-fält för sekundär identitet

Flera identitetsfält kan läggas till i ett schema. Icke-primära identiteter kallas ofta sekundära identiteter. För att kunna koppla offlineköp till onlinebeteende lägger vi till crmId som en sekundär identifierare i `Luma Loyalty Schema` och senare i våra webbeventdata. Vi uppdaterar `Luma Loyalty Schema`:

1. Öppna `Luma Loyalty Schema`
1. Välj `Luma Identity Profile Field group`
1. Välj `crmId` fält
1. Kontrollera **[!UICONTROL Identitet]** box
1. Välj `Luma CRM Id` namnutrymme från **[!UICONTROL Identitetsnamnutrymmen]** listruta
1. Välj **[!UICONTROL Använd]** och sedan väljer **[!UICONTROL Spara]** knapp för att spara ändringarna

   ![Sekundär identitet](assets/identity-loyalty-secondaryId.png)

## Slutför schemarelationerna

Nu när vi har etiketterat våra identitetsfält kan vi slutföra konfigurationen av schemarelationerna mellan Lumas produktkatalog och händelsescheman:

1. Öppna `Luma Offline Purchase Events Schema`
1. Välj **[!UICONTROL Handelsinformation]** fältgrupp
1. Välj **[!UICONTROL productListItems]** > **[!UICONTROL SKU]** fält
1. Kontrollera **[!UICONTROL Relation]** box
1. Välj `Luma Product Catalog Schema` som **[!UICONTROL Referensschema]**
1. `Luma Product SKU` ska fyllas i automatiskt som **[!UICONTROL Namnutrymme för referensidentitet]**
1. Välj **[!UICONTROL Använd]**
1. Välj **[!UICONTROL Spara]**

   ![Referensfält](assets/identity-offlinePurchase-relationship.png)

Upprepa den här processen om du vill skapa en relation mellan `Luma Web Events Schema` och `Luma Product Catalog Schema`.

Observera att när du har definierat relationen anges den i båda **[!UICONTROL Disposition]** och **[!UICONTROL Struktur]** i schemaredigeraren.

![Relationsvisualisering i schemaredigeraren](assets/identity-webEvents-relationship.png)

<!--need to verify that the relationship schema works-->

## Ytterligare resurser

* [Identitetstjänstens dokumentation](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=sv)
* [Identitetstjänstens API](https://www.adobe.io/experience-platform-apis/references/identity-service/)

Nu när våra identiteter är på plats kan vi [skapa våra datauppsättningar](create-datasets.md)!
