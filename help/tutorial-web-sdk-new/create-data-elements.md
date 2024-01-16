---
title: Skapa dataelement
description: Lär dig hur du skapar ett XDM-objekt och mappar dataelement till det i taggar. Den här lektionen ingår i självstudiekursen Implementera Adobe Experience Cloud med Web SDK.
feature: Tags
source-git-commit: f08866de1bd6ede50bda1e5f8db6dbd2951aa872
workflow-type: tm+mt
source-wordcount: '1469'
ht-degree: 0%

---

# Skapa dataelement

Lär dig hur du skapar de grundläggande dataelement som behövs för att hämta in data med Experience Platform Web SDK. Samla in både innehåll- och identitetsdata på [Luma demo site](https://luma.enablementadobe.com/content/luma/us/en.html). Lär dig hur du använder XDM-schemat som du skapade tidigare för att samla in data med datatypen Variabel för Platform Web SDK.

>[!NOTE]
>
> I demonstrationssyfte bygger övningarna i den här lektionen på det exempel som används under [Konfigurera ett schema](configure-schemas.md) steg; skapa XDM-objekt som fångar innehåll som visas och identiteter för användare på [Luma demo site](https://luma.enablementadobe.com/content/luma/us/en.html).

>[!IMPORTANT]
>
>Informationen i den här lektionen kommer från `[!UICONTROL digitalData]` datalager på Luma-webbplatsen. Om du vill visa datalagret öppnar du utvecklarkonsolen och skriver in `[!UICONTROL digitalData]` för att se hela datalagret.![digitalt datalager](assets/data-element-data-layer.png)


Oberoende av Platform Web SDK måste du fortsätta att skapa dataelement inuti taggegenskapen som mappar till datainsamlingsvariabler från webbplatsen, till exempel ett datalager, HTML-attribut eller andra. När du har skapat dessa dataelement måste du mappa dem till XDM-schemat som du skapade under [konfigurera scheman](configure-schemas.md) lektion. Därför består det av två åtgärder att skapa dataelement:

1. Mappa webbplatsvariabler till dataelement, och
1. Mappa dessa dataelement till ett XDM-objekt

För steg 1 fortsätter du att mappa datalagret till dataelement på det sätt du gör just nu, med hjälp av någon av bastaggens tilläggstyper för dataelement. För steg 2 har plattformstillägget Web SDK följande typer av dataelement tillgängliga:

* ID för händelsesammanslagning
* Identitetskarta
* Variabel
* XDM-objekt

I den här lektionen fokuseras elementtypen Variable. Du skapar ett dataelement för att samla in Luma-besökares aktivitet baserat på det tillgängliga datalagret på Luma-webbplatsen. I nästa lektion får du lära dig mer om identitetskartan.

>[!NOTE]
>
> Elementtyper för händelselänknings-ID och XDM-objektdata används sällan för kantfall.

## Utbildningsmål

När lektionen är slut kan du:

* Förstå olika metoder för att mappa ett datalager till XDM
* Skapa dataelement för inhämtning av innehållsdata
* Mappa dataelement till ett XDM-objektdataelement


## Förutsättningar

Du har en förståelse för vad ett datalager är, och vet hur det [Luma demo site](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} datalager och veta hur du refererar till dataelement i taggar. Du måste ha utfört följande steg i självstudiekursen.

* [Konfigurera ett XDM-schema](configure-schemas.md)
* [Konfigurera ett identitetsnamnutrymme](configure-identities.md)
* [Konfigurera ett datastream](configure-datastream.md)
* [Web SDK-tillägget är installerat i taggegenskapen](install-web-sdk.md)

>[!IMPORTANT]
>
>The [Experience Cloud ID-tjänsttillägg](https://exchange.adobe.com/experiencecloud.details.100160.adobe-experience-cloud-id-launch-extension.html) behövs inte vid implementering av Adobe Experience Platform Web SDK eftersom ID-tjänstfunktionen är inbyggd i Platform Web SDK.

## Datalagermetoder

Det finns flera sätt att mappa data från datalagret till XDM med taggfunktionerna i Adobe Experience Platform. Nedan visas några fördelar och ikoner med tre olika strategier:

* [Implementera XDM i datalagret](create-data-elements.md#implement-xdm-in-the-data-layer)
* [Mappa till XDM i datastream](create-data-elements.md#map-to-xdm-in-the-datastream)
* [Mappa till XDM i taggar](create-data-elements.md#map-data-layer-in-tags)

>[!NOTE]
>
>Exemplen i den här självstudiekursen följer kartan till XDM när det gäller taggar.


### Implementera XDM i datalagret

Detta innebär att det fullständigt definierade XDM-objektet används som struktur för datalagret. Därefter mappar du hela datalagret till ett XDM-objektdataelement i Adobe-taggar. Om implementeringen inte använder en tagghanterare kan det här tillvägagångssättet vara idealiskt eftersom du kan skicka data till XDM direkt från programmet med [XDM-kommandot sendEvent](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#sending-xdm-data). Om du använder Adobe-taggar kan du skapa ett anpassat kodelement som hämtar hela datalagret som ett genomströmningsJSON-objekt till XDM. Därefter mappar du genomströmnings-JSON till XDM-objektfältet i åtgärden Skicka händelse.

Nedan visas ett exempel på hur datalagret skulle se ut med formatet Adobe Client Data Layer:

+++XDM i datalagrets exempel

```JSON
window.adobeDataLayer.push({
"eventType": "web.webPageDetails.pageViews",
"web":{
         "webInteraction":{
            "linkClicks":{
               "id":"",
               "value":""
            },
            "URL":"",
            "name":"",
            "region":"",
            "type":""
         },
         "webPageDetails":{
            "pageViews":{
               "id":"",
               "value":"1"
            },
            "URL":"https://luma.enablementadobe.com/",
            "isErrorPage":"",
            "isHomePage":"",
            "name":"luma:home",
            "server":"enablementadobe.com",
            "siteSection":"home",
            "viewName":""
         },
         "webReferrer":{
            "URL":"",
            "type":""
         }
      }
});
```

+++

Proffs

* Hoppar över steg för att mappa enskilda datalagervariabler till XDM
* Kan vara snabbare att driftsätta om ditt utvecklingsteam äger taggning i digitalt beteende

Kon

* Fullständigt beroende av utvecklingsteamet och utvecklingscykeln för uppdatering av vilka data som skickas till XDM
* Begränsad flexibilitet eftersom XDM får exakt nyttolast från datalagret
* Det går inte att använda inbyggda taggar, som skrapning, beständighet, funktioner för snabb distribution
* Det går inte att använda datalagret för pixlar från tredje part
* Ingen möjlighet att omvandla data mellan datalagret och XDM

### Mappa till XDM i datastream

Den här metoden använder den inbyggda funktionaliteten i datastream-konfigurationen som kallas [Dataförberedelse för datainsamling](https://experienceleague.adobe.com/docs/experience-platform/datastreams/data-prep.html) och hoppar över mappning av datalagervariabler till XDM i taggar.

Proffs

* Flexibelt eftersom du kan mappa enskilda variabler till XDM
* Möjlighet att [beräkna nya värden](https://experienceleague.adobe.com/docs/experience-platform/data-prep/functions.html) eller [transformera datatyper](https://experienceleague.adobe.com/docs/experience-platform/data-prep/data-handling.html) från ett datalager innan det går till XDM
* Utnyttja [Mappningsgränssnitt](https://experienceleague.adobe.com/docs/experience-platform/datastreams/data-prep.html#create-mapping) för att mappa fält i källdata till XDM med ett användargränssnitt där du kan peka och klicka

Kon

* Det går inte att använda datalagervariabler som dataelement för pixlar från tredje part på klientsidan, men de kan användas med händelsevidarebefordran av Adobe-taggar
* Det går inte att använda funktionen för att klippa i taggfunktionen i Adobe Experience Platform
* Underhållskomplexiteten ökar om datalagret mappas både i taggar och i datastream

### Mappa datalager i taggar

Detta innebär att mappa enskilda datalagervariabler ELLER datalagerobjekt till dataelement i taggar och slutligen till XDM. Detta är det traditionella sättet att implementera med hjälp av ett tagghanteringssystem.

Proffs

* Den mest flexibla metoden eftersom du kan styra enskilda variabler och omvandla data innan det når XDM
* Kan använda Adobe-taggar som utlöser och skrapningsfunktioner för att skicka data till XDM
* Kan mappa dataelement till pixlar från tredje part på klientsidan

Kon

* Kan ta längre tid att implementera

>[!TIP]
>
> Google datalager
> 
> Om din organisation redan använder Google Analytics och har det traditionella Google dataLayer-objektet på din webbplats, kan du använda [Google Data Layer-tillägg](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/google-data-layer/overview.html?lang=en) i Adobe-taggar. På så sätt kan ni driftsätta Adobe-teknik snabbare utan att behöva be IT-avdelningen om support. Om datalagret för Google mappas till XDM följer du samma steg som ovan.

>[!IMPORTANT]
>
>Som tidigare nämnts följer exemplen i den här självstudiekursen mappningen till XDM när det gäller taggar.

## Skapa dataelement för att hämta datalagret

Innan du skapar XDM-objektet skapar du följande uppsättning dataelement för [Luma demo site](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} datalager:

1. Gå till **[!UICONTROL Dataelement]** och markera **[!UICONTROL Lägg till dataelement]** (eller **[!UICONTROL Skapa nytt dataelement]** om det inte finns några befintliga dataelement i taggegenskapen)

   ![Skapa dataelement](assets/data-element-create.jpg)

1. Namnge dataelementet `page.pageInfo.pageName`
1. Använd **[!UICONTROL JavaScript-variabel]** **[!UICONTROL Dataelementtyp]** för att peka på ett värde i Lumas datalager: `digitalData.page.pageInfo.pageName`

1. Markera rutorna för **[!UICONTROL Använd gemener]** och **[!UICONTROL Rensa text]** standardisera ärendet och ta bort ovidkommande utrymmen

1. Lämna `None` som **[!UICONTROL Lagringstid]** inställning eftersom det här värdet är olika på alla sidor

1. Välj **[!UICONTROL Spara]**

   ![Dataelement för sidnamn](assets/data-element-pageName.jpg)

Skapa ytterligare fyra dataelement genom att följa samma steg:

* **`page.pageInfo.server`**  mappad till
  `digitalData.page.pageInfo.server`

* **`page.pageInfo.hierarchie1`**  mappad till
  `digitalData.page.pageInfo.hierarchie1`

* **`user.profile.attributes.username`**  mappad till
  `digitalData.user.0.profile.0.attributes.username`

* **`user.profile.attributes.loggedIn`** mappad till
  `digitalData.user.0.profile.0.attributes.loggedIn`

* **`cart.orderId`** mappad till `digitalData.cart.orderId` (du använder detta under [Konfigurationsanalys](setup-analytics.md) lektion)


>[!CAUTION]
>
>The [!UICONTROL JavaScript-variabel] dataelementtypen behandlar arrayreferenser som punkter i stället för hakparenteser, så att användarnamnets dataelement refereras som `digitalData.user[0].profile[0].attributes.username` **fungerar inte**.

## Skapa dataelement för variabel

mappa dataelementen till XDM med hjälp av **[!UICONTROL Variabel]** dataelement som definierar det schema som används för XDM-objektet. Det här objektet bör följa XDM-schemat som du skapade under [Konfigurera ett schema](configure-schemas.md) lektion.

Så här skapar du ett variabeldataelement:

1. Välj **[!UICONTROL Lägg till dataelement]**
1. Namnge dataelementet `xdm.variable.content`. Vi rekommenderar att du prefix med &quot;xdm&quot; för dataelementen som är specifika för XDM för att bättre organisera taggegenskaperna
1. Välj **[!UICONTROL Adobe Experience Platform Web SDK]** som **[!UICONTROL Tillägg]**
1. Välj **[!UICONTROL Variabel]** som **[!UICONTROL Dataelementtyp]**
1. Välj lämplig Experience Platform **[!UICONTROL Sandbox]**
1. Välj lämplig **[!UICONTROL Schema]**, i detta fall `Luma Web Event Data`
1. Välj **[!UICONTROL Spara]**

   ![Variabeldataelement](assets/analytics-tags-data-element-xdm-variable.png)

<!-- There are different ways to map data elements to XDM object fields. You can map individual data elements to individual XDM fields or map data elements to entire XDM objects as long as your data element matches the exact key-value pair schema present in the XDM object. In this lesson, you will capture content data by mapping to individual fields. You will learn how to [map a data element to an entire XDM object](setup-analytics.md#Map-an-entire-array-to-an-XDM-Object) in the [Setup Analytics](setup-analytics.md) lesson. 

Create an XDM object to capture content data:

1. In the left navigation, select **[!UICONTROL Data Elements]**
1. Select **[!UICONTROL Add Data Element]**
1. **[!UICONTROL Name]** the data element **`xdm.content`**
1. As the **[!UICONTROL Extension]** select `Adobe Experience Platform Web SDK`
1. As the **[!UICONTROL Data Element Type]** select `XDM object`
1. Select the Platform **[!UICONTROL Sandbox]** in which you created the XDM schema in during the [Configure an XDM Schema](configure-schemas.md) lesson, in this example `DEVELOPMENT Mobile and Web SDK Courses`
1. As the **[!UICONTROL Schema]**, select your `Luma Web Event Data` schema:

    ![XDM object](assets/data-element-xdm.content-fields.png)

    >[!NOTE]
    >
    >The sandbox corresponds to the Experience Platform sandbox in which you created the schema. There can be multiple sandboxes available in your Experience Platform instance, so make sure to select the right one. Always work in development first, then production.

1. Scroll down until you reach the **`web`** object
1. Select to open it

    ![Web Object](assets/data-element-pageviews-xdm-object.png)


1. Map the following web XDM variables to data elements

    * **`web.webPageDetials.name`** to `%page.pageInfo.pageName%`
    * **`web.webPageDetials.server`** to `%page.pageInfo.server%`
    * **`web.webPageDetials.siteSection`** to `%page.pageInfo.hierarchie1%`

    ![XDM object](assets/data-element-xdm.content.png)

1. Next, find the `identityMap` object in the schema and select it
 
1. Map to the `identityMap.loginID` data element

1. Select **[!UICONTROL Save]**

   ![Data Collection interface](assets/identity-dataElements-xdmContent-LumaSchema-identityMapSelect3.png)

-->

I slutet av dessa steg bör du skapa följande dataelement:

| CORE-tilläggsdataelement | Webbsidedataelement för plattforms-SDK |
-----------------------------|-------------------------------
| `cart.orderId` | `xdm.variable.content` |
| `page.pageInfo.hierarchie1` | |
| `page.pageInfo.pageName` | |
| `page.pageInfo.server` | |
| `user.profile.attributes.loggedIn` | |
| `user.profile.attributes.username` | |


>[!TIP]
>
>I framtiden [Skapa en taggregel](create-tag-rule.md) lektion, lär dig hur **[!UICONTROL Variabel]** kan du stapla flera regler i taggar med hjälp av **[!UICONTROL Uppdatera typ av variabelåtgärd]**. Sedan kan du oberoende skicka XDM-objektet till Adobe Experience Platform Edge Network med en separat **[!UICONTROL Åtgärdstyp för Skicka händelse]**.

Med dessa dataelement på plats är du redo att börja skicka data till Platform Edge Network med en taggregel. Men först lär du dig att samla in identiteter med Web SDK.

[Nästa: ](create-identities.md)

>[!NOTE]
>
>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Web SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela med dig av dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
