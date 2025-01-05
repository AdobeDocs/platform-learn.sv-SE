---
title: Adobe Journey Optimizer - Konfigurera en batchbaserad resa
description: I det här avsnittet konfigurerar du en e-postgruppsresa för att skicka ett nyhetsbrev
kt: 5342
doc-type: tutorial
exl-id: 52b2e019-e408-4160-87b7-2aabd0f3c68f
source-git-commit: 9865b5697abe2d344fb530636a1afc3f152a9e8f
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 0%

---

# 3.4.2 Konfigurera en kampanj

Logga in på Adobe Journey Optimizer på [Adobe Experience Cloud](https://experience.adobe.com). Klicka på **Journey Optimizer**.

![ACOP](./../../../modules/ajo-b2c/module3.1/images/acophome.png)

Du omdirigeras till vyn **Hem** i Journey Optimizer. Kontrollera först att du använder rätt sandlåda. Sandlådan som ska användas kallas `--aepSandboxName--`. Du kommer sedan att vara i vyn **Hem** i din sandlåda `--aepSandboxName--`.

![ACOP](./../../../modules/ajo-b2c/module3.1/images/acoptriglp.png)


## 3.4.2.1 Skapa målgrupper

Innan ni skapar er kampanj bör ni definiera den målgrupp som ska ta emot kampanjen. Om du vill skapa en målgrupp går du till **Publiker** på den vänstra menyn. Där ser du alla tidigare målgrupper.

Klicka på **+ Skapa publik**.

![Journey Optimizer](./images/audcampaign1.png)

Välj **Skapa regel** och klicka på **Skapa**.

![Journey Optimizer](./images/audcampaign2.png)

Markera fältet **XDM Individual Profile > Personal Email > Address** och lägg till det på arbetsytan. Ange regelvillkoret till **exists**.

För att undvika att skicka e-postmeddelanden till andra användare i din delade utbildningsmiljö kan du även lägga till ett filter som **Förnamn är lika med -ditt förnamn-**.

Ange målgruppens namn till `--aepUserLdap-- - All customers with email` och klicka på **Publish**.

![Journey Optimizer](./images/audcampaign3.png)

Din målgrupp publiceras nu och kan användas i en kampanj.

## 3.4.2.2 Skapa kampanj för nyhetsbrev

Nu ska ni skapa en kampanj. Till skillnad från den händelsebaserade resan från föregående övning, som bygger på inkommande upplevelsehändelser, målgruppsposter eller utträde för att utlösa en resa för en viss kund, riktar kampanjer sig mot en hel målgrupp en gång med unikt innehåll som nyhetsbrev, engångskampanjer eller allmän information eller regelbundet med liknande innehåll som skickas regelbundet, till exempel födelsedagskampanjer och påminnelser.

Gå till **Kampanjer** på menyn och klicka på **Skapa kampanj**.

![Journey Optimizer](./images/oc43.png)

Välj **Schemalagd - marknadsföring** och klicka på **Skapa**.

![Journey Optimizer](./images/campaign1.png)

Konfigurera följande när kampanjen skapas:

- **Namn**: `--aepUserLdap-- - CitiSignal Newsletter`.
- **Beskrivning**: Månadsnyhetsbrev
- **Identitetstyp**: ändra till e-post

Klicka på **Välj målgrupp**.

![Journey Optimizer](./images/campaign2.png)

För **målgruppen** väljer du målgruppen som du skapade i föregående steg, `--aepUserLdap-- - All customers with email`. Klicka på **Spara**.

![Journey Optimizer](./images/campaign2a.png)

För **åtgärden** väljer du **E-post** och väljer en befintlig **e-postkonfiguration**. Du redigerar innehållet om några minuter.

![Journey Optimizer](./images/campaign3.png)

Välj **På ett visst datum och en viss tid** för **Schemalägg** och ange en valtid.

![Journey Optimizer](./images/campaign4.png)

Nu kan du börja skapa själva e-postmeddelandet. Bläddra lite uppåt och klicka på **Redigera innehåll**.

![Journey Optimizer](./images/campaign5.png)

Då ser du det här. Använd följande för **Subject line**: `Your monthly CitiSignal update has arrived.`. Klicka sedan på **Redigera e-postbrödtext**.

![Journey Optimizer](./images/campaign6.png)

Välj **Design från grunden**.

![Journey Optimizer](./images/campaign7.png)

Då ser du det här. På den vänstra menyn hittar du de strukturkomponenter som du kan använda för att definiera e-postmeddelandets struktur (rader och kolumner).

Dra och släpp 3 gånger en **1:1-kolumn** på arbetsytan, 1 gång en 1:2-kolumn åt vänster och 1 gång en 2:1-kolumn åt höger som ska ge dig den här strukturen:

![Journey Optimizer](./images/campaign8.png)

Gå till **Fragment** på den vänstra menyn. Dra rubriken som du skapade tidigare i [övning 3.1.2.1](./../module3.1/ex2.md) till den första komponenten på arbetsytan. Dra sidfoten som du skapade tidigare i [övning 3.1.2.2](./../module3.1/ex2.md) till den sista komponenten på arbetsytan.

![Journey Optimizer](./images/campaign9.png)

Klicka på ikonen **+** i den vänstra menyn. Gå till **Innehåll** för att börja lägga till innehåll på arbetsytan.

![Journey Optimizer](./images/campaign10.png)

Dra och släpp en **Text**-komponent på den andra raden.

![Journey Optimizer](./images/campaign11.png)

Markera standardtexten i komponenten **Skriv texten här.** och ersätt den med texten nedan. Ändra justeringen till **Centrera**.

```javascript
Hi {{profile.person.name.firstName}}

As a CitiSignal member, you're part of a dynamic community that's constantly evolving to meet your needs. We're committed to delivering innovative solutions that enhance your digital lifestyle and keep you ahead of the curve.

Stay connected.
```

![Journey Optimizer](./images/campaign12.png)

Dra och släpp en **bild**-komponent på den tredje och fjärde raden. Klicka på **Bläddra** på den tredje raden.

![Journey Optimizer](./images/campaign13.png)

Öppna mappen **citi-signal-images**, klicka för att markera bilden **Offer_AirPods.jpg** och klicka på **Select**.

![Journey Optimizer](./images/campaign14.png)

Klicka på **Bläddra** på bildplatshållaren på den fjärde raden.

![Journey Optimizer](./images/campaign15.png)

Öppna mappen **citi-signal-images**, klicka för att markera bilden **Offer_Phone.jpg** och klicka på **Select**.

![Journey Optimizer](./images/campaign16.png)

Dra och släpp en **Text** -komponent på den tredje och fjärde raden.

![Journey Optimizer](./images/campaign17.png)

Markera standardtexten i komponenten på den tredje raden **Skriv texten här.** och ersätt den med texten nedan.

```javascript
Get AirPods for free:

Experience seamless connectivity like never before with CitiSignal. Sign up for select premium plans and receive a complimentary pair of Apple AirPods. Stay connected in style with our unbeatable offer.
```

Markera standardtexten i komponenten på den fjärde raden **Skriv texten här.** och ersätt den med texten nedan.

```javascript
We'll pay off your phone:

Make the switch to CitiSignal and say goodbye to phone payments! Switching to CitiSignal has never been more rewarding. Say farewell to hefty phone bills as we help pay off your phone, up to 800$!
```

![Journey Optimizer](./images/campaign18.png)

Ditt enkla nyhetsbrev är nu klart. Klicka på **Spara**.

![Journey Optimizer](./images/ready.png)

Gå tillbaka till kontrollpanelen för kampanjer genom att klicka på **pilen** bredvid texten för ämnesraden i det övre vänstra hörnet.

![Journey Optimizer](./images/campaign19.png)

Klicka på **Granska för att aktivera**.

![Journey Optimizer](./images/campaign20.png)

Du kan då få det här felet. Om så är fallet kan du behöva vänta i upp till 24 timmar tills målgruppen har utvärderats och sedan försöka aktivera kampanjen igen. Du kan också behöva uppdatera schemat för din kampanj så att den körs vid ett senare tillfälle.

Klicka på **Aktivera**.

![Journey Optimizer](./images/campaign21.png)

När kampanjen är aktiverad kommer den att köras.

![Journey Optimizer](./images/campaign22.png)

Din kampanj är nu aktiverad. E-postmeddelandet med nyhetsbrevet skickas så som du har definierat det i ditt schema, och kampanjen stoppas så snart som det senaste e-postmeddelandet har skickats.

Du bör också få e-postadressen till den demoprofil du skapade tidigare.

![Journey Optimizer](./images/campaign23.png)

Du har gjort klart den här övningen.

Nästa steg: [3.4.3 Använda segmentbaserad personalisering i ett e-postmeddelande](./ex3.md)

[Gå tillbaka till modul 3.4](./journeyoptimizer.md)

[Gå tillbaka till Alla moduler](../../../overview.md)
