---
title: Skapa ett dataelement och en regel för att spåra appnedladdningar
description: Skapa ett dataelement och en regel för att spåra appnedladdningar
feature: Web SDK
exl-id: 8012ba48-38ac-4fb5-9876-8f57d1c5da5d
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 0%

---

# Skapa ett dataelement och en regel för att spåra appnedladdningar

Som en påminnelse när du spårar när en användare klickar på [!UICONTROL Ladda ned appen] -länk överfördes du till datalagret enligt följande:

```js
window.adobeDataLayer.push({
  "event": "downloadAppClicked",
  "eventInfo": {
    "web": {
      "webInteraction": {
        "URL": "https://example.com/download",
        "name": "App Download",
        "type": "download"
      }
    }
  }
});
```

Du använde `eventInfo` som anger för datalagret att kommunicera dessa data tillsammans med händelsen, men till _not_ bevara data i datalagret. För en länkklickning är det inte användbart att lägga till information om den klickade länken till datalagret eftersom den inte kan användas för andra händelser som inträffar senare på sidan.

För den här implementeringen skickar du en upplevelsehändelse till Adobe Experience Platform som innehåller det sammanslagna resultatet av (1) det beräknade läget för datalagret och (2) innehållet i `eventInfo`.

För att göra detta måste du skapa ett dataelement som sammanfogar dessa två informationssegment.

## Skapa ett dataelement

Så här skapar du ett lämpligt dataelement:

1. Klicka [!UICONTROL Dataelement] i den vänstra menyn.
1. Klicka sedan på [!UICONTROL Skapa nytt dataelement] länk.
1. Ange dataelementets namn, `computedStateAndEventInfo`.
1. För [!UICONTROL Tillägg] fält, markera [!UICONTROL Core] om det inte redan är markerat.
1. För [!UICONTROL Dataelementtyp] fält, markera **[!UICONTROL Sammanfogade objekt]**. Med det här dataelementet kan du sammanfoga flera objekt. Det sammanfogade resultatet returneras av dataelementet.
1. Lägg till det första objektet som du vill ta med i sammanfogningen. Retur `%event.fullState%` i [!UICONTROL Objekt (obligatoriskt)] fält. Vid användning inuti en regel som utlöses av en [!UICONTROL Publicerade data] rule-händelse refererar det här till det beräknade läget för Adobe-klientdatalagret när regeln utlöstes.
1. Klicka på  **[!UICONTROL Lägg till ytterligare]** -kommando.
1. Lägg till det andra objektet. Retur `%event.eventInfo%` i [!UICONTROL Objekt (obligatoriskt)] fält. Vid användning inuti en regel som utlöses av en [!UICONTROL Publicerade data] rule-händelse, detta refererar till `eventInfo` som har skickats till Adobe-klientdatalagret.
1. Spara dataelementet genom att klicka på [!UICONTROL Spara] -knappen.
   ![computedStateAndEventInfo, dataelement](../assets/computed-state-and-event-info-data-element.png)

Dataelementet är färdigt.

## Skapa en regel

Så här skapar du regeln för att spåra klick på [!UICONTROL Ladda ned appen] länk:

1. Klicka **[!UICONTROL Regler]** i den vänstra menyn.
1. Klicka **[!UICONTROL Lägg till regel]**.
1. Retur **_Klicka på länken Hämta program_** i [!UICONTROL Namn] fält.

## Lägg till en händelse

1. Klicka på **[!UICONTROL Lägg till]** knapp under [!UICONTROL Händelser]. Du visar nu att du är med i eventvyn.
1. För [!UICONTROL Tillägg] fält, markera **[!UICONTROL Adobe-klientdatalager]**.
1. För [!UICONTROL Händelsetyp] fält, markera **[!UICONTROL Publicerade data]**.
1. Klicka **[!UICONTROL Behåll ändringar]**.
   ![Hämta klickningshändelse för app](../assets/download-app-clicked-event.png)
Eftersom du bara vill att den här regeln ska aktiveras när `downloadAppClicked` händelsen skickas till datalagret, välj **[!UICONTROL Specifik händelse]** radio under [!UICONTROL Lyssna på] och text **_downloadAppClick_** till [!UICONTROL Händelse/nyckel att registrera för]  textfält som visas.

## Lägga till en åtgärd

Nu när du är tillbaka i regelvyn:

1. Klicka på **[!UICONTROL Lägg till]** knapp under [!UICONTROL Åtgärder].
1. Du bör nu vara med i åtgärdsvyn. För [!UICONTROL Tillägg] fält, markera **[!UICONTROL Adobe Experience Platform Web SDK]**. För [!UICONTROL Åtgärdstyp] fält, markera **[!UICONTROL Skicka händelse]**.
1. I [!UICONTROL Typ] fält till höger, välj `web.webinteraction.linkClicks`.
1. För [!UICONTROL XDM-data] klickar du på dataelementets väljarknapp till höger och väljer **[!UICONTROL computedStateAndEventInfo]**. Det här är dataelementet som du nyss skapade.
1. För den här regeln (till skillnad från andra regler som du har skapat) ska du kontrollera **[!UICONTROL Dokumentet tas bort]** kryssrutan.
   ![Kryssrutan för dokumentet tas bort](../assets/document-will-unload.png)
1. Spara funktionsmakrot genom att klicka på **[!UICONTROL Behåll ändringar]** -knappen.

>[!TIP]
>
>The [!UICONTROL Dokumentet tas bort från funktionen] anger för SDK att användaren navigerar bort från sidan när han/hon klickar på länken. Detta är viktigt eftersom SDK kan göra begäran även om användaren navigerar bort från sidan, eftersom begäran fortsätter att köras i bakgrunden och når servern. Om den här kryssrutan inte är markerad kommer begäran inte att utföras på det här sättet och kommer därför troligtvis att avbrytas när det aktuella dokumentet tas bort.
>
>Du kanske frågar dig själv: &quot;Det låter bra. Varför är inte det här alternativet alltid aktiverat då?&quot;
>
>Det är lite komplicerat, men när den här funktionen används används en webbläsarmetod som kallas [`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon) för att skicka begäran. När en begäran skickas med `sendBeacon`tillåter inte webbläsaren SDK (eller något annat) att komma åt data som returneras från servern. Om SDK skulle använda den här funktionen för varje begäran skulle SDK aldrig kunna ta emot några data från servern. Därför är det viktigt att du kontrollerar [!UICONTROL Dokumentet tas bort] kryssrutan endast när det aktuella dokumentet tas bort. I så fall kan svarsdata ändå tas bort.

## Spara regeln

Din regel bör nu vara fullständig.

1. Klicka **[!UICONTROL Spara]** i det övre högra hörnet.
   ![Hämta applänk klickad regel](../assets/download-app-link-clicked-rule.png)

[Nästa: ](publish-the-library.md)

>[!NOTE]
>
>Tack för att du har lagt ned din tid på att lära dig om datainsamling. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela med dig av dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)