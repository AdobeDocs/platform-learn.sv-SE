---
title: Implementera ett datalager på en produktsida
description: Implementera ett datalager på en produktsida
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: a72011a5-ea9c-45df-a0f3-5eb40bc99d3f
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 0%

---

# Implementera ett datalager på en produktsida

I den här självstudiekursen implementerar du Adobe Client Data Layer för en vanlig e-handelswebbplats. Om du inte redan har gjort det, läs [Så här använder du datalagret för klienten i Adobe](how-to-use-the-adobe-client-data-layer.md) först för att förstå hur Adobe klientdatalager fungerar.

Låt oss anta att användaren bläddrar bland dina produkter och klickar på en skumrulle för att få veta mer. Användaren kommer till informationssidan för skumrullen.

Här är HTML för din enkla produktinformationssida:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>Product Page</title>
    <script>
      // Code will go here.
    </script>
  </head>
  <body>
    <h1>Foam Roller</h1>
    <p>This foam roller is composed of durable material that holds its shape and delivers deep tissue therapy. Purchase now for only $18.95!</p>
    <button type="button">Add to cart</button>
    <a href="https://example.com/download">Download the app</a>
  </body>
</html>
```

Som du kanske har märkt, finns det `<head>` -taggen finns det en `<script>` -tagg. Här placerar du JavaScript-koden. Du behöver inte placera `<script>` tagga inuti `<head>`, men om data flyttas till datalagret så snart som möjligt blir det snabbt tillgängligt för marknadsföraren att skicka till Adobe Experience Platform innan användaren lämnar sidan.

Innanför `<script>` börjar du med att skapa `adobeDataLayer` och sedan överföra lämplig händelse- och datainformation till arrayen. Data överensstämmer med XDM-schemat [du skapade tidigare](../configure-the-server/create-a-schema.md).

```js
window.adobeDataLayer = window.adobeDataLayer || [];
window.adobeDataLayer.push({
  "event": "pageViewed",
  "web": {
    "webPageDetails": {
      "name": "Foam Roller",
      "siteSection": "Equipment"
    },
  }
});
window.adobeDataLayer.push({
  "event": "productViewed",
  "productListItems": [
    {
      "SKU": "eqfr08",
      "currencyCode": "USD",
      "name": "Foam Roller",
      "priceTotal": 18.95
    }
  ]
});
```

I det här exemplet har du gjort två penslar till datalagret som vart och ett innehåller en `event` nyckel. Inklusive `event` key kommunicerar inte bara vilken händelse som har inträffat på sidan, utan gör det också enklare för marknadsföraren att skapa lämpliga regler i Adobe Experience Platform Tags.

Den första push-åtgärden till datalagret meddelar avlyssnare (taggregler) att användaren har visat sidan. Dessutom läggs sidnamnet och webbplatsavsnittet till i datalagret.

Den andra push-åtgärden till datalagret meddelar avlyssnare (taggregler) att användaren har visat en produkt. Det lägger också till produktinformation i datalagret.

## Lägg i kundvagnen

Du vill antagligen också spåra när användaren klickar på [!UICONTROL Lägg i kundvagnen] -knappen.

Om du vill göra det skapar du en funktion som anropas när användaren klickar på [!UICONTROL Lägg i kundvagnen] -knappen.

```js
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
```

När den här funktionen anropas kontrollerar den först om det redan finns en kundvagn för en användare. Detta görs vanligtvis genom att kontrollera om det finns en viss cookie eller variabel. Om vagnen inte finns trycker du på `cartOpened` -händelsen i datalagret. Därefter trycker du på `productAddedToCart` -händelsen i datalagret. Produktinformationen finns redan i datalagret, så du behöver inte lägga till den igen.

Lägg till en `onclick` attributet till [!UICONTROL Lägg i kundvagnen] knapp som anropar din nya `onAddToCartClick` funktion.

Resultatet av HTML-sidan ska se ut så här:

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
    </script>
  </head>
  <body>
    <h1>Foam Roller</h1>
    <p>This foam roller is composed of durable material that holds its shape and delivers deep tissue therapy. Purchase now for only $18.95!</p>
    <button type="button" onclick="onAddToCartClick()">Add to cart</button>
    <a href="https://example.com/download">Download the app</a>
  </body>
</html>
```

## Ladda ned appen

En sista sak att göra är att spåra när användaren klickar på _[!UICONTROL Ladda ned appen]_ länk.

Om du vill göra det skapar du en funktion som anropas när användaren klickar på _[!UICONTROL Ladda ned appen]_ länk.

```js
window.onDownloadAppClick = function(event) {
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
```

I det här fallet är informationen om länken inkapslad i en `eventInfo` nyckel. Som beskrivs i [Så här använder du datalagret för klienten i Adobe](how-to-use-the-adobe-client-data-layer.md)anger detta att datalagret ska kommunicera dessa data tillsammans med händelsen, men till _not_ bevara data i datalagret. För en länkklickning är det inte praktiskt att lägga till information om den klickade länken till datalagret eftersom den inte gäller hela sidan och inte gäller för andra händelser som kan inträffa.

Lägg till en `onclick` attributet till [!UICONTROL Ladda ned appen] länk som anropar din nya `onDownloadAppClick` funktion.

Resultatet av HTML-sidan ska se ut så här:

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
  </head>
  <body>
    <h1>Foam Roller</h1>
    <p>This foam roller is composed of durable material that holds its shape and delivers deep tissue therapy. Purchase now for only $18.95!</p>
    <button type="button" onclick="onAddToCartClick()">Add to cart</button>
    <a href="https://example.com/download" onclick="onDownloadAppClick()">Download the app</a>
  </body>
</html>
```
