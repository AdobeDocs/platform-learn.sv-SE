---
title: Samla in och mappa analysdata
description: Lär dig hur du samlar in och mappar data för Adobe Analytics i en mobilapp.
solution: Data Collection,Experience Platform,Analytics
hide: true
source-git-commit: cd1efbfaa335c08cbcc22603fe349b4594cc1056
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 1%

---

# Samla in och mappa analysdata

Lär dig hur du mappar mobildata till Adobe Analytics.

The [event](events.md) data som du har samlat in och skickat till Platform Edge Network i tidigare lektioner vidarebefordras till de tjänster som konfigurerats i ditt datastam, inklusive Adobe Analytics. Du mappar data till rätt variabler i rapportsviten.

![Arkitektur](assets/architecture-aa.png)

## Förutsättningar

* Understanding of ExperienceEvent tracking.
* XDM-data har skickats i exempelappen.
* Datastream har konfigurerats för Adobe Analytics

## Utbildningsmål

I den här lektionen kommer du att:

* Konfigurera dataströmmen med Adobe Analytics-tjänsten.
* Förstå automatisk mappning av analysvariabler.
* Ställ in bearbetningsregler för att mappa XDM-data till analysvariabler.

## Lägg till Adobe Analytics datastream-tjänst

Om du vill skicka XDM-data från Edge Network till Adobe Analytics konfigurerar du Adobe Analytics-tjänsten till den datastream som du konfigurerar som en del av [Skapa ett datastream](create-datastream.md).

1. I gränssnittet för datainsamling väljer du **[!UICONTROL Datastreams]** och din datastream.

1. Välj sedan ![Lägg till](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Lägg till tjänst]**.

1. Lägg till **[!UICONTROL Adobe Analytics]** från [!UICONTROL Tjänst] lista,

1. Ange namnet på rapportsviten från Adobe Analytics som du vill använda i **[!UICONTROL Report Suite-ID]**.

1. Aktivera tjänsten genom att växla **[!UICONTROL Aktiverad]** på.

1. Välj **[!UICONTROL Spara]**.

   ![Lägg till Adobe Analytics som datastream-tjänst](assets/datastream-service-aa.png)


## Automatisk mappning

Många av XDM-standardfälten mappas automatiskt till analysvariabler. Se hela listan [här](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/adobe-analytics/automatically-mapped-vars.html?lang=en).

### Exempel 1 - s.products

Ett bra exempel är [variabeln products](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=en) som inte kan fyllas med bearbetningsregler. Med en XDM-implementering skickar du alla nödvändiga data i `productListItems` och `s.products` fylls i automatiskt via Analytics-mappning.

Det här objektet:

```swift
"productListItems": [
    [
      "name":  "Yoga Mat",
      "SKU": "5829",
      "priceTotal": "49.99",
      "quantity": 1
    ],
    [
      "name":  "Water Bottle",
      "SKU": "9841",
      "priceTotal": "30.00",
      "quantity": 3
    ]
]
```

resulterar i

```
s.products = ";Yoga Mat;1;49.99,;Water Bottle,3,30.00"
```

>[!NOTE]
>
>För närvarande `productListItems[N].SKU` ignoreras av automatisk mappning.


### Exempel 2 - scAdd

Om du tittar närmare på alla händelser har de två fälten `value` (obligatoriskt) och `id` (valfritt). The `value` fältet används för att öka antalet händelser. The `id` fältet används för serialisering.

Det här objektet:

```swift
"commerce" : {
  "productListAdds" : {
    "value" : 1
  }
}
```

resulterar i

```
s.events = "scAdd"
```

Det här objektet:

```swift
"commerce" : {
  "productListAdds" : {
    "value" : 1,
    "id": "321435"
  }
}
```

resulterar i

```
s.events = "scAdd:321435"
```

## Validera med Assurance

Använda [Säkerhet](assurance.md) du kan bekräfta att du skickar en upplevelsehändelse, att XDM-data är korrekta och att Analytics-mappningen sker som förväntat. Exempel:

1. Skicka händelsen productListAdds.

1. Visa ExperienceEvent-träffen.

   ![xdm-träff i analytics](assets/analytics-assurance-experiencevent.png)

1. Granska XDM-delen av JSON.

   ```json
   "xdm" : {
     "productListItems" : [ {
       "SKU" : "LLWS05.1-XS",
       "name" : "Desiree Fitness Tee",
       "priceTotal" : 24
     } ],
   "timestamp" : "2023-08-04T12:53:37.662Z",
   "eventType" : "commerce.productListAdds",
   "commerce" : {
     "productListAdds" : {
       "id" : "LLWS05.1-XS",
       "value" : 1
     }
   }
   // ...
   ```

1. Granska **[!UICONTROL analytics.mapping]** -händelse.

   ![xdm-träff i analytics](assets/analytics-assurance-mapping.png)

Observera följande i Analytics-mappningen:

* **[!UICONTROL händelser]** är ifyllda med `scAdd` baserat på `commerce.productListAdds`.
* **[!UICONTROL pl]** (variabeln products) fylls i med ett sammanfogat värde baserat på `productListItems`.
* Det finns annan intressant information i den här händelsen, inklusive alla kontextdata.


## Mappa med kontextdata

XDM-data som vidarebefordras till Analytics konverteras till [kontextdata](https://experienceleague.adobe.com/docs/mobile-services/ios/getting-started-ios/proc-rules.html?lang=en) med både standardfält och anpassade fält.

Kontextens datanyckel konstrueras enligt den här syntaxen:

```
a.x.[xdm path]
```

Exempel:

```
// Standard Field
a.x.commerce.saveforlaters.value

// Custom Field
a.x._techmarketingdemos.appinformation.appstatedetails.screenname
```

>[!NOTE]
>
>Anpassade fält placeras under din Experience Cloud-organisationsidentifierare.
>
>`_techmarketingdemos` ersätts med organisationens unika värde.

Om du vill mappa dessa XDM-kontextdata till analysdata i rapportsviten kan du:

* Lägg till **[!UICONTROL Adobe Analytics ExperienceEvent, fullständigt tillägg]** fältgrupp till ditt schema.

  ![Fältgrupp för Analytics ExperienceEvent FullExtension](assets/schema-analytics-extension.png)
* Skapa regler i taggegenskapen för att mappa kontextdata till fälten i fältgruppen Adobe Analytics ExperienceEvent Full Extension. Till exempel karta `_techmarketingdemo.appinformation.appstatedetails.screenname` till `_experience.analytics.customDimensions.eVars.eVar2`.

<!-- Old processing rules section
Here is what a processing rule using this data might look like:

* You **[!UICONTROL Overwrite value of]** (1) **[!UICONTROL App Screen Name (eVar2)]** (2) with the value of **[!UICONTROL a.x._techmarketingdemo.appinformation.appstatedetails.screenname]** (3) if **[!UICONTROL a.x._techmarketingdemo.appinformation.appstatedetails.screenname]** (4) **[!UICONTROL is set]** (5).

* You **[!UICONTROL Set event]** (6) **[!UICONTROL Add to Wishlist (Event 3)]** (7) to **[!UICONTROL a.x.commerce.saveForLaters.value(Context)]** (8) if **[!UICONTROL a.x.commerce.saveForLaters.value(Context)]** (9) **[!UICONTROL is set]** (10).

![analytics processing rules](assets/analytics-processing-rules.png)

>[!IMPORTANT]
>
>
>Some of the automatically mapped variables may not be available for use in processing rules.
>
>
>The first time you map to a processing rule, the interface does not show you the context data variables from the XDM object. To fix that select any value, Save, and come back to edit. All XDM variables should now appear.


Additional information about processing rules and context data can be found [here](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/implementation-basics/map-contextdata-variables-into-props-and-evars-with-processing-rules.html?lang=en).

>[!TIP]
>
>Unlike previous mobile app implementations, there is no distinction between a page / screen views and other events. Instead you can increment the **[!UICONTROL Page View]** metric by setting the **[!UICONTROL Page Name]** dimension in a processing rule. Since you are collecting the custom `screenName` field in the tutorial, it is highly recommended to map screen name to **[!UICONTROL Page Name]** in a processing rule.

-->

>[!SUCCESS]
>
>Du har konfigurerat appen för att mappa Experience Edge XDM-objekt till Adobe Analytics-variabler som aktiverar Adobe Analytics-tjänsten i ditt datastam och som använder bearbetningsregler där det är tillämpligt.<br/> Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Mobile SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Nästa: **[Experience Platform](platform.md)**
