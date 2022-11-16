---
title: Skapa regler för spårning av sidvy och e-handelshändelser
description: Skapa regler för spårning av sidvy och e-handelshändelser
exl-id: 00bf3374-9319-47ce-a75a-2b94f793c938
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 0%

---

# Skapa regler för spårning av sidvy och e-handelshändelser

Om du vill spåra att användaren har visat produktsidan skapar du en regel i Adobe Experience Platform [!DNL Tags].

1. Klicka på **[!UICONTROL Regler]** i navigeringen till vänster och klicka sedan på **[!UICONTROL Skapa ny regel]**.

1. Ange regelnamnet **_Visad sida_**.

## Lägg till en händelse

1. Klicka på **[!UICONTROL Lägg till]** knapp under [!UICONTROL Händelser]. Du visar nu att du är med i eventvyn. För [!UICONTROL Tillägg] fält, markera **[!UICONTROL Adobe-klientdatalager]**. För [!UICONTROL Händelsetyp] fält, markera **[!UICONTROL Publicerade data]**.
1. Eftersom du bara vill att den här regeln ska aktiveras när `pageViewed` händelsen skickas till datalagret, markera **[!UICONTROL Specifik händelse]** under [!UICONTROL Lyssna på] och text **_pageViewed_** till [!UICONTROL Händelse/nyckel att registrera för] textfält.
1. Klicka **[!UICONTROL Behåll ändringar]**.
   ![Sidvisad händelse](../assets/page-viewed-event.png)

## Lägga till en åtgärd

Nu när du är tillbaka i regelvyn:

1. Klicka på **[!UICONTROL Lägg till]** knapp under [!UICONTROL Åtgärder]. Du bör nu vara med i åtgärdsvyn. För [!UICONTROL Tillägg] fält, markera **[!UICONTROL Adobe Experience Platform Web SDK]**. För [!UICONTROL Åtgärdstyp] fält, markera **[!UICONTROL Skicka händelse]**. Med den här åtgärden kan du skicka en upplevelsehändelse till Adobe Experience Platform Edge Network.
1. I mitten av skärmen hittar du [!UICONTROL Typ] fält och markera **`web.webpagedetails.pageViews`**. Det här är en av de kanoniska händelsetyper som Adobe Experience Platform tillhandahåller. Det representerar en sidvy.
1. För [!UICONTROL XDM-data] fält, ange **`%event.fullState%`**. Detta anger att det beräknade läget (kallas även fullständigt läge) för datalagret, som hämtas när regeln aktiveras. Detta ska skickas som en del av upplevelsehändelsen.
1. Klicka på **[!UICONTROL Behåll ändringar]** -knappen.
   ![Sidvisningsåtgärd](../assets/page-viewed-action.png)

Om de data du överförde till datalagret från webbplatsen inte överensstämmer med ditt XDM-schema, eller om du bara vill skicka en del av datalagrets beräknade tillstånd, använder du [!UICONTROL XDM-objekt] dataelementtyp (tillhandahålls av Adobe Experience Platform Web SDK-tillägget) för att skapa ett lämpligt objekt som matchar ditt schema.

## Spara regeln

1. Spara regeln genom att klicka **[!UICONTROL Spara]**.
   ![Visningsregel för sida](../assets/page-viewed-rule.png)

## Upprepa processen

Upprepa processen ovan för att skapa regler för när en produkt visas, en kundvagn öppnas och en produkt läggs till i kundvagnen. De enda skillnaderna mellan reglerna är regelnamnet, det värde som anges i [!UICONTROL Händelse/nyckel att registrera för] i [!UICONTROL Publicerade data] och [!UICONTROL Typ] i [!UICONTROL Skicka händelse] åtgärd. Här är värdena för varje regel:

Produktvisningsregel:

* **Regelnamn**: _Visad produkt_
* **Händelse/nyckel att registrera för** inom [!UICONTROL Publicerade data] händelse: `productViewed`
* **Typ** inom [!UICONTROL Skicka händelse] åtgärd: `commerce.productViews`

Öppen kundvagnsregel:

* **Regelnamn**: _Bild öppnad_
* **Händelse/nyckel att registrera för** inom [!UICONTROL Publicerade data] händelse: `cartOpened`
* **Typ** inom [!UICONTROL Skicka händelse] åtgärd: `commerce.productListOpens`

Produkt som lagts till i kundvagnsregel:

* **Regelnamn**: _Produkt tillagd i kundvagn_
* **Händelse/nyckel att registrera för** inom [!UICONTROL Publicerade data] händelse: `productAddedToCart`
* **Typ** inom [!UICONTROL Skicka händelse] åtgärd: `commerce.productListAdds`

Sedan hanterar vi spårningsklickningar på [!UICONTROL Ladda ned appen] länk.

[Nästa: ](create-a-data-element-and-rule-for-tracking-app-downloads.md)

>[!NOTE]
>
>Tack för att du har lagt ned din tid på att lära dig om datainsamling. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela med dig av dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)
