---
title: Konfigurera Adobe Analytics med Experience Platform Web SDK
description: Lär dig hur du konfigurerar Adobe Analytics med Experience Platform Web SDK. Den här lektionen ingår i självstudiekursen Implementera Adobe Experience Cloud med Web SDK.
solution: Data Collection, Analytics
source-git-commit: 26545b660b70daf4296ec2afbc067065f77def01
workflow-type: tm+mt
source-wordcount: '2876'
ht-degree: 0%

---

# Konfigurera Adobe Analytics med Platform Web SDK

Lär dig konfigurera Adobe Analytics med [Experience Platform Web SDK](https://experienceleague.adobe.com/docs/platform-learn/data-collection/web-sdk/overview.html), skapa taggregler för att skicka data till Adobe Analytics och validera att Analytics hämtar in data som förväntat.

[Adobe Analytics](https://experienceleague.adobe.com/docs/analytics.html) är en branschledande applikation som ger er möjlighet att förstå era kunder som människor och styra verksamheten med kundanalys.

![Web SDK till Adobe Analytics-diagram](assets/dc-websdk-aa.png)

## Utbildningsmål

När lektionen är klar kan du:

* Konfigurera ett datastream för att aktivera Adobe Analytics
* Förstå skillnaden mellan automatiskt mappade och manuellt mappade XDM-variabler för Analytics
* Konfigurera ett XDM-schema för Adobe Analytics-specifika variabler
* Ange eVar för produktsyntaxmarknadsföring med hjälp av XDM
* Åsidosätt ett datastream för att skicka data till ett annat Adobe Analytics-rapportpaket
* Validera Adobe Analytics-variabler med Experience Platform Debugger
* Använd Adobe Analytics bearbetningsregler för att ange anpassade variabler
* Validera data som har fångats in av Adobe Analytics med Adobe Experience Platform Assurance
* Validera data hämtas av Adobe Analytics med Real-Time Reports

## Förutsättningar

För att slutföra lektionen måste du först:

* Bekanta dig med och få tillgång till Adobe Analytics.

* Ha minst ett test-/dev-rapportpaket-ID. Om du inte har någon test-/dev-rapportsserie som du kan använda för den här självstudiekursen, [skapa en](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html).

* Slutför de tidigare lektionerna i avsnitten Inledande konfiguration och Tagginställningar i den här självstudien.

## Konfigurera datastream

Platform Web SDK skickar data från din webbplats till Platform Edge Network. Din datastream talar sedan om för Platform Edge Network till vilket Adobe Analytics rapporterar att dina data ska vidarebefordras.

1. Gå till [Datainsamling](https://experience.adobe.com/#/data-collection){target="blank"} gränssnitt
1. Välj **[!UICONTROL Datastreams]**
1. Markera tidigare skapade `Luma Web SDK: Development Environment` datastream

   ![Välj dataströmmen för Luma Web SDK](assets/datastream-luma-web-sdk-development.png)

1. Välj **[!UICONTROL Add Service]**
   ![Lägg till en tjänst i datastream](assets/datastream-analytics-addService.png)
1. Välj **[!UICONTROL Adobe Analytics]** som **[!UICONTROL Service]**
1. Ange  **[!UICONTROL Report Suite ID]** av din utvecklingsrapportsserie
1. Välj **[!UICONTROL Save]**

   ![DataStream Save analytics](assets/datastream-add-analytics.png)

   >[!TIP]
   >
   >Lägg till fler rapportsviter genom att välja **[!UICONTROL Add Report Suite]** motsvarar taggning i flera programsviter.

>[!WARNING]
>
>I den här självstudiekursen konfigurerar du bara Adobe Analytics rapportsvit för din utvecklingsmiljö. När du skapar datastreams för din egen webbplats skapar du ytterligare datastreams och rapportsviter för dina staging- och produktionsmiljöer.

## XDM-scheman och analysvariabler

Grattis! Du har redan konfigurerat ett schema som är kompatibelt med Adobe Analytics i [Konfigurera ett schema](configure-schemas.md) lektion!

Men du kanske undrar hur jag ställer upp alla mina proppar, evar och events?

Det finns flera metoder som kan användas samtidigt:

1. Ange XDM-standardfält och andra mappas automatiskt till analysvariabler.
1. Mappa ytterligare XDM-fält till Analytics-variabler i Analytics-bearbetningsregler.
1. Mappa till Analytics-variabler direkt i XDM-schemat.

<!-- Implementing Platform Web SDK should be as product-agnostic as possible. For Adobe Analytics, mapping eVars, props, and events doesn't occur during schema creation, nor during the tag rules configuration as it has been done traditionally. Instead, every XDM key-value pair becomes a Context Data Variable that maps to an Analytics variable in one of two ways: 

1. Automatically mapped variables using reserved XDM fields
1. Manually mapped variables using Analytics Processing Rules

To understand what XDM variables are auto-mapped to Adobe Analytics, please see [Variables automatically mapped in Analytics](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/adobe-analytics/automatically-mapped-vars.html?lang=en). Any variable that is not auto-mapped must be manually mapped. 

 1. **Product-agnostic XDM**: maintain a semantic key-value pair XDM schema and use [Adobe Analytics Processing Rules](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/processing-rules.html) to map the XDM fields to eVars, props, and so on. By a semantic XDM schema, we mean that the field names themselves have meaning. For example, the field name `web.webPageDetails.pageName` has more meaning than say `prop1` or `evar3`.


 1. **Analytics-specific XDM**: Use a purpose-built Adobe Analytics field group in the XDM schema called `Adobe Analytics ExperienceEvent Template`
 
The approach Adobe has seen customers prefer is the **Analytics-specific XDM**, because it skips the mapping step in the Adobe Analytics Processing Rules interface. The steps in this lesson use the **Analytics-specific XDM** approach.
-->

### Automatiskt mappade fält

Många XDM-fält mappas automatiskt till analysvariabler.

Schemat som skapats i [Konfigurera ett schema](configure-schemas.md) lektionen innehåller några automatiskt mappade till analysvariabler, som beskrivs i följande tabell:

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
>Ange inte en tom sträng eller null till  `productListItems[].SKU`. Detta har den oönskade effekten av att mappa till produktnamnet i variabeln s.products.

Den senaste listan över mappningar finns på [Variabelmappning för analyser i Adobe Experience Edge](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/adobe-analytics/automatically-mapped-vars.html).


### Mappning med analysbearbetningsregler

Alla fält i XDM-schemat blir tillgängliga för Adobe Analytics som Context Data Variables med följande prefix `a.x.`. Exempel: `a.x.web.webinteraction.region`

I den här övningen mappar du en XDM-variabel till en prop. Följ de här stegen för alla anpassade mappningar du måste göra för alla `eVar`, `prop`, `event`, eller variabel som är tillgänglig via bearbetningsregler.

1. Gå till Analytics-gränssnittet
1. Gå till [!UICONTROL Admin] > [!UICONTROL Admin Tools] > [!UICONTROL Report Suites]
1. Välj den rapport för utveckling/test som du använder för självstudiekursen > [!UICONTROL Edit Settings] > [!UICONTROL General] > [!UICONTROL Processing Rules]

   ![Köp av analyser](assets/analytics-process-rules.png)

1. Skapa en regel till **[!UICONTROL Overwrite value of]** `[!UICONTROL Product SKU (prop1)]` till `a.x.productlistitems.0.sku`. Kom ihåg att lägga till en anteckning om varför du skapar regeln och namnge regeltiteln. Välj **[!UICONTROL Save]**

   ![Köp av analyser](assets/analytics-set-processing-rule.png)

   >[!IMPORTANT]
   >
   >Första gången du mappar till en bearbetningsregel visas inte kontextdatavariablerna från XDM-objektet. Om du vill åtgärda det väljer du ett värde, Spara och återgå till att redigera. Alla XDM-variabler ska nu visas.

### Mappa till analysvariabler i XDM-schemat

Ett alternativ till bearbetningsregler är att mappa till Analytics-variabler i XDM-schemat med hjälp av `Adobe Analytics ExperienceEvent Template` fältgrupp. Detta tillvägagångssätt har blivit populärt eftersom många användare tycker att det är enklare än att konfigurera bearbetningsregler, men om du ökar storleken på XDM-nyttolasten kan det i sin tur öka profilstorleken i andra program som Real-Time CDP.

Lägg till `Adobe Analytics ExperienceEvent Template` fältgrupp till ditt schema:

1. Öppna [Datainsamling](https://experience.adobe.com/#/data-collection){target="blank"} gränssnitt
1. Välj **[!UICONTROL Schemas]** från vänster navigering
1. Se till att du är i sandlådan som du använder från självstudiekursen
1. Öppna `Luma Web Event Data` schema
1. I **[!UICONTROL Field Groups]** avsnitt, markera **[!UICONTROL Add]**
1. Hitta `Adobe Analytics ExperienceEvent Template` fältgrupp och lägg till den i ditt schema


Ange nu en eVar för varuexponering i produktsträngen. Med `Adobe Analytics ExperienceEvent Template` kan du mappa variabler till marknadsföring av eVars eller händelser i produktsträngen. Detta kallas även inställning **Produktsyntaxmarknadsföring**.

1. Gå tillbaka till taggegenskapen

1. Öppna regeln `ecommerce - library loaded - set product details variables - 20`

1. Öppna **[!UICONTROL Set Variable]** åtgärd

1. Markera för att öppna `_experience > analytics > customDimensions > eVars > eVar1`

1. Ange **[!UICONTROL Value]** till `%product.productInfo.title%`

1. Välj **[!UICONTROL Keep Changes]**

   ![Produktens SKU XDM-objektsvariabel](assets/set-up-analytics-product-merchandising.png)

1. Välj **[!UICONTROL Save]** för att spara regeln

Som du just såg kan i stort sett alla Analytics-variabler anges i `Adobe Analytics ExperienceEvent Template` fältgrupp.

>[!NOTE]
>
> Lägg märke till `_experience` objekt under `productListItems` > `Item 1`. Ange alla variabler under den här [!UICONTROL object] anger produktsyntaxen eVars eller Events.


### Skicka data till en annan rapportserie

Du kanske vill ändra vilka data i Adobe Analytics rapportserie som skickas till när besökarna finns på vissa sidor. Detta kräver en konfiguration i både datastream och en regel.

#### Konfigurera en åsidosättning av ett datastream-rapportpaket

Så här konfigurerar du en åsidosättningsinställning för Adobe Analytics-rapportsviten i datastream:

1. Öppna ditt datastream
1. Redigera **[!UICONTROL Adobe Analytics]** genom att öppna ![mer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) och sedan välja **[!UICONTROL Edit]**

   ![Skriv över datastream](assets/datastream-edit-analytics.png)

1. Välj **[!UICONTROL Advance Options]** att öppna **[!UICONTROL Report Suite Overrides]**

1. Markera de rapportsviter som du vill åsidosätta. I detta fall `Web SDK Course Dev` och `Web SDK Course Stg`

1. Välj Spara

   ![Skriv över datastream](assets/analytics-datastreams-edit-adobe-analytics-configurations-report-suites.png)


#### Skicka en sidvy till en annan rapportserie med åsidosättning av datastream

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

1. Som **[!UICONTROL XDM data]** väljer du `xdm.variable.content` du skapade i [Skapa dataelement](create-data-elements.md) lektion

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

## Validera Adobe Analytics for Platform Web SDK

I [Felsökning](validate-with-debugger.md) i lektionen lärde du dig att inspektera XDM-begäran på klientsidan med plattformsfelsökaren och webbläsarutvecklarkonsolen, som liknar hur du felsöker en `AppMeasurement.js` Implementering av analyser. Du har också lärt dig att validera begäranden på serversidan för Platform Edge Network som skickas till Adobe-program och hur du visar en fullt bearbetad nyttolast med hjälp av Assurance.

För att validera att Analytics hämtar in data korrekt via Experience Platform Web SDK måste du gå två steg längre:

1. Validera hur data bearbetas av XDM-objektet på Platform Edge Network med hjälp av funktionen Edge Trace i Experience Platform-felsökaren
1. Validera hur data behandlas av Analytics med bearbetningsregler och realtidsrapporter
1. Validera hur data bearbetas fullt ut av Analytics med Adobe Experience Platform Assurance

### Använd kantkalkering

Lär dig hur du validerar att Adobe Analytics spelar in ECID, sidvisningar, produktsträngen och e-handelshändelser med Edge Trace-funktionen i felsökaren för Experience Platform.

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

### Åsidosättningar av rapporteringsprogramsvit

Ovanför du konfigurerade en åsidosättning av datastream för [Lumas hemsida](https://luma.enablementadobe.com/content/luma/us/en.html).  Validera konfigurationen

1. Leta efter en rad med **[!UICONTROL Datastream config after override was applied]**. Här hittar du den primära rapportsviten och de extra rapportsviterna som har konfigurerats för åsidosättningar av rapportsviten.

   ![Verifiering av åsidosättningslista för Analytics-rapportsviten](assets/aep-debugger-datastream-override.png)

1. Bläddra nedåt till raden som börjar med **[!UICONTROL Analytics Automatic Mapping]**  och verifiera att `[!UICONTROL reportSuiteIds]` visar rapportsviten som du angav i dina åsidosättningskonfigurationer

   ![Analytics Report Suite Override Call Validation](assets/aep-debugger-analytics-report-suite-override.png)

### Vyer av innehållssidor

Gå till en produktsida som [Didi Sport Watch produktsida](https://luma.enablementadobe.com/content/luma/us/en/products/gear/watches/didi-sport-watch.html#24-WG02).  Verifiera att innehållssidvisningar hämtas av Analytics.

1. Leta efter `[!UICONTROL c.a.x.web.webpagedetails.pageviews.value]=1`.
1. Bläddra nedåt för att se `[!UICONTROL gn]` variabel. Det är den dynamiska syntaxen i Analytics för `[!UICONTROL s.pageName]` variabel. Det hämtar sidnamnet från datalagret.

   ![Produktsträng för Analytics](assets/analytics-debugger-edge-page-view.png)

### Produktsträng och e-handelshändelser

Eftersom du redan är på en produktsida fortsätter den här övningen att använda samma Edge Trace för att validera att produktdata hämtas av Analytics. Både produktsträngen och e-handelshändelserna mappas automatiskt XDM-variabler till Analytics. Så länge du har mappat till rätt `productListItem` XDM-variabeln while [konfigurera ett XDM-schema för Adobe Analytics](setup-analytics.md#configure-an-xdm-schema-for-adobe-analytics)tar Platform Edge Network hand om att mappa data till rätt analysvariabler.

**Verifiera först att `Product String` är inställt**

1. Leta efter `[!UICONTROL c.a.x.productlistitems.][0].[!UICONTROL sku]`. Variabeln hämtar det dataelementvärde som du har mappat till `productListItems.item1.sku` tidigare i den här lektionen
1. Sök även efter `[!UICONTROL c.a.x.productlistitems.][0].[!UICONTROL _experience.analytics.customdimensions.evars.evar1]`. Variabeln hämtar det dataelementvärde som du har mappat till `productListItems.item1._experience.analytics.customdimensions.evars.evar1`
1. Bläddra nedåt för att se `[!UICONTROL pl]` variabel. Det är den dynamiska syntaxen för produktsträngvariabeln Analytics
1. Observera att produktnamnet från datalagret mappas både till `[!UICONTROL c.a.x.productlistitems.][0].[!UICONTROL sku]` och `[!UICONTROL product]` -parametern i produktsträngen.  Dessutom mappas produkttiteln från datalagret till merchandising evar1 i produktsträngen.

   ![Produktsträng för Analytics](assets/analytics-debugger-prodstring.png)

   Edge Trace behandlar `commerce` händelser något annorlunda än `productList` dimensioner. Du ser inte att en kontextdatavariabel är mappad på samma sätt som du ser produktnamnet mappat till `[!UICONTROL c.a.x.productlistitem.[0].name]` ovan. I stället visar Edge Trace den slutliga automatiska händelsemappningen i Analytics `event` variabel. Platform Edge Network mappar det så länge du mappar till rätt XDM `commerce` variabel while [konfigurera schema för Adobe Analytics](setup-analytics.md#configure-an-xdm-schema-for-adobe-analytics); i detta fall `commerce.productViews.value=1`.

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



## Validera Adobe Analytics med Adobe Experience Platform Assurance

Adobe Experience Platform Assurance är en produkt från Adobe Experience Cloud som hjälper er att inspektera, bevisa, simulera och validera hur ni samlar in data eller levererar upplevelser via er webbplats och mobilapplikation.

Ovanför du har verifierat att Adobe Analytics spelar in ECID, sidvisningar, produktsträngen och e-handelshändelser med Edge Trace-funktionen i felsökaren för Experience Platform.  Du validerade också den mappningen av prop1 med bearbetningsregler och realtidsrapporter.  Sedan validerar du dessa händelser med Adobe Experience Platform Assurance.

>[!NOTE]
>
>För att validera dina Adobe Analytics-data med Adobe Experience Platform Assurance måste du [Aktivera användaråtkomst till Adobe Experience Platform Assurance](https://experienceleague.adobe.com/docs/experience-platform/assurance/user-access.html)

### Öppna Adobe Experience Platform Assurance

Det finns flera sätt att få åtkomst till Assurance:

1. Via Adobe Experience Platform
1. Via Adobe Experience Platform Data Collection
1. Via loggar i Adobe Experience Platform Debugger (rekommenderas)

Bläddra nedåt och välj för att få åtkomst till försäkringen via Adobe Experience Platform **[!UICONTROL Assurance]** till vänster på den räls som finns under **[!UICONTROL DATA COLLECTION]**.  Välj **[!UICONTROL "Web SDK Tutorial 3"]** -session för att komma åt händelser som genererats i föregående avsnitt.
![Säkerhet via Adobe Experience Platform](assets/assurance-open-aep.png)

Om du vill få åtkomst till försäkringen via Adobe Experience Platform Data Collection väljer du **[!UICONTROL Assurance]** till vänster på den räls som finns under **[!UICONTROL DATA COLLECTION]**.  Välj **[!UICONTROL "Web SDK Tutorial 3"]** -session för att komma åt händelser som genererats i föregående avsnitt.\
![Säkerhet genom Adobe Experience Platform Data Collection](assets/assurance-open-data-collection.png)

Gå till Felsökning för Experience Platform i det vänstra navigeringsfältet för att få åtkomst till försäkringen via Adobe Experience Platform Debugger **[!UICONTROL Logs]** väljer du **[!UICONTROL Edge]** och markera **[!UICONTROL Connect]**.  När anslutningen till Edge Network är upprättad väljer du den externa länkikonen. Vi rekommenderar att du får åtkomst till Assurance via Felsökning eftersom webbsessioner för närvarande måste startas från Felsökning.
![Säkerhet genom Adobe Experience Platform Data Collection](assets/assurance-open-aep-debugger.png)

I **[!UICONTROL "Web SDK Tutorial 3"]** Anmäl session **[!UICONTROL "hitdebugger"]** i sökfältet Händelser för att filtrera resultaten till data som skickats efter bearbetning i Adobe Analytics.
![Adobe-analys för Assurance-efterbearbetade data](assets/assurance-hitdebugger.png)

### Experience Cloud ID-validering med Assurance

Om du vill validera att Adobe Analytics hämtar ECID-numret markerar du en fyr och öppnar nyttolasten.  Leverantören för denna fyr ska vara **[!UICONTROL com.adobe.analytics.hitdebugger]**
![Adobe Analytics validation with Assurance](assets/assurance-hitdebugger-payload.png)

Bläddra sedan nedåt till **[!UICONTROL mcvisId]** för att validera att ECID-numret är korrekt inhämtat
![Experience Cloud ID-validering med Assurance](assets/assurance-hitdebugger-mcvisId.png)

### Validering av vyerna på innehållssidan med Assurance

Använd samma fyr för att kontrollera att vyerna för innehållssidor är mappade till rätt Adobe Analytics-variabel.
Bläddra nedåt till **[!UICONTROL pageName]** för att validera att `Page Name` är korrekt infångad
![Validering av sidnamn med Assurance](assets/assurance-hitdebugger-content-pagename.png)

### Produktsträng och validering av e-handelshändelser med Assurance

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
>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Web SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela med dig av dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
