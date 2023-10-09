---
title: Mappa data till analysdata
description: Lär dig hur du samlar in och mappar data för Adobe Analytics i en mobilapp.
solution: Data Collection,Experience Platform,Analytics
hide: true
exl-id: 631588df-a540-41b5-94e3-c8e1dc5f240b
source-git-commit: d7410a19e142d233a6c6597de92f112b961f5ad6
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 0%

---

# Samla in och mappa analysdata

Lär dig hur du mappar mobildata till Adobe Analytics.

The [event](events.md) data som du har samlat in och skickat till Platform Edge Network i tidigare lektioner vidarebefordras till de tjänster som konfigurerats i ditt datastam, inklusive Adobe Analytics. Du mappar data till rätt variabler i rapportsviten.

![Arkitektur](assets/architecture-aa.png)

## Förutsättningar

* Understanding of ExperienceEvent tracking.
* XDM-data har skickats i exempelappen.
* En Adobe Analytics rapportserie som du kan använda för den här lektionen.

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

Använda [Säkerhet](assurance.md) du kan bekräfta att du skickar en upplevelsehändelse, att XDM-data är korrekta och att Analytics-mappningen sker som förväntat.

1. Granska [installationsanvisningar](assurance.md#connecting-to-a-session) för att ansluta simulatorn eller enheten till Assurance.

1. Skicka en **[!UICONTROL productListAdds]** händelse (lägg till en produkt i korgen).

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

### Använda en fältgrupp

* Lägg till **[!UICONTROL Adobe Analytics ExperienceEvent, fullständigt tillägg]** fältgrupp till ditt schema.

  ![Fältgrupp för Analytics ExperienceEvent FullExtension](assets/schema-analytics-extension.png)

* Bygg XDM-nyttolaster i appen, i enlighet med fältgruppen Adobe Analytics ExperienceEvent Full Extension, i likhet med vad du har gjort i [Spåra händelsedata](events.md) lektion, eller
* Skapa regler i taggegenskapen som använder regelåtgärder för att bifoga eller ändra data till fältgruppen Adobe Analytics ExperienceEvent Full Extension. Mer information finns i [Bifoga data till SDK-händelser](https://developer.adobe.com/client-sdks/documentation/user-guides/attach-data/) eller [Ändra data i SDK-händelser](https://developer.adobe.com/client-sdks/documentation/user-guides/attach-data/).


### Använd bearbetningsregler

Så här ser en bearbetningsregel ut när den här informationen används:

* Du **[!UICONTROL Skriv över värde för]** (1) **[!UICONTROL Programskärmens namn (eVar2)]** (2) med värdet av **[!UICONTROL a.x._techmarketingdemo.appinformation.appstatedetails.screenname]** (3) om **[!UICONTROL a.x._techmarketingdemo.appinformation.appstatedetails.screenname]** (4) **[!UICONTROL är inställt]** (5)

* Du **[!UICONTROL Ange händelse]** (6) **[!UICONTROL Lägg till i önskelista (händelse 3)]** (7) till **[!UICONTROL a.x.commerce.saveForLaters.value(Context)]** (8) om **[!UICONTROL a.x.commerce.saveForLaters.value(Context)]** (9) **[!UICONTROL är inställt]** (10)

![regler för analysbearbetning](assets/analytics-processing-rules.png)

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
>Till skillnad från tidigare mobilappsimplementeringar finns det ingen skillnad mellan en sida-/skärmvy och andra händelser. I stället kan du öka stegvis **[!UICONTROL Sidvy]** genom att ställa in **[!UICONTROL Sidnamn]** i en bearbetningsregel. Eftersom du samlar in anpassade `screenName` i självstudiekursen rekommenderar vi att du mappar skärmnamn till **[!UICONTROL Sidnamn]** i en bearbetningsregel.


>[!SUCCESS]
>
>Du har konfigurerat appen för att mappa Experience Edge XDM-objekt till Adobe Analytics-variabler som aktiverar Adobe Analytics-tjänsten i ditt datastam och som använder bearbetningsregler där det är tillämpligt.<br/> Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Mobile SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Nästa: **[Skicka data till Experience Platform](platform.md)**
