---
title: Foundation - datainmatning - datainmatning från offlinekällor
description: Foundation - datainmatning - datainmatning från offlinekällor
kt: 5342
doc-type: tutorial
exl-id: a4909a47-0652-453b-ae65-ba4c261f087c
source-git-commit: fc5750ca614be30c3bd25b4f80ab45c5725a7649
workflow-type: tm+mt
source-wordcount: '1471'
ht-degree: 0%

---

# 1.2.4 Datainmatning från offlinekällor

I den här övningen är målet att lägga in externa data som CRM-data i plattformen.

## Utbildningsmål

- Lär dig generera testdata
- Lär dig hur du importerar CSV
- Lär dig använda webbgränssnittet för datainmatning via arbetsflöden
- Förstå funktionerna för datahantering i Experience Platform

## Resurser

- Mockaro: [https://www.mockaroo.com/](https://www.mockaroo.com/)
- Adobe Experience Platform: [https://experience.adobe.com/platform/](https://experience.adobe.com/platform/)

## Uppgifter

- Skapa en CSV-fil med demodata. Importera CSV-filen i Adobe Experience Platform med hjälp av de tillgängliga arbetsflödena.
- Förstå datastyrningsalternativ i Adobe Experience Platform

## Skapa en CRM-datauppsättning med ett datagenereringsverktyg

För den här övningen behöver du 1 000 exempelrader med CRM-data.

Öppna Mockaroo-mallen genom att gå till [https://www.mockaroo.com/12674210](https://www.mockaroo.com/12674210).

![Datainmatning](./images/mockaroo.png)

I mallen ska du lägga märke till följande fält:

- id
- first_name
- last_name
- e-post
- kön
- födelsedatum
- home_latitude
- home_longitude
- country_code
- stad
- land
- crmId
- consent.email
- consent.commercialEmail
- consent.any

Alla dessa fält har definierats för att producera data som är kompatibla med plattformen.

Om du vill generera din CSV-fil klickar du på knappen **[!UICONTROL Generate Data]** som skapar och hämtar en CSV-fil med 1 000 rader med demodata.

![Datainmatning](./images/dd.png)

Öppna CSV-filen för att se innehållet.

![Datainmatning](./images/excel.png)

När CSV-filen är klar kan du fortsätta med importen i AEP.

### Verifiera datauppsättningen

Gå till [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

![Datainmatning](./images/home.png)

Innan du fortsätter måste du välja en **[!UICONTROL sandbox]**. Sandlådan som ska markeras har namnet ``--aepSandboxName--``.

![Datainmatning](./images/sb1.png)

Klicka på **[!UICONTROL Datasets]** på menyn till vänster på skärmen i Adobe Experience Platform.

![Datainmatning](./images/menudatasetssb.png)

Du kommer att använda en delad datamängd. Den delade datamängden har redan skapats och kallas **[!UICONTROL Demo System - Profile Dataset for CRM (Global v1.1)]**. Klicka för att öppna den.

![Datainmatning](./images/emeacrmoverview.png)

På översiktsskärmen ser du tre viktiga informationsdelar.

>[!NOTE]
>
>Det är möjligt att vyn för datauppsättningen är tom, om ingen aktivitet har skett under de senaste 7 dagarna.

![Datainmatning](./images/dashboard.png)

Först och främst visar kontrollpanelen [!UICONTROL Dataset Activity] det totala antalet CRM-poster i datauppsättningen och de inkapslade batcharna och deras status

![Datainmatning](./images/batchids.png)

För det andra kan du genom att bläddra nedåt på sidan kontrollera när grupper av data har importerats, hur många poster som har registrerats och även om batchen har tagits med eller inte. **[!UICONTROL Batch ID]** är identifieraren för ett specifikt batchjobb och **[!UICONTROL Batch ID]** är viktig eftersom den kan användas för att felsöka varför en specifik batch inte kunde registreras.

Fliken [!UICONTROL Dataset] Info visar till sist viktig information, som [!UICONTROL Dataset ID] (som är viktig även för felsökningsperspektivet), datauppsättningens namn och om datauppsättningen har aktiverats för profilen.

![Datainmatning](./images/datasetsettings.png)

Den viktigaste inställningen här är länken mellan datauppsättningen och schemat. Schemat definierar vilka data som kan importeras och hur dessa data ska se ut.

I det här fallet använder vi **[!UICONTROL Demo System - Profile Schema for CRM (Global v1.1)]**, som är mappad mot klassen för **[!UICONTROL Profile]** och har implementerat tillägg, som även kallas fältgrupper.

![Datainmatning](./images/ds_schemalink.png)

Genom att klicka på schemats namn kommer du till översikten [!UICONTROL Schema] där du kan se alla fält som har aktiverats för det här schemat.

![Datainmatning](./images/schemads.png)

Alla scheman måste ha en anpassad, primär beskrivare definierad. När det gäller CRM-datauppsättningen har schemat definierat att fältet **[!UICONTROL crmId]** ska vara den primära identifieraren. Om du vill skapa ett schema och länka det till [!UICONTROL Real-time Customer Profile] måste du definiera en anpassad [!UICONTROL Field Group] som refererar till din primära beskrivning.

Du kan också se att vår primära identitet finns i `--aepTenantId--.identification.core.crmId`, länkad till [!UICONTROL namespace] i **[!UICONTROL Demo System - CRMID]**.

![Datainmatning](./images/schema_descriptor.png)

Alla scheman och som sådana ska alla datauppsättningar som ska användas i [!UICONTROL Real-time Customer Profile] ha en [!UICONTROL Primary identifier]. [!UICONTROL Primary Identifier] är identifieraranvändaren av varumärket för en kund i den datauppsättningen. När det gäller en CRM-datauppsättning kan det vara e-postadressen eller CRM-ID:t, när det gäller en Call Center-datauppsättning kan det vara en kunds mobilnummer.

Det är bästa sättet att skapa ett separat, specifikt schema för varje datauppsättning och att ange beskrivningen för varje datauppsättning specifikt för att matcha hur de aktuella lösningar som används av varumärket fungerar.

### Mappa en CSV-fil till ett XDM-schema med ett arbetsflöde

Målet med denna övning är att lägga in CRM-data i AEP. Alla data som är inkapslade i Platform ska mappas mot det specifika XDM-schemat. Det du för närvarande har är en CSV-datauppsättning med 1 000 rader på ena sidan och en datauppsättning som är länkad till ett schema på den andra sidan. Om du vill läsa in CSV-filen i den datauppsättningen måste en mappning göras. Vi har **[!UICONTROL Workflows]** tillgängligt i Adobe Experience Platform för att underlätta den här kartläggningen.

Klicka på **[!UICONTROL Map CSV to XDM Schema]** och sedan på **[!UICONTROL Launch]** för att starta processen.

![Datainmatning](./images/workflows.png)

På nästa skärm måste du välja en datauppsättning att importera filen till. Du kan välja mellan att välja en befintlig datauppsättning eller att skapa en ny. För den här övningen återanvänder vi en befintlig: välj **[!UICONTROL Demo System - Profile Dataset for CRM (Global v1.1)]** enligt nedan och lämna de andra inställningarna inställda på standard.

Klicka på **Nästa**.

![Datainmatning](./images/datasetselection.png)

Dra och släpp CSV-filen eller klicka på **[!UICONTROL Choose files]** och navigera på datorn till skrivbordet och välj CSV-filen.

![Datainmatning](./images/dragdrop.png)

När du har valt en CSV-fil överförs den omedelbart och du kommer att se en förhandsgranskning av filen inom några sekunder.

Klicka på **Nästa**.

![Datainmatning](./images/previewcsv.png)

Du måste nu mappa kolumnrubrikerna från CSV-filen med en XDM-egenskap i **[!UICONTROL Demo System - Profile Dataset for CRM]**.

Adobe Experience Platform har redan gjort några förslag åt dig genom att försöka länka [!UICONTROL Source Attributes] till [!UICONTROL Target Schema Fields].

>[!NOTE]
>
>Om du ser några fel på mappningsskärmen behöver du inte oroa dig. Efter att ha följt instruktionerna nedan kommer dessa fel att åtgärdas.

![Datainmatning](./images/mapschema.png)

För [!UICONTROL Schema Mappings] har Adobe Experience Platform redan försökt länka samman fält. Alla förslag på mappning är dock inte korrekta. Du måste nu uppdatera **målfälten** en i taget.

#### födelsedatum

Source-schemafältet **bornDate** ska länkas till målfältet **person.bornDate**.

![Datainmatning](./images/tfbd.png)

#### stad

Source-schemafältet **city** ska länkas till målfältet **homeAddress.city**.

![Datainmatning](./images/tfcity.png)

#### land

Source-schemafältet **country** ska länkas till målfältet **homeAddress.country**.

![Datainmatning](./images/tfcountry.png)

#### country_code

Source-schemafältet **country_code** ska länkas till målfältet **homeAddress.countryCode**.

![Datainmatning](./images/tfcountrycode.png)

#### e-post

Source-schemafältet **email** ska länkas till målfältet **personalEmail.address**.

![Datainmatning](./images/tfemail.png)

#### krut

Source-schemafältet **crmid** ska länkas till målfältet **`--aepTenantId--`.identify.core.crmId**.

![Datainmatning](./images/tfemail1.png)

#### first_name

Source-schemafältet **first_name** ska länkas till målfältet **person.name.firstName**.

![Datainmatning](./images/tffname.png)

#### kön

Source-schemafältet **kön** ska länkas till målfältet **person.kön**.

![Datainmatning](./images/tfgender.png)

#### home_latitude

Source-schemafältet **home_latitude** ska länkas till målfältet **homeAddress._schema.latitude**.

![Datainmatning](./images/tflat.png)

#### home_longitude

Source-schemafältet **home_longitude** ska länkas till målfältet **homeAddress._schema.longitude**.

![Datainmatning](./images/tflon.png)

#### id

Source-schemafältet **id** ska länkas till målfältet **_id**.

![Datainmatning](./images/tfid1.png)

#### last_name

Source-schemafältet **last_name** ska länkas till målfältet **person.name.lastName**.

![Datainmatning](./images/tflname.png)

#### consents.marketing.email.val

Source-schemafältet **last_name** ska länkas till målfältet **consents.marketing.email.val**.

![Datainmatning](./images/cons1.png)

#### consents.marketing.commercialEmail.val

Source-schemafältet **last_name** ska länkas till målfältet **consents.marketing.commercialEmail.val**.

![Datainmatning](./images/cons2.png)

#### consents.marketing.any.val

Source Schemafältet **last_name** ska länkas till målfältet **consents.marketing.any.val**.

![Datainmatning](./images/cons3.png)

Du borde ha den här nu. Klicka på **Slutför**.

![Datainmatning](./images/overview.png)

När du har klickat på **[!UICONTROL Finish]** visas översikten för **Dataflöd** och efter några minuter kan du uppdatera skärmen för att se om arbetsflödet har slutförts. Klicka på **namnet på måldatauppsättningen**.

![Datainmatning](./images/dfsuccess.png)

Du kommer då att se datauppsättningen där ditt intag har bearbetats och du kommer att se en [!UICONTROL Batch ID] som har importerats just nu, med 1 000 poster inkapslade och statusen **[!UICONTROL Success]**. Klicka på **[!UICONTROL Preview Dataset]**.

![Datainmatning](./images/ingestdataset.png)

Nu visas ett litet urval av datauppsättningen för att säkerställa att inlästa data är korrekta.

![Datainmatning](./images/previewdata.png)

När data har lästs in kan du definiera rätt datastyrningsmetod för vår datamängd.

### Lägga till datastyrning i datauppsättningen

Nu när era kunddata är insamlade måste ni se till att datauppsättningen styrs på rätt sätt för användnings- och exportkontroll. Klicka på fliken **[!UICONTROL Data Governance]** och observera att du kan ange flera typer av begränsningar: Kontrakt, Identitet och Känslig, Partnerekosystem och Anpassad.

![Datainmatning](./images/dsgovernance.png)

Låt oss begränsa identitetsdata för hela datauppsättningen. Håll pekaren över datauppsättningsnamnet och klicka på pennikonen för att redigera inställningarna.

![Datainmatning](./images/pencil.png)

Gå till **[!UICONTROL Identity Labels]** så ser du att alternativet **[!UICONTROL I2]** är markerat. Det förutsätter att alla informationsdelar i den här datauppsättningen åtminstone är indirekt identifierbara för personen.

Klicka på **[!UICONTROL Save Changes]**.

![Datainmatning](./images/identity.png)

I en annan modul ska vi göra en djupdykning i vilket ramverk för datastyrning och etiketter ska användas.

Detta innebär att du nu har inhämtat och klassificerat CRM-data i Adobe Experience Platform.

Nästa steg: [1.2.5 Data Landing Zone](./ex5.md)

[Gå tillbaka till modul 1.2](./data-ingestion.md)

[Gå tillbaka till Alla moduler](../../../overview.md)
