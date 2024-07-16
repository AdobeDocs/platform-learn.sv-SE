---
title: Modelldata i scheman
seo-title: Model data in schemas | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Modelldata i scheman
description: I den här lektionen ska du modellera Lumas data i scheman. Det här är en av de längsta lektionerna i självstudiekursen, så ta ett glas vatten och slipp!
role: Data Architect
feature: Schemas
jira: KT-4348
thumbnail: 4348-model-data-in-schemas.jpg
exl-id: 317f1c39-7f76-4074-a246-ef19f044cb85
source-git-commit: 8e470d8a0c9fee7389ac60a743431fe81012fa0f
workflow-type: tm+mt
source-wordcount: '2476'
ht-degree: 0%

---

# Modelldata i scheman

<!-- 60min -->
I den här lektionen ska du modellera Lumas data i scheman. Det här är en av de längsta lektionerna i självstudiekursen, så ta ett glas vatten och slipp!

Standardisering och interoperabilitet är viktiga begrepp bakom Adobe Experience Platform. Experience Data Model (XDM) är ett försök att standardisera kundupplevelsedata och definiera scheman för kundupplevelsehantering.

XDM är en öppet dokumenterad specifikation som utformats för att förbättra möjligheterna med digitala upplevelser. Det innehåller gemensamma strukturer och definitioner för alla program som används för att kommunicera med plattformstjänster. Genom att följa XDM-standarder kan alla kundupplevelsedata införlivas i en gemensam representation som kan ge insikter på ett snabbare och mer integrerat sätt. Ni kan få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och uttrycka kundattribut i personaliseringssyfte.

XDM är det grundläggande ramverk som gör att Adobe Experience Cloud, som drivs av Experience Platform, kan leverera rätt budskap till rätt person, i rätt kanal, i precis rätt ögonblick. Metoden som Experience Platform bygger på, **XDM System**, används för att göra Experience Data Model-scheman tillgängliga för plattformstjänster.

<!--
This seems too lengthy. The video should suffice

Key terms:

* **Schema**: a representation of your data. A schema is comprised of a class and optional field groups and is used to create datasets. A schema includes behavioral attributes, timestamp, identity, attribute definitions, and relationships.
* **XDM Profile Class**: a common schema class used to represent record data
* **XDM ExperienceEvent Class**: a common schema class used to represent time-series data
* **Field group**: allows users to extend reusable fields that contain variables defining one or more attribute intended to be included in a schema or added to a class.
* **Standard Field group**: an open-source Field group built to conform to common industry standards, used to accelerate implementation and support repeatable services operating on the data
* **Data type**: a reusable object with properties in a hierarchical representation. These can be standard types or custom-defined defined types to describe your own data in your own way (for example, a collection of fields that you use to describe your products). Unlike Field groups, data types can be used in schemas regardless of the class.
* **Field**: a field is the lowest level element of a schema. Each field has a name for referencing and a type to identify the type of data that it contains. Field types can include, integer, number, string, Boolean and schema.
-->

**Dataarkitekter** måste skapa scheman utanför den här självstudiekursen, men **Dataingenjörer** kommer att ha ett nära samarbete med de scheman som skapas av dataarkitekten.

Innan du börjar övningarna ska du titta på den här korta videon och lära dig mer om scheman och Experience Data Model (XDM):
>[!VIDEO](https://video.tv.adobe.com/v/27105?learn=on)

>[!TIP]
>
> För en djupdykning i datamodellering i Experience Platform rekommenderar vi att du tar kursen [Model Your Customer Experience Data with XDM](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm), som är tillgänglig kostnadsfritt på Experience League!

## Behörigheter krävs

I lektionen [Konfigurera behörigheter](configure-permissions.md) ställer du in alla åtkomstkontroller som krävs för att slutföra lektionen.

<!--, specifically:

* Permission items **[!UICONTROL Data Modeling]** > **[!UICONTROL View Schemas]** and **[!UICONTROL Manage Schemas]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
* Developer-role access to the `Luma Tutorial Platform` product profile (for API)-->


<!--
## Luma's goals
-->

## Skapa bonusschema via användargränssnittet

I den här övningen ska vi skapa ett schema för Lumas lojalitetsdata.

1. Gå till användargränssnittet för plattformen och se till att din sandlåda är markerad.
1. Gå till **[!UICONTROL Schemas]** i den vänstra navigeringen.
1. Markera knappen **[!UICONTROL Create schema]** högst upp till höger.
   ![Schema med OOTB-fältgrupp](assets/schemas-loyaltyCreateSchema.png)

1. I arbetsflödet för att skapa schema väljer du **[!UICONTROL Individual Profile]** som basklass för ditt schema, eftersom vi modellerar attribut för en enskild kund (punkter, status och så vidare).
1. Välj **[!UICONTROL Next]**.
   ![Välj basklass](assets/schemas-loyaltySelectBaseClass.png)

1. Ange `Luma Loyalty Schema` i textfältet **[!UICONTROL Schema display name]**. På arbetsytan nedan kan du även granska och verifiera grundschemastrukturen som tillhandahålls av den klass du har valt.
1. Välj **[!UICONTROL Finish]** om du vill skapa ditt schema.
   ![Slutför skapandet av bonusschemat](assets/schemas-loyaltyFinishSchemaCreation.png)

### Lägg till standardfältgrupper

När schemat har skapats omdirigeras du till schemaredigeraren där du kan lägga till fält i schemat. Du kan lägga till enskilda fält direkt i schemat eller använda fältgrupper. Observera att alla enskilda fält fortfarande är kopplade till en klass eller fältgrupp. Du kan välja bland en stor uppsättning standardfältgrupper från Adobe eller skapa egna. När ni börjar utforma egna data i Experience Platform är det bra att bekanta sig med de branschledande fältgrupperna från Adobe. När det är möjligt är det en god praxis att använda dem eftersom de ibland driver tjänster längre fram i kedjan, t.ex. kundens AI, Attribution AI och Adobe Analytics.

När du arbetar med egna data är det viktigt att du tar reda på vilken av dina egna data som ska samlas in i Platform och hur de ska modelleras. Det här stora avsnittet diskuteras mer ingående i kursen [Modellera dina kundupplevelsedata med XDM](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm). I den här självstudiekursen kommer jag att vägleda dig genom implementeringen av några förbestämda scheman.

Så här lägger du till fältgrupper:

1. Välj **[!UICONTROL Add]** under rubriken **[!UICONTROL Field Groups]**.
   ![Lägg till en ny fältgrupp](assets/schemas-loyalty-addFieldGroup.png)
1. Välj följande fältgrupper i **[!UICONTROL Add Field groups]** modal:
   1. **[!UICONTROL Demographic Details]** för grundläggande kunddata som namn och födelsedatum
   1. **[!UICONTROL Personal Contact Details]** om du vill ha grundläggande kontaktinformation som e-postadress och telefonnummer
1. Du kan förhandsgranska fälten i fältgruppen genom att markera ikonen till höger om raden.
   ![Välj standardfältgrupper](assets/schemas-loyalty-addFirstTwoFieldGroups.png)

1. Markera rutan **[!UICONTROL Industry]** > **[!UICONTROL Retail]** om du vill visa branschspecifika fältgrupper.
1. Välj **[!UICONTROL Loyalty Details]** om du vill lägga till fälten för bonusprogram.
1. Välj **[!UICONTROL Add field groups]** om du vill lägga till alla tre fältgrupperna i schemat.
   ![Lägg till standardfältgrupper i bonusschema](assets/schemas-loyalty-saveOotbMixins.png)


Ta dig tid att utforska schemats aktuella status. Fältgrupperna har lagt till standardfält som är relaterade till en person, deras kontaktinformation och lojalitetsprogrammets status. Dessa två fältgrupper kan vara användbara när du skapar scheman för det egna företagets data. Markera en specifik fältgruppsrad eller markera kryssrutan bredvid fältgruppnamnet för att se hur visualiseringen ändras.

Välj **[!UICONTROL Save]** om du vill spara schemat.
![Spara schemat](assets/schemas-loyalty-saveSchema.png)

>[!NOTE]
>
>Det är okej om en fältgrupp lägger till ett fält för en datapunkt som du inte samlar in. &quot;faxPhone&quot; kan till exempel vara ett fält där Luma inte samlar in data. Det är okej. Bara för att ett fält har definierats i schemat betyder det inte att data för det *måste* hämtas senare. Du kan även ta bort fältet från schemat.

### Lägga till en anpassad fältgrupp

Nu ska vi skapa en anpassad fältgrupp.

Medan lojalitetsfältgruppen innehöll ett `loyaltyID`-fält vill Luma hantera alla sina systemidentifierare i en enda grupp för att säkerställa konsekvens i alla sina scheman.

Fältgrupper måste skapas i schemaarbetsflödet. Du kan antingen:

* Lägg till ett nytt anpassat fält i schemat först och skapa sedan en anpassad fältgrupp, eller
* Skapa först en anpassad fältgrupp och lägg sedan till fält i den.

I den här självstudiekursen börjar vi med att skapa en anpassad fältgrupp.

Så här skapar du fältgruppen:

1. Välj **[!UICONTROL Add]** under rubriken **[!UICONTROL Schema Field Groups]**
   ![Lägg till en ny fältgrupp](assets/schemas-loyalty-addFieldGroup.png)
1. Välj **[!UICONTROL Create new field group]**
1. Använd `Luma Identity profile field group` som **[!UICONTROL Display name]**
1. Använd `system identifiers for XDM Individual Profile class` som **[!UICONTROL Description]**
1. Välj **[!UICONTROL Add field groups]**
   ![Lägg till en ny fältgrupp](assets/schemas-loyalty-nameFieldGroup.png)

Den nya, tomma fältgruppen läggs till i ditt schema. Knapparna **[!UICONTROL +]** kan användas för att lägga till nya fält på valfri plats i hierarkin. I det här fallet vill vi lägga till fält på rotnivå:

1. Välj **[!UICONTROL +]** bredvid schemats namn. Då läggs ett nytt fält till under ditt innehavar-id-namnutrymme för att hantera konflikter mellan dina anpassade fält och alla standardfält.
1. Lägg till information om det nya fältet i sidofältet **[!UICONTROL Field properties]**:
   1. **[!UICONTROL Field name]**: `systemIdentifier`
   1. **[!UICONTROL Display name]**: `System Identifier`
   1. **[!UICONTROL Type]**: **[!UICONTROL Object]**
   1. I listrutan **[!UICONTROL Field Group]** väljer du den **Luma Identity-profilfältgrupp** som vi har skapat.
      ![Lägg till en ny fältgrupp](assets/schemas-loyalty-addSystemIdentifier.png)
   1. Välj **[!UICONTROL Apply]**
      ![Använd nya fältegenskaper](assets/schemas-loyalty-applySystemIdentifier.png)

Lägg nu till två fält under objektet `systemIdentifier`:

1. Första fältet
   1. **[!UICONTROL Field name]**: `loyaltyId`
   1. **[!UICONTROL Display name:]** `Loyalty Id`
   1. **[!UICONTROL Type]**: **[!UICONTROL String]**
1. Andra fältet
   1. **[!UICONTROL Field Name]**: `crmId`
   1. **[!UICONTROL Display Name]**: `CRM Id`
   1. **[!UICONTROL Type]**: **[!UICONTROL String]**

Din nya fältgrupp bör se ut så här. Välj knappen **[!UICONTROL Save]** om du vill spara ditt schema, men lämna schemat öppet för nästa övning.
![Förmånsfältgruppen har slutförts](assets/schemas-loyalty-identityFieldGroupComplete.png)

## Skapa en datatyp

Fältgrupper, till exempel din nya `Luma Identity profile field group`, kan återanvändas i andra scheman, vilket gör att du kan tillämpa standarddatadefinitioner i flera system. Men de kan bara återanvändas _i scheman som delar en klass_, i det här fallet klassen för enskild XDM-profil.

Datatypen är en annan flerfältskonstruktor som kan återanvändas i scheman _över flera klasser_. Låt oss konvertera vårt nya `systemIdentifier`-objekt till en datatyp:

Med `Luma Loyalty Schema` fortfarande öppen markerar du objektet `systemIdentifier` och väljer **[!UICONTROL Convert to new data type]**

![Förmånsfältgruppen har slutförts](assets/schemas-loyalty-convertToDataType.png)

Om du **[!UICONTROL Cancel]** lämnar schemat och navigerar till fliken **[!UICONTROL Data types]** ser du din nya datatyp. Vi kommer att använda den här datatypen senare i lektionen.

![Förmånsfältgruppen har slutförts](assets/schemas-loyalty-confirmDataType.png)


## Skapa CRM-schema via API

Nu ska vi skapa ett schema med API:t.

>[!TIP]
>
> Om du föredrar att hoppa över API-övningen kan du skapa följande schema med metoden för användargränssnittet:
>
> 1. Använd klassen [!UICONTROL Individual Profile]
> 1. Ge den namnet `Luma CRM Schema`
> 1. Använd följande fältgrupper: Demografiska uppgifter, personliga kontaktuppgifter och Luma Identity-profilgrupp

Först skapar vi det tomma schemat:

1. Öppna [!DNL Postman]
1. Om du inte har någon åtkomsttoken öppnar du begäran **[!DNL OAuth: Request Access Token]** och väljer **Skicka** för att begära en ny åtkomsttoken.
1. Öppna dina miljövariabler och ändra värdet för **CONTAINER_ID** från `global` till `tenant`. Kom ihåg att du måste använda `tenant` när du vill interagera med dina egna anpassade element i Platform, till exempel skapa ett schema.
1. Välj **Spara**
   ![Ändra CONTAINER_ID till klient](assets/schemas-crm-changeContainerId.png)
1. Öppna begäran **[!DNL Schema Registry API > Schemas > Create a new custom schema.]**
1. Öppna fliken **Brödtext** och klistra in följande kod och välj **Skicka** för att göra API-anropet. Det här anropet skapar ett nytt schema med samma `XDM Individual Profile`-basklass:

   ```json
   {
     "type": "object",
     "title": "Luma CRM Schema",
     "description": "Schema for CRM data of Luma Retail ",
     "allOf": [{
       "$ref": "https://ns.adobe.com/xdm/context/profile"
     }]
   }
   ```

   >[!NOTE]
   >
   >Namnområdesreferenserna i detta och efterföljande kodexempel (till exempel `https://ns.adobe.com/xdm/context/profile`) kan hämtas med list-API-anrop med **[!DNL CONTAINER_ID]** och acceptera sidhuvudet inställt på rätt värden. Vissa är också lättåtkomliga i användargränssnittet.

1. Du bör få ett `201 Created`-svar
1. Kopiera `meta:altId` från svarstexten. Vi kommer att använda den senare i en annan övning.
   ![Skapa CRM-schemat](assets/schemas-crm-createSchemaCall.png)

1. Det nya schemat ska vara synligt i användargränssnittet, men utan fältgrupper
   ![Skapa CRM-schemat](assets/schemas-loyalty-emptySchemaInTheUI.png)

>[!NOTE]
>
> Du kan även hämta `meta:altId`- eller schema-ID:t genom att göra API-begäran **[!DNL Schema Registry API > Schemas > Retrieve a list of schemas within the specified container.]** med **[!UICONTROL CONTAINER_ID]** inställd på `tenant` och ett accept-huvud `application/vnd.adobe.xdm+json`.

>[!TIP]
>
> Vanliga problem med detta samtal och troliga fixar:
>
> * Ingen autentiseringstoken: Kör **OAuth: Begär åtkomsttoken**-begäran för att generera en ny token
> * `401: Not Authorized to PUT/POST/PATCH/DELETE for this path : /global/schemas/`: Uppdatera miljövariabeln **CONTAINER_ID** från `global` till `tenant`
> * `403: PALM Access Denied. POST access is denied for this resource from access control`: Verifiera dina användarbehörigheter i Admin Console

### Lägg till standardfältgrupper

Nu är det dags att lägga till fältgrupperna i schemat:

1. Öppna begäran **[!DNL Schema Registry API > Schemas > Update one or more attributes of a custom schema specified by ID.]** i [!DNL Postman]
1. Klistra in värdet `meta:altId` från föregående svar som `SCHEMA_ID` på fliken **Params**
1. Öppna fliken Brödtext och klistra in följande kod och välj **Skicka** för att göra API-anropet. Det här anropet lägger till standardfältgrupperna i din `Luma CRM Schema`:

   ```json
   [{
       "op": "add",
       "path": "/allOf/-",
       "value": {
         "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
       }
     },
     {
       "op": "add",
       "path": "/allOf/-",
       "value": {
         "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
       }
     }
   ]
   ```

1. Du bör få statusen 200 OK för svaret och fältgrupperna ska vara synliga som en del av ditt schema i användargränssnittet

   ![Standardfältgrupper har lagts till](assets/schemas-crm-addMixins.png)


### Lägg till anpassad fältgrupp

Nu ska vi lägga till `Luma Identity profile field group` i schemat. Först måste vi hitta ID:t för vår nya fältgrupp med hjälp av en list-API:

1. Öppna begäran **[!DNL Schema Registry API > Field groups > Retrieve a list of field groups within the specified container.]**
1. Välj knappen **Skicka** om du vill hämta en lista över alla anpassade fältgrupper i ditt konto
1. Hämta `$id`-värdet för `Luma Identity profile field group` (ditt värde skiljer sig från värdet i den här skärmbilden)
   ![Hämta listan med fältgrupper](assets/schemas-crm-getListOfMixins.png)
1. Öppna begäran **[!DNL Schema Registry API > Schemas > Update one or more attributes of a custom schema specified by ID.]** igen
1. Fliken **Params** bör fortfarande ha `$id` för ditt schema
1. Öppna fliken **Brödtext** och klistra in följande kod som ersätter värdet `$ref` med värdet `$id` för din `Luma Identity profile field group`:

   ```json
   [{
     "op": "add",
     "path": "/allOf/-",
     "value": {
       "$ref": "REPLACE_WITH_YOUR_OWN_FIELD_GROUP_ID"
     }
   }]
   ```

1. Välj **Skicka**
   ![Lägger till identitetsfältgruppen](assets/schemas-crm-addIdentityMixin.png)

Kontrollera att fältgruppen har lagts till i schemat genom att kontrollera både API-svaret och gränssnittet.

## Skapa offlineköpshändelseschema

Nu skapar vi ett schema baserat på klassen **[!UICONTROL Experience Event]** för Lumas offlineköp. Eftersom du nu bekantar dig med användargränssnittet i schemaredigeraren kommer jag att minska antalet skärmbilder i instruktionerna:

1. Skapa ett schema med klassen **[!UICONTROL Experience Event]**.
1. Namnge schemat `Luma Offline Purchase Events Schema`.
1. Lägg till standardfältgruppen **[!UICONTROL Commerce Details]** för att hämta information om vanliga order. Tillbringa några minuter med att utforska objekten inuti.
1. Sök efter `Luma Identity profile field group`. Den är inte tillgänglig! Kom ihåg att fältgrupper är kopplade till en klass, och eftersom vi använder en annan klass för det här schemat kan vi inte använda det. Vi måste lägga till en ny fältgrupp för klassen XDM ExperienceEvent som innehåller identitetsfälten. Vår datatyp kommer att göra det väldigt enkelt!
1. Markera alternativknappen **[!UICONTROL Create new field group]**
1. Ange **[!UICONTROL Display name]** som `Luma Identity ExperienceEvent field group` och välj knappen **[!UICONTROL Add field groups]**
1. Välj **[!UICONTROL +]** bredvid schemats namn.
1. Ange `systemIdentifier` som **[!UICONTROL Field Name]**.
1. Ange `System Identifier` som **[!UICONTROL Display Name]**.
1. Som **[!UICONTROL Type]** väljer du **System Identifier**, som är den anpassade datatypen som du skapade tidigare.
1. Som **[!UICONTROL Field Group]** väljer du **Luma Identity ExperienceEvent-fältgruppen**.
1. Markera knappen **[!UICONTROL Apply]**.
1. Markera knappen **[!UICONTROL Save]**.

Observera hur datatypen lade till alla fält!

![Lägg till datatypen i fältgruppen](assets/schemas-offlinePurchases-addDatatype.png)

Välj också **[!UICONTROL XDM ExperienceEvent]** under rubriken **[!UICONTROL Class]** och inspektera några av fälten som klassen bidragit med. Observera att fält för _id och tidsstämplar krävs när klassen XDM ExperienceEvent används. Dessa fält måste fyllas i för varje post som du infogar när du använder det här schemat:

![Experience Event Base-struktur](assets/schemas-offlinePurchase-experienceEventbase.png)

## Skapa webbhändelseschema

Nu ska vi skapa ett till schema för Lumas webbplatsdata. Nu bör du vara expert på att skapa scheman! Bygg följande schema med dessa egenskaper

| Egenskap | Värde |
|---------------|-----------------|
| Klass | Experience Event |
| Schemanamn | Schema för webbhändelser i Luma |
| Fältgrupp | AEP Web SDK ExperienceEvent |
| Fältgrupp | Consumer Experience Event |

Markera fältgruppen **[!UICONTROL Consumer Experience Event]**. Den här fältgruppen innehåller objekten commerce och productListItems som också fanns i [!UICONTROL Commerce Details]. [!UICONTROL Consumer Experience Event] är en kombination av flera andra standardfältgrupper som också är tillgängliga separat. Fältgruppen [!UICONTROL AEP Web SDK ExperienceEvent] innehåller även andra fältgrupper, inklusive några av de i [!UICONTROL Consumer Experience Event]. Lyckligtvis smälter de ihop sömlöst.

Observera att vi inte lade till `Luma Identity ExperienceEvent field group` i det här schemat. Det beror på att Web SDK har ett annat sätt att samla in identiteter. Om du väljer klassen **[!UICONTROL XDM ExperienceEvent]** i avsnittet **[!UICONTROL Composition]** i schemaredigeraren kommer du att märka att ett av fälten som läggs till som standard kallas **[!UICONTROL IdentityMap]**. [!DNL IdentityMap] används av olika Adobe-program för att länka till plattformen. Du kommer att se hur identiteter skickas till plattformen via identityMap i lektionen om direktuppspelning.


## Skapa produktkatalogschema

Genom att använda fältgrupperna [!UICONTROL Commerce Details] och [!UICONTROL Consumer Experience Event] rapporterar Luma information om produktrelaterade händelser via standarddatatypen productListItems. Men de har också ytterligare produktinformationsfält som de vill skicka till Platform. I stället för att fylla i alla dessa fält i sina butiks- och e-handelssystem föredrar Luma att importera fälten direkt från sitt produktkatalogsystem. Med en &quot;schemarelation&quot; kan du definiera en relation mellan två scheman för klassificering eller sökning. Luma använder en relation för att klassificera sin produktinformation. Vi börjar processen nu och slutför den i slutet av nästa lektion.

>[!NOTE]
>
>Om du är en befintlig Analytics- eller Target-kund är klassificering av enheter med schemarelationer detsamma som SAINT-klassificeringar eller överföring av din produktkatalog för Recommendations

Först måste vi skapa ett schema för Lumas produktkatalog med en anpassad klass:

1. Markera knappen **[!UICONTROL Create schema]**.
1. Välj alternativet **[!UICONTROL Other]** i arbetsflödet Skapa schema.
   ![Skapa nytt schema](assets/schemas-newSchema-browseClasses.png)
1. Markera knappen **[!UICONTROL Create class]**
1. Ge den namnet `Luma Product Catalog Class`
1. Lämna **[!UICONTROL Behavior]** som **[!UICONTROL Record]**
1. Markera knappen **[!UICONTROL Create]**.
   ![Skapa ny klass](assets/schemas-productClass.png)
1. Den **Luma-produktkatalogklass** som du har skapat visas i tabellen Classes nedan. Kontrollera att klassen är markerad och välj sedan **[!UICONTROL Next]**.
   ![Ny klass har lagts till](assets/schemas-productClassSelected.png)
1. Namnge schemat `Luma Product Catalog Schema`.
1. Skapa en ny [!UICONTROL field group] med namnet `Luma Product Catalog field group` med följande fält:
   1. productName: Produktnamn: String
   1. productCategory: Product Category: String
   1. productColor: Produktfärg: String
   1. productSku: Product SKU: String | Obligatoriskt
   1. productSize: Produktstorlek: String
   1. productPrice: Product Price: Double
1. schemat **[!UICONTROL Save]**

Ditt nya schema bör se ut så här. Observera hur fältet `productSku` visas i avsnittet [!UICONTROL Required fields]:
![Produktschema](assets/schemas-productSchema.png)

Nästa steg är att definiera relationen mellan de två ExperienceEvent-scheman och `Luma Product Catalog Schema`, men det finns några ytterligare steg som vi måste ta i nästa lektion innan vi kan göra det.


## Ytterligare resurser

* [Experience Data Model (XDM) - systemdokumentation](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=sv)
* [API för schemaregister](https://www.adobe.io/experience-platform-apis/references/schema-registry/)


Nu när du har dina scheman kan du [mappa identiteter](map-identities.md)!
