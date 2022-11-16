---
title: Publicera biblioteket
description: Publicera biblioteket
exl-id: b2657835-f320-4d58-b99b-f88aad660259
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---

# Publicera biblioteket

Nu är det dags att driftsätta taggbiblioteket på er webbplats.

## Skapa ett bibliotek

Först måste du skapa ett bibliotek som innehåller de tillägg, regler och dataelement som du har skapat.

1. Om du vill skapa ett bibliotek väljer du **[!UICONTROL Publiceringsflöde]** i den vänstra menyn.
1. Välj **[!UICONTROL Lägg till bibliotek]**. Du bör se vyn för att skapa bibliotek.
   ![skapa taggbibliotek](../assets/tags-library-creation.png)

1. Ge biblioteket ett namn, som **_Demo_**.
1. Välj **[!UICONTROL Utveckling]** i [!UICONTROL Miljö] listruta.
1. Klicka på **[!UICONTROL Lägg till alla ändrade resurser]**.
Nu bör du se alla tillägg, regler och dataelement som listas under [!UICONTROL Resursändringar].
1. Klicka **[!UICONTROL Spara och bygg till utveckling]**.

## Lägg till inbäddningskoden i HTML

Nu måste du lägga till en script-tagg på produktsidan HTML som läser in det nya taggbiblioteket.

1. Starta genom att klicka **[!UICONTROL Miljö]** i den vänstra menyn. Du bör se tre olika miljöer.
   ![Märkordsmiljöer](../assets/tags-environments.png)
1. Klicka på paketikonen på **[!UICONTROL Utveckling]** miljörad under _Installera_ kolumn. Anvisningar om hur du installerar Launch-biblioteksskriptet på sidan finns.
   ![Installationsanvisningar för taggar](../assets/tags-installation-instructions.png)
1. Kopiera skripttaggen (det finns en knapp för att kopiera till Urklipp).
1. Öppna produktsidan HTML och infoga script-taggen före `</head>` -tagg. HTML ska se ut så här:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>Product Page</title>
    <script>
      window.adobeDataLayer = window.adobeDataLayer || [];
      window.adobeDataLayer.push({
        "event": "pageViewed",
        "web": {
          "webPageDetails": {
            "name": "Foam Roller",
            "siteSection": "Equipment"
          },
        },
        "productListItems": [
          {
            "SKU": "eqfr08",
            "currencyCode": "USD",
            "name": "Foam Roller",
            "priceTotal": 18.95
          }
        ]
      });
      window.adobeDataLayer.push({
        "event": "productViewed"
      });
      window.onAddToCartClick = function() {
        // In a real implementation, you would change this condition to 
        // only pass if a cart doesn't already exist. You would typically 
        // do this by checking a cookie or variable value.
        if (true) {
          window.adobeDataLayer.push({
            "event": "cartOpened",
          });
        }
        window.adobeDataLayer.push({
          "event": "productAddedToCart"
        });
      };
      window.onDownloadAppClick = function() {
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
      };
    </script>
    <!--Swap this script tag with your own-->
    <script src="https://assets.adobedtm.com/xxxxxxxxxxxx/xxxxxxxxxxxx/launch-xxxxxxxxxxxx-development.min.js" async></script>
  </head>
  <body>
    <h1>Foam Roller</h1>
    <p>This foam roller is composed of durable material that holds its shape and delivers deep tissue therapy. Purchase now for only $18.95!</p>
    <button type="button" onclick="onAddToCartClick()">Add to cart</button>
    <a href="https://example.com/download" onclick="onDownloadAppClick()">Download the app</a>
  </body>
</html>
```

Kolla in [publiceringsdokumentation för taggar](https://experienceleague.adobe.com/docs/experience-platform/tags/publish/overview.html) om du vill veta mer om publiceringsprocessen.

Nu ska du testa din nya implementering!

[Nästa: ](../test-the-implementation.md)

>[!NOTE]
>
>Tack för att du har lagt ned din tid på att lära dig om datainsamling. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela med dig av dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)
