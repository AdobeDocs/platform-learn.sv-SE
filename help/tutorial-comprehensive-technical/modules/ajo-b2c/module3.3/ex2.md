---
title: Offer decisioning - Konfigurera erbjudanden och beslut-ID
description: Offer decisioning - Konfigurera erbjudanden och beslut-ID
kt: 5342
doc-type: tutorial
exl-id: 1418398b-d192-4d0b-b372-4be73fc153ed
source-git-commit: c531412a2c0a5c216f49560e01fb26b9b7e71869
workflow-type: tm+mt
source-wordcount: '1428'
ht-degree: 1%

---

# 3.3.2 Konfigurera erbjudanden och beslut

## 3.3.2.1 Skapa personaliserade erbjudanden

I den här övningen skapar du fyra **Personaliserade erbjudanden**. Här följer de uppgifter som ska beaktas när erbjudandena skapas:

| Namn | Datumintervall | Bildlänk för e-post | Bildlänk för webben | Text | Prioritet | Kvalificering | Språk |
|-----|------------|----------------------|--------------------|------|:--------:|--------------|:-------:|
| `--aepUserLdap-- - Nadia Elements Shell` | idag - 1 månad senare | https://bit.ly/3nPiwdZ | https://bit.ly/2INwXjt | `{{ profile.person.name.firstName }}, 10% discount on Nadia Elements Shell` | 25 | alla - kvinnliga kunder | Engelska (USA) |
| `--aepUserLdap-- - Radiant Tee` | idag - 1 månad senare | https://bit.ly/2HfA17v | https://bit.ly/3pEIdzn | `{{ profile.person.name.firstName }}, 5% discount on Radiant Tee` | 15 | alla - kvinnliga kunder | Engelska (USA) |
| `--aepUserLdap-- - Zeppelin Yoga Pant` | idag - 1 månad senare | https://bit.ly/2IOaItW | https://bit.ly/2INZHZd | `{{ profile.person.name.firstName }}, 10% discount on Zeppelin Yoga Pant` | 25 | alla - Manliga kunder | Engelska (USA) |
| `--aepUserLdap-- - Proteus Fitness Jackshirt` | idag - 1 månad senare | https://bit.ly/330a43n | https://bit.ly/36USaQW | `{{ profile.person.name.firstName }}, 5% discount on Proteus Fitness Jackshirt` | 15 | alla - Manliga kunder | Engelska (USA) |

{style="table-layout:auto"}

Logga in på Adobe Journey Optimizer på [Adobe Experience Cloud](https://experience.adobe.com). Klicka på **Journey Optimizer**.

![ACOP](./../../../modules/ajo-b2c/module3.1/images/acophome.png)

Du omdirigeras till vyn **Hem** i Journey Optimizer. Kontrollera först att du använder rätt sandlåda. Sandlådan som ska användas kallas `--aepSandboxName--`. Om du vill ändra från en sandlåda till en annan klickar du på **PRODUKTIONSprodukt (VA7)** och väljer sandlådan i listan. I det här exemplet heter sandlådan **AEP Enablement FY22**. Du kommer sedan att vara i vyn **Hem** i din sandlåda `--aepSandboxName--`.

![ACOP](./../../../modules/ajo-b2c/module3.1/images/acoptriglp.png)

Klicka på **Erbjudanden** på den vänstra menyn och gå sedan till **Erbjudanden**. Klicka på **+ Skapa erbjudande**.

![Beslutsregel](./images/offers1.png)

Du kommer då att se den här popup-rutan. Välj **Personaliserat erbjudande** och klicka på **Nästa**.

![Beslutsregel](./images/offers2.png)

Du finns nu i vyn **Detaljer**.

![Beslutsregel](./images/offers3.png)

I det här fallet måste du konfigurera erbjudandet `--aepUserLdap-- - Nadia Elements Shell`. Använd informationen i tabellen ovan för att fylla i fälten. I det här exemplet är namnet på det anpassade erbjudandet **vangeluw - Nadia Elements Shell**. Ange också **Startdatum och starttid** till igår och **Slutdatum och sluttid** till ett datum om en månad från och med nu.

När du är klar, borde du ha den här. Klicka på **Nästa**.

![Beslutsregel](./images/offers4.png)

Du måste nu skapa **representationer**. Representationer är en kombination av en **placering** och en verklig resurs.

För **Representation 1** väljer du:

- Kanal: Webb
- Placering: Webb - Bild
- Innehåll: URL
- Offentlig plats: kopiera URL:en från kolumnen **Bildlänk för webben** i tabellen ovan

![Beslutsregel](./images/addcontent1.png)

Du kan också välja **Resursbibliotek** för innehållet och sedan klicka på **Bläddra**.

![Beslutsregel](./images/addcontent2.png)

Därefter visas en popup-meny i Assets-biblioteket, gå till mappen **enablement-assets** och markera bildfilen **nadia-web.png**. Klicka sedan på **Markera**.

![Beslutsregel](./images/addcontent3.png)

Då ser du det här:

![Beslutsregel](./images/addcontentrep20.png)

Klicka på **+ Lägg till representation**.

![Beslutsregel](./images/addrep.png)

Välj **Representation 2**:

- Kanal: E-post
- Placering: E-post - bild
- Innehåll: URL
- Offentlig plats: kopiera URL:en från kolumnen **Bildlänk för e-post** i tabellen ovan

![Beslutsregel](./images/addcontentrep21.png)

Du kan också välja **Resursbibliotek** för innehållet och sedan klicka på **Bläddra**.

![Beslutsregel](./images/addcontent2b.png)

Därefter visas en popup-meny i Assets-biblioteket, gå till mappen **enablement-assets** och markera bildfilen **nadia-email.png**. Klicka sedan på **Markera**.

![Beslutsregel](./images/addcontent3b.png)

Då ser du det här:

![Beslutsregel](./images/addcontentrep20b.png)

Klicka sedan på **+ Lägg till representation**.

![Beslutsregel](./images/addrep.png)

För **representation 3** väljer du:

- Kanal: Icke-digital
- Placement: Non-digital - Text

Sedan måste du lägga till innehåll. I det här fallet innebär det att du lägger till texten som ska användas som en uppmaning till åtgärd.

Klicka på **Lägg till innehåll**.

![Beslutsregel](./images/addcontentrep31.png)

Du kommer då att se den här popup-rutan.

![Beslutsregel](./images/addcontent3text.png)

Välj **Egen text** och fyll i dessa fält:

Titta på fältet **Text** från tabellen ovan och ange den texten här, i det här fallet: `{{ profile.person.name.firstName }}, 10% discount on Nadia Elements Shell`.

Du kommer också att märka att du kan välja valfritt profilattribut och inkludera det som ett dynamiskt fält i erbjudandetexten. I det här exemplet ser fältet `{{ profile.person.name.firstName }}` till att förnamnet på kunden som ska få erbjudandet inkluderas i erbjudandetexten.

Då ser du det här. Klicka på **Spara**.

![Beslutsregel](./images/addcontentrep3text.png)

Du har den här nu. Klicka på **Nästa**.

![Beslutsregel](./images/addcontentrep3textdone.png)

Då ser du det här:

![Beslutsregel](./images/constraints.png)

Välj **Efter definierad beslutsregel** och klicka på ikonen **+** för att lägga till regeln **alla - kvinnliga kunder**.

![Beslutsregel](./images/constraints1.png)

Då ser du det här. Fyll i **Prioritet** enligt tabellen ovan. Klicka på **Nästa**.

![Beslutsregel](./images/constraints2.png)

Därefter visas en översikt över ditt nya **personaliserade erbjudande**.

![Beslutsregel](./images/offeroverview.png)

Klicka slutligen på **Spara och godkänn**.

![Beslutsregel](./images/saveapprove.png)

Du kommer då att se att ditt nya personaliserade erbjudande blir tillgängligt i Översikt över erbjudanden:

![Beslutsregel](./images/offeroverview1.png)

Du bör nu upprepa stegen ovan för att skapa de tre andra personliga erbjudandena för produkterna Radiant Tee, Zeppelin Yoga Pant och Proteus Fitness Jackshirte.

När du är klar bör du visa alla dina erbjudanden på skärmen **Erbjud översikter** för **personaliserade erbjudanden**.

![Slutliga erbjudanden](./images/finaloffers.png)

## 3.3.2.2 Skapa ett reserverbjudande

När du har skapat fyra anpassade erbjudanden bör du nu konfigurera ett **Reserverbjudande**.

Kontrollera att du är i vyn **Erbjudanden**:

![Slutliga erbjudanden](./images/finaloffers.png)

Klicka på **+ Skapa erbjudande**.

![Beslutsregel](./images/createoffer.png)

Du kommer då att se den här popup-rutan. Välj **Reserverbjudande** och klicka på **Nästa**.

![Beslutsregel](./images/foffers2.png)

Då ser du det här:

![Beslutsregel](./images/foffers3.png)

Ange det här namnet för ditt reserverbjudande: `--aepUserLdap-- - Luma Fallback Offer`. Klicka på **Nästa**.

![Beslutsregel](./images/foffers4.png)

Du måste nu skapa **representationer**. Representationer är en kombination av en **placering** och en verklig resurs.

För **Representation 1** väljer du:

- Kanal: Webb
- Placering: Webb - Bild
- Innehåll: URL
- Offentlig plats: `https://bit.ly/3nBOt9h`

![Beslutsregel](./images/addcontent1fb.png)

Du kan också välja **Resursbibliotek** för innehållet och sedan klicka på **Bläddra**.

![Beslutsregel](./images/addcontent2fb.png)

Därefter visas ett popup-fönster i Assets-biblioteket, gå till mappen **enablement-assets** och markera bildfilen **spriteyogastraps-web.png**. Klicka sedan på **Markera**.

![Beslutsregel](./images/addcontent3fb.png)

Då ser du det här:

![Beslutsregel](./images/addcontentrep20fb.png)

Välj **Representation 2**:

- Kanal: E-post
- Placering: E-post - bild
- Innehåll: URL
- Offentlig plats: `https://bit.ly/3nF4qvE`

![Beslutsregel](./images/addcontentrep21fb.png)

Du kan också välja **Resursbibliotek** för innehållet och sedan klicka på **Bläddra**.

![Beslutsregel](./images/addcontent2bfb.png)

Därefter visas ett popup-fönster i Assets-biblioteket, gå till mappen **enablement-assets** och markera bildfilen **spriteyogastraps-email.png**. Klicka sedan på **Markera**.

![Beslutsregel](./images/addcontent3bfb.png)

Då ser du det här:

![Beslutsregel](./images/addcontentrep20bfb.png)

Klicka sedan på **+ Lägg till representation**.

![Beslutsregel](./images/addrep.png)

För **representation 3** väljer du:

- Kanal: Icke-digital
- Placement: Non-digital - Text

Sedan måste du lägga till innehåll. I det här fallet innebär det att du lägger till bildlänken.

Klicka på **Lägg till innehåll**.

![Beslutsregel](./images/addcontentrep21text.png)

Du kommer då att se den här popup-rutan.

![Beslutsregel](./images/addcontent2text.png)

Välj **Egen text** och fyll i dessa fält:

Ange texten `{{ profile.person.name.firstName }}, discover our Sprite Yoga Straps!` och klicka på **Spara**.

![Beslutsregel](./images/faddcontent3text.png)

Då ser du det här. Klicka på **Nästa**.

![Beslutsregel](./images/faddcontentrep3.png)

Därefter visas en översikt över ditt nya **Reserverbjudande**. Klicka på **Slutför**.

![Beslutsregel](./images/fofferoverview.png)

Klicka slutligen på **Spara och godkänn**.

![Beslutsregel](./images/saveapprovefb.png)

På skärmen **Erbjudandeöversikter** ser du nu följande:

![Slutliga erbjudanden](./images/ffinaloffers.png)

## 3.3.2.3 Skapa din samling

En samling används för att **filtrera** ut en delmängd av erbjudanden från listan med personaliserade erbjudanden och använda den som en del av ett beslut för att snabba upp beslutsprocessen.

Gå till **Samlingar**. Klicka på **+ Skapa samling**.

![Beslutsregel](./images/collections.png)

Du kommer då att se den här popup-rutan. Konfigurera din samling så här. Klicka på **Nästa**.

- Samlingsnamn: använd `--aepUserLdap-- - Luma Collection`
- Välj **Skapa statisk samling**.

![Beslutsregel](./images/createcollectionpopup1.png)

På nästa skärm väljer du de fyra **Personaliserade erbjudanden** som du skapade i föregående övning. Klicka på **Spara**.

![Beslutsregel](./images/createcollectionpopup2.png)

Nu ser du det här:

![Beslutsregel](./images/colldone.png)

## 3.3.2.4 Ta ett beslut

I ett beslut kombineras praktik, en samling personaliserade erbjudanden och ett reserverbjudande som slutligen ska användas av Offera decisioningen för att hitta det bästa erbjudandet för en viss profil, baserat på varje enskild personaliserad erbjudandeegenskap som prioritet, begränsning av behörighet och begränsning av antalet användare.

Gå till **Beslut** om du vill konfigurera ditt **beslut**. Klicka på **+ Skapa aktivitet**.

![Beslutsregel](./images/activitydd.png)

Då ser du det här:

![Beslutsregel](./images/activity1.png)

Fyll i fälten så här. Klicka på **Nästa**.

- Namn: `--aepUserLdap-- - Luma Decision`
- Startdatum och starttid: igår
- Slutdatum och sluttid: idag + 1 månad

![Beslutsregel](./images/activity2.png)

På nästa skärm måste du lägga till praktik i beslutsomfattningar. Du måste skapa beslutsomfattningar för placeringarna **Webb - Bild**, **E-post - Bild** och **Ej digital - Text**.

![Beslutsregel](./images/addplacements.png)

Skapa först beslutsomfånget för **Icke-digital - text** genom att välja platsen i listrutan. Klicka sedan på knappen **Lägg till** för att lägga till utvärderingskriterier.

![Beslutsregel](./images/activity3.png)

Markera din samling `--aepUserLdap-- - Luma Collection` och klicka på **Lägg till**.

![Beslutsregel](./images/activity4text.png)

Då ser du det här. Klicka på knappen **-** för att lägga till ett nytt beslutsomfång.

![Beslutsregel](./images/activity5text.png)

Välj placeringen **Webb - bild** och lägg till din samling `--aepUserLdap-- - Luma Collection` under utvärderingskriterier. Klicka sedan på knappen **+** igen för att lägga till ett nytt beslutsområde.

![Beslutsregel](./images/activity6text.png)

Välj placeringen **E-post - bild** och lägg till din samling `--aepUserLdap-- - Luma Collection` under utvärderingskriterier. Klicka sedan på **Nästa**.

![Beslutsregel](./images/activity4.png)

Du måste nu välja ditt **Reserverbjudande**, som har namnet `--aepUserLdap-- - Luma Fallback Offer`. Klicka på **Nästa**.

![Beslutsregel](./images/activity10.png)

Granska ditt beslut. Klicka på **Slutför**.

![Beslutsregel](./images/activity11.png)

Klicka på **Spara och aktivera** på popup-menyn.

![Beslutsregel](./images/activity12.png)

Slutligen kommer du att se ditt beslut i översikten:

![Beslutsregel](./images/activity13.png)

Du har nu konfigurerat ditt beslut. Ditt beslut är nu öppet och kan användas för att leverera optimerade och personaliserade erbjudanden till era kunder i realtid.

Nästa steg: [3.3.3 Förbered din datainsamling-klientegenskap och Web SDK-inställningar för Offer decisioning](./ex3.md)

[Gå tillbaka till modul 3.3](./offer-decisioning.md)

[Gå tillbaka till Alla moduler](./../../../overview.md)
