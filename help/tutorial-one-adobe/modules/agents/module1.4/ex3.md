---
title: Implementera Brand Concierge med datainsamlingstaggar
description: Implementera Brand Concierge med datainsamlingstaggar
kt: 5342
doc-type: tutorial
source-git-commit: 3704abb57e9fa64c2ff6d6914b6da8b46a5f44aa
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---

# 1.4.3 Implementera Brand Concierge med datainsamlingstaggar

>[!IMPORTANT]
>
>Den här övningen är under arbete och är inte färdig än.

## Taggegenskap för datainsamling

Brand Concierge måste skicka data till Adobe Experience Platform. För att göra det måste Web SDK (eller alloy.js) distribueras till din webbplats.

För att göra detta möjligt måste du nu skapa en taggegenskap för datainsamling.

Gå till [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Öppna **datainsamling**.

![Brand Concierge](./images/aep101.png)

Klicka på **Ny egenskap**.

![Brand Concierge](./images/aep102.png)

Ange namnet `--aepUserLdap-- - CitiSignal Website + Brand Concierge` och ange även webbplatsens domän.

Klicka på **Spara**.

![Brand Concierge](./images/aep103.png)

Sök efter din egendom och öppna den sedan.

![Brand Concierge](./images/aep104.png)

Gå till **Tillägg** och sedan till **Katalog**.

![Brand Concierge](./images/aep105.png)

Sök efter `web sdk` och klicka sedan på tillägget **Adobe Experience Platform Web SDK**. Klicka på **Installera**.

![Brand Concierge](./images/aep106.png)

Du borde se det här då. Du behöver bara ange informationen för din datastream här. Det gör du genom att rulla ned lite.

![Brand Concierge](./images/aep107.png)

För alla tre miljöerna **Produktion**, **Förproduktion** och **Utveckling** väljer du följande:

- **Sandbox**: `--aepUserLdap-- - bc`
- **Datastream**: `--aepUserLdap-- - Brand Concierge`

Klicka på **Spara**.

![Brand Concierge](./images/aep108.png)

Du borde se det här då. Gå till **Regler**.

![Brand Concierge](./images/aep108a.png)

Klicka på **Skapa ny regel**.

![Brand Concierge](./images/aep109.png)

Ange namnet: `Homepage`. Klicka sedan på **+ Lägg till** under **HÄNDELSER**.

![Brand Concierge](./images/aep110.png)

Välj följande alternativ:

- **Tillägg**: **Core**
- **Händelsetyp**: **Biblioteket har lästs in (sidan överst)**

Klicka på **Behåll ändringar**.

![Brand Concierge](./images/aep111.png)

Du borde se det här då. Klicka på **+ Lägg till** under **VILLKOR**.

![Brand Concierge](./images/aep112.png)

Välj följande alternativ:

- **Logiktyp**: **Normal**
- **Tillägg**: **Core**
- **Villkorstyp**: **Sökväg utan frågesträng**
- **sökvägen är lika med ...**: ange webbplatsens domän, i det här fallet `https://vangeluw.adobedemosystem.com/`

Klicka på **Behåll ändringar**.

![Brand Concierge](./images/aep113.png)

Du borde se det här då. Klicka på **+ Lägg till** under **ÅTGÄRDER**.

![Brand Concierge](./images/aep114.png)

Välj följande alternativ:

- **Tillägg**: **Core**
- **Åtgärdstyp**: **Anpassad kod**
- **Språk**: **JavaScript**

Klicka på **Öppna redigeraren**.

![Brand Concierge](./images/aep115.png)

Klistra in följande kod:

```javascript
window["alloy"]("sendEvent", {
        conversation: {fetchConversationalExperience: true}
    }).then(result=> {
        console.log("Conversation experience fetched", result);
        window["alloy"]("bootstrapConversationalExperience", {
            selector: "#brand-concierge-mount",
						// src: "main.js",
            src: "https://experience-stage.adobe.net/solutions/experience-platform-brand-concierge-web-agent/static-assets/main.js",
            stylingConfigurations: window.styleConfiguration,
						stickySession: true
        })
    });
```

Klicka på **Spara**.

![Brand Concierge](./images/aep116.png)

Du borde se det här då. Klicka på **Behåll ändringar**.

![Brand Concierge](./images/aep117.png)

Du borde se det här då. Klicka på **Spara**.

![Brand Concierge](./images/aep118.png)

Gå till **Publiceringsflöde**. Klicka på **Lägg till bibliotek**.

![Brand Concierge](./images/aep119.png)

Ange namnet: `Dev`, välj **Utveckling (utveckling)** för miljön och klicka sedan på **Lägg till alla ändrade resurser**.

Klicka på **Spara och skapa för utveckling**.

![Brand Concierge](./images/aep120.png)

Efter några minuter kommer ditt bibliotek att byggas. Vänta tills du ser den **gröna punkten** intill **Dev**. Gå sedan till **Miljöer**.

![Brand Concierge](./images/aep121.png)

Klicka på ikonen **Installera** för miljön **Utveckling**.

![Brand Concierge](./images/aep122.png)

Du borde se det här då. Klicka på knappen **kopiera** för att kopiera sökvägen till ditt bibliotek. Du måste implementera detta på din webbplats.

Bibliotekssökvägen ska se ut så här:
`<script src="https://assets.adobedtm.com/XXXXXXX/XXXXXXXX/launch-XXXXXXXXX-development.min.js" async></script>`

![Brand Concierge](./images/aep123.png)

Gå tillbaka till [Brand Concierge](./brandconcierge.md){target="_blank"}

[Gå tillbaka till alla moduler](./../../../overview.md){target="_blank"}