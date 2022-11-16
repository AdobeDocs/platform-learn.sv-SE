---
title: Testa implementeringen
description: Testa implementeringen
exl-id: 66eb1d4e-32eb-45fc-8da4-8d3c04dc3c7a
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 0%

---

# Testa implementeringen

Nu när du har konfigurerat webbsidan och driftsatt taggbiblioteket i Adobe Experience Platform är det dags att testa implementeringen.

1. Öppna din produktsida i webbläsaren. Du kan göra detta genom att klicka _Fil_ sedan _Öppna fil..._ i webbläsaren eller så kan du placera sidan på en webbserver och ange rätt URL.

När sidan har lästs in bör du se något liknande:
![Webbsida](assets/webpage.png)

Det är inte vackert, men det gör jobbet.

## Inspect sidvy och produktvy

1. Öppna utvecklarverktygen i webbläsaren och klicka på nätverkspanelen. Uppdatera sidan.
Nu bör du se fyra förfrågningar:
* product.html - Din webbsida.
* launch-############-development.js - Startbiblioteket.
* interact - sidvisningshändelsen som skickas till servern.
* interact - Produktvyhändelsen som skickas till servern.
Inspect nyttolasten för varje begäran:
1. För den första `interact` begäran, du bör kunna se nyttolasten som skickas med en `eventType` av `web.webpagedetails.pageViews`.
   ![Granskning av begäran om sidvisning](assets/webpage-page-viewed-inspection.png)
1. För den andra `interact` begäran, du bör kunna se nyttolasten som skickas med en `eventType` av `commerce.productViews`.
   ![Kontroll av förfrågningar i produktvyn](assets/webpage-product-view-inspection.png)
1. Granska resten av de data som skickas, inklusive produktinformationen.

## Inspect i kundvagnen och lägg till i kundvagnen

1. Klicka nu på **_Lägg i kundvagnen_**button.

Du bör se ytterligare två förfrågningar, den första med en `eventType` av `commerce.productListOpens` (för att öppna en ny kundvagn) och den andra med `eventType` av `commerce.productListAdds` (för att lägga produkten i kundvagnen).

## Inspect-händelsen klicka på nedladdningsappen

Beroende på vilken webbläsare du använder kan du ta bort nätverkspanelen genom att klicka på en länk som leder dig bort från den aktuella sidan. Eftersom du vill undersöka nätverksbegäran för den klickningshändelse som inträffar direkt innan du navigerar bort från sidan, måste du konfigurera webbläsaren så att nätverksloggarna på sidorna bevaras.

1. Bevara nätverksloggar genom att antingen kontrollera en **_Bevara logg_** i nätverkspanelen (Chrome, Safari, Edge) eller genom att klicka på en kugghjulsikon och markera en **_Beständiga loggar_** på den visade menyn (Firefox).
1. Klicka på **_Ladda ned appen_** länk. Du borde se en till `interact` visas begäran i nätverkspanelen.
1. Leta reda på begäran med en `eventType` av `web.webinteraction.linkClicks`och granska informationen om länken som du klickade på.

## Kontrollera att data kommer in i Adobe Experience Platform datamängd

Nu när begäranden skickas ska du kontrollera om data kommer in i den Adobe Experience Platform-datauppsättning du har skapat.

1. Navigera till **[!UICONTROL Datauppsättningar]** i Adobe Experience Platform.
1. Välj [datauppsättning](configure-the-server/create-a-dataset.md) som du skapade för den här självstudiekursen.
Du kan behöva vänta några minuter, men snart ska du se indikationer på att data bearbetas och infogas i datauppsättningen. Du bör också se om bearbetningen lyckades eller misslyckades. Om det misslyckades ser du varför det misslyckades. Fel uppstår oftast eftersom de data du skickar inte matchar schemat och du måste justera data eller schema därefter.
   ![Inmatning av datauppsättning](assets/dataset-ingestion.png)

## Använda Adobe Experience Platform Debugger-tillägget

Mer information om hur implementeringen fungerar både i webbläsaren och på Adobe-servrar finns i webbläsartillägget Adobe Experience Platform Debugger!

[Adobe Experience Platform Debugger extension for Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

[Adobe Experience Platform Debugger extension for Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-experience-platform-dbg/)

[Nästa: ](summary.md)

>[!NOTE]
>
>Tack för att du har lagt ned din tid på att lära dig om datainsamling. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela med dig av dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)