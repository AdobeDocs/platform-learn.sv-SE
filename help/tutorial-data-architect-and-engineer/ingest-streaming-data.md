---
title: Infoga strömmande data
seo-title: Ingest streaming data | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Infoga strömmande data
description: I den här lektionen strömmar du data till Experience Platform med Web SDK.
role: Data Engineer
feature: Data Ingestion
kt: 4348
thumbnail: 4348-ingest-streaming-data.jpg
exl-id: 09c24673-af8b-40ab-b894-b4d76ea5b112
source-git-commit: b2e1bf08d9fb145ba63263dfa078c96258342708
workflow-type: tm+mt
source-wordcount: '3346'
ht-degree: 0%

---

# Infoga strömmande data

<!--1hr-->

I den här lektionen direktuppspelar du data med Adobe Experience Platform Web SDK.

Det finns två huvudsakliga uppgifter vi måste utföra i gränssnittet för datainsamling:

* Vi måste implementera Web SDK på Lumas webbplats för att skicka data om besöksaktivitet från webbplatsen till Adobe Edge-nätverket. Vi ska göra en enkel implementering med hjälp av taggar (tidigare Launch)

* Vi måste konfigurera en datastream, som meddelar Edge-nätverket var data ska vidarebefordras. Vi kommer att konfigurera den så att den skickar data till `Luma Web Events` datauppsättning i vår plattformssandlåda.

**Datatekniker** måste kunna importera strömmande data utanför den här självstudiekursen. När du implementerar Adobe Experience Platform SDK för webb eller mobiler är det oftast en webb- eller mobilutvecklare som arbetar med att skapa datalager och taggegenskapskonfigurationen.

Innan du börjar övningarna ska du titta på dessa två korta videoklipp för att lära dig mer om strömmande data och Web SDK:
>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

>[!NOTE]
>
>Den här självstudiekursen fokuserar på direktuppspelning från webbplatser med Web SDK, men du kan även direktuppspela data med [Adobe Mobile SDK](https://developer.adobe.com/client-sdks/documentation/), [Apache Kafka Connect](https://github.com/adobe/experience-platform-streaming-connect)och andra mekanismer.

## Behörigheter krävs

I [Konfigurera behörigheter](configure-permissions.md) lektionen anger du alla åtkomstkontroller som krävs för att slutföra lektionen.

<!--
* Permission items **[!UICONTROL Launch]** > **[!UICONTROL Property Rights]** > **[!UICONTROL Approve]**, **[!UICONTROL Develop]**, **[!UICONTROL Manage Environments]**, **[!UICONTROL Manage Extensions]**, and **[!UICONTROL Publish]**
* Permission item **[!UICONTROL Launch]** > **[!UICONTROL Company Rights]** > **[!UICONTROL Manage Properties]**
* User-role access to the `Luma Tutorial Launch` product profile
* Admin-role access to the `Luma Tutorial Launch` product profile
* Permission items **[!UICONTROL Platform]** > **[!UICONTROL Data Ingestion]** > **[!UICONTROL View Sources]** and **[!UICONTROL Manage Sources]**
* Permission items **[!UICONTROL Platform]** > **[!UICONTROL Data Management]** > **[!UICONTROL View Datasets]** and **[!UICONTROL Manage Datasets]**
* Permission items **[!UICONTROL Platform]** > **[!UICONTROL Profiles]** > **[!UICONTROL View Profiles]**, **[!UICONTROL Manage Profiles]** and **[!UICONTROL Export Audience Segment]**
* Permission item **[!UICONTROL Platform]** > **[!UICONTROL Sandbox Administration]** > **[!UICONTROL View Sandboxes]**
* Permission item **[!UICONTROL Platform]** > **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
-->

<!--## Create a streaming source

1. Log into the [Experience Platform  user interface](https://experience.adobe.com/platform/)
1. Go to **[!UICONTROL Sources]** in the left navigation
1. Filter the list by selecting **[!UICONTROL Streaming]**
1. In the **[!UICONTROL HTTP API]** section, select the **[!UICONTROL Configure]** button
    ![Configure an HTTP API streaming source](assets/websdk-source-confiigureHTTPAPI.png)
1. On the **[!UICONTROL Authentication]** step, enter `Luma Web Events Source` as the **[!UICONTROL Account name]** and select the **[!UICONTROL Connect to source]** button (we don't need to enable authentication since the data will be originating from website visitors)
    ![Configure an HTTP API streaming source](assets/websdk-source-connectSource.png)
1. Once connected, select the **[!UICONTROL Next]** button to proceed to the next step in the workflow
1. On the **[!UICONTROL Select data]** step, choose **[!UICONTROL Existing Dataset]**, select your `Luma Web Events Dataset`, and then select the **[!UICONTROL Next]** button
    ![Select your dataset](assets/websdk-source-selectDataset.png)
1. On the **[!UICONTROL Dataflow detail]** step, select the **[!UICONTROL Next]** button:
    ![Select Next](assets/websdk-source-dataflowName.png)
    <!--What is a good practice for naming the data flow vs the source-->
<!--
1. On the **[!UICONTROL Review]** step, review your source details and select the **[!UICONTROL Finish]** button:
    ![Select Finish](assets/websdk-source-review.png)
-->

## Konfigurera datastream

Först konfigurerar vi datastream. En dataström talar om för Adobe Edge nätverk var data ska skickas när de har tagits emot från Web SDK-anropet. Vill du till exempel skicka data till Experience Platform, Adobe Analytics eller Adobe Target? Datastreams hanteras i användargränssnittet för datainsamling (tidigare Launch) och är viktiga för datainsamling med Web SDK.

Skapa [!UICONTROL datastream]:

1. Logga in på [Experience Platform datainsamlingsgränssnitt](https://experience.adobe.com/launch/)

   <!--when will the edge config go live?-->

1. Välj **[!UICONTROL Datastreams]** i den vänstra navigeringen
1. Välj **[!UICONTROL Ny datastream]** i det övre högra hörnet

   ![Välj datastölar i den vänstra navigeringen](assets/websdk-edgeConfig-clickNav.png)


1. För **[!UICONTROL Eget namn]**, ange `Luma Platform Tutorial` (lägg till ditt namn i slutet om flera personer från ditt företag använder den här självstudiekursen)
1. Välj **[!UICONTROL Spara]** knapp

   ![Namnge datastrammet och spara](assets/websdk-edgeConfig-name.png)

På nästa skärm anger du var du vill skicka data. Så här skickar du data till Experience Platform:

1. Växla på **[!UICONTROL Adobe Experience Platform]** för att visa ytterligare fält
1. För **[!UICONTROL Sandbox]**, markera `Luma Tutorial`
1. För **[!UICONTROL Händelsedatauppsättning]**, markera `Luma Web Events Dataset`
1. Om du använder andra Adobe-program kan du utforska de andra avsnitten och se vilken information som krävs i Edge Configuration för dessa andra lösningar. Kom ihåg att Web SDK utvecklades inte bara för att strömma data till Experience Platform, utan även för att ersätta alla tidigare JavaScript-bibliotek som används av andra Adobe-program. Edge Configuration används för att ange kontoinformationen för varje program som du vill skicka data till.
1. Välj **[!UICONTROL Spara]**

   ![Konfigurera dataströmmen och spara](assets/websdk-edgeConfig-addEnvironment.png)

När Edge Configuration har sparats visas tre miljöer för utveckling, mellanlagring och produktion. Ytterligare utvecklingsmiljöer kan läggas till:
![Varje Edge-konfiguration kan ha flera miljöer](assets/websdk-edgeConfig-environments.png)
Alla tre miljöerna innehåller den plattformsinformation du just angav. Dessa uppgifter kan dock konfigureras på olika sätt i olika miljöer. Du kan till exempel låta varje miljö skicka data till en annan plattformssandlåda. I den här självstudiekursen kommer vi inte att göra någon ytterligare anpassning av vår datastream.

## Installera Web SDK-tillägget

### Lägg till en egenskap

Först måste vi skapa en taggegenskap (tidigare en taggegenskap). En egenskap är en behållare för alla JavaScript-skript, regler och andra funktioner som krävs för att samla in information från en webbsida och skicka den till olika platser.

Så här skapar du en egenskap:

1. Gå till **[!UICONTROL Egenskaper]** i den vänstra navigeringen
1. Välj **[!UICONTROL Ny egenskap]** knapp
   ![Lägg till en ny egenskap](assets/websdk-property-addNewProperty.png)
1. Som **[!UICONTROL Namn]**, ange `Luma Platform Tutorial` (lägg till ditt namn i slutet om flera personer från ditt företag använder den här självstudiekursen)
1. Som **[!UICONTROL Domäner]**, ange `enablementadobe.com` (förklaras senare)
1. Välj **[!UICONTROL Spara]**

   ![Egenskapsinformation](assets/websdk-property-propertyDetails.png)

<!--
After saving the property, you might see an error message like the one below. If so, this is because you don't actually have access to the property you just created. To fix this, we need to go to the Admin Console to give yourself access:
    ![Error after saving the profile](assets/websdk-property-errorCreating.png)

To give yourself access to the property:

1. In a separate browser tab, log into the [Admin Console](https://adminconsole.adobe.com/)
1. Go to **[!UICONTROL Products]** from the top navigation
1. Select **[!UICONTROL Adobe Experience Platform Launch]** on the left navigation
1. Go to your `Luma Tutorial Launch` product profile
1. Go to the **[!UICONTROL Permissions]** tab
1. On the **[!UICONTROL Properties]** row, select **[!UICONTROL Edit]**
    ![Edit the Property Permissions](assets/websdk-adminconsole-editPermissions.png)
1. Select the "+" icon to move your `Luma Platform Tutorial` property to the right-hand side and select the **[!UICONTROL Save]** button to update the permissions
   
    ![Add the new property](assets/websdk-adminconsole-addProperty.png)

Now switch back to your browser tab with the Data Collection interface still open. Reload the page and the `Luma Platform Tutorial` property should display in the list. Select to open the property:

![Luma Platform Tutorial should appear](assets/websdk-property-showsInList.png)
-->

## Lägg till Web SDK-tillägget

Nu när du har en egenskap kan du lägga till Web SDK med ett tillägg. Ett tillägg är ett kodpaket som utökar gränssnittet och funktionerna i datainsamlingen. Så här lägger du till tillägget:

1. Öppna taggegenskapen
1. Gå till **[!UICONTROL Tillägg]** i den vänstra navigeringen
1. Gå till **[!UICONTROL Katalog]** tab
1. Det finns många tillägg för taggar. Filtrera katalogen med termen `Web SDK`
1. I **[!UICONTROL Adobe Experience Platform Web SDK]** väljer du **[!UICONTROL Installera]** knapp
   ![Installera Adobe Experience Platform Web SDK-tillägget](assets/websdk-property-addExtension.png)
1. Det finns flera konfigurationer tillgängliga för Web SDK-tillägget, men det finns bara två som vi kommer att konfigurera för den här självstudiekursen. Uppdatera **[!UICONTROL Edge Domain]** till `data.enablementadobe.com`. Med den här inställningen kan du ange cookies från första part med Web SDK-implementeringen, vilket rekommenderas. Senare i den här lektionen kommer du att kartlägga en webbplats på `enablementadobe.com` till din taggegenskap. CNAME för `enablementadobe.com` domänen har redan konfigurerats så att `data.enablementadobe.com` kommer att vidarebefordra till Adobe-servrar. När du implementerar Web SDK på din egen webbplats måste du skapa en CNAME för dina egna datainsamlingssyften, till exempel `data.YOUR_DOMAIN.com`
1. Från **[!UICONTROL Datastream]** listruta, välj `Luma Platform Tutorial` datastream.
1. Du kan gärna titta på andra konfigurationsalternativ (men ändra dem inte!) och sedan markera **[!UICONTROL Spara]**
   <!--is edge domain required for first party? when will it break?-->
   <!--any other fields that should be highlighted-->
   ![](assets/websdk-property-configureExtension.png)



## Skapa en regel för att skicka data

Nu ska vi skapa en regel för att skicka data till plattformen. En regel är en kombination av händelser, villkor och åtgärder som talar om för taggarna att göra något. Så här skapar du en regel:

1. Gå till **[!UICONTROL Regler]** i den vänstra navigeringen
1. Välj **[!UICONTROL Skapa ny regel]** knapp
   ![Skapa en regel](assets/websdk-property-createRule.png)
1. Namnge regeln `All Pages - Library Loaded`
1. Under **[!UICONTROL Händelser]** väljer du **[!UICONTROL Lägg till]** knapp
   ![Namnge regeln och lägg till en händelse](assets/websdk-property-nameRule.png)
1. Använd **[!UICONTROL Core]** **[!UICONTROL Tillägg]** och markera **[!UICONTROL Bibliotek inläst (sidan ovanpå)]** som **[!UICONTROL Händelsetyp]**. Den här inställningen innebär att vår regel aktiveras när startbiblioteket läses in på en sida.
1. Välj **[!UICONTROL Behåll ändringar]** för att återgå till huvudlinjeraster
   ![Lägg till händelsen Biblioteksinläsning](assets/websdk-property-addEvent.png)
1. Lämna **[!UICONTROL Villkor]** tom, eftersom vi vill att den här regeln ska köras på alla sidor, enligt det namn vi gav den
1. Under **[!UICONTROL Åtgärder]** väljer du **[!UICONTROL Lägg till]** knapp
1. Använd **[!UICONTROL Adobe Experience Platform Web SDK]** **[!UICONTROL Tillägg]** och markera **[!UICONTROL Skicka händelse]** som **[!UICONTROL Åtgärdstyp]**
1. Till höger väljer du **[!UICONTROL web.webpagedetails.pageViews]** från **[!UICONTROL Typ]** listruta. Detta är ett av XDM-fälten i `Luma Web Events Schema`
1. Välj **[!UICONTROL Behåll ändringar]** för att återgå till huvudlinjeraster
   ![Lägg till åtgärden Skicka händelse](assets/websdk-property-addAction.png)
1. Välj **[!UICONTROL Spara]** för att spara regeln\
   ![Spara regeln](assets/websdk-property-saveRule.png)

## Publicera regeln i ett bibliotek

Därefter ska vi publicera regeln i vår utvecklingsmiljö så att vi kan verifiera att den fungerar.

<!--
There are a few quick steps we must take in the **[!UICONTROL Publishing]** section of Launch.


### Create a host

Launch libraries can be hosted on Adobe's Content Delivery Network (CDN) or on your own servers. In this tutorial, we will use Adobe's CDN since it is faster to set up:

1. Go to **[!UICONTROL Hosts]** in the left navigation
1. Select the **[!UICONTROL Create New Host]** button
    ![Create a new host](assets/websdk-property-createHost.png)   
1. For the **[!UICONTROL Name]**, enter `Adobe CDN`
1. For the **[!UICONTROL Type]**, select **[!UICONTROL Managed by Adobe]**
1. Select the **[!UICONTROL Save]** button to complete the setup of the host
    ![Configure the host](assets/websdk-property-hostDetails.png)   

### Create an environment

Environments allow you to have different versions of a library in different publishing environments to accommodate your publishing workflow. For example, the fully tested version of your library can be published to a Production environment, while new changes are being created in a Development environment. You can also use different hosts for each environment. To create an environment:

1. Go to **[!UICONTROL Environments]** in the left navigation
1. Select the **[!UICONTROL Create New Environment]** button
    ![Create a new environment](assets/websdk-property-createEnvironment.png) 
1. Under **[!UICONTROL Development]** select **[!UICONTROL Select]**   
    ![Select the environment type](assets/websdk-property-selectEnvironment.png) 
1. For the **[!UICONTROL Name]**, enter `Development`
1. For the **[!UICONTROL Select Host]** dropdown, select `Adobe CDN`
1. Select the **[!UICONTROL Save]** button to complete the setup of the environment
    ![Configure the environment](assets/websdk-property-configureEnv.png)
1. You will see a modal with URL and other implementation details of this library. These are critical for a real Launch implementation, but we don't need to worry about them for this tutorial. Select the **[!UICONTROL Close]** button to exit the modal.

### Create and publish the library

Now let's bundle the contents of our property&mdash;currently an extension and a rule&mdash;into a library. 
-->

Så här skapar du ett bibliotek:

1. Gå till **[!UICONTROL Publiceringsflöde]** i den vänstra navigeringen
1. Välj **[!UICONTROL Lägg till bibliotek]**
   ![Välj Lägg till bibliotek](assets/websdk-property-pubAddNewLib.png)
1. För **[!UICONTROL Namn]**, ange `Luma Platform Tutorial`
1. För **[!UICONTROL Miljö]**, markera `Development`
1. Välj **[!UICONTROL Lägg till alla ändrade resurser]** -knappen. (Förutom [!UICONTROL Adobe Experience Platform Web SDK] och `All Pages - Library Loaded` -regeln visas också [!UICONTROL Core] tillägget har lagts till som innehåller det grundläggande JavaScript som krävs för alla Launch-webbegenskaper.)
1. Välj **[!UICONTROL Spara och bygg för utveckling]** knapp
   ![Skapa och bygg biblioteket](assets/websdk-property-buildLibrary.png)

Det kan ta några minuter att skapa biblioteket och när det är klart visas en grön punkt till vänster om biblioteksnamnet:
![Bygget är klart](assets/websdk-property-buildComplete.png)

Som du kan se på [!UICONTROL Publiceringsflöde] på skärmen finns det mycket mer i publiceringsprocessen som ligger utanför kursen. Vi kommer bara att använda ett enda bibliotek i vår utvecklingsmiljö.

## Validera data i begäran

### Lägg till Adobe Experience Platform Debugger

Felsökaren Experience Platform är ett tillägg för webbläsarna Chrome och Firefox som gör att du kan se Adobe-tekniken som används på dina webbsidor. Ladda ned den version du föredrar:

* [Firefox-tillägg](https://addons.mozilla.org/sv-SE/firefox/addon/adobe-experience-platform-dbg/)
* [Kromtillägg](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

Om du aldrig har använt Felsökning tidigare - och den här är en annan än den tidigare Adobe Experience Cloud Debugger - kan du titta på den här översiktsvideon med fem minuter:

>[!VIDEO](https://video.tv.adobe.com/v/32156?quality=12&learn=on)

### Öppna Lumas webbplats

I den här självstudiekursen använder vi en öppen version av demonstrationswebbplatsen för Luma. Vi öppnar den och bokmärker den:

1. Öppna [Lumas webbplats](https://luma.enablementadobe.com/content/luma/us/en.html).
1. Bokmärk sidan så att den kan användas i resten av självstudiekursen

Den här värdbaserade webbplatsen är anledningen till att vi använde `enablementadobe.com` i [!UICONTROL Domäner] fält för den ursprungliga taggegenskapskonfigurationen och varför vi använde `data.enablementadobe.com` som vår förstahandsdomän i [!UICONTROL Adobe Experience Platform Web SDK] tillägg. Jag hade en plan!

![Lumas hemsida](assets/websdk-luma-homepage.png)

### Använd Experience Platform Debugger för att mappa till taggegenskapen

Felsökaren i Experience Platform har en cool funktion som gör att du kan ersätta en befintlig taggegenskap med en annan. Detta är användbart för validering och gör att vi kan hoppa över många implementeringssteg i den här självstudiekursen.

1. Kontrollera att Luma-webbplatsen är öppen och välj ikonen för Experience Platform-felsökningstillägget
1. Felsökaren öppnar och visar information om den hårdkodade implementeringen, som inte har med den här självstudiekursen att göra (du kan behöva läsa in Luma-webbplatsen igen när du har öppnat Felsökning)
1. Bekräfta att felsökaren är **[!UICONTROL Ansluten till Luma]**&quot; enligt bilden nedan och välj sedan &quot;**[!UICONTROL lock]**&quot; om du vill låsa felsökaren till Luma-webbplatsen.
1. Välj **[!UICONTROL Logga in]** till höger om du vill autentisera.
1. Gå till **[!UICONTROL Starta]** i den vänstra navigeringen
1. Välj fliken Konfiguration
1. Till höger om där den visar dig **[!UICONTROL Sidinbäddningskoder]**&#x200B;öppnar du **[!UICONTROL Åtgärder]** och markera **[!UICONTROL Ersätt]**

   ![Välj Åtgärder > Ersätt](assets/websdk-debugger-replaceLibrary.png)
1. Eftersom du är autentiserad kommer felsökaren att hämta in de tillgängliga egenskaperna och miljöerna för Launch. Välj `Luma Platform Tutorial` property
1. Välj `Development` miljö
1. Välj **[!UICONTROL Använd]** knapp
   ![Välj den alternativa taggegenskapen](assets/websdk-debugger-selectProperty.png)
1. Lumas webbplats kommer nu att läsas in igen _med taggegenskapen_. Hjälp, jag har blivit hackad! Skämtar bara.
   ![tagg, egenskap ersatt](assets/websdk-debugger-propertyReplaced.png)
1. Gå till **[!UICONTROL Sammanfattning]** i den vänstra navigeringen för att se information om [!UICONTROL Starta] property
   ![Fliken Sammanfattning](assets/websdk-debugger-summary.png)
1. Gå till **[!UICONTROL AEP Web SDK]** i den vänstra navigeringen för att se **[!UICONTROL Nätverksförfrågningar]**
1. Öppna **[!UICONTROL händelser]** rad

   ![Adobe Experience Platform Web SDK-begäran](assets/websdk-debugger-platformNetwork.png)
1. Se hur vi kan se `web.webpagedetails.pageView` händelsetyp som anges i [!UICONTROL Skicka händelse] och andra färdiga variabler som följer `AEP Web SDK ExperienceEvent Mixin` format
   ![Händelseinformation](assets/websdk-debugger-eventDetails.png)
1. Den här typen av förfrågningsinformation visas också i webbläsarens webbutvecklingsverktyg **Nätverk** -fliken. Öppna den och läs in sidan igen. Filter för samtal med `interact` för att hitta samtalet markerar du det och tittar sedan på **Sidhuvuden** tab, **Begär nyttolast** område.
   ![Fliken Nätverk](assets/websdk-debugger-networkTab.png)
1. Gå till **Svar** och notera hur ECID-värdet ingår i svaret. Kopiera det här värdet så som du kommer att använda det för att validera profilinformationen i nästa övning.
   ![Fliken Nätverk](assets/websdk-debugger-networkTab-response.png)



## Validera data i Experience Platform

Du kan validera att data landar i Platform genom att titta på de batchar med data som kommer in i `Luma Web Events Dataset`. (Jag vet, det kallas dataöverföring men nu säger jag att det kommer i grupper! Den direktuppspelas i realtid till en profil, så att den kan användas för segmentering och aktivering i realtid, men skickas gruppvis var 15:e minut till datasjön.)

Så här validerar du data:

1. Gå till **[!UICONTROL Datauppsättningar]** i den vänstra navigeringen
1. Öppna `Luma Web Events Dataset` och bekräfta att en batch har kommit fram. Kom ihåg att de skickas var 15:e minut, så du kanske måste vänta på att gruppen ska visas.
1. Välj **[!UICONTROL Förhandsgranska datauppsättning]** knapp
   ![Öppna datauppsättningen](assets/websdk-platform-dataset.png)
1. Observera hur du kan markera olika fält i schemat till vänster i förhandsgranskningen för att förhandsgranska dessa specifika datapunkter:
   ![Förhandsgranska fälten](assets/websdk-platform-datasetPreview.png)

Du kan också bekräfta att den nya profilen visas:

1. Gå till **[!UICONTROL Profiler]** i den vänstra navigeringen
1. Välj **[!UICONTROL ECID]** och söka efter ditt ECID-värde (kopiera det från svaret). Profilen kommer att ha ett eget id, som är skilt från ECID.
1. Välj **[!UICONTROL Profil-ID]** för att öppna profilen
   ![Hitta och öppna profilen](assets/websdk-platform-openProfile.png)
1. Välj **[!UICONTROL Händelser]** för att se de sidor du visade
   ![Profilhändelser](assets/websdk-platform-profileEvents.png)\
   <!--![](assets/websdk-platform-confirmProfile.png)-->

## Lägg till anpassade data till händelsen

### Skapa ett dataelement för sidnamn

1. I tagggränssnittet för datainsamling, i det övre högra hörnet av ditt `Luma Platform Tutorial` -egenskap, öppna **[!UICONTROL Välj ett arbetsbibliotek]** listruta och välj `Luma Platform Tutorial` bibliotek. Den här inställningen gör det enklare att publicera ytterligare uppdateringar till vårt bibliotek.
1. Gå till **[!UICONTROL Dataelement]** i den vänstra navigeringen
1. Välj **[!UICONTROL Skapa nytt dataelement]** knapp

   ![Skapa ett nytt dataelement](assets/websdk-property-createNewDataElement.png)
1. Som **[!UICONTROL Namn]**, ange `Page Name`
1. Som **[!UICONTROL Dataelementtyp]**, markera `JavaScript Variable`
1. Som **[!UICONTROL JavaScript-variabelnamn]**, ange `digitalData.page.pageInfo.pageName`
1. Om du vill standardisera värdeformatet markerar du kryssrutorna för **[!UICONTROL Använd gemener]** och **[!UICONTROL Rensa text]**
1. Se till att `Luma Platform Tutorial` är markerat som arbetsbibliotek
1. Välj **[!UICONTROL Spara i bibliotek]**
   ![Skapa ett dataelement för sidnamn](assets/websdk-property-dataElement-pageName.png)

### Mappa sidnamnet till XDM-objektets dataelement

Nu ska vi mappa vårt sidnamn till Web SDK.

>[!IMPORTANT]
>
>För att kunna utföra den här uppgiften måste vi se till att din användare först har tillgång till sandlådan Prod. Om du inte redan har tillgång till Prod-sandlådan från en annan produktprofil kan du snabbt öppna din `Luma Tutorial Platform` profil och lägga till behörighetsobjektet **[!UICONTROL Sandlådor]** > **[!UICONTROL Prod]**. När du har gjort det kan du göra en SKIFT-omläsning på dataelementsidan för att rensa cacheminnet
>![Lägg till Prod-sandlådan](assets/websdk-property-permissionToLoadSchema.png)

På **[!UICONTROL Dataelement]** sida:

1. Skapa ett nytt dataelement
1. Som **[!UICONTROL Namn]**, ange `XDM Object`
1. Som **[!UICONTROL Tillägg]**, markera `Adobe Experience Platform Web SDK`
1. Som **[!UICONTROL Dataelementtyp]**, markera `XDM object`
1. Som **[!UICONTROL Sandbox]** väljer du `Luma Tutorial` sandlåda
1. Som **[!UICONTROL Schema]** väljer du `Luma Web Events Schema`
1. Välj `web.webPageDetails.name` fält
1. Som **[!UICONTROL Värde]**, markerar du ikonen för att öppna ett modalt val av dataelement och väljer `Page Name` dataelement
1. Välj **[!UICONTROL Spara i bibliotek]**

   ![Mappa sidnamnet till XDM-objektets dataelement](assets/websdk-property-dataElement-createXDMObject.png)

Samma process används för att mappa ytterligare anpassade data på webbplatsen till XDM-fält.

### Lägg till XDM-data till åtgärden Skicka händelse

Nu när du har data mappade till XDM-fält kan du inkludera dem i åtgärden Skicka händelse:

1. Gå till **[!UICONTROL Regler]** screen
1. Öppna `All Pages - Library Loaded` regel
1. Öppna `Adobe Experience Platform Web SDK - Send Event` åtgärd
1. Som **[!UICONTROL XDM-data]**, markerar du ikonen för att öppna ett modalt val av dataelement och väljer `XDM Object` dataelement
1. Välj **[!UICONTROL Behåll ändringar]** knapp
   ![Lägg till XDM-data till åtgärden Skicka händelse](assets/websdk-property-addXDMtoSendEvent.png)
1. Nu när du har `Luma Platform Tutorial` har valts som ditt arbetsbibliotek för de senaste övningarna och dina senaste ändringar har sparats direkt i biblioteket. Istället för att behöva publicera ändringarna via skärmen Publiceringsflöde kan du bara öppna listrutan med den blå knappen och välja **[!UICONTROL Spara i bibliotek och bygge]**
   ![Spara i bibliotek och bygge](assets/websdk-property-saveAndBuildUpdatedSendEvent.png)

Detta börjar bygga upp ett nytt taggbibliotek med de tre ändringar du just gjorde.

### Validera XDM-data

Nu bör du kunna läsa in Lumas hemsida igen, när den mappas till taggegenskapen med hjälp av felsökaren som du lärde dig tidigare, och se att sidnamnsfältet fylls i i i begäran!
![Validera XDM-data](assets/websdk-debugger-pageName.png)

Du kan också validera de sidnamnsdata som togs emot i Platform genom att förhandsgranska datauppsättningen och profilen.

## Skicka ytterligare identiteter

Din Web SDK-implementering skickar nu händelser med Experience Cloud ID (ECID) som primär identifierare. ECID genereras automatiskt av Web SDK och är unikt per enhet och webbläsare. En enskild kund kan ha flera ECID:n beroende på vilken enhet och webbläsare de använder. Så hur får vi en enhetlig bild av den här kunden och kan länka deras onlineaktivitet till våra CRM-, Loyalty- och Offline Purchase-data? Det gör vi genom att samla in ytterligare identiteter under deras session och på ett avgörande sätt länka deras profil via identitetssammanfogning.

Om du kommer ihåg det, nämnde jag att vi skulle använda ECID och CRM ID som identiteter för våra webbdata i [Mappa identiteter](map-identities.md) lektion. Låt oss samla in CRM-ID:t med Web SDK!

### Lägg till dataelement för CRM-ID

Först lagrar vi CRM-ID i ett dataelement:

1. Lägg till ett dataelement med namnet i tagggränssnittet `CRM Id`
1. Som **[!UICONTROL Dataelementtyp]**, markera **[!UICONTROL JavaScript-variabel]**
1. Som **[!UICONTROL JavaScript-variabelnamn]**, ange `digitalData.user.0.profile.0.attributes.username`
1. Välj **[!UICONTROL Spara i bibliotek]** knapp (`Luma Platform Tutorial` bör fortfarande vara ditt arbetsbibliotek)
   ![Lägg till dataelement för CRM-ID](assets/websdk-property-dataElement-crmId.png)

### Lägg till CRM-ID i dataelementet för identitetskartan

Nu när vi har hämtat CRM-ID-värdet måste vi associera det med en särskild dataelementtyp som kallas för [!UICONTROL Identitetskarta] dataelement:

1. Lägg till ett dataelement med namnet `Identities`
1. Som **[!UICONTROL Tillägg]**, markera **[!UICONTROL Adobe Experience Platform Web SDK]**
1. Som **[!UICONTROL Dataelementtyp]**, markera **[!UICONTROL Identitetskarta]**
1. Som **[!UICONTROL Namnutrymme]**, ange `Luma CRM Id`, vilket är [!UICONTROL namespace] som vi skapat tidigare

   >[!WARNING]
   >
   >Med Adobe Experience Platform Web SDK-tillägget version 2.2 kan du välja namnutrymme från en ifylld listruta med de faktiska värdena i ditt plattformskonto. Tyvärr är den här funktionen ännu inte&quot;sandlådemedveten&quot;, vilket innebär att `Luma CRM Id` i listrutan. Detta kan hindra dig från att slutföra den här övningen. Vi skickar en lösning när vi har bekräftat.

1. Som **[!UICONTROL ID]**, markerar du ikonen för att öppna ett modalt val av dataelement och väljer `CRM Id` dataelement
1. Som **[!UICONTROL Autentiserat läge]**, markera **[!UICONTROL Autentiserad]**
1. Lämna **[!UICONTROL Primär]** _avmarkerad_. Eftersom CRM-ID inte finns för de flesta besökare på Luma-webbplatsen är det definitivt du _vill inte åsidosätta ECID som primär identifierare_. Det skulle vara sällsynt att använda något annat än ECID som primär identifierare. Vanligtvis anger jag inte standardinställningarna i dessa instruktioner, men jag ringer upp den här för att hjälpa dig att undvika problem senare i din egen implementering.
1. Välj **[!UICONTROL Spara i bibliotek]** knapp (`Luma Platform Tutorial` bör fortfarande vara ditt arbetsbibliotek)
   ![Lägg till CRM-ID i dataelementet för identitetskartan](assets/websdk-property-dataElement-identityMap.png)

>[!NOTE]
>
>Du kan skicka flera identifierare med [!UICONTROL Identitetskarta] datatyp.

### Lägg till datamappningsdataelementet för identitet i XDM-objektet

Det finns ytterligare ett dataelement som måste uppdateras - XDM-objektets dataelement. Det kan verka konstigt att behöva uppdatera tre separata dataelement för att skicka den här identiteten, men den här processen är utformad för att skalas för flera identiteter. Oroa dig inte, vi är nästan klara med den här lektionen!

1. Öppna XDM-objektdataelementet
1. Öppna fältet IdentityMap XDM
1. Som **[!UICONTROL Dataelement]**, markerar du ikonen för att öppna ett modalt val av dataelement och väljer `Identities` dataelement
1. Nu när du har `Luma Platform Tutorial` har valts som ditt arbetsbibliotek för de senaste övningarna och dina senaste ändringar har sparats direkt i biblioteket. Istället för att behöva publicera ändringarna via skärmen Publiceringsflöde kan du öppna listrutan med den blå knappen och välja **[!UICONTROL Spara i bibliotek och bygge]**
   ![Lägg till dataelementet IdentityMap i XDM-objektet](assets/websdk-property-dataElement-addIdentitiesToXDMObject.png)


### Validera identiteten

Så här verifierar du att CRM-ID:t nu skickas av Web SDK:

1. Öppna [Lumas webbplats](https://luma.enablementadobe.com/content/luma/us/en.html)
1. Mappa den till taggegenskapen med Felsökning, enligt tidigare instruktioner
1. Välj **Inloggning** länk längst upp till höger på Lumas webbplats
1. Logga in med inloggningsuppgifterna `test@adobe.com`/`test`
1. Kontrollera Experience Platform Web SDK-anropet i Felsökning (**[!UICONTROL Adobe Experience Platform Web SDK]** > **[!UICONTROL Nätverksförfrågningar]** > **[!UICONTROL händelser]** av den senaste begäran) och du bör se `lumaCrmId`:
   ![Validera identiteten i Felsökning](assets/websdk-debugger-confirmIdentity.png)
1. Slå upp användarprofilen med ECID-namnutrymmet och ange ett nytt värde. I profilen visas CRM-ID:t och även lojalitets-ID:t samt profilinformation som namn och telefonnummer. Alla identiteter och data har sammanfogats till en enda kundprofil i realtid!
   ![Validera identiteten i plattformen](assets/websdk-platform-lumaCrmIdProfile.png)


## Ytterligare resurser

* [Implementera Adobe Experience Cloud med webb-SDK](/help/tutorial-web-sdk/overview.md)
* [Direktuppspelningsdokumentation](https://experienceleague.adobe.com/docs/experience-platform/ingestion/streaming/overview.html?lang=sv)
* [API-referens för direktuppspelning](https://www.adobe.io/experience-platform-apis/references/data-ingestion/#tag/Streaming-Ingestion)

Bra jobbat! Det var mycket information om Web SDK och Launch. Det är mycket mer involverat i en fullfjädrad implementering, men det är grunderna som hjälper dig att komma igång och se resultaten i Platform.

>[!NOTE]
>
>Nu när du är klar med inmatningslektionen för direktuppspelning kan du ta bort [!UICONTROL Prod] sandlåda från `Luma Tutorial Platform` produktprofil


Datatekniker, om du vill kan du hoppa fram till [lektion för att köra frågor](run-queries.md).

Dataarkitekter kan du gå vidare till [sammanfogningsprinciper](create-merge-policies.md)!
