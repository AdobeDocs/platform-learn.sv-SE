---
title: Skapa en taggregel
description: Lär dig hur du skickar en händelse till Platform Edge Network med ditt XDM-objekt med hjälp av en taggregel. Den här lektionen ingår i självstudiekursen Implementera Adobe Experience Cloud med Web SDK.
feature: Tags
source-git-commit: f08866de1bd6ede50bda1e5f8db6dbd2951aa872
workflow-type: tm+mt
source-wordcount: '1153'
ht-degree: 0%

---

# Skapa en taggregel

Lär dig hur du skickar en händelse till Platform Edge Network med ditt XDM-objekt med hjälp av en taggregel. En taggregel är en kombination av händelser, villkor och åtgärder som instruerar taggegenskapen att göra något.

>[!NOTE]
>
> I demonstrationssyfte bygger övningarna i den här lektionen på det exempel som användes under [Skapa identiteter](create-identities.md) steg; skicka en XDM-händelseåtgärd för att hämta innehåll och identiteter från användare på [Luma demo site](https://luma.enablementadobe.com/content/luma/us/en.html).


## Utbildningsmål

När lektionen är slut kan du:

* Använd en namnkonvention för att hantera regler i taggar
* Skicka en XDM-händelse genom att använda åtgärdstyperna Uppdatera variabel och Skicka händelse i en taggregel
* Publicera en taggregel i ett utvecklingsbibliotek


## Förutsättningar

Du känner till datainsamlingstaggar och [Luma demo site](https://luma.enablementadobe.com/content/luma/us/en.html)och du måste ha slutfört följande lektioner i självstudiekursen:

* [Konfigurera ett XDM-schema](configure-schemas.md)
* [Konfigurera ett identitetsnamnutrymme](configure-identities.md)
* [Konfigurera ett datastream](configure-datastream.md)
* [Web SDK-tillägget är installerat i taggegenskapen](install-web-sdk.md)
* [Skapa dataelement](create-data-elements.md)
* [Skapa identiteter](create-identities.md)

## Namnkonventioner

Om du vill hantera regler i taggar bättre bör du följa en standardnamnkonvention. I den här självstudiekursen används en namnkonvention med tre delar:

* [**plats**] - [**event**] - [**verktyg**] (**sekvens**)

där

1. **plats** är den eller de sidor på webbplatsen där regeln utlöses
1. **event** är utlösaren för regeln
1. **verktyg** är det eller de program som används i åtgärdssteget för den regeln
1. **sekvens** är den ordning i vilken regeln ska utlösas i förhållande till andra regler
<!-- minor update -->

## Skapa taggregel

I taggar används regler för att utföra åtgärder (brandanrop) under olika förhållanden. Tillägget Platform Web SDK-taggar innehåller två åtgärder som kommer att användas i den här lektionen:

* **[!UICONTROL Uppdatera variabel]** mappar dataelement till XDM-fält
* **[!UICONTROL Skicka händelse]** skickar XDM-objektet till Experience Platform Edge Network

### Uppdatera variabel

Skapa den här första regeln som en&quot;global konfiguration&quot; för att ställa in alla viktiga innehållsvariabler i XDM-objektet med plattformens Web SDK:er **[!UICONTROL Uppdatera variabel]** åtgärd. Skapa sedan en andra regel, sekvenserad för att aktiveras efter den första, och skicka XDM-objektet till Platform Edge Network med **[!UICONTROL Skicka händelse]** åtgärd. Senare i den här självstudiekursen skickar du olika XDM-fält baserat på vilken typ av sida besökaren är på (till exempel produktartiklar på produktsidor). Du uppnår detta genom att sekvensera reglerna som innehåller **[!UICONTROL Uppdatera variabel]** åtgärder före regeln som använder **[!UICONTROL Skicka händelse]** åtgärd.

Så här skapar du en taggregel:

1. Öppna taggegenskapen som du använder för den här självstudien

1. Gå till **[!UICONTROL Regler]** till vänster navigering

1. Välj **[!UICONTROL Skapa ny regel]** knapp

   ![Skapa en regel](assets/rules-create.png)

1. Namnge regeln `all pages global content variables - page bottom - AA (order 1)`

1. I **[!UICONTROL Händelser]** avsnitt, markera **[!UICONTROL Lägg till]**

   ![Namnge regeln och lägg till en händelse](assets/rule-name-new.png)

1. Använd **[!UICONTROL Kärntillägg]** och markera `Page Bottom` som **[!UICONTROL Händelsetyp]**

1. Under **[!UICONTROL Namn]** field, name it `Core - Page Bottom - order 1`. Detta hjälper dig att beskriva utlösaren med ett beskrivande namn.

1. Välj **[!UICONTROL Avancerat]** listruta och ange `1` in **[!UICONTROL Beställning]**

   >[!NOTE]
   >
   > Ju högre tal du anger, desto senare i den övergripande ordningen för de åtgärder som utlöses.

1. Välj **[!UICONTROL Behåll ändringar]** för att återgå till huvudlinjeraster
   ![Välj utlösare för sidan längst ned](assets/create-tag-rule-trigger-bottom.png)

1. I **[!UICONTROL Åtgärder]** avsnitt, markera **[!UICONTROL Lägg till]**

1. Som **[!UICONTROL Tillägg]**, markera **[!UICONTROL Adobe Experience Platform Web SDK]**

1. Som **[!UICONTROL Åtgärdstyp]**, markera **[!UICONTROL Uppdatera variabel]**

1. Som **[!UICONTROL Dataelement]** väljer du `xdm.variable.content` du skapade i [Skapa dataelement](create-data-elements.md) lektion

   ![Uppdatera variabelschema](assets/create-rule-update-variable.png)

Kartlägg dina [!UICONTROL dataelement] till [!UICONTROL schema] används av ditt XDM-objekt.

>[!NOTE]
> 
> Du kan mappa till enskilda egenskaper eller hela objekt. I det här exemplet mappar du till enskilda egenskaper.


1. Bläddra nedåt tills du når **`web`** object

1. Markera för att öppna den

1. Mappa följande dataelement till motsvarande `web` XDM-variabler

   * **`web.webPageDetials.name`** till `%page.pageInfo.pageName%`
   * **`web.webPageDetials.server`** till `%page.pageInfo.server%`
   * **`web.webPageDetials.siteSection`** till `%page.pageInfo.hierarchie1%`

   ![Uppdatera variabelinnehåll](assets/create-rule-xdm-variable-content.png)

1. Gå till `identityMap` objekt i schemat och markera det

1. Mappa till `identityMap.loginID` dataelement

   ![Uppdatera variabelidentitetskarta](assets/create-rule-variable-identityMap.png)

1. Leta reda på fältet eventType och markera det

1. Ange värdet `web.webpagedetails.pageViews`

   >[!WARNING]
   >
   > Den här listrutan fyller i **`xdm.eventType`** i XDM-objektet. Du kan även skriva frihandsetiketter i det här fältet, men vi rekommenderar att du **inte** som det har negativa effekter med Platform.

   >[!TIP]
   >
   > Så här förstår du vilka värden som ska fyllas i `eventType` måste du gå till schemasidan och välja `eventType` om du vill visa de föreslagna värdena på den högra listen.

   ![Uppdatera variabelidentitetskarta](assets/create-tag-rule-eventType.png)


1. Välj **[!UICONTROL Behåll ändringar]** och sedan **[!UICONTROL Spara]** regeln på nästa skärm för att slutföra skapandet av regeln

### Skicka händelse

Nu när du har angett variablerna kan du skapa den andra regeln som skickar XDM-objektet till Platform Edge Network med **[!UICONTROL Skicka händelse]** åtgärdstyp.

1. Till höger väljer du **[!UICONTROL Lägg till regel]** för att skapa en annan regel

1. Namnge regeln `all pages send event - page bottom - AA (order 50)`

1. I **[!UICONTROL Händelser]** avsnitt, markera **[!UICONTROL Lägg till]**

1. Använd **[!UICONTROL Kärntillägg]** och markera `Page Bottom` som **[!UICONTROL Händelsetyp]**

1. Under **[!UICONTROL Namn]** field, name it `Core - Page Bottom - order 50`. Detta hjälper dig att beskriva utlösaren med ett beskrivande namn.

1. Välj **[!UICONTROL Avancerat]** listruta och ange `50` in **[!UICONTROL Beställning]**. Detta garanterar att den andra regeln aktiveras efter den första regeln som du anger som utlösare `1`.

1. Välj **[!UICONTROL Behåll ändringar]** för att återgå till huvudlinjeraster
   ![Välj utlösare för sidan längst ned](assets/create-tag-rule-trigger-bottom-send.png)

1. I **[!UICONTROL Åtgärder]** avsnitt, markera **[!UICONTROL Lägg till]**

1. Som **[!UICONTROL Tillägg]**, markera  **[!UICONTROL Adobe Experience Platform Web SDK]**

1. Som  **[!UICONTROL Åtgärdstyp]**, markera  **[!UICONTROL Skicka händelse]**

1. Som **[!UICONTROL XML]** väljer du `xdm.variable.content` dataelement som skapades i föregående lektion

1. Välj **[!UICONTROL Behåll ändringar]** för att återgå till huvudlinjeraster

   ![Lägg till åtgärden Skicka händelse](assets/create-rule-send-event-action.png)
1. Välj **[!UICONTROL Spara]** för att spara regeln

   ![Spara regeln](assets/create-rule-save-rule.png)

## Publicera regeln i ett bibliotek

Publicera sedan regeln i utvecklingsmiljön så att du kan verifiera att den fungerar.

Så här skapar du ett bibliotek:

1. Gå till **[!UICONTROL Publiceringsflöde]** till vänster navigering

1. Välj **[!UICONTROL Lägg till bibliotek]**

   ![Välj Lägg till bibliotek](assets/rule-publish-library.png)
1. För **[!UICONTROL Namn]**, ange `Luma Web SDK Tutorial`
1. För **[!UICONTROL Miljö]**, markera `Development`
1. Välj  **[!UICONTROL Lägg till alla ändrade resurser]**

   >[!NOTE]
   >
   >    Förutom Adobe Experience Platform Web SDK och `all pages global content variables - page bottom - AA (order 50)` -regeln, du ser taggkomponenterna som skapades i tidigare lektioner. Tillägget Core innehåller det grundläggande JavaScript som krävs för alla egenskaper för webbtaggar.

1. Välj **[!UICONTROL Spara och bygg för utveckling]**

   ![Skapa och bygg biblioteket](assets/create-tag-rule-library-changes.png)

Det kan ta några minuter att skapa biblioteket och när det är klart visas en grön punkt till vänster om biblioteksnamnet:

![Bygget är klart](assets/create-rule-development-success.png)

Som du kan se på [!UICONTROL Publiceringsflöde] på skärmen finns det mycket mer i publiceringsprocessen som ligger utanför kursen. I den här självstudiekursen används bara ett bibliotek i din utvecklingsmiljö.

Nu kan du validera data i begäran med Adobe Experience Platform Debugger.

[Nästa ](validate-with-debugger.md)

>[!NOTE]
>
>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Web SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela med dig av dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
