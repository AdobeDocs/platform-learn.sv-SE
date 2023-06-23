---
title: Publicera biblioteket
description: Publicera biblioteket
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 2fc072df-24f2-4fea-848f-0a973deca2f8
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---

# Publicera biblioteket

Nu är det dags att driftsätta taggbiblioteket på er webbplats.

## Skapa ett bibliotek

Först måste du skapa ett bibliotek som innehåller de tillägg, regler och dataelement som du har skapat. Om du vill skapa ett bibliotek väljer du [!UICONTROL Publiceringsflöde] i den vänstra menyn.

Välj [!UICONTROL Lägg till bibliotek].

Du bör se vyn för att skapa bibliotek.

![skapa taggbibliotek](../../../assets/implementation-strategy/tags-library-creation.png)

Ge biblioteket ett namn, som _Demo_. Välj [!UICONTROL Utveckling] i [!UICONTROL Miljö] listruta. Klicka sedan på [!UICONTROL Lägg till alla ändrade resurser].

Nu bör du se alla tillägg, regler och dataelement som listas under [!UICONTROL Resursändringar]. Klicka [!UICONTROL Spara och bygg till utveckling].

## Lägg till inbäddningskoden i HTML

Nu måste du lägga till en script-tagg på produktsidan HTML som läser in det nya taggbiblioteket.

Starta genom att klicka [!UICONTROL Miljö] i den vänstra menyn. Du bör se tre olika miljöer.

![Märkordsmiljöer](../../../assets/implementation-strategy/tags-environments.png)

Klicka på paketikonen på [!UICONTROL Utveckling] miljörad. Anvisningar om hur du installerar Launch-biblioteksskriptet på sidan finns.

![Installationsanvisningar för taggar](../../../assets/implementation-strategy/tags-installation-instructions.png)

Kopiera skripttaggen (det finns en knapp för att kopiera till Urklipp). Öppna produktsidan HTML och infoga script-taggen före `</head>` -tagg. HTML ska se ut så här:

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
