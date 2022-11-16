---
title: Testa implementeringen
description: Testa implementeringen
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
kt: 10447
hide: true
hidefromtoc: true
exl-id: e2213c23-d395-4c57-8c6c-0319cd0fb0ac
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 0%

---

# Testa implementeringen

Nu när du har konfigurerat webbsidan och driftsatt taggbiblioteket i Adobe Experience Platform är det dags att testa implementeringen.

Öppna din produktsida i webbläsaren. Du kan göra detta genom att klicka _Fil_ sedan _Öppna fil..._ i webbläsaren eller så kan du placera sidan på en webbserver och ange rätt URL.

När sidan har lästs in bör du se något liknande:

![Webbsida](../../assets/implementation-strategy/webpage.png)

Det är inte vackert, men det kommer att göra jobbet.

## Inspect sidvy och produktvy

Öppna utvecklarverktygen i webbläsaren och klicka på nätverkspanelen. Uppdatera sidan.

Nu bör du se fyra förfrågningar:

1. product.html - Din webbsida.
2. launch-############-development.js - Startbiblioteket.
3. interact - sidvisningshändelsen som skickas till servern.
4. interact - Produktvyhändelsen som skickas till servern.

Du kan själv kontrollera nyttolasterna för varje begäran. För den första `interact` begäran, du bör kunna se nyttolasten som skickas med en `eventType` av `web.webpagedetails.pageViews`.

![Granskning av begäran om sidvisning](../../assets/implementation-strategy/webpage-page-viewed-inspection.png)

För den andra `interact` begäran, du bör kunna se nyttolasten som skickas med en `eventType` av `commerce.productViews`.

![Kontroll av förfrågningar i produktvyn](../../assets/implementation-strategy/webpage-product-view-inspection.png)

Du får gärna gå runt resten av de data som skickas, inklusive produktinformationen.

## Inspect i kundvagnen och lägg till i kundvagnen

Klicka nu på _Lägg i kundvagnen_ -knappen.

Du bör se ytterligare två förfrågningar, den första med en `eventType` av `commerce.productListOpens` (för att öppna en ny kundvagn) och den andra med `eventType` av `commerce.productListAdds` (för att lägga produkten i kundvagnen).

## Inspect-händelsen klicka på nedladdningsappen

Beroende på vilken webbläsare du använder kan du ta bort nätverkspanelen genom att klicka på en länk som leder dig bort från den aktuella sidan. Eftersom du vill undersöka nätverksbegäran för den klickningshändelse som inträffar direkt innan du navigerar bort från sidan, måste du konfigurera webbläsaren så att nätverksloggarna på sidorna bevaras. Detta görs antingen genom att kontrollera en _Bevara logg_ i nätverkspanelen (Chrome, Safari, Edge) eller genom att klicka på en kugghjulsikon och markera en _Beständiga loggar_ på den visade menyn (Firefox).

Klicka nu på _Ladda ned appen_ länk.

Du borde se en till `interact` visas begäran i nätverkspanelen. Om du inspekterar din förfrågan bör du hitta en `eventType` av `web.webinteraction.linkClicks` samt information om den länk som du klickade på.

## Kontrollera att data kommer in i Adobe Experience Platform datamängd

Nu när förfrågningar skickas vill du också kontrollera om data kommer in i den Adobe Experience Platform-datauppsättning som du skapade. Börja med att navigera till [!UICONTROL Datauppsättningar] i Adobe Experience Platform.

Markera den datauppsättning som du skapade tidigare.

Du kan behöva vänta några minuter, men snart ska du se indikationer på att data bearbetas och infogas i datauppsättningen. Du bör också se om bearbetningen lyckades eller misslyckades. Om det misslyckas kommer du att se varför det misslyckades. Fel uppstår oftast eftersom de data du skickar inte matchar schemat och du måste justera data eller schema därefter.

![Inmatning av datauppsättning](../../assets/implementation-strategy/dataset-ingestion.png)

## Använda Adobe Experience Platform Debugger-tillägget

Mer information om hur implementeringen fungerar både i webbläsaren och på Adobe-servrar finns i webbläsartillägget Adobe Experience Platform Debugger!

[Adobe Experience Platform Debugger extension for Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

[Adobe Experience Platform Debugger extension for Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-experience-platform-dbg/)
