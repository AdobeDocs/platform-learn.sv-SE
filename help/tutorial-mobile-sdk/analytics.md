---
title: Analysmappning
description: Lär dig hur du samlar in data för Adobe Analytics i en mobilapp.
solution: Data Collection,Experience Platform,Analytics
exl-id: 406dc687-643f-4f7b-a8e7-9aad1d0d481d
source-git-commit: bc53cb5926f708408a42aa98a1d364c5125cb36d
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 1%

---

# Analysmappning

Lär dig hur du mappar mobildata till Adobe Analytics.

>[!INFO]
>
> Den här självstudiekursen kommer att ersättas med en ny självstudiekurs om hur du använder en ny exempelapp i slutet av november 2023


The [event](events.md) data som du har samlat in och skickat till Platform Edge Network i tidigare lektioner vidarebefordras till de tjänster som konfigurerats i ditt datastam, inklusive Adobe Analytics. Du behöver bara mappa data till rätt variabler i rapportsviten.

## Förutsättningar

* Understanding of ExperienceEvent tracking.
* XDM-data har skickats i exempelappen.
* Datastream har konfigurerats för Adobe Analytics

## Utbildningsmål

I den här lektionen kommer du att:

* Förstå automatisk mappning av analysvariabler.
* Ställ in bearbetningsregler för att mappa XDM-data till analysvariabler.

## Automatisk mappning

Många av XDM-standardfälten mappas automatiskt till analysvariabler. Se hela listan [här](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/adobe-analytics/automatically-mapped-vars.html?lang=en).

### Exempel 1 - s.products

Ett bra exempel är [variabeln products](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=en) som inte kan fyllas med bearbetningsregler. Med en XDM-implementering skickas alla nödvändiga data i productListItems och s.products fylls i automatiskt via Analytics-mappning.

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

Detta ger följande resultat:

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

Detta ger följande resultat:

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

Detta ger följande resultat:

```
s.events = "scAdd:321435"
```

## Validera med Assurance

Använda [Verktyget Assurance QA](assurance.md) du kan bekräfta att du skickar en ExperienceEvent, att XDM-data är korrekta och att Analytics-mappningen sker som förväntat. Exempel:

1. Skicka händelsen productListAdds.

   ```swift
   var xdmData: [String: Any] = [
     "eventType": "commerce.productListAdds",
     "commerce": [
       "productListAdds": [
         "value": 1
       ]
     ],
     "productListItems": [
       [
         "name": "neve studio dance jacket - (blue)",
         "SKU": "test-sku",
         "priceTotal": 69
       ]
     ]
   ]
   let addToCartEvent = ExperienceEvent(xdm: xdmData)
   Edge.sendEvent(experienceEvent: addToCartEvent)
   ```

1. Visa ExperienceEvent-träffen.

   ![xdm-träff i analytics](assets/mobile-analytics-assurance-xdm.png)

1. Granska XDM-delen av JSON.

   ```json
     "xdm" : {
       "productListItems" : [ {
         "priceTotal" : 69,
         "SKU" : "test-sku",
         "name" : "neve studio dance jacket - (blue)"
       } ],
       "timestamp" : "2021-10-22T22:03:37Z",
       "commerce" : {
         "productListAdds" : {
           "value" : 1
         }
       },
       "eventType" : "commerce.productListAdds",
       //...
     }
   ```

1. Granska `analytics.mapping` -händelse.

   ![xdm-träff i analytics](assets/mobile-analytics-assurance-mapping.png)

Observera följande i Analytics-mappningen:

* Händelser fylldes i med scAdd baserat på `commerce.productListAdds`.
* pl (produktvariabel) fylldes i med ett sammanfogat värde baserat på `productListItems`.
* Det finns annan intressant information i den här händelsen, inklusive alla kontextdata.


## Mappa med kontextdata

XDM-data som vidarebefordras till Analytics konverteras till [kontextdata](https://experienceleague.adobe.com/docs/mobile-services/ios/getting-started-ios/proc-rules.html?lang=en) med både standardfält och anpassade fält.

Kontextens datanyckel konstrueras enligt den här syntaxen:

```
a.x.[xdm path]
```

Exempel:

```
//Standard Field
a.x.commerce.saveforlaters.value

//Custom Field
a.x._techmarketingdemos.appinformationa.appstatedetails.screenname
```

>[!NOTE]
>
>Anpassade fält placeras under din Experience Cloud-organisationsidentifierare.
>
>&quot;_techmarketingdemos&quot; ersätts med din organisations unika värde.

Så här ser en bearbetningsregel ut när den här informationen används:

![regler för analysbearbetning](assets/mobile-analytics-processing-rules.png)

>[!IMPORTANT]
>
>
>Vissa av de automatiskt mappade variablerna kanske inte är tillgängliga för användning i bearbetningsregler.
>
>
>Första gången du mappar till en bearbetningsregel visas inte kontextdatavariablerna från XDM-objektet. Om du vill åtgärda det väljer du ett värde, Spara och återgå till att redigera. Alla XDM-variabler ska nu visas.


Ytterligare information om bearbetningsregler och kontextdata finns [här](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/implementation-basics/map-contextdata-variables-into-props-and-evars-with-processing-rules.html?lang=en).

>[!TIP]
>
>Till skillnad från tidigare mobilappsimplementeringar finns det ingen skillnad mellan en sida-/skärmvy och andra händelser. I stället kan du öka stegvis **[!UICONTROL Sidvy]** genom att ställa in **[!UICONTROL Sidnamn]** i en bearbetningsregel. Eftersom du samlar in anpassade `screenName` i självstudiekursen rekommenderar vi att du mappar detta till **[!UICONTROL Sidnamn]** i en bearbetningsregel.


Nästa: **[Experience Platform](platform.md)**

>[!NOTE]
>
>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Mobile SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)