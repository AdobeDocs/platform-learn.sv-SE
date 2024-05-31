---
title: Konfigurera Adobe Analytics med Experience Platform Web SDK
description: Lär dig hur du konfigurerar Adobe Analytics med Experience Platform Web SDK. Den här lektionen ingår i självstudiekursen Implementera Adobe Experience Cloud med Web SDK.
solution: Data Collection, Analytics
jira: KT-15408
exl-id: de86b936-0a47-4ade-8ca7-834c6ed0f041
source-git-commit: c5318809bfd475463bac3c05d4f35138fb2d7f28
workflow-type: tm+mt
source-wordcount: '2628'
ht-degree: 0%

---

# Konfigurera Adobe Analytics med Adobe Experience Platform Web SDK

Lär dig konfigurera Adobe Analytics med [Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/en/docs/platform-learn/data-collection/web-sdk/overview), skapa taggregler för att skicka data till Adobe Analytics och validera att Analytics hämtar in data som förväntat.

[Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics) är en branschledande applikation som ger er möjlighet att förstå era kunder som människor och styra verksamheten med kundanalys.

![Web SDK till Adobe Analytics-diagram](assets/dc-websdk-aa.png)

## Utbildningsmål

När lektionen är klar kan du:

* Konfigurera ett datastream för att aktivera Adobe Analytics
* Ta reda på vilka XDM-standardfält som automatiskt mappas till analysvariabler
* Ange analysvariabler i dataobjektet
* Skicka data till en annan rapportserie genom att åsidosätta datastream
* Validera Adobe Analytics-variabler med Felsökning och Assurance

## Förutsättningar

För att slutföra lektionen måste du först:

* Bekanta dig med och få tillgång till Adobe Analytics.

* Ha minst ett test-/dev-rapportpaket-ID. Om du inte har någon test-/dev-rapportsserie som du kan använda för den här självstudiekursen, [skapa en](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/c-new-report-suite/t-create-a-report-suite).

* Slutför de tidigare lektionerna i avsnitten Inledande konfiguration och Tagginställningar i den här självstudien.

## Konfigurera datastream

Platform Web SDK skickar data från din webbplats till Platform Edge Network. Din datastream talar sedan om för Platform Edge Network till vilken Adobe Analytics-rapport säger att dina data ska skickas.

1. Gå till [Datainsamling](https://experience.adobe.com/#/data-collection){target="blank"} gränssnitt
1. Välj **[!UICONTROL Datastreams]**
1. Markera tidigare skapade `Luma Web SDK: Development Environment` datastream

   ![Välj dataströmmen för Luma Web SDK](assets/datastream-luma-web-sdk-development.png)

1. Välj **[!UICONTROL Add Service]**
   ![Lägg till en tjänst i datastream](assets/datastream-analytics-addService.png)
1. Välj **[!UICONTROL Adobe Analytics]** som **[!UICONTROL Service]**
1. Ange **[!UICONTROL Report Suite ID]** av din utvecklingsrapportsserie
1. Välj **[!UICONTROL Save]**

   ![DataStream Save analytics](assets/datastream-add-analytics.png)

   >[!TIP]
   >
   >Lägg till fler rapportsviter genom att välja **[!UICONTROL Add Report Suite]** motsvarar taggning i flera programsviter.

>[!WARNING]
>
>I den här självstudiekursen konfigurerar du bara Adobe Analytics rapportsvit för din utvecklingsmiljö. När du skapar datastreams för din egen webbplats bör du skapa ytterligare datastreams och rapportsviter för dina staging- och produktionsmiljöer.

## Ange analysvariabler

Det finns flera sätt att ställa in Analytics-variabler i en Web SDK-implementering:

1. Automatisk mappning av XDM-fält till analysvariabler (automatiskt).
1. Ange fält i dialogrutan `data` objekt (rekommenderas).
1. Mappa XDM-fält till Analytics-variabler i Analytics-bearbetningsregler (rekommenderas inte längre).
1. Mappa till Analytics-variabler direkt i XDM-schemat (rekommenderas inte längre).

Från maj 2024 behöver du inte längre skapa ett XDM-schema för att implementera Adobe Analytics med Platform Web SDK. The `data` -objekt (och `data.variable` dataelement som du skapade i den här självstudiekursen) kan användas för att ställa in alla anpassade Analytics-variabler. Att ställa in dessa variabler i dataobjektet kommer att kännas bekant för befintliga analyskunder, är mer effektivt än att använda gränssnittet för bearbetningsregler och förhindrar att onödiga data tar upp utrymme i kundprofiler i realtid (viktigt om du har Real-time Customer Data Platform eller Journey Optimizer).

### Automatiskt mappade fält

Många XDM-fält mappas automatiskt till analysvariabler. Den senaste listan över mappningar finns på [Variabelmappning för analyser i Adobe Experience Edge](https://experienceleague.adobe.com/en/docs/experience-platform/edge/data-collection/adobe-analytics/automatically-mapped-vars).

Detta inträffar om _även om du inte har definierat ett anpassat schema_. Experience Platform Web SDK samlar automatiskt in vissa data och skickar dem till Platform Edge Network som XDM-fält. Web SDK läser till exempel den aktuella sidans URL och skickar den som `web.webPageDetails.URL`. Det här fältet vidarebefordras till Adobe Analytics och fyller automatiskt i sidans URL-rapporter i Adobe Analytics.

När du implementerar Web SDK för analyser och plattformsbaserade program skapar du ett anpassat XDM-schema, som du har gjort i den här självstudiekursen i [Konfigurera ett schema](configure-schemas.md) lektion. Några av de XDM-fält som du har implementerat för automatisk mappning till analysvariabler, enligt beskrivningen i följande tabell:

| XDM till Analytics - automappade variabler | Adobe Analytics-variabel |
|-------|---------|
| `identitymap.ecid.[0].id` | mitten |
| `web.webPageDetails.name` | s.pageName |
| `web.webPageDetails.server` | s.server |
| `web.webPageDetails.siteSection` | s.channel |
| `commerce.productViews.value` | prodView |
| `commerce.productListViews.value` | scView |
| `commerce.checkouts.value` | scCheckout |
| `commerce.purchases.value` | köp |
| `commerce.order.currencyCode` | s.currencyCode |
| `commerce.order.purchaseID` | s.purchaseID |
| `productListItems[].SKU` | s.products=;product name;;;; (primär - se anmärkning nedan) |
| `productListItems[].name` | s.products=;product name;;;; (fallback - se anm. nedan) |
| `productListItems[].quantity` | s.products=;;produktkvantitet; |
| `productListItems[].priceTotal` | s.product=;;;produktpris; |

De enskilda avsnitten i Analytics-produktsträngen anges via olika XDM-variabler under `productListItems` -objekt.

>18 augusti 2022 `productListItems[].SKU` prioriterar mappning till produktnamnet i variabeln s.products.
>Värdet som anges till `productListItems[].name` mappas endast till produktnamnet om `productListItems[].SKU` finns inte. Annars är den omappad och tillgänglig i kontextdata.
>Ange inte en tom sträng eller null till `productListItems[].SKU`. Detta har den oönskade effekten av att mappa till produktnamnet i variabeln s.products.

### Ange variabler i dataobjektet

Ange variabler i `data` är det rekommenderade sättet att ställa in Analytics-variabler med Web SDK. Om du ställer in variabler i dataobjektet kan även alla automatiskt mappade variabler skrivas över.

För det första, vad är `data` objekt? I alla Web SDK-händelser kan du skicka två objekt med anpassade data, `data` -objektet och `xdm` -objekt. Båda skickas till Platform Edge Network, men bara till `xdm` -objektet skickas till datauppsättningen Experience Platform. Egenskaper i `data` kan mappas på Edge till `xdm` fält som använder funktionen Dataprep för datainsamling, men som annars inte skickas till Experience Platform. Detta gör det till ett idealiskt sätt att skicka data till program som Analytics, som inte är inbyggt i Experience Platform.

Här är de två objekten i ett generiskt Web SDK-anrop:

![data- och xdm-objekt](assets/analytics-data-object-intro.png)

Adobe Analytics har konfigurerats för att söka efter egenskaper i `data.__adobe.analytics` och använda dem för analysvariabler.

Nu gör vi det här.

Vi använder `data.variable` dataelement t


<!--


### Map to Analytics variables with processing rules

All fields in the XDM schema become available to Adobe Analytics as Context Data Variables with the following prefix `a.x.`. For example, `a.x.web.webinteraction.region`

In this exercise, you map one XDM variable to a prop. Follow these same steps for any custom mapping that you must do for any `eVar`, `prop`, `event`, or variable accessible via Processing Rules.

1. Go to the Analytics interface
1. Go to [!UICONTROL Admin] > [!UICONTROL Admin Tools] > [!UICONTROL Report Suites ]
1. Select the dev/test report suite that you are using for the tutorial > [!UICONTROL Edit Settings] > [!UICONTROL General] > [!UICONTROL Processing Rules]

    ![Analytics Purchase](assets/analytics-process-rules.png)   

1. Create a rule to **[!UICONTROL Overwrite value of]** `[!UICONTROL Product SKU (prop1)]` to `a.x.productlistitems.0.sku`. Remember to add a note about why you are creating the rule and name your rule title. Select **[!UICONTROL Save]**

    ![Analytics Purchase](assets/analytics-set-processing-rule.png)   

    >[!IMPORTANT]
    >
    >The first time you map to a processing rule, the UI does not show you the context data variables from the XDM object. To fix that select any value, Save, and come back to edit. All XDM variables should now appear.

### Map to Analytics variables using the Adobe Analytics field group

An alternative to processing rules is to map to Analytics variables in the XDM schema using the `Adobe Analytics ExperienceEvent Template` field group. This approach has gained popularity because many users find it simpler than configuring processing rules, however, by increasing the size of the XDM payload it could in turn increase the profile size in other applications like Real-Time CDP.

To add the `Adobe Analytics ExperienceEvent Template` field group to your schema:

1. Open the [Data Collection](https://experience.adobe.com/#/data-collection){target="blank"} interface
1. Select **[!UICONTROL Schemas]** from the left navigation
1. Make sure you are in the sandbox you are using from the tutorial
1. Open your `Luma Web Event Data` schema
1. In the **[!UICONTROL Field Groups]** section, select **[!UICONTROL Add]**
1. Find the `Adobe Analytics ExperienceEvent Template` field group and add it to your schema


Now, set a merchandising eVar in the product string. With the `Adobe Analytics ExperienceEvent Template` field group, you are able to map variables to merchandising eVars or events within the product string. This is also known as setting **Product Syntax Merchandising**. 

1. Go back to your tag property

1. Open the rule `ecommerce - library loaded - set product details variables - 20`

1. Open the **[!UICONTROL Set Variable]** action

1. Select to open `_experience > analytics > customDimensions > eVars > eVar1`

1. Set the **[!UICONTROL Value]** to `%product.productInfo.title%`

1. Select **[!UICONTROL Keep Changes]**

    ![Product SKU XDM object Variable](assets/set-up-analytics-product-merchandising.png)

1. Select **[!UICONTROL Save]** to save the rule

As you just saw, basically all of the Analytics variables can be set in the `Adobe Analytics ExperienceEvent Template` field group.

>[!NOTE]
>
> Notice the `_experience` object under `productListItems` > `Item 1`. Setting any variable under this [!UICONTROL object] sets Product Syntax eVars or Events.

-->

## Skicka data till en annan rapportserie

Du kanske vill ändra vilka data i Adobe Analytics rapportserie som skickas till när besökarna finns på vissa sidor. Detta kräver en konfiguration i både datastream och en regel.

### Konfigurera datastream för åsidosättning av en rapportserie

Så här konfigurerar du åsidosättningsinställningen för Adobe Analytics-rapportsviten i datastream:

1. Öppna ditt datastream
1. Redigera **[!UICONTROL Adobe Analytics]** genom att öppna ![mer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) och sedan välja **[!UICONTROL Edit]**

   ![Skriv över datastream](assets/datastream-edit-analytics.png)

1. Välj **[!UICONTROL Advance Options]** att öppna **[!UICONTROL Report Suite Overrides]**

1. Markera de rapportsviter som du vill åsidosätta. I detta fall `Web SDK Course Dev` och `Web SDK Course Stg`

1. Välj **[!UICONTROL Save]**

   ![Skriv över datastream](assets/analytics-datastreams-edit-adobe-analytics-configurations-report-suites.png)


### Konfigurera en regel för åsidosättning av en rapportserie

Låt oss skapa en regel för att skicka ytterligare ett sidvisningsanrop till en annan rapportserie. Använd åsidosättningsfunktionen för datastream för att ändra rapportsviten för en sida med hjälp av **[!UICONTROL Send Event]** Åtgärd.

1. Skapa en ny regel, kalla den `homepage - library loaded - AA report suite override - 51`

1. Markera plustecknet under **[!UICONTROL Event]** lägga till en ny utlösare

1. Under **[!UICONTROL Extension]**, markera **[!UICONTROL Core]**

1. Under **[!UICONTROL Event Type]**, markera **[!UICONTROL library loaded]**

1. Markera för att öppna **[!UICONTROL Advanced Options]**, skriva in `51`. Detta garanterar att regeln körs efter `all pages - library loaded - send event - 50` som ställer in baslinje-XDM med **[!UICONTROL Update variable]** åtgärdstyp.

   ![Åsidosättning av analysrapportsSuite](assets/set-up-analytics-rs-override.png)

1. Under **[!UICONTROL Conditions]**, välj **[!UICONTROL Add]**

1. Lämna **[!UICONTROL Logic Type]** as **[!UICONTROL Regular]**

1. Lämna **[!UICONTROL Extensions]** as **[!UICONTROL Core]**

1. Välj **[!UICONTROL Condition Type]** as **[!UICONTROL Path Without Query String]**

1. Till höger, lämna **[!UICONTROL Regex]** växla inaktiverad

1. Under **[!UICONTROL path equals]** set `/content/luma/us/en.html`. För demonstrationswebbplatsen Luma säkerställer den att regeln endast aktiveras på startsidan

1. Välj **[!UICONTROL Keep Changes]**

   ![Villkor för åsidosättning av analysrapportsserie](assets/set-up-analytics-override-condition.png)

1. Under **[!UICONTROL Actions]** välj **[!UICONTROL Add]**

1. Som **[!UICONTROL Extension]**, markera **[!UICONTROL Adobe Experience Platform Web SDK]**

1. Som **[!UICONTROL Action Type]**, markera **[!UICONTROL Send Event]**

1. Som **[!UICONTROL Type]**, markera `web.webpagedetails.pageViews`

1. Som **[!UICONTROL XDM data]** väljer du `xdm.variable.content` dataelement som du skapade i [Skapa dataelement](create-data-elements.md) lektion

   ![Åsidosättning av analysdataström](assets/set-up-analytics-datastream-override-1.png)

1. Bläddra nedåt till **[!UICONTROL Datastream Configurations Overrides]** section

1. Lämna **[!UICONTROL Development]** har valts.

   >[!TIP]
   >
   >    Den här fliken avgör i vilken taggmiljö åsidosättningen sker. I det här exemplet anger du bara utvecklingsmiljön, men när du distribuerar den till produktionen måste du också göra det i **[!UICONTROL Production]** miljö.


1. Välj **[!UICONTROL Datastream]**, i detta fall `Luma Web SDK: Development Environment`

1. Under **[!UICONTROL Report suites]** väljer du den rapportwebbplats som du vill åsidosätta. I detta fall `tmd-websdk-course-stg`.

1. Välj **[!UICONTROL Keep Changes]**

1. Och **[!UICONTROL Save]** din regel

   ![Åsidosättning av analysdataström](assets/analytics-tags-report-suite-override.png)


## Bygg en utvecklingsmiljö

Lägg till nya dataelement och regler i `Luma Web SDK Tutorial` och bygga om utvecklingsmiljön.

Grattis! Nästa steg är att validera din Adobe Analytics-implementering via Experience Platform Web SDK.

## Validera Adobe Analytics med felsökning

Lär dig hur du validerar att Adobe Analytics spelar in ECID, sidvisningar, produktsträngen och e-handelshändelser med Edge Trace-funktionen i felsökaren för Experience Platform.

I [Felsökning](validate-with-debugger.md) i lektionen lärde du dig att inspektera XDM-begäran på klientsidan med plattformsfelsökaren och webbläsarutvecklarkonsolen, som liknar hur du felsöker en `AppMeasurement.js` Implementering av analyser. Du har också lärt dig att validera begäranden på serversidan för Platform Edge Network som skickas till Adobe-program och hur du visar en fullt bearbetad nyttolast med hjälp av Assurance.

För att validera att Analytics hämtar in data korrekt via Experience Platform Web SDK måste du gå två steg längre:

1. Validera hur data bearbetas av XDM-objektet på Platform Edge Network med hjälp av funktionen Edge Trace i Experience Platform Debugger
1. Validera hur data bearbetas fullt ut av Analytics med Adobe Experience Platform Assurance

### Experience Cloud ID-validering

1. Gå till [Luma demo site](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"}
1. Välj inloggningsknappen högst upp till höger och använd inloggningsuppgifterna u: test@adobe.com p: test to authenticate
1. Öppna felsökaren för Experience Platform och [växla taggegenskapen på webbplatsen till din egen utvecklingsegenskap](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tags-property)


1. Om du vill aktivera Edge Trace går du till Felsökning för Experience Platform, i den vänstra navigeringen väljer du **[!UICONTROL Logs]** väljer du **[!UICONTROL Edge]** och markera **[!UICONTROL Connect]**

   ![Koppla kantkalkering](assets/analytics-debugger-edgeTrace.png)

1. Den kommer att vara tom tills vidare

   ![Ansluten kantkalkering](assets/analytics-debugger-edge-connected.png)

1. Uppdatera Luma-sidan och kontrollera felsökaren i Experience Platform igen. Du bör se data som skickats. Raden börjar med **[!UICONTROL Analytics Automatic Mapping]** är Adobe Analytics fyr
1. Markera för att öppna båda `[!UICONTROL mappedQueryParams]` listruta och den andra listrutan för att visa Analytics-variabler

   ![Kantkalkering för analysfyr](assets/analytics-debugger-edge-analytics.png)

   >[!TIP]
   >
   >Den andra listrutan motsvarar det ID för analysrapportsserie som du skickar data till. Det ska matcha din egen rapportsserie, inte den i skärmbilden.

1. Bläddra nedåt för att hitta `[!UICONTROL c.a.x.identitymap.ecid.[0].id]`. Det är en kontextdatavariabel som hämtar ECID
1. Fortsätt rulla nedåt tills du ser Analytics `[!UICONTROL mid]` variabel. Båda ID:n överensstämmer med enhetens Experience Cloud ID.
1. På Lumas webbplats

   ![Analytics ECID](assets/analytics-debugger-ecid.png)

   >[!NOTE]
   >
   >Eftersom du är inloggad bör du ägna en stund åt att validera det autentiserade ID:t `112ca06ed53d3db37e4cea49cc45b71e` för användaren **`test@adobe.com`** tas också med i `[!UICONTROL c.a.x.identitymap.lumacrmid.[0].id]`

### Åsidosättningsvalidering av rapportsviten

Ovanför du konfigurerade en åsidosättning av datastream för [Lumas hemsida](https://luma.enablementadobe.com/content/luma/us/en.html).  Validera konfigurationen

1. Leta efter en rad med **[!UICONTROL Datastream config after override was applied]**. Här hittar du den primära rapportsviten och de extra rapportsviterna som har konfigurerats för åsidosättningar av rapportsviten.

   ![Verifiering av åsidosättningslista för Analytics-rapportsviten](assets/aep-debugger-datastream-override.png)

1. Bläddra nedåt till raden som börjar med **[!UICONTROL Analytics Automatic Mapping]**  och verifiera att `[!UICONTROL reportSuiteIds]` visar rapportsviten som du angav i dina åsidosättningskonfigurationer

   ![Analytics Report Suite Override Call Validation](assets/aep-debugger-analytics-report-suite-override.png)

### Validering av vyer av innehållssidor

Gå till en produktsida som [Didi Sport Watch produktsida](https://luma.enablementadobe.com/content/luma/us/en/products/gear/watches/didi-sport-watch.html#24-WG02).  Verifiera att innehållssidvisningar hämtas av Analytics.

1. Leta efter `[!UICONTROL c.a.x.web.webpagedetails.pageviews.value]=1`.
1. Bläddra nedåt för att se `[!UICONTROL gn]` variabel. Det är den dynamiska syntaxen i Analytics för `[!UICONTROL s.pageName]` variabel. Det hämtar sidnamnet från datalagret.

   ![Produktsträng för Analytics](assets/analytics-debugger-edge-page-view.png)

### Produktsträng och validering av e-handelshändelser

Eftersom du redan är på en produktsida fortsätter den här övningen att använda samma Edge Trace för att validera att produktdata hämtas av Analytics. Både produktsträngen och e-handelshändelserna mappas automatiskt XDM-variabler till Analytics. Så länge du har mappat till rätt `productListItem` XDM-variabeln while [konfigurera ett XDM-schema för Adobe Analytics](setup-analytics.md#configure-an-xdm-schema-for-adobe-analytics)tar Platform Edge Network hand om att mappa data till rätt analysvariabler.

**Verifiera först att `Product String` är inställt**

1. Leta efter `[!UICONTROL c.a.x.productlistitems.][0].[!UICONTROL sku]`. Variabeln hämtar det dataelementvärde som du har mappat till `productListItems.item1.sku` tidigare i den här lektionen
1. Sök även efter `[!UICONTROL c.a.x.productlistitems.][0].[!UICONTROL _experience.analytics.customdimensions.evars.evar1]`. Variabeln hämtar det dataelementvärde som du har mappat till `productListItems.item1._experience.analytics.customdimensions.evars.evar1`
1. Bläddra nedåt för att se `[!UICONTROL pl]` variabel. Det är den dynamiska syntaxen för produktsträngvariabeln Analytics
1. Observera att produktnamnet från datalagret mappas både till `[!UICONTROL c.a.x.productlistitems.][0].[!UICONTROL sku]` och `[!UICONTROL product]` -parametern i produktsträngen.  Dessutom mappas produkttiteln från datalagret till merchandising evar1 i produktsträngen.

   ![Produktsträng för Analytics](assets/analytics-debugger-prodstring.png)

   Edge Trace behandlar `commerce` händelser något annorlunda än `productList` dimensioner. Du ser inte att en kontextdatavariabel är mappad på samma sätt som du ser produktnamnet mappat till `[!UICONTROL c.a.x.productlistitem.[0].name]` ovan. I stället visar Edge Trace den slutliga automatiska händelsemappningen i Analytics `event` variabel. Platform Edge Network mappar den så länge du mappar till rätt XDM `commerce` variabel while [konfigurera schema för Adobe Analytics](setup-analytics.md#configure-an-xdm-schema-for-adobe-analytics); i detta fall `commerce.productViews.value=1`.

1. Gå tillbaka till Experience Platform Debugger-fönstret och rulla nedåt till `[!UICONTROL events]` variabel, är inställd på `[!UICONTROL prodView]`

1. Obs! `[!UICONTROL c.a.x.eventType]` är inställd på `commerce.productViews` eftersom du är på en produktsida.

   >[!TIP]
   >
   > The `ecommerce - pdp library loaded - AA (order 20)` regeln skriver över värdet för `eventType` anges av `all pages global content variables - library loaded - AA (order 1)` styckelinje efter att den har ställts in att utlösas senare i sekvensen


   ![Analytics - produktvy](assets/analytics-debugger-prodView.png)

**Validera resten av e-handelshändelser och produktsträngar för Analytics**

1. Lägg till [Didi Sport Watch](https://luma.enablementadobe.com/content/luma/us/en/products/gear/watches/didi-sport-watch.html#24-WG02) till kundvagn
1. Gå till [Kundsida](https://luma.enablementadobe.com/content/luma/us/en/user/cart.html), kontrollera Edge Trace för

   * `eventType` ange till `commerce.productListViews`
   * `[!UICONTROL events: "scView"]`och
   * produktsträngen är inställd

   ![Vy för analyskundvagn](assets/analytics-debugger-cartView.png)

1. Fortsätt till kassan, kontrollera Edge Trace för

   * `eventType` ange till `commerce.checkouts`
   * `[!UICONTROL events: "scCheckout"]`och
   * produktsträngen är inställd

   ![Utcheckning av analyser](assets/analytics-debugger-checkout.png)

1. Fyll ut bara **Förnamn** och **Efternamn** fält i leveransformuläret och välj **Fortsätt**. På nästa sida väljer du **Montera beställning**
1. På bekräftelsesidan kan du kontrollera Edge Trace för

   * `eventType` ange till `commerce.purchases`
   * Inköpshändelse som ställs in `[!UICONTROL events: "purchase"]`
   * Valutakodvariabeln anges `[!UICONTROL cc: "USD"]`
   * Inköps-ID anges `[!UICONTROL pi]`
   * Produktsträng `[!UICONTROL pl]` ange produktnamn, kvantitet och pris

   ![Köp av analyser](assets/analytics-debugger-purchase.png)



## Validera Adobe Analytics med Assurance

Adobe Experience Platform Assurance hjälper er att inspektera, bevisa, simulera och validera hur ni samlar in data eller levererar upplevelser via er webbplats och mobilapplikation.

I den föregående övningen validerade du att Adobe Analytics spelar in ECID, sidvisningar, produktsträngen och e-handelshändelser med Edge Trace-funktionen i felsökaren för Experience Platform.  Sedan validerar du dessa händelser med Adobe Experience Platform Assurance, ett alternativt gränssnitt för att få tillgång till samma data i Edge Trace.

Som du lärde dig i [Säkerhet](validate-with-assurance.md) kan du starta en Assurance-session på flera olika sätt. Eftersom du redan har Adobe Experience Platform Debugger öppen med en Edge Trace-session som initierats från den senaste övningen rekommenderar vi att du får åtkomst till Assurance via Felsökning:
![Säkerhet genom Adobe Experience Platform Data Collection](assets/assurance-open-aep-debugger.png)

I **[!UICONTROL "Web SDK Tutorial 3"]** Anmäl session **[!UICONTROL "hitdebugger"]** i sökfältet Händelser för att filtrera resultaten till data som bearbetats i Adobe Analytics Post.
![Adobe-analys för Assurance-efterbearbetade data](assets/assurance-hitdebugger.png)

### Experience Cloud ID-validering

Om du vill validera att Adobe Analytics hämtar ECID-numret markerar du en fyr och öppnar nyttolasten.  Leverantören för denna fyr ska vara **[!UICONTROL com.adobe.analytics.hitdebugger]**
![Adobe Analytics validation with Assurance](assets/assurance-hitdebugger-payload.png)

Bläddra sedan nedåt till **[!UICONTROL mcvisId]** för att validera att ECID-numret är korrekt inhämtat
![Experience Cloud ID-validering med Assurance](assets/assurance-hitdebugger-mcvisId.png)

### Validering av vyer av innehållssidor

Använd samma fyr för att kontrollera att vyerna för innehållssidor är mappade till rätt Adobe Analytics-variabel.
Bläddra nedåt till **[!UICONTROL pageName]** för att validera att `Page Name` är korrekt infångad
![Validering av sidnamn med Assurance](assets/assurance-hitdebugger-content-pagename.png)

### Produktsträng och validering av e-handelshändelser

Om du följer samma valideringsexempel som används vid validering med Experience Platform Debugger ovan, fortsätter du att använda samma fyr för att validera `Ecommerce Events` och `Product String`.

1. Sök efter nyttolast där **[!UICONTROL events]** innehåller `prodView`
   ![Produktsträngsvalidering med Assurance](assets/assurance-hitdebugger-prodView-event.png)
1. Bläddra nedåt till **[!UICONTROL product-string]** för att validera `Product String`.
   * Anteckna `Product SKU` och `Merchandizing eVar1`.
1. Bläddra nedåt och validera att `prop1`som du konfigurerade med bearbetningsreglerna i föregående avsnitt innehåller `Product SKU`\
   ![Produktsträng med verifiering av variabler för marknadsföring med Assurance](assets/assurance-hitdebugger-prodView-productString-merchVar.png)

Fortsätt att validera implementeringen genom att granska kundvagnen, kassan och köphändelserna.

1. Sök efter nyttolast där **[!UICONTROL events]** innehåller `scView` och validera produktsträngen.
   ![Produktsträngsvalidering med Assurance](assets/assurance-hitdebugger-scView-event.png)
1. Sök efter nyttolast där **[!UICONTROL events]** innehåller `scCheckout` och validera produktsträngen.
   ![Produktsträngsvalidering med Assurance](assets/assurance-hitdebugger-scView-event.png)
1. Sök efter nyttolast där **[!UICONTROL events]** innehåller `purchase`
   ![Produktsträngsvalidering med Assurance](assets/assurance-hitdebugger-purchase-event.png)
1. Vid validering av `purchase` händelsen observera att `Product String` ska innehålla `Product SKU`, `Product Quantity` och `Product Total Price`.
1. Dessutom `purchase` validera att `purchase-id` och/eller `purchaseId` är inställda


Grattis! Du lyckades! Det här är slutet av lektionen och nu är du redo att implementera Adobe Analytics med Platform Web SDK för din egen webbplats.

[Nästa: ](setup-audience-manager.md)

>[!NOTE]
>
>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Web SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela med dig av dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
