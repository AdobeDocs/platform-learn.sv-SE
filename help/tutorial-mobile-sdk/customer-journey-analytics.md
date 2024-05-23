---
title: Rapportera och analysera mobilappsdata med Customer Journey Analytics
description: Lär dig hur du rapporterar och analyserar interaktionen med din mobilapp med Customer Journey Analytics.
solution: Data Collection,Experience Platform,Analytics
hide: true
hidefromtoc: true
source-git-commit: 9607ec77a891a85a8bae2a2622e74d59588e1dbf
workflow-type: tm+mt
source-wordcount: '3121'
ht-degree: 0%

---

# Rapportera och analysera med Customer Journey Analytics

Lär dig hur du rapporterar och analyserar mobilappsinteraktioner med Customer Journey Analytics.

Händelsedata för mobilappar, som du samlade in och skickade till Platform Edge Network i tidigare lektioner, vidarebefordras till de tjänster som konfigurerats i din datastam. Om du följde [Skicka data till Experience Platform](platform.md) lektionen, att data nu lagras i datavjön på Experience Platform som datamängder. Och dessa data finns sedan tillgängliga för Customer Journey Analytics att användas för rapportering och analys.

Till skillnad från Adobe Analytics är Customer Journey Analytics ett program som *använder* data från datauppsättningar som du har skapat i Experience Platform och som appen skickar data till. Med Adobe Experience Platform Mobile SDK skickar du inga data direkt till Customer Journey Analytics. I stället använder Customer Journey Analytics data från datauppsättningarna i Experience Platform.

Den här lektionen i självstudiekursen fokuserar på att rapportera och analysera data som hämtats in från Luma-självstudieversionen. En av de unika möjligheterna i Customer Journey Analytics är att kombinera data från olika källor (CRM, butiksadress, lojalitetsprogram, callcenter) och kanaler (webb, mobil, offline) för att ge djupgående insikter i kundresorna. Denna möjlighet ligger utanför den här lektionens räckvidd. Se [Customer Journey Analytics - översikt](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-overview/cja-overview) för mer information.


## Förutsättningar

Din organisation måste etableras och tillstånd beviljas för Customer Journey Analytics. Du måste ha administrationsåtkomst till Customer Journey Analytics.


## Utbildningsmål

I den här lektionen kommer du att:

- Skapa en anslutning för att definiera de datauppsättningar från Experience Platform som du vill använda i Customer Journey Analytics.
- Skapa en datavy för att förbereda data från datauppsättningar för din rapportering och analys
- Skapa ett projekt för att skapa rapporter och visualiseringar så att ni kan analysera data från mobilappen.

Den här beställningen är avsiktlig. I Customer Journey Analytics är en rapport i Analysis Workspace beroende av en datavy. Och en datavy är beroende av en anslutning.


## Skapa en anslutning

En anslutning i Customer Journey Analytics definierar de datauppsättningar (och de data i dessa datauppsättningar) från Experience Platform som du vill använda för rapportering och analys.

1. Navigera till gränssnittet Customer Journey Analytics med Apps ![Appar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Apps_18_N.svg) i det övre högra hörnet.

1. Välj **[!UICONTROL Connections]** på den övre menyraden.

1. Se till att du väljer **[!UICONTROL List]** i anslutningsgränssnittet. En lista över befintliga anslutningar visas.

1. Välj **[!UICONTROL Create new connection]**.

1. I **[!UICONTROL Connections]** > **[!UICONTROL Untitled connection]** skärm, in **[!UICONTROL Connection settings]**

   1. Ange en **[!UICONTROL Connection name]**, till exempel `Luma App - AEP Mobile SDK Tutorial Connection`.
   2. Ange en **[!UICONTROL Connection description]**, till exempel `Connection for the Luma app used in the AEP Mobile SDK tutorial`.

      I **[!UICONTROL Data settings]**:

   3. Välj den sandlåda som du har använt för att samla in mobilappsdata, till exempel **[!UICONTROL Mobile and Web SDK Courses]**.
   4. Välj **[!UICONTROL less than 1 million]** från **[!UICONTROL Average number of daily events]**.

   5. Välj **[!UICONTROL Add datasets]** för att välja de datauppsättningar från Experience Platform som du vill använda i Customer Journey Analytics.

      ![CJA-anslutningar 1](assets/cja-connections-1.png)

   6. I **[!UICONTROL Add datasets]** guide, **[!UICONTROL Select datasets]** steg,

      1. välj följande datauppsättningar:

         - **[!UICONTROL Luma Mobile App Event Dataset]**, den datauppsättning du skapade som en del av [Skapa en datauppsättning](platform.md#create-a-dataset) i lektionen Experience Platform.
         - **[!UICONTROL ODE DecisionEvents - *sandlådenamn *]beslut**
         - **[!UICONTROL AJO Push Tracking Event Datasets]**

      1. Välj **[!UICONTROL Next]**.

         ![CJA-anslutningar 2](assets/cja-connections-2.png)

   7. I **[!UICONTROL Add datasets]** guide, **[!UICONTROL Datasets settings]** måste du definiera informationen för varje händelsedatamängd.
      1. Se följande tabeller för rätt inställningar:

         | Datauppsättning | Person-ID<br/>Ãr | Tidsstämpel<br>Jesse | ③ för datakälltyp | Importera alla nya ④ | Fyll i alla befintliga ⑤ |
         |---|---|---|---|---|---|
         | Luma Mobile App Event-datauppsättning | identityMap | tidsstämpel | Mobilappsdata | enable | enable |
         | ODE-beslutshändelser - *sandlådenamn* beslut | identityMap | tidsstämpel | Mobilappsdata | enable | enable |
         | AJO Push Tracking Experience, händelsedatauppsättning | identityMap | tidsstämpel | Mobilappsdata | enable | enable |

         ![CJA-anslutningar 3](assets/cja-connections-3.png)

      1. Välj **[!UICONTROL Add datasets]**.

1. Tillbaka i **[!UICONTROL Connections]** > **[!UICONTROL Luma App - AEP Mobile SDK Tutorial Connection]**, markera **[!UICONTROL Save]** för att spara anslutningen.

   ![CJA-anslutningar 4](assets/cja-connections-4.png)

Du har nu definierat din anslutning och Customer Journey Analytics lägger till data från datauppsättningarna i sin egen interna databas. Datainsamlingen kan ta en stund, beroende på mängden data. Förvänta dig ett par timmar innan data visas i Customer Journey Analytics för din självstudieapp.

Så här visar du anslutningsstatus:

1. Välj **[!UICONTROL Connections]** i huvudgränssnittet i Customer Journey Analytics.
1. Välj till exempel namnet på anslutningen **[!UICONTROL Luma App - AEP Mobile SDK Tutorial Connection]**.

I **[!UICONTROL Connections]** > **[!UICONTROL Luma App - AEP Mobile SDK Tutorial Connection]** ser du:

1. Information om totalt antal poster som lagts till, poster som hoppats över och poster som tagits bort. Se till att du väljer **[!UICONTROL All datasets]** och välj en lämplig tidsperiod för att visa information om anslutningen. Du kan använda ![Kalender](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Calendar_18_N.svg) för att öppna en dialogruta där du kan välja tidsperioden.
1. Information för enskilda datauppsättningar om poster som lagts till, poster som hoppats över, poster som tagits bort med mera.

   ![CJA-anslutningar 6](assets/cja-connections-6.png)


## Skapa en datavy

När posterna har lagts till från datauppsättningarna till Customer Journey Analytics kan du skapa en datavy som definierar vilka komponenter av data som du vill rapportera om.

En datavy är en behållare som är specifik för Customer Journey Analytics och som gör att du kan avgöra hur data från en anslutning ska tolkas. Du kan konfigurera standard- och schemafält, från alla datauppsättningar som du har definierat i anslutningen, som komponenter (dimensioner, mått) i Analysis Workspace.

En datavy i Customer Journey Analytics är mycket flexibel när det gäller att konfigurera och definiera data från anslutningen. I den här självstudiekursen använder du bara de funktioner som krävs för din rapportering och analys. Se [Datavyer](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/data-views) för mer information.


Så här skapar du en datavy:

1. Navigera till gränssnittet Customer Journey Analytics med Apps ![Appar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Apps_18_N.svg) i det övre högra hörnet.

1. Välj **[!UICONTROL Data views]** på den övre menyraden.
1. Välj **[!UICONTROL Create new data view]**.
1. I **[!UICONTROL Data views >]** måste du se till att **[!UICONTROL Configure]** är markerad.

   1. Välj din anslutning i den nedrullningsbara listan Inställningar för anslutning, till exempel **[!UICONTROL Luma App - AEP Mobile SDK Tutorial Connection]**.
   1. Ange ett namn för datavyn, till exempel: `Luma App - AEP Mobile SDK Tutorial Data view`.
   1. Välj **[!UICONTROL Save and continue]**.

      ![CJA-datavy 1](assets/cja-dataview-1.png)

1. I **[!UICONTROL Components]** -fliken i **[!UICONTROL Luma App - AEP Mobile SDK Tutorial Data view]** kan ni definiera de mätvärden och mått som ni vill använda när ni rapporterar i mobilappen. Som standard är ett antal standardmått och -mått (som gemensamt kallas för komponenter) redan konfigurerade för datavyn. Men datavyn kräver fler komponenter. <br/>Om du vill lägga till ett schemafält från ditt tidigare definierade schema eller från rutscheman (se [Skapa ett schema](create-schema.md) lektion), som en komponent (mått eller mått):

   1. Hitta schemafältet:

      - söka efter komponenten med hjälp av ![Sök](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Search_18_N.svg) ***[!UICONTROL Search schema fields]*** sökfält. Till exempel: `productListAdd`, eller

        ![CJA-datavy 2a](assets/cja-dataview-2a.png)

      - gå ned till schemafältet i ![Mapp](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) **[!UICONTROL Event datasets]** ![Chevron](https://spectrum.adobe.com/static/icons/ui_18/ChevronSize100.svg). <br/>Till exempel: ![Mapp](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) **[!UICONTROL Event datasets]** ![Chevron](https://spectrum.adobe.com/static/icons/ui_18/ChevronSize100.svg) ![Mapp](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) **[!UICONTROL commerce]** ![Chevron](https://spectrum.adobe.com/static/icons/ui_18/ChevronSize100.svg) ![Mapp](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) **[!UICONTROL productListAdds]** ![Chevron](https://spectrum.adobe.com/static/icons/ui_18/ChevronSize100.svg)

        ![CJA-datavy 2a](assets/cja-dataview-2b.png)

   1. Dra det specifika schemafältet från rutan Schemafält och släpp det på panelen **[!UICONTROL METRICS]** eller **[!UICONTROL DIMENSIONS]** listan i [!UICONTROL Included components] fönster.

      ![CJA-datavy 2a](assets/cja-dataview-3.png)

   1. Du kan konfigurera inställningarna för en komponent. Markera komponenten och konfigurera inställningarna i den högra rutan. <br/>Du kan t.ex. byta namn **[!UICONTROL commerce.productListAdds]** till `Product Add To Lists` med **[!UICONTROL COMPONENT SETTINGS]** > **[!UICONTROL Component name]** i den högra rutan.

      ![CJA DataView 3b](assets/cja-dataview-3b.png)

      Eller konfigurera **[!UICONTROL INCLUDE EXCLUDE VALUES]**.

      ![Komponentinställningar för CJA-datavyn](assets/cja-dataview-component-settings.png)

   1. Nu när du förstår hur du lägger till fält i datavyn och konfigurerar den resulterande komponenten kan du använda tabellerna nedan för att visa en lista med schemafält som ska läggas till som mått eller dimension. Använd **Schema Path** kolumnvärde från tabellen nedan om du vill söka efter eller gå till det specifika schemafältet. När du har dragit och släppt ska du kontrollera **Komponentinställningar** kolumnvärde i tabellen om specifika inställningar krävs för en komponent, som att ändra dess **[!UICONTROL Component name]** eller definiera **[!UICONTROL INCLUDE EXCLUDE VALUES]**.

      ![Komponentinställningar för CJA-datavyn](assets/cja-dataview-component-settings.png)

      **METRIK**

      | Komponentnamn | Datauppsättning | Datatyp för schema | Schema Path | Komponentinställningar |
      |---|---|---|---|---|
      | Avvisa | AJO Push Tracking Experience, händelsedatauppsättning för Luma-mobilapp, händelsedatauppsättning för Luma-mobilapp | Heltal | _experience.decisioning.<br/>propositionEventType.dismiss | Komponentnamn: `Dismiss` |
      | Avbeställ | AJO Push Tracking Experience, händelsedatauppsättning för Luma-mobilapp, händelsedatauppsättning för Luma-mobilapp | Heltal | _experience.decisioning.<br/>propositionEventType.unsubscribe | Komponentnamn: `Unsubscribe` |
      | Utlösare | AJO Push Tracking Experience, händelsedatauppsättning för Luma-mobilapp, händelsedatauppsättning för Luma-mobilapp | Heltal | _experience.decisioning.<br/>propositionEventType.trigger | Komponentnamn: `Trigger` |
      | Visa | AJO Push Tracking Experience, händelsedatauppsättning för Luma-mobilapp, händelsedatauppsättning för Luma-mobilapp | Heltal | _experience.decisioning.<br/>propositionEventType.display | Komponentnamn: `Display` |
      | Skicka | AJO Push Tracking Experience, händelsedatauppsättning för Luma-mobilapp, händelsedatauppsättning för Luma-mobilapp | Heltal | _experience.decisioning.<br/>propositionEventType.send | Komponentnamn: `Send` |
      | Interagera | AJO Push Tracking Experience, händelsedatauppsättning för Luma-mobilapp, händelsedatauppsättning för Luma-mobilapp | Heltal | _experience.decisioning.<br/>propositionEventType.interact | Komponentnamn: `Interact` |
      | Platshändelser | AJO Push Tracking Experience Event Dataset, Luma Mobile App Event Dataset, ODE DecisionEvents - beslut för mobil och webb-sdk-kurser | Sträng | Händelsetyp | Komponentnamn: `Location Events`<br/><br/>![Inkludera/exkludera](assets/cja-dataview-include-exclude.png) |
      | Produktvyer | Luma Mobile App Event-datauppsättning | Dubbel | commerce.productViews.value | Komponentnamn: `Product Views` |
      | Lägg till produkt i listor | Luma Mobile App Event-datauppsättning | Dubbel | commerce.productListAdds.value | Komponentnamn: `Product Add To Lists` |
      | Inköp | Luma Mobile App Event-datauppsättning | Dubbel | commerce.purchases.value | Komponentnamn: `Purchases` |
      | Spara för senare | Luma Mobile App Event-datauppsättning | Dubbel | commerce.saveForLaters.value | Komponentnamn: `Save For Laters` |
      | Appinteraktioner | Luma Mobile App Event-datauppsättning | Dubbel | _techmarketingdemos.appInformation.<br/>appInteraction.appAction.value | Komponentnamn: `App Interactions` |
      | Skärmvyer | Luma Mobile App Event-datauppsättning | Dubbel | _techmarketingdemos.appInformation.<br/>appStateDetails.screenView.value | Komponentnamn: `Screen Views` |

      {style="table-layout:auto"}

      Observera hur schemafältet för platshändelsemåttet använder **[!UICONTROL INCLUDE EXCLUDE VALUES]** för att räkna händelsetyper som innehåller `location`.

      När du har lagt till alla schemafält från tabellen ovan som en måttkomponent, konfigureras datavyn för **[!UICONTROL METRICS]** ska se ut så här:

      ![CJA Datview 4](assets/cja-dataview-4.png)

      **DIMENSIONER**

      | Komponentnamn | Datauppsättning | Datatyp för schema | Schema Path | Komponentinställningar |
      |---|---|---|---|---|
      | Ort | AJO Push Tracking Experience, händelsedatauppsättning för Luma-mobilapp, händelsedatauppsättning för Luma-mobilapp | Sträng | placeContext.geo.city | Komponentnamn: `City` |
      | Händelsetyper | AJO Push Tracking Experience Event Dataset, Luma Mobile App Event Dataset, ODE DecisionEvents - beslut för mobil och webb-sdk-kurser | Sträng | eventType | Komponentnamn: `Event Types` |
      | Namn på beslutsalternativ | AJO Push Tracking Experience Event Dataset, Luma Mobile App Event Dataset, ODE DecisionEvents - beslut för mobil och webb-sdk-kurser | Sträng | _experience.decisioning.<br/>propositioner.items.name | Komponentnamn: `Decision Option Name` |
      | Namn på appinteraktion | Luma Mobile App Event-datauppsättning | Sträng | _techmarketingdemos.appInformation.<br/>appInteraction.name | Komponentnamn: `App Interaction Name` |
      | Skärmnamn | Luma Mobile App Event-datauppsättning | Sträng | _techmarketingdemos.appInformation.<br/>appStateDetails.screenName | Komponentnamn: `Screen Name` |
      | Aktivitetsnamn | ODE-beslutEvenemang - beslut om mobil- och webbsdk-kurser | Sträng | _experience.decisioning.<br/>propositionDetails.activity.name | Komponentnamn: `Activity Name` |
      | Namn på erbjudande | ODE-beslutEvenemang - beslut om mobil- och webbsdk-kurser | Sträng | _experience.decisioning.<br/>propositionDetails.selections.name | Komponentnamn: `Offer Name` |

      {style="table-layout:auto"}

      När du har lagt till alla schemafält från tabellen ovan som en dimensionskomponent konfigurerar datavyn för **[!UICONTROL DIMENSIONS]** ska se ut så här:

      ![CJA Datview 4](assets/cja-dataview-5.png)

   1. Välj **[!UICONTROL Save and continue]**.

1. The **[!UICONTROL Settings]** -fliken i **[!UICONTROL Luma App - AEP Mobile SDK Tutorial Data view]** I kan du konfigurera filter och sessionsinställningar. I den här självstudiekursen behövs ingen ytterligare konfiguration.

   - Välj **[!UICONTROL Save and finish]**.

Du har definierat datavyn och allt finns på plats för att börja skapa rapporter och visualiseringar.

## Skapa ett projekt

Du använder Workspace-projekt i Customer Journey Analytics för att skapa rapporter och visualiseringar. Det finns många möjligheter att skapa omfattande rapporter och engagerande visualiseringar, men alla dessa möjligheter ligger utanför kursens räckvidd. Se [Översikt över arbetsytan](https://experienceleague.adobe.com/en/docs/customer-journey-analytics-learn/tutorials/analysis-workspace/workspace-projects/analysis-workspace-overview) och [Skapa ett nytt projekt](https://experienceleague.adobe.com/en/docs/customer-journey-analytics-learn/tutorials/analysis-workspace/workspace-projects/build-a-new-project) för mer information.

I det här avsnittet av lektionen skapar du ett projekt som visar rapporter och visualiseringar om:

- Appanvändning: använda informationen om skärm- och appinteraktioner.
- Commerce: använda e-handelshändelser, som produktvyn, för att lägga till i kundvagn och inköp.
- Erbjudanden: använda erbjudanden som visas i appen.
- Lagra besök: använda (simulerade) geofence-händelser från appen.

Så här skapar du ditt projekt:

1. Navigera till gränssnittet Customer Journey Analytics med Apps ![Appar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Apps_18_N.svg) i det övre högra hörnet.

1. Välj **[!UICONTROL Workspace]** på den övre menyraden.

1. Välj **[!UICONTROL Create project]**.

   1. Välj **[!UICONTROL Blank Workspace project]** i popup-dialogrutan.

      ![CJA-projekt - 1](assets/cja-projects-1.png)

   1. Välj **[!UICONTROL Create]**.

1. Du får se **[!UICONTROL New project]** gränssnitt. I det här gränssnittet kan du skapa rapporter och visualiseringar.

1. Välj namnet på projektet (**[!UICONTROL New project]**) och ange ett eget namn för projektet. Till exempel: `Luma App - AEP Mobile SDK Tutorial Project`.
   ![CJA-projekt 2](assets/cja-projects-2.png)

1. Spara projektet genom att välja **[!UICONTROL Project]** > **[!UICONTROL Save]**.
   ![CJA-projekt 3](assets/cja-projects-3.png)

1. I **[!UICONTROL Save]** dialogruta, ignorera alla andra fält och markera **[!UICONTROL Save]**.
   ![CJA-projekt 4](assets/cja-projects-4.png)


>[!IMPORTANT]
>
>   Kom ihåg att spara projektet regelbundet, annars försvinner ändringarna. Du kan snabbt spara projektet med **[!UICONTROL ctrl + s]** (Windows) eller **[!UICONTROL ⌘ (cmd) + s]** (macOS)

Du har nu konfigurerat ditt projekt. Det finns redan en friformspanel på huvudarbetsytan som innehåller en friformstabell. Du kommer snart att lägga till komponenter i den här tabellen, men du måste först se till att friformspanelen använder rätt datavy och rätt tidsperiod.


1. Välj datavyn i listrutan. Till exempel: **[!UICONTROL Luma App - AEP Mobile SDK Tutorial Data view]**. Om du inte kan se datavyn i listan väljer du **[!UICONTROL Show all]** längst ned i listrutan.
   ![CJA-projekt 5](assets/cja-projects-5.png)

1. Ange lämplig tidsperiod för panelen genom att välja standardinställningen **[!UICONTROL This month]** och på popup-panelen definierar du start- och slutdatum. Eller använd en **[!UICONTROL Preset]**, gilla **[!UICONTROL Last 6 full months]** och markera **[!UICONTROL Apply]**.
   ![CJA-projekt 6](assets/cja-projects-6.png)


### Appanvändning

Du vill rapportera hur appen används. Du har lagt till den nödvändiga koden i appen för att registrera appinteraktioner och vilka skärmar som används i appen (se [Spåra händelser](events.md) lektion) och du vill nu rapportera om dessa data.

#### Skärmnamn

Först vill du rapportera vilka skärmar som har visats i appen.

1. Byt namn på **[!UICONTROL Freeform]** panel till `App Usage`.

1. Byt namn på **[!UICONTROL Freeform table]** till `Screen Names`.

1. Välj **[!UICONTROL Show all]** nedanför **[!UICONTROL METRICS]** lista.

1. Dra och släpp **[!UICONTROL Screen Views]** komponent på [!UICONTROL _Släpp **mått**här (eller någon annan komponent)_)].
   ![CJA-projekt 7](assets/cja-projects-7.png)
I frihandstabellen visas nu skärmvyer för de dagar som du har valt för den angivna tidsperioden. Du vill dock visa skärmvyer för de olika skärmar som används i appen.

1. Visa **[!UICONTROL DIMENSIONS]** lista med komponenter, välja ![Kryss](https://spectrum.adobe.com/static/icons/ui_18/CrossSize100.svg) för att ta bort ![Händelse](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Event_18_N.svg) **[!UICONTROL Metrics]** filter från komponenterna.
   ![CJA-projekt 8](assets/cja-projects-8.png)

1. Välj **[!UICONTROL Show all]** nedanför **[!UICONTROL DIMENSIONS]** lista.

1. Dra och släpp **[!UICONTROL Screen Name]** -komponenten på **[!UICONTROL Day]** header. Åtgärden visar ![Byt](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Switch_18_N.svg) **[!UICONTROL Replace]** för att ange att dimensionen ska ersättas.
   ![CJA-projekt 9](assets/cja-projects-9.png)

Din första rapport är klar och visar skärmvisningar för de olika skärmnamn du har definierat i appen.

![CJA-projekt 10](assets/cja-projects-10.png)

Glöm inte att spara projektet!

#### Appinteraktioner

Du vill också rapportera hur användarna interagerade med appen.

1. Välj ![Lägg till](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) och från popup-fönstret ![Frihandsregister](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Table_18_N.svg) om du vill lägga till en ny friformstabell.
   ![CJA-projekt 11](assets/cja-projects-11.png)

1. Byt namn **[!UICONTROL Freeform table (2)]** till `App Interactions`.

1. Dra och släpp **[!UICONTROL App Interactions]** mått på [!UICONTROL _Släpp **mått**här (eller någon annan komponent)_)].

1. Dra och släpp **[!UICONTROL App Interaction Name]** dimension på **[!UICONTROL Day]** huvud som ska ersätta dimensionen.

Din andra rapport är nu klar och visar appinteraktioner.
![CJA-projekt 12](assets/cja-projects-12.png)

Informationen är begränsad huvudsakligen eftersom du implementerat `MobileSDK.shared.sendAppInteractionEvent(actionName: "<actionName>")` API-anrop enbart på inloggningsskärmen. Om du lägger till det här API-anropet på fler skärmar i din app blir den här rapporten mer informativ.

Glöm inte att spara projektet!


### Commerce

Nu vill du rapportera om e-handelshändelser som inträffar i appen på en separat panel.

#### Commerce Events

1. Välj ![Lägg till](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) utanför aktuell [!UICONTROL App Usage] för att skapa en ny panel.
   ![CJA-projekt 13](assets/cja-projects-13.png)

1. Se till att du väljer lämplig tidsperiod.

1. Välj ![Frihandsregister](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Table_18_N.svg) **[!UICONTROL Freeform table]** om du vill skapa en ny friformstabell.
   ![CJA-projekt 14](assets/cja-projects-14.png)

1. Byt namn **[!UICONTROL Panel]** till `Commerce`.

1. Byt namn **[!UICONTROL Freeform table]** till `Commerce Events`.

1. Dra och släpp **[!UICONTROL Product Views]** till [!UICONTROL _Släpp **mått**här (eller någon annan komponent)_)].

1. Dra och släpp **[!UICONTROL Product Add To Lists]** måttet till höger om **[!UICONTROL Product Views]** om du vill infoga den här kolumnen i frihandstabellen. Säkerställ **[!UICONTROL + Add]** (i blått) visas när du infogar kolumnen.
   ![CJA-projekt 15](assets/cja-projects-15.png)

1. Upprepa föregående steg för att lägga till **[!UICONTROL Save For Laters]** mätvärden och **[!UICONTROL Purchases]** mätvärden till frihandstabellen.

1. Dra och släpp **[!UICONTROL Month]** -dimensionen ovanpå **[!UICONTROL Day]** för att ändra rapporteringen från dag till månad.

Dina **[!UICONTROL Commerce Events]** är nu klar och visar hur användarna har tittat på produkter, lagt till produkter i önskelistan, sparade produkter för senare eller till och med köpt produkterna.
![CJA-projekt 16](assets/cja-projects-16.png)

Glöm inte att spara projektet!

#### Utfall

Baserat på föregående rapport vill du visualisera utfallet i e-handelstratten: hur många användare som visade produkter har också lagt till produkter i kundvagnar. Och hur många användare som har lagt till produkter i sina varukorgar har också sparat dessa produkter för senare tid. Och så vidare.

1. Välj ![Lägg till](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) inom **[!UICONTROL Commerce]** och från popup-menyn ![Utfall](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ConversionFunnel_18_N.svg) (som representerar utfallsvisualiseringen).

1. Välj **[!UICONTROL Product Views]** från [!UICONTROL *Lägg till kontaktyta*] listruta.
   ![CJA-projekt 18](assets/cja-projects-18.png)
Du kan också dra och släppa **[!UICONTROL Products View]** dimension under **[!UICONTROL All people]** dimension i **[!UICONTROL Fallout]** visualisering.

1. Upprepa ovanstående steg för **[!UICONTROL Product Add To Lists]** och **[!UICONTROL Purchases]** dimensioner. Dina **[!UICONTROL Fallout]** visualisering visar nu en visuell representation av konverteringstratten för dina produkter.
   ![CJA-projekt 19](assets/cja-projects-19.png)

Glöm inte att spara projektet!


### Erbjudanden

Du vill rapportera hur många erbjudanden och vilka erbjudanden som visas för appanvändarna.

#### Månadsöversikt

1. Välj ![Lägg till](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) utanför den aktuella Commerce-panelen för att skapa en ny panel.

1. Byt namn på **[!UICONTROL Panel]** till `Offers`.

1. Se till att du väljer lämplig period.

1. Välj ![Frihandsregister](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Table_18_N.svg) Frihandstabell för att skapa en ny frihandstabell.

1. Byt namn på **[!UICONTROL Freeform table]** till `Monthly Overview`.

1. Dra och släpp **[!UICONTROL Display]** till [!UICONTROL _Släpp **mått**här (eller någon annan komponent)_)].

1. Dra och släpp **[!UICONTROL Month]** dimension på **[!UICONTROL Day]** kolumn som ska ersätta dimensionen.

Nu har du en rapport som visar de månatliga erbjudanden som visas för användarna i appen.
![CJA Projects 20](assets/cja-projects-20.png)

Glöm inte att spara projektet!


#### Erbjudanden till människor

Du vill också ha en rapport som visar vilka erbjudanden som visades i vilka nummer appanvändarna fick.

1. Välj ![Lägg till](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) inom **[!UICONTROL Offers]** panel och ![Frihandsregister](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Table_18_N.svg)från popup-fönstret för att lägga till en ny friformstabell.

1. Byt namn **[!UICONTROL Freeform table (2)]** till `People`.

1. Dra och släpp **[!UICONTROL People]** till [!UICONTROL _Släpp **mått**här (eller någon annan komponent)_)].

1. Dra och släpp **[!UICONTROL Activity Name]** på **[!UICONTROL Day]** kolumn som ska ersätta dimensionen.

1. Högerklicka på raden för att identifiera ett eller flera av de offertbeslut som du definierade i dialogrutan [Skapa och visa erbjudanden med Beslutshantering](journey-optimizer-offers.md) lektion. Till exempel: **[!UICONTROL Luma - Mobile App Decision]**.

1. Välj **[!UICONTROL Breakdown]** > **[!UICONTROL Dimensions]** > **[!UICONTROL Offer Name]**. Det här valet kommer att dela upp dimensionen Aktivitetsnamn i Erbjudandenamn.
   ![CJA Projects 20b](assets/cja-projects-20b.png)

Du har nu en rapport som visar de enskilda erbjudanden som visas för det här erbjudandebeslutet för den valda perioden för appanvändarna.
![CJA-projekt 21](assets/cja-projects-21.png)

Glöm inte att spara projektet!


### Butiksbesök

Slutligen vill ni rapportera om butiksbesök.

1. Välj ![Lägg till](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) utanför den aktuella panelen Erbjudanden för att skapa en ny panel.

1. Byt namn på **[!UICONTROL Panel]** till `Store Visits`.

1. Se till att du väljer lämplig period.

1. Välj ![Frihandsregister](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Table_18_N.svg) Frihandstabell för att skapa en ny frihandstabell.

1. Byt namn **[!UICONTROL Freeform table]** till `Store Entries / Exits Across Cities`.

1. Dra och släpp **[!UICONTROL Location Events]** till [!UICONTROL _Släpp **mått**här (eller någon annan komponent)_)]. Rapporten visar nu en daglig översikt över alla platshändelser som inträffade i appen. Kom ihåg hur du specifikt konfigurerade den här dimensionen som en del av [datavy](#create-a-data-view).

1. Dra och släpp **[!UICONTROL City]** dimension på **[!UICONTROL Day]** kolumnrubrik som ska ersätta dimensionen. Rapporten visar nu städerna för platshändelserna.

1. Om du vill ta bort geopositioneringshändelser utan associerade städer väljer du ![Filter](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Filter_18_N.svg)och från **[!UICONTROL Search]** popup, stänga av **[!UICONTROL Include "No value"]** väljer **[!UICONTROL Apply]**.

   ![CJA-projekt 22](assets/cja-projects-22.png)

   Den här åtgärden tar bort **[!UICONTROL No value]** rad från rapporten.

1. Markera alla rader i tabellen, högerklicka och välj Brytning > Dimension > Händelsetyper på snabbmenyn.

Nu har du en rapport som visar att användare befinner sig i och utanför butiksplatserna (som du definierade dessa platser i [Platser](places.md) lektion).

![CJA-projekt 23](assets/cja-projects-23.png)

Observera att du kan använda beacons om du verkligen vill rapportera om personer som fysiskt besöker din butik. Men förhoppningsvis har ni lyckats fånga upp begreppet rapportering av geolokaliseringsdata.

## Nästa steg

Nu bör du ha en grundläggande förståelse för hur du kan rapportera och visualisera om användningen av mobilappar, interaktioner med mera med Customer Journey Analytics.

>[!SUCCESS]
>
>
>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Mobile SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Nästa: **[Slutsats och nästa steg](conclusion.md)**
