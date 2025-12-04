---
title: Implementera Brand Concierge på din webbplats
description: Implementera Brand Concierge på din webbplats
kt: 5342
doc-type: tutorial
source-git-commit: ea5fa4694205a94f63d277fdcf2018951fa31fbc
workflow-type: tm+mt
source-wordcount: '1335'
ht-degree: 0%

---

# 1.4.2 Implementera Brand Concierge på din webbplats

>[!IMPORTANT]
>
>För att slutföra den här övningen måste du ha tillgång till en fungerande AEM Assets CS-redigeringsmiljö och en AEM CS/EDS-webbplats.
>
>Om du inte har någon sådan miljö går du till [Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./../../../modules/asset-mgmt/module2.1/aemcs.md){target="_blank"}. Följ instruktionerna där så får du tillgång till en sådan miljö.

>[!IMPORTANT]
>
>Om du tidigare har konfigurerat ett AEM CS-program med en AEM Assets CS-miljö kan det bero på att din AEM CS-sandlåda är i viloläge. Eftersom det tar 10-15 minuter att dölja en sådan sandlåda, är det en bra idé att starta separationsprocessen nu så att du inte behöver vänta på den vid ett senare tillfälle.

## 1.4.2.1 Konfigurera webbplatsen så att Brand Concierge - AEM Author visas

För att Brand Concierge ska kunna visas på din webbplats måste du skapa ett nytt anpassat block som ska läggas till på en ny sida, och du måste se till att den nya sidan läggs till i navigeringen på din webbplats.

Du måste nu konfigurera följande i den här ordningen:

- Skapa ett nytt anpassat block som ska användas för att läsa in Brand Concierge på din webbplats.
- Skapa en ny sida för Brand Concierge på din webbplats.
- Länka det nya anpassade blocket till den nya Brand Concierge-sidan.
- Lägg till en referens för att navigera till den nya Brand Concierge-sidan i webbplatsens navigeringsrubrikfil.

### Skapa nytt anpassat block

Om du vill skapa det nya anpassade blocket navigerar du till GitHub-databasen som är länkad till din webbplats.

![Blockera](./images/block1.png)

#### component-definition.json

Bläddra nedåt tills du ser filen **component-definition.json** och öppna den

![Blockera](./images/block8.png)

Klicka på ikonen **pencl** för att börja redigera filen.

![Blockera](./images/block8a.png)

Bläddra nedåt tills du ser **blocken**. Ställ in markören under den avslutande parentesen för komponenten **Cards**

![Blockera](./images/block9.png)

Klistra in den här koden och ange ett kommatecken **,** efter kodblocket:

```json
{
  "title": "BrandConcierge",
  "id": "brandconcierge",
  "plugins": {
    "xwalk": {
      "page": {
        "resourceType": "core/franklin/components/block/v1/block",
        "template": {
          "name": "BrandConcierge",
          "model": "brandconcierge"
        }
      }
    }
  }
},
```

Klicka på **Verkställ ändringar..**.

![Blockera](./images/block10.png)

Klicka på **Verkställ ändringar**.

![Blockera](./images/block10a.png)

#### component-models.json

Bläddra nedåt tills du ser filen **component-models.json** och klicka på ikonen **pencil** för att börja redigera filen.

![Blockera](./images/block11.png)

Bläddra nedåt tills du ser det sista objektet. Placera markören bredvid den sista komponentens avslutande parentes.

![Blockera](./images/block12.png)

Ange ett kommatecken **,**, tryck sedan på Retur och klistra in koden på nästa rad:

```json
{
  "id": "brandconcierge",
  "fields": []
}
```

Klicka på **Verkställ ändringar..**.

![Blockera](./images/block13.png)

Klicka på **Verkställ ändringar**.

![Blockera](./images/block13a.png)

#### component-filters.json

Bläddra nedåt tills du ser filen **component-filters.json** och klicka på ikonen **penna** för att börja redigera filen.

![Blockera](./images/block14.png)

Du borde se det här då.

![Blockera](./images/block14a.png)

Under **section** anger du ett komma `,` och klistrar in ID:t för komponenten `"brandconcierge"` efter den aktuella sista raden.

Klicka på **Verkställ ändringar..**.

![Blockera](./images/block15.png)

Klicka på **Verkställ ändringar**.

![Blockera](./images/block15a.png)

#### brandconcierge.css

När du skapar ett block är det bäst att skapa en fil för formateringen av blocket, och det bör ha samma namn som blocket. bör du nu skapa den filen, som vi lämnar tom tills vidare.

Gå till mappen **blocks**. Klicka sedan på **Lägg till fil** och välj **Skapa ny fil**.

![Blockera](./images/css1.png)

Ange `brandconcierge/brandconcierge.css` i textrutan. Filen kan vara tom tills vidare. Klicka på **Verkställ ändringar..**.

![Blockera](./images/css2.png)

Klicka på **Verkställ ändringar**.

![Blockera](./images/css3.png)

#### brandconcierge.js

När du skapar ett block är det bäst att skapa en fil för javascript-objektet som hör till blocket, och det bör ha samma namn som blocket.

Klicka på **Lägg till fil** och välj **Skapa ny fil**.

![Blockera](./images/js1.png)

Ange `brandconcierge.js` i textrutan. Filen kan vara tom tills vidare. Klicka på **Verkställ ändringar..**.

```javascript
export default function decorate(block) {
  block.setAttribute('id', 'brand-concierge-mount');
}
```

![Blockera](./images/js2.png)

Klicka på **Verkställ ändringar**.

![Blockera](./images/js3.png)

### Skapa ny sida och länka nytt anpassat block

Gå till [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. Klicka på ditt **program** för att öppna det.

![AEMCS](./images/aemcs6.png)

Klicka sedan på de 3 punkterna **..** på fliken **Miljö** och klicka på **Visa detaljer**.

![AEMCS](./images/aemcs9.png)

Du kommer då att se din miljöinformation. Klicka på URL:en för din **författarmiljö**.

>[!NOTE]
>
>Det är möjligt att din miljö är i viloläge. Om så är fallet måste du avviloera din miljö först.

![AEMCS](./images/aemcs10.png)

Du bör då se din AEM Author-miljö. Gå till **Webbplatser**.

![AEMCS](./images/block21.png)

Gå till **CitiSignal**. Klicka på **Skapa** och välj **Sida**.

![AEMCS](./images/block23.png)

Välj **Sida** och klicka på **Nästa**.

![AEMCS](./images/block24.png)

Ange följande värden:

- Titel: **Brand Concierge**
- Namn: **brandconcierge**
- Sidtitel: **Brand Concierge**

Klicka på **Skapa**.

![AEMCS](./images/block25.png)

Välj **Öppna**.

![AEMCS](./images/block22.png)

Du borde se det här då.

![AEMCS](./images/block26.png)

Klicka i det tomma området för att markera komponenten **section**. Klicka sedan på plusikonen **+** på den högra menyn.

![AEMCS](./images/block27.png)

Du bör sedan se ditt anpassade block visas i listan med tillgängliga block. Klicka för att markera den.

![AEMCS](./images/block28.png)

Du bör då se ett tomt block som läggs till på den här sidan. Det här blocket läses in dynamiskt med de javacript-bibliotek som du lägger till i nästa steg.

Klicka på **Publicera**.

![AEMCS](./images/block29.png)

Klicka på **Publicera** igen.

![AEMCS](./images/block30.png)

Den nya sidan publiceras nu och kan nu läggas till i navigeringsrubriken i nästa steg.

### Uppdatera navigeringsrubrikfil

Gå till **CitiSignal** i översikten för AEM Sites och markera kryssrutan för filen **Header/nav**. Klicka på **Redigera**.

![AEMCS](./images/nav0.png)

Markera fältet **Text** på förhandsgranskningsskärmen och klicka sedan på fältet **Text** till höger på skärmen för att redigera det.

![AEMCS](./images/nav0a.png)

Skapa ett nytt menyalternativ på navigeringsmenyn med texten `Brand Concierge`. Markera sedan texten **Brand Concierge** och klicka på ikonen **link** .

![AEMCS](./images/nav1.png)

Ange detta för fältet **Sökväg eller URL** `/content/CitiSignal/brandconcierge.html` och ange `Brand Concierge` som fältnamn **Titel**. Klicka på **Spara**.

![AEMCS](./images/nav3.png)

Du borde ha den här då. Klicka på **Klar**.

![AEMCS](./images/nav4.png)

Du borde ha den här då. Klicka på **Publicera**.

![AEMCS](./images/nav4a.png)

Klicka på **Publicera** igen.

![AEMCS](./images/nav5.png)

Den nya sidan läggs nu till på menyn.

## 1.4.2.2 Konfigurera din webbplats så att den visar Brand Concierge - GitHub

När du har uppdaterat innehållet i AEM Author-miljön måste du nu uppdatera en del av koden i GitHub-databasen som används för webbplatsen.

### JavaScript-bibliotek

Följande bibliotek krävs för att implementera Brand Concierge på din webbplats som körs på AEM CS/EDS:

- [styleconfigurations.js](./assets/styleconfigurations.js)
- [alloy.js](./assets/alloy.js)
- [brandconciergemain.js](./assets/brandconciergemain.js)

Ladda ned alla tre filerna till skrivbordet.

![Brand Concierge](./images/aem0.png)

Gå till GitHub-projektet på din AEM CS/EDS-webbplats. Gå till **skript**.

![Brand Concierge](./images/aem1.png)

Klicka på **Lägg till fil** och välj sedan **Överför filer**.

![Brand Concierge](./images/aem3.png)

Klicka på **Välj dina filer**.

![Brand Concierge](./images/aem3a.png)

Markera alla 3 filerna **styleConfigurations.js, alloy.js och brandconciergemain.js** på skrivbordet och klicka på **Öppna**.

![Brand Concierge](./images/aem4.png)

Klicka på **Verkställ ändringar**.

![Brand Concierge](./images/aem5.png)

### Uppdatera head.html

I föregående steg överförde du tre nya bibliotek. Dessa bibliotek måste nu läsas in när webbplatsen har lästs in och du kan göra det genom att lägga till referenser till dessa filer i filen **head.html**.

Dessutom måste du ange instruktioner i filen **head.html** för att se till att biblioteken läses in i rätt ordning och på rätt sätt.

Gå till GitHub-projektet på AEM CS/EDS-webbplatsen genom att klicka på **Kod**.

![Brand Concierge](./images/aem6.png)

Rulla ner lite. Öppna filen **head.html**.

![Brand Concierge](./images/aem7.png)

Klicka på ikonen **penna** om du vill redigera filen.

![Brand Concierge](./images/aem8.png)

Du borde se det här då.

![Brand Concierge](./images/aem9.png)

Rulla ned till rad 43 och klistra in följande:

Det finns två fält i nedanstående kod som du behöver uppdatera:

>[!IMPORTANT]
>
>- **datastreamId** är för närvarande inställt på &quot;XXXXX&quot; och måste ersättas med ID:t för datastream som du skapade i föregående steg.
>- **orgId** måste ersättas av IMS-organisations-ID:t för din Adobe Experience Cloud-instans.

```javascript
<script src="/scripts/styleconfigurations.js"></script>

<script>
		!function (n, o) {
      o.forEach(function (o) {
        n[o] || ((n.__alloyNS = n.__alloyNS ||
          []).push(o), n[o] = function () {
            var u = arguments; return new Promise(
              function (i, l) { n[o].q.push([i, l, u]) })
          }, n[o].q = [])
      })
    }
      (window, ["alloy"]);
	</script>


<script src="/scripts/alloy.js"></script>

<script>
	alloy("configure", {
		defaultConsent: "in",
        edgeDomain: "edge.adobedc.net",
        edgeBasePath: "ee",
        datastreamId: "XXXXX", // replace datastreamId
        orgId: "--aepImsOrgId--", // replace ims org Id
        debugEnabled: true,
        idMigrationEnabled: false,
        thirdPartyCookiesEnabled: false,
        prehidingStyle: ".personalization-container { opacity: 0 !important }",
    });

window["alloy"]("sendEvent", {
    conversation: {
        fetchConversationalExperience: true
    }
}).then(result => {
    console.log("Conversation experience fetched", result);
    window["alloy"]("bootstrapConversationalExperience", {
        selector: "#brand-concierge-mount",
        src: "/scripts/brandconciergemain.js",
        stylingConfigurations: window.styleConfiguration,
        stickySession: true // create a sticky session cookie with expiration
    })
});
</script>
```

Klicka på **Verkställ ändring..**.

![Brand Concierge](./images/aem10.png)

Klicka på **Verkställ ändring**.

![Brand Concierge](./images/aem11.png)

Du har nu uppdaterat den kod som krävs för att läsa in biblioteken på webbplatsen.

![Brand Concierge](./images/aem12.png)

## 1.4.2.3 Testa konfigurationen

Du kan nu testa dina ändringar på din webbplats genom att gå till `main--citisignal-aem-accs--XXX.aem.page` eller `main--citisignal-aem-accs--XXX.aem.live` efter att du har ersatt XXX med ditt GitHub-användarkonto, som i det här exemplet är `woutervangeluwe`.

I det här exemplet blir den fullständiga URL:en följande:
`https://main--citisignal-aem-accs--woutervangeluwe.aem.page` och/eller `https://main--citisignal-aem-accs--woutervangeluwe.aem.live`.

Det kan ta en stund innan alla resurser visas korrekt, eftersom de måste publiceras först.

Du borde se det här då. Klicka på **Brand Concierge**.

![Brand Concierge](./images/aem13.png)

Du bör då se denna Brand Concierge där du kan skriva din uppmaning.

![Brand Concierge](./images/aem14.png)

Gå tillbaka till [Brand Concierge](./brandconcierge.md){target="_blank"}

[Gå tillbaka till alla moduler](./../../../overview.md){target="_blank"}