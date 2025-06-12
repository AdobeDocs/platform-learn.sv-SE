---
title: AEM CS - grundläggande anpassat block
description: AEM CS - grundläggande anpassat block
kt: 5342
doc-type: tutorial
exl-id: 57c08a88-d885-471b-ad78-1dba5992da9d
source-git-commit: 457e7d0dec233edf75717fb9930585a3511bdc65
workflow-type: tm+mt
source-wordcount: '814'
ht-degree: 1%

---

# 1.1.4 Utveckla ett enkelt anpassat block

## 1.1.4.1 Konfigurera din lokala utvecklingsmiljö

Gå till [https://desktop.github.com/download/](https://desktop.github.com/download/){target="_blank"}, hämta och installera **Github Desktop**.

![Blockera](./images/block1.png){zoomable="yes"}

När du har installerat Github Desktop går du till GitHub-versionen som du skapade i föregående övning. Klicka på **&lt;> Kod** och sedan på **Öppna med GitHub Desktop**.

![Blockera](./images/block2.png){zoomable="yes"}

Din GitHub-repo öppnas sedan i GitHub Desktop. Du kan ändra den **lokala sökvägen**. Klicka på **Klona**.

![Blockera](./images/block3.png){zoomable="yes"}

En lokal mapp kommer nu att skapas.

![Blockera](./images/block4.png){zoomable="yes"}

Öppna Visual Studio-kod. Gå till **Arkiv** > **Öppna mapp**.

![Blockera](./images/block5.png){zoomable="yes"}

Välj den mapp som används av GitHub-konfigurationen för **citisignal**.

![Blockera](./images/block6.png){zoomable="yes"}

Nu ser du att mappen är öppen i Visual Studio Code. Nu kan du skapa ett nytt block.

![Blockera](./images/block7.png){zoomable="yes"}

## 1.1.4.2 Skapa ett enkelt anpassat block

Adobe rekommenderar att du utvecklar block i tre faser:

- Skapa definitionen och modellen för blocket, granska det och ta det till produktion.
- Skapa innehåll med det nya blocket.
- Implementera dekoration och stilar för det nya blocket.

### component-definition.json

Öppna filen **component-definition.json** i Visual Studio Code.

![Blockera](./images/block8.png){zoomable="yes"}

Bläddra nedåt tills du ser komponenten **Quote**. Placera markören bredvid den sista komponentens avslutande parentes.

![Blockera](./images/block9.png){zoomable="yes"}

Klistra in den här koden och ange ett kommatecken **,** efter kodblocket:

```json
{
  "title": "FiberOffer",
  "id": "fiberoffer",
  "plugins": {
    "xwalk": {
      "page": {
        "resourceType": "core/franklin/components/block/v1/block",
        "template": {
          "name": "FiberOffer",
          "model": "fiberoffer",
          "offerText": "<p>Fiber will soon be available in your region!</p>",
          "offerCallToAction": "Get your offer now!",
          "offerImage": ""
        }
      }
    }
  }
}
```

Spara ändringarna.

![Blockera](./images/block10.png){zoomable="yes"}

### component-models.json

Öppna filen **component-models.json** i Visual Studio Code.

![Blockera](./images/block11.png){zoomable="yes"}

Bläddra nedåt tills du ser det sista objektet. Placera markören bredvid den sista komponentens avslutande parentes.

![Blockera](./images/block12.png){zoomable="yes"}

Ange ett kommatecken **,**, tryck sedan på Retur och klistra in koden på nästa rad:

```json
{
  "id": "fiberoffer",
  "fields": [
     {
       "component": "richtext",
       "name": "offerText",
       "value": "",
       "label": "Offer Text",
       "valueType": "string"
     },
     {
       "component": "richtext",
       "valueType": "string",
       "name": "offerCallToAction",
       "label": "Offer CTA",
       "value": ""
     },
     {
       "component": "reference",
       "valueType": "string",
       "name": "offerImage",
       "label": "Offer Image",
        "multi": false
     }
   ]
}
```

Spara ändringarna.

![Blockera](./images/block13.png){zoomable="yes"}

### component-filters.json

Öppna filen **component-filters.json** i Visual Studio-koden.

![Blockera](./images/block14.png){zoomable="yes"}

Under **section** anger du ett kommatecken **,** och ID:t för din komponent, **defiffer**, efter den aktuella sista raden.

Spara ändringarna.

![Blockera](./images/block15.png){zoomable="yes"}

## 1.1.4.3 Genomför dina ändringar

Du har nu gjort flera ändringar i ditt projekt som behöver implementeras i GitHub-databasen igen. Öppna **GitHub Desktop** om du vill göra det.

Du bör sedan se de 3 filer som du just redigerade under **Ändringar**. Granska ändringarna.

![Blockera](./images/block16.png){zoomable="yes"}

Ange ett namn för din PR, `Fiber Offer custom block`. Klicka på **Verkställ för huvudsidan**.

![Blockera](./images/block17.png){zoomable="yes"}

Du borde se det här då. Klicka på **Push origin**.

![Blockera](./images/block18.png){zoomable="yes"}

Efter några sekunder har dina ändringar överförts till din GitHub-databas.

![Blockera](./images/block19.png){zoomable="yes"}

Gå till ditt GitHub-konto i webbläsaren och till databasen som du skapade för CitiSignal. Du bör då se något liknande och visa att dina ändringar har tagits emot.

![Blockera](./images/block20.png){zoomable="yes"}

## 1.1.4.4 Lägg till blocket på en sida

Nu när ditt grundläggande offertblock har definierats och implementerats i CitiSignal-projektet kan du lägga till ett **fiberoffer** -block på en befintlig sida.

Gå till [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. Klicka på ditt **program** för att öppna det.

![AEMCS](./images/aemcs6.png){zoomable="yes"}

Klicka sedan på de 3 punkterna **..** på fliken **Miljö** och klicka på **Visa detaljer**.

![AEMCS](./images/aemcs9.png){zoomable="yes"}

Du kommer då att se din miljöinformation. Klicka på URL:en för din **författarmiljö**.

>[!NOTE]
>
>Det är möjligt att din miljö är i viloläge. Om så är fallet måste du avviloera din miljö först.

![AEMCS](./images/aemcs10.png){zoomable="yes"}

Du bör då se din AEM Author-miljö. Gå till **Webbplatser**.

![AEMCS](./images/block21.png){zoomable="yes"}

Gå till **CitiSignal** > **us** > **en**.

![AEMCS](./images/block22.png){zoomable="yes"}

Klicka på **Skapa** och välj **Sida**.

![AEMCS](./images/block23.png){zoomable="yes"}

Välj **Sida** och klicka på **Nästa**.

![AEMCS](./images/block24.png){zoomable="yes"}

Ange följande värden:

- Titel: **CitiSignal Fiber**
- Namn: **citisign-fiber**
- Sidrubrik: **CitiSignal Fiber**

Klicka på **Skapa**.

![AEMCS](./images/block25.png){zoomable="yes"}

Du borde se det här då.

![AEMCS](./images/block26.png){zoomable="yes"}

Klicka i det tomma området för att markera komponenten **section**. Klicka sedan på plusikonen **+** på den högra menyn.

![AEMCS](./images/block27.png){zoomable="yes"}

Du bör sedan se ditt anpassade block visas i listan med tillgängliga block. Klicka för att markera den.

![AEMCS](./images/block28.png){zoomable="yes"}

Då visas fält som **Erbjud text**, **Erbjud CTA** och **Erbjud bild** som läggs till i redigeraren. Klicka på **+ Lägg till** i fältet **Erbjud bild** för att välja en bild.

![AEMCS](./images/block29.png){zoomable="yes"}

Du borde se det här då. Klicka för att öppna mappen **citisign**.

![AEMCS](./images/blockpub1.png){zoomable="yes"}

Välj bilden **product-enrichment-1.png**. Klicka på **Markera**.

![AEMCS](./images/blockpub2.png){zoomable="yes"}

Du borde ha den här då. Klicka på **Publicera**.

![AEMCS](./images/blockpub3.png){zoomable="yes"}

Klicka på **Publicera** igen.

![AEMCS](./images/blockpub4.png){zoomable="yes"}

Din nya sida har publicerats.

## 1.1.4.5 Lägg till din nya sida på navigeringsmenyn

Gå till **CitiSignal** > **Fragment** i AEM Sites-översikten och markera kryssrutan för **Header**. Klicka på **Redigera**.

![AEMCS](./images/nav0.png){zoomable="yes"}

Lägg till ett menyalternativ på navigeringsmenyn med texten `Fiber`. Markera texten **Fiber** och klicka på ikonen **link** .

![AEMCS](./images/nav1.png){zoomable="yes"}

Ange den här för **URL** `/us/en//citisignal-fiber` och klicka på ikonen **V** för att bekräfta.

![AEMCS](./images/nav3.png){zoomable="yes"}

Du borde ha den här då. Klicka på **Publicera**.

![AEMCS](./images/nav4.png){zoomable="yes"}

Klicka på **Publicera** igen.

![AEMCS](./images/nav5.png){zoomable="yes"}

Du kan nu visa ändringarna av din webbplats genom att gå till `main--citisignal--XXX.aem.page/us/en/` och/eller `main--citisignal--XXX.aem.live/us/en/` efter att du ersatt XXX med ditt GitHub-användarkonto, som i det här exemplet är `woutervangeluwe`.

I det här exemplet blir den fullständiga URL:en följande:
`https://main--citisignal--woutervangeluwe.aem.page/us/en/` och/eller `https://main--citisignal--woutervangeluwe.aem.live/us/en/`.

Du borde se det här då. Klicka på **Fiber**.

![AEMCS](./images/nav6.png){zoomable="yes"}

Här är ditt grundläggande anpassade block, men det återges nu på webbplatsen.

![AEMCS](./images/nav7.png){zoomable="yes"}

Nästa steg: [1.1.5 Avancerat anpassat block](./ex5.md){target="_blank"}

Gå tillbaka till [Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./aemcs.md){target="_blank"}

[Gå tillbaka till alla moduler](./../../../overview.md){target="_blank"}
