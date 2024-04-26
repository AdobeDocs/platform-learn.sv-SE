---
title: Skapa taggregler
description: Lär dig hur du skickar en händelse till Platform Edge Network med ditt XDM-objekt med hjälp av en taggregel. Den här lektionen ingår i självstudiekursen Implementera Adobe Experience Cloud med Web SDK.
feature: Tags
exl-id: e06bad06-3ee3-475f-9b10-f0825a48a312
source-git-commit: 78df0fb4e2f2b56b829c54c08a16f860192592d1
workflow-type: tm+mt
source-wordcount: '1745'
ht-degree: 0%

---

# Skapa taggregler

Lär dig hur du skickar händelser till Platform Edge Network med ditt XDM-objekt med hjälp av taggregler. En taggregel är en kombination av händelser, villkor och åtgärder som instruerar taggegenskapen att göra något. Med Platform Web SDK används regler för att skicka händelser till Platform Edge Network med rätt data.

## Utbildningsmål

När lektionen är slut kan du:

* Använd en namnkonvention för att hantera regler i taggar
* Skicka en händelse med XDM-fält med åtgärderna Uppdatera variabel och Skicka händelse
* Stapla flera uppsättningar XDM-fält över flera regler
* Mappa enskilda eller hela arraydataelement till XDM-objektet
* Publicera en taggregel i ett utvecklingsbibliotek


## Förutsättningar

Du känner till datainsamlingstaggar och [Luma demo site](https://luma.enablementadobe.com/content/luma/us/en.html) och har avslutat tidigare lektioner i självstudiekursen:

* [Konfigurera ett XDM-schema](configure-schemas.md)
* [Konfigurera ett identitetsnamnutrymme](configure-identities.md)
* [Konfigurera ett datastream](configure-datastream.md)
* [Installera SDK-tillägg för webben](install-web-sdk.md)
* [Skapa dataelement](create-data-elements.md)
* [Skapa identiteter](create-identities.md)

## Namnkonventioner

Om du vill hantera regler i taggar bättre bör du följa en standardnamnkonvention. I den här självstudiekursen används en namnkonvention med fem delar:

* [**plats**] - [**event**] - [**syfte**] - [**beställa**]

där

1. **plats** är den eller de sidor på webbplatsen där regeln utlöses
1. **event** är utlösaren för regeln
1. **syfte** är huvudåtgärden som utförs av regeln
1. **beställa** är den ordning i vilken regeln ska utlösas i förhållande till andra regler
<!-- minor update -->

## Skapa taggregler

I taggar används regler för att utföra åtgärder (brandanrop) under olika förhållanden. Tillägget Platform Web SDK-taggar innehåller två åtgärder som kommer att användas i den här lektionen:

* **[!UICONTROL Update variable]** mappar dataelement till egenskaper i ett XDM-objekt
* **[!UICONTROL Send Event]** skickar XDM-objektet till Experience Platform Edge Network

I resten av lektionen:

1. Skapa en regel med **[!UICONTROL Update variable]** åtgärd för att definiera en&quot;global konfiguration&quot; av XDM-fält.

1. Skapa ytterligare regler med **[!UICONTROL Update variable]** åtgärd som åsidosätter vår&quot;globala konfiguration&quot; och bidrar till ytterligare XDM-fält under vissa förhållanden (t.ex. genom att lägga till produktinformation på produktsidor).

1. Skapa en annan regel med **[!UICONTROL Send Event]** som skickar hela XDM-objektet till Adobe Experience Platform Edge Network.

Alla dessa regler kommer att ordnas korrekt med hjälp av[!UICONTROL order]&quot;.

Den här videon ger en översikt över processen:

>[!VIDEO](https://video.tv.adobe.com/v/3427710/?learn=on)

### Globala konfigurationsfält

Så här skapar du en taggregel för de globala XDM-fälten:

1. Öppna taggegenskapen som du använder för den här självstudien

1. Gå till **[!UICONTROL Rules]** till vänster navigering

1. Välj **[!UICONTROL Create New Rule]** knapp

   ![Skapa en regel](assets/rules-create.png)

1. Namnge regeln `all pages - library loaded - set global variables - 1`

1. I **[!UICONTROL Events]** avsnitt, markera **[!UICONTROL Add]**

   ![Namnge regeln och lägg till en händelse](assets/rule-name-new.png)

1. Använd **[!UICONTROL Core Extension]** och markera **[!UICONTROL Library Loaded (Page Top)]** som **[!UICONTROL Event Type]**

1. Välj **[!UICONTROL Advanced]** listruta och ange `1` som **[!UICONTROL Order]**

   >[!NOTE]
   >
   > Ju lägre ordernummer, desto tidigare körs det. Därför ger vi vår&quot;globala konfiguration&quot; ett lågt ordernummer.

1. Välj **[!UICONTROL Keep Changes]** för att återgå till huvudlinjeraster
   ![Välj utlösare för inläst bibliotek](assets/create-tag-rule-trigger-loaded.png)

1. I **[!UICONTROL Actions]** avsnitt, markera **[!UICONTROL Add]**

1. Som **[!UICONTROL Extension]**, markera **[!UICONTROL Adobe Experience Platform Web SDK]**

1. Som **[!UICONTROL Action Type]**, markera **[!UICONTROL Update variable]**

1. Som **[!UICONTROL Data element]** väljer du `xdm.variable.content` du skapade i [Skapa dataelement](create-data-elements.md) lektion

   ![Uppdatera variabelschema](assets/create-rule-update-variable.png)

Kartlägg dina [!UICONTROL data elements] till [!UICONTROL schema] används av ditt XDM-objekt. Du kan mappa till enskilda egenskaper eller hela objekt. I det här exemplet mappar du till enskilda egenskaper:

1. Sök efter fältet eventType och markera det

1. Ange värdet `web.webpagedetails.pageViews`

   >[!TIP]
   >
   > Så här förstår du vilka värden som ska fyllas i `eventType` måste du gå till schemasidan och välja `eventType` om du vill visa de föreslagna värdena på den högra listen. Du kan också ange ett nytt värde om det behövs.
   > ![eventType föreslagna värden på schemasidan](assets/create-tag-rule-eventType.png)

1. Gå till `identityMap` objekt i schemat och markera det

1. Mappa till `identityMap.loginID` dataelement

   ![Uppdatera variabelidentitetskarta](assets/create-rule-variable-identityMap.png)


   >[!TIP]
   >
   > XDM-fält inkluderas inte i nätverksbegäran om dataelementet är null. Därför gäller att när användaren inte är autentiserad och `identityMap.loginID` dataelementet är null, `identityMap` kommer inte att skickas. Därför kan vi definiera den i vår&quot;globala konfiguration&quot;.

1. Bläddra nedåt tills du når **`web`** object

1. Markera för att öppna den

1. Mappa följande dataelement till motsvarande `web` XDM-variabler

   * **`web.webPageDetials.name`** till `%page.pageInfo.pageName%`
   * **`web.webPageDetials.server`** till `%page.pageInfo.server%`
   * **`web.webPageDetials.siteSection`** till `%page.pageInfo.hierarchie1%`

1. Ange `web.webPageDetials.pageViews.value` till `1`

   ![Uppdatera variabelinnehåll](assets/create-rule-xdm-variable-content.png)

   >[!TIP]
   >
   > Medan ingen `eventType` ange till `web.webpagedetails.pageViews` eller `web.webPageDetails.pageViews.value` krävs för att Adobe Analytics ska kunna bearbeta en fyr som en sidvy är det praktiskt att ha ett standardsätt att indikera en sidvy för andra program i senare led.


1. Välj **[!UICONTROL Keep Changes]** och sedan **[!UICONTROL Save]** regeln på nästa skärm för att slutföra skapandet av regeln


### Produktsidesfält

Börja använda nu **[!UICONTROL Update variable]** i ytterligare sekvensregler för att berika XDM-objektet innan det skickas till [!UICONTROL Platform Edge Network].

>[!TIP]
>
>Regelordningen bestämmer vilken regel som körs först när en händelse utlöses. Om två regler har samma händelsetyp körs den med det lägsta talet först.
> 
>![rule-order](assets/set-up-analytics-sequencing.png)

Börja med att spåra produktvyer på Lumas produktinformationssida:

1. Välj **[!UICONTROL Add Rule]**
1. Ge den ett namn  [!UICONTROL `ecommerce - library loaded - set product details variables - 20`]
1. Välj ![+ symbol](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) under Händelse för att lägga till en ny utlösare
1. Under **[!UICONTROL Extension]**, markera **[!UICONTROL Core]**
1. Under **[!UICONTROL Event Type]**, markera **[!UICONTROL Library Loaded (Page Top)]**
1. Markera för att öppna **[!UICONTROL Advanced Options]**, skriva in `20`. Detta garanterar att regeln körs efter `all pages - library loaded - set global variables - 1` som anger den globala konfigurationen.

   ![XDM-regler för analyser](assets/set-up-analytics-pdp.png)

1. Under **[!UICONTROL Conditions]**, välj **[!UICONTROL Add]**
1. Lämna **[!UICONTROL Logic Type]** as **[!UICONTROL Regular]**
1. Lämna **[!UICONTROL Extension]** as **[!UICONTROL Core]**
1. Välj **[!UICONTROL Condition Type]** as **[!UICONTROL Path Without Query String]**
1. Till höger aktiverar du **[!UICONTROL Regex]** växla
1. Under **[!UICONTROL path equals]** set `/products/`. För demonstrationswebbplatsen Luma säkerställer den att regeln endast aktiveras på produktsidor
1. Välj **[!UICONTROL Keep Changes]**

   ![XDM-regler för analyser](assets/set-up-analytics-product-condition.png)

1. Under **[!UICONTROL Actions]** välj **[!UICONTROL Add]**
1. Välj **[!UICONTROL Adobe Experience Platform Web SDK]** extension
1. Välj **[!UICONTROL Action Type]** as **[!UICONTROL Update variable]**
1. Bläddra nedåt till `commerce` object
1. Öppna **[!UICONTROL productViews]** objekt och ange **[!UICONTROL value]** till `1`

   ![konfigurera produktvy](assets/set-up-analytics-prodView.png)

   >[!TIP]
   >
   >Setting commerce.productViews.value=1 in XDM mappar automatiskt till `prodView` händelse i Analytics

1. Bläddra nedåt till `eventType` och ange `commerce.productViews`

   >[!NOTE]
   >
   >Eftersom den här regeln har en högre ordning skrivs den över `eventType` anges i regeln &quot;global konfiguration&quot;. `eventType` kan bara innehålla ett värde, och vi rekommenderar att du ställer in det med händelsen för det högsta värdet.

1. Bläddra nedåt till och markera `productListItems` array
1. Välj **[!UICONTROL Provide individual items]**
1. Välj **[!UICONTROL Add Item]**

   ![Anger produktvisningshändelse](assets/set-up-analytics-xdm-individual.png)

   >[!CAUTION]
   >
   >The **`productListItems`** är en `array` datatyp så att data förväntas komma in som en samling element. På grund av Luma-demonstrationswebbplatsens datalagerstruktur och eftersom det bara är möjligt att visa en produkt i taget på Luma-webbplatsen, lägger du till objekt individuellt. När du implementerar på din egen webbplats, beroende på din datalagerstruktur, kanske du kan tillhandahålla en hel array.

1. Markera för att öppna **[!UICONTROL Item 1]**
1. Karta **`productListItems.item1.SKU`** till `%product.productInfo.sku%`

   ![Produktens SKU XDM-objektsvariabel](assets/set-up-analytics-sku.png)

1. Välj **[!UICONTROL Keep Changes]**

1. Välj **[!UICONTROL Save]** för att spara regeln


### Kundvagnsfält

Du kan mappa hela arrayen till ett XDM-objekt, förutsatt att arrayen matchar formatet för XDM-schemat. Elementet med anpassade koddata `cart.productInfo` du skapade tidigare slingor genom `digitalData.cart.cartEntries` datalagerobjekt på Luma och översätter det till det format som krävs för `productListItems` XDM-schemats objekt.

Se jämförelsen nedan av Luma-webbplatsens datalager (vänster) till det översatta dataelementet (höger) för att illustrera:

![XDM-objektmatrisformat](assets/data-element-xdm-array.png)

Jämför dataelementet med `productListItems` struktur (tips, det ska matcha).

>[!IMPORTANT]
>
>Observera hur numeriska variabler översätts, med strängvärden i datalagret som `price` och `qty` formateras om till tal i dataelementet. Dessa formatkrav är viktiga för dataintegriteten i plattformar och fastställs under [konfigurera scheman](configure-schemas.md) steg. I exemplet **[!UICONTROL quantity]** använder **[!UICONTROL Integer]** datatyp.
> ![XDM-schemadatatyp](assets/set-up-analytics-quantity-integer.png)

Låt oss mappa vår array till XDM-objektet:


1. Skapa en ny regel med namnet `ecommerce - library loaded - set shopping cart variables - 20`
1. Välj ![+ symbol](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) under Händelse för att lägga till en ny utlösare
1. Under **[!UICONTROL Extension]**, markera **[!UICONTROL Core]**
1. Under **[!UICONTROL Event Type]**, markera **[!UICONTROL Library Loaded (Page Top)]**
1. Markera för att öppna **[!UICONTROL Advanced Options]**, skriva in `20`
1. Välj **[!UICONTROL Keep Changes]**

   ![XDM-regler för analyser](assets/set-up-analytics-cart-sequence.png)

1. Under **[!UICONTROL Conditions]**, välj **[!UICONTROL Add]**
1. Lämna **[!UICONTROL Logic Type]** as **[!UICONTROL Regular]**
1. Lämna **[!UICONTROL Extensions]** as **[!UICONTROL Core]**
1. Välj **[!UICONTROL Condition Type]** as **[!UICONTROL Path Without Query String]**
1. Till höger, **inte** aktivera **[!UICONTROL Regex]** växla
1. Under **[!UICONTROL path equals]** set `/content/luma/us/en/user/cart.html`. För Luma demo-webbplatsen säkerställer det att regeln endast aktiveras på kundvagnssidan
1. Välj **[!UICONTROL Keep Changes]**

   ![XDM-regler för analyser](assets/set-up-analytics-cart-condition.png)

1. Under **[!UICONTROL Actions]** välj **[!UICONTROL Add]**
1. Välj **[!UICONTROL Adobe Experience Platform Web SDK]** extension
1. Välj **[!UICONTROL Action Type]** as **[!UICONTROL Update variable]**
1. Bläddra nedåt till `commerce` och väljer att öppna det.
1. Öppna **[!UICONTROL productListViews]** objekt och ange **[!UICONTROL value]** till `1`

   ![konfigurera produktvy](assets/set-up-analytics-cart-view.png)

   >[!TIP]
   >
   >Setting commerce.productListViews.value=1 in XDM mappar automatiskt till `scView` händelse i Analytics

1. Välj `eventType` och ange till `commerce.productListViews`

1. Bläddra nedåt till och markera **[!UICONTROL productListItems]** array

1. Välj **[!UICONTROL Provide entire array]**

1. Mappa till **`cart.productInfo`** dataelement

1. Välj **[!UICONTROL Keep Changes]**

1. Välj **[!UICONTROL Save]** för att spara regeln

Skapa ytterligare två regler för utcheckning och köp enligt samma mönster med skillnaderna nedan:

**Regelnamn**: `ecommerce  - library loaded - set checkout variables - 20`

1. **[!UICONTROL Condition]**: /content/luma/us/en/user/checkout.html
1. Ange `eventType` till `commerce.checkouts`
1. Ange `commerce.checkout.value` till `1`

   >[!TIP]
   >
   >Det här motsvarar inställningen `scCheckout` händelse i Analytics


**Regelnamn**: `ecommerce - library loaded - set purchase variables -  20`

1. **[!UICONTROL Condition]**: /content/luma/us/en/user/checkout/order/thank-you.html
1. Ange `eventType` till `commerce.purchases`
1. Ange `commerce.purchases.value` till `1`

   >[!TIP]
   >
   >Det här motsvarar inställningen `purchase` händelse i Analytics

1. Ange `commerce.order.purchaseID` till `cart.orderId` dataelement
1. Ange `commerce.order.currencyCode` till hårdkodat värde `USD`

   ![Ange purchaseID för Analytics](assets/set-up-analytics-purchase.png)

   >[!TIP]
   >
   >Det här motsvarar inställningen `s.purchaseID` och `s.currencyCode` variabler i Analytics

1. Bläddra nedåt till och markera **[!UICONTROL productListItems]** array
1. Välj **[!UICONTROL Provide entire array]**
1. Mappa till **`cart.productInfo.purchase`** dataelement
1. Välj **[!UICONTROL Save]**

När du är klar bör du se följande regler som skapats.

![XDM-regler för analyser](assets/set-up-analytics-rules.png)


### Skicka händelseregel

Nu när du har ställt in variablerna kan du skapa en regel som skickar hela XDM-objektet till Platform Edge Network med **[!UICONTROL Send event]** åtgärd.

1. Välj till höger **[!UICONTROL Add Rule]** för att skapa en annan regel

1. Namnge regeln `all pages - library loaded - send event - 50`

1. I **[!UICONTROL Events]** avsnitt, markera **[!UICONTROL Add]**

1. Använd **[!UICONTROL Core Extension]** och markera `Library Loaded (Page Top)` som **[!UICONTROL Event Type]**

1. Välj **[!UICONTROL Advanced]** listruta och ange `50` in **[!UICONTROL Order]**. Detta garanterar att den andra regeln aktiveras efter den första regeln som du anger som utlösare `1`.

1. Välj **[!UICONTROL Keep Changes]** för att återgå till huvudlinjeraster
   ![Välj utlösare för inläst bibliotek](assets/create-tag-rule-trigger-loaded-send.png)

1. I **[!UICONTROL Actions]** avsnitt, markera **[!UICONTROL Add]**

1. Som **[!UICONTROL Extension]**, markera  **[!UICONTROL Adobe Experience Platform Web SDK]**

1. Som  **[!UICONTROL Action Type]**, markera  **[!UICONTROL Send event]**

1. Som **[!UICONTROL XDM]** väljer du `xdm.variable.content` dataelement som skapades i föregående lektion

1. Välj **[!UICONTROL Keep Changes]** för att återgå till huvudlinjeraster

   ![Lägg till åtgärden Skicka händelse](assets/create-rule-send-event-action.png)
1. Välj **[!UICONTROL Save]** för att spara regeln

   ![Spara regeln](assets/create-rule-save-rule.png)

## Publicera regeln i ett bibliotek

Publicera sedan regeln i utvecklingsmiljön så att du kan verifiera att den fungerar.

Så här skapar du ett bibliotek:

1. Gå till **[!UICONTROL Publishing Flow]** till vänster navigering

1. Välj **[!UICONTROL Add Library]**

   ![Välj Lägg till bibliotek](assets/rule-publish-library.png)
1. För **[!UICONTROL Name]**, ange `Luma Web SDK Tutorial`
1. För **[!UICONTROL Environment]**, markera `Development`
1. Välj  **[!UICONTROL Add All Changed Resources]**

   >[!NOTE]
   >
   >    Du bör se alla taggkomponenter som har skapats i tidigare lektioner. Tillägget Core innehåller det grundläggande JavaScript som krävs för alla egenskaper för webbtaggar.

1. Välj **[!UICONTROL Save & Build for Development]**

   ![Skapa och bygg biblioteket](assets/create-tag-rule-library-changes.png)

Det kan ta några minuter att skapa biblioteket och när det är klart visas en grön punkt till vänster om biblioteksnamnet:

![Bygget är klart](assets/create-rule-development-success.png)

Som du kan se på [!UICONTROL Publishing Flow] på skärmen finns det mycket mer i publiceringsprocessen som ligger utanför kursen. I den här självstudiekursen används bara ett bibliotek i din utvecklingsmiljö.

Nu kan du validera data i begäran med Adobe Experience Platform Debugger.

[Nästa ](validate-with-debugger.md)

>[!NOTE]
>
>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Web SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela med dig av dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
