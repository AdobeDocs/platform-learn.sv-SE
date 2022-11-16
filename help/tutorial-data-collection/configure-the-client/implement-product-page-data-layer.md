---
title: Implementera ett datalager på en produktsida
description: Implementera ett datalager på en produktsida
exl-id: 0debf34a-48d4-4029-b790-7fd78865c334
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 0%

---

# Implementera ett datalager på en produktsida

I den här självstudiekursen implementerar du Adobe Client Data Layer för en vanlig e-handelswebbplats. Om du inte redan har gjort det, läs [Så här använder du datalagret för klienten i Adobe](how-to-use-the-adobe-client-data-layer.md) först med att förstå Adobe-klientdatalagret.

Låt oss anta att användaren bläddrar bland dina produkter och klickar på en skumrulle för att få veta mer. Användaren kommer till informationssidan för skumrullen.

## Skapa en enkel produktinformationssida

1. Kopiera och klistra in följande kod i en ny HTML-fil och spara den på datorn.

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

Innanför `<head>` -taggen finns det en `<script>` -tagg. Här placerar du JavaScript-koden. Du behöver inte placera `<script>` -taggen inuti `<head>` rekommenderas. Detta garanterar att data blir tillgängliga för datalagret så snart som möjligt för att stödja en mängd olika användningsfall.

## Lägg till datalagret Adobe

1. Innanför `<script>` lägger du till koden som skapar `adobeDataLayer` och sedan överför lämplig händelse- och datainformation till arrayen. Data överensstämmer med XDM-schemat [du skapade tidigare](../configure-the-server/create-a-schema.md).

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

I det här exemplet har du gjort två penslar till datalagret som vart och ett innehåller en `event` nyckel. Inklusive `event` -tangenten kommunicerar inte bara vilken händelse som har inträffat på sidan, utan gör det också enklare för marknadsföraren att skapa lämpliga regler inuti -taggar.

Den första överföringen till datalagret meddelar avlyssnare (taggregler) att användaren har visat sidan. Dessutom läggs sidnamnet och webbplatsavsnittet till i datalagret.

Den andra överföringen till datalagret meddelar avlyssnare (taggregler) att användaren har visat en produkt. Det lägger också till produktinformation i datalagret.

## Lägg till kod för kundvagn för att lägga till spårning

I den här självstudiekursen håller du reda på när användaren klickar på [!UICONTROL Lägg i kundvagnen] -knappen.

1. Kopiera och klistra in koden efter datalagerkoden. Funktionen anropas när användaren klickar på [!UICONTROL Lägg i kundvagnen] -knappen.

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

Den här funktionen kontrollerar först om det redan finns en kundvagn för en användare.  Om kundvagnen inte finns trycker du på `cartOpened` -händelsen till datalagret. Senare trycker du på `productAddedToCart` -händelsen i datalagret. Produktinformationen finns redan i datalagret, så du behöver inte lägga till den igen.

## Lägg till attribut till kundvagnsknappen

1. Lägg till en `onclick` attributet till [!UICONTROL Lägg i kundvagnen] knapp som anropar din nya `onAddToCartClick` funktion.

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

## Lägg till kod för uppföljning av appnedladdning

En sista sak att spåra är när användaren klickar på _[!UICONTROL Ladda ned appen]_ länk.

1. Om du vill göra det kopierar och klistrar du in koden under kundvagnen och lägger till kod. Den här funktionen anropas när användaren klickar på _[!UICONTROL Ladda ned appen]_ länk.

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

## Lägg till attribut för att hämta applänken

1. Lägg till en `onclick` attributet till [!UICONTROL Ladda ned appen] länk som anropar din nya `onDownloadAppClick` funktion.

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

[Nästa: ](create-a-tags-property-and-install-extensions.md)

>[!NOTE]
>
>Tack för att du har lagt ned din tid på att lära dig om datainsamling. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela med dig av dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)
