---
title: Adobe Experience Platform Data Collection & Servervidarebefordran i realtid - Skapa och konfigurera en anpassad webkrok
description: Skapa och konfigurera en anpassad webkrok
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '1093'
ht-degree: 0%

---

# 2.5.3 Skapa och konfigurera en anpassad webkrok

## 2.5.3.1 Skapa en egen webbkrok

Gå till [https://webhook.site/](https://webhook.site/). Du kommer att se något liknande:

![demo](./images/webhook1.png)

Du kommer att se din unika URL, som ser ut så här: `https://webhook.site/585126a1-41fc-4721-864b-d4aa8c268a1d`.

Den här webbplatsen har nu skapat den här webbokroken åt dig och du kan konfigurera den i **[!DNL Event Forwarding property]** för att testa vidarebefordran av händelser.

## 2.5.3.2 Uppdatera egenskapen för händelsevidarebefordran: Skapa ett dataelement

Gå till [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/) och gå till **Händelsevidarebefordran**. Sök i egenskapen för vidarebefordran av händelser och klicka på den för att öppna den.

![Adobe Experience Platform Data Collection SSF](./images/prop1.png)

Gå till **Dataelement** på den vänstra menyn. Klicka på **Skapa nytt dataelement**.

![Adobe Experience Platform Data Collection SSF](./images/de1.png)

Sedan visas ett nytt dataelement att konfigurera.

![Adobe Experience Platform Data Collection SSF](./images/de2.png)

Gör följande val:

- Ange **XDM-händelse** som **namn**.
- Som **tillägg** väljer du **kärna**.
- Som **dataelementtyp** väljer du **Sökväg**.
- Ange **arc.event.xdm** som **sökväg**. Genom att ange den här sökvägen filtrerar du ut avsnittet **XDM** från den händelsenyttolast som skickas av webbplatsen eller mobilappen till Adobe Edge.

Du kommer nu att ha den här. Klicka på **Spara**.

![Adobe Experience Platform Data Collection SSF](./images/de3.png)

>[!NOTE]
>
>I ovanstående sökväg görs en referens till **arc**. **arc** står för Adobe Resource Context och **arc** står alltid för det högsta tillgängliga objektet som är tillgängligt i Server Side-kontexten. Anrikningar och omvandlingar kan läggas till i det **arc**-objektet med Adobe Experience Platform Data Collection Server-funktioner.
>
>I ovanstående sökväg görs en referens till **event**. **event** står för en unik händelse och Adobe Experience Platform Data Collection Server utvärderar alltid varje enskild händelse. Ibland kan du se en referens till **händelser** i nyttolasten som skickas av Web SDK-klientsidan, men i Adobe Experience Platform Data Collection Server utvärderas varje händelse individuellt.

## 2.5.3.3 Uppdatera din Adobe Experience Platform Data Collection Server-egenskap: Skapa en regel

Gå till **Regler** på den vänstra menyn. Klicka på **Skapa ny regel**.

![Adobe Experience Platform Data Collection SSF](./images/rl1.png)

Därefter visas en ny regel att konfigurera. Ange **Namn**: **Alla sidor**. För den här övningen behöver du inte konfigurera något villkor. I stället ska du konfigurera en åtgärd. Klicka på knappen **+ Lägg till** under **Åtgärder**.

![Adobe Experience Platform Data Collection SSF](./images/rl2.png)

Då ser du det här. Gör följande val:

- Välj **tillägget**: **Adobe Cloud Connector**.
- Välj **åtgärdstyp**: **Ring upp hämtning**.

Det bör ge dig det här **namnet**: **Adobe Cloud Connector - ring hämtningssamtal**. Nu bör du se det här:

![Adobe Experience Platform Data Collection SSF](./images/rl4.png)

Konfigurera sedan följande:

- Ändra förfrågningsmetoden från GET till **POST**
- Ange URL:en för den anpassade webkrok du skapade i något av de föregående stegen på webbplatsen [https://webhook.site/](https://webhook.site/) som ser ut så här: `https://webhook.site/585126a1-41fc-4721-864b-d4aa8c268a1d`

Du borde ha den här nu. Gå sedan till **Brödtext**.

![Adobe Experience Platform Data Collection SSF](./images/rl6.png)

Då ser du det här. Klicka på dataelementsikonen enligt nedan.

![Adobe Experience Platform Data Collection SSF](./images/rl7.png)

På popup-menyn markerar du dataelementet **XDM Event** som du skapade i föregående steg. Klicka på **Markera**.

![Adobe Experience Platform Data Collection SSF](./images/rl8.png)

Då ser du det här. Klicka på **Behåll ändringar**.

![Adobe Experience Platform Data Collection SSF](./images/rl9.png)

Då ser du det här. Klicka på **Spara**.

![Adobe Experience Platform Data Collection SSF](./images/rl10.png)

Du har nu konfigurerat din första regel i en händelsevidarebefordringsegenskap. Gå till **Publiceringsflöde** om du vill publicera ändringarna.
Öppna utvecklingsbiblioteket **Main** genom att klicka på **Edit** enligt indikationen.

![Adobe Experience Platform Data Collection SSF](./images/rl11.png)

Klicka på knappen **Lägg till alla ändrade resurser**, varefter du ser regeln och dataelementet visas i det här biblioteket. Klicka sedan på **Spara och bygg för utveckling**. Ändringarna distribueras nu.

![Adobe Experience Platform Data Collection SSF](./images/rl13.png)

Efter några minuter ser du att distributionen är klar och klar att testas.

![Adobe Experience Platform Data Collection SSF](./images/rl14.png)

## 2.5.3.4 Testa konfigurationen

Gå till [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). När du har loggat in med din Adobe ID ser du det här. Klicka på webbplatsprojektet för att öppna det.

![DSN](../../gettingstarted/gettingstarted/images/web8.png)

Nu kan du följa nedanstående flöde för att komma åt webbplatsen. Klicka på **Integrationer**.

![DSN](../../gettingstarted/gettingstarted/images/web1.png)

På sidan **Integrationer** måste du välja den datainsamlingsegenskap som skapades i övning 0.1.

![DSN](../../gettingstarted/gettingstarted/images/web2.png)

Du kommer då att se din demowebbplats öppnas. Markera URL-adressen och kopiera den till Urklipp.

![DSN](../../gettingstarted/gettingstarted/images/web3.png)

Öppna ett nytt inkognito-webbläsarfönster.

![DSN](../../gettingstarted/gettingstarted/images/web4.png)

Klistra in webbadressen till demowebbplatsen, som du kopierade i föregående steg. Du ombeds sedan logga in med din Adobe ID.

![DSN](../../gettingstarted/gettingstarted/images/web5.png)

Välj kontotyp och slutför inloggningsprocessen.

![DSN](../../gettingstarted/gettingstarted/images/web6.png)

Därefter visas webbplatsen i ett inkognitivt webbläsarfönster. För varje demonstration måste du använda ett nytt, inkognitivt webbläsarfönster för att läsa in webbadressen till demowebbplatsen.

![DSN](../../gettingstarted/gettingstarted/images/web7.png)

När du öppnar din webbläsarutvecklarvy kan du inspektera nätverksbegäranden enligt nedan. När du använder filtret **interact** visas nätverksbegäranden som skickas av Adobe Experience Platform Data Collection Client till Adobe Edge.

![Adobe Experience Platform Data Collection Setup](./images/hook1.png)

Om du väljer oformaterad nyttolast går du till [https://jsonformatter.org/json-pretty-print](https://jsonformatter.org/json-pretty-print) och klistrar in nyttolasten. Klicka på **Gör vacker**. Sedan ser du JSON-nyttolasten, **events** -objektet och **xdm** -objektet. I ett av de föregående stegen, när du definierade dataelementet, använde du referensen **arc.event.xdm**, vilket resulterar i att du tolkar **xdm** -objektet för den här nyttolasten.

![Adobe Experience Platform Data Collection Setup](./images/hook2.png)

Växla vy till webbplatsen [https://webhook.site/](https://webhook.site/) som du använde i något av föregående steg. Nu bör du ha en vy som liknar den här, där nätverksbegäranden visas på den vänstra menyn. Du ser nyttolasten **xdm** som filtrerades bort från nätverksbegäran som visades ovan.

![Adobe Experience Platform Data Collection Setup](./images/hook3.png)

Bläddra nedåt en bit i nyttolasten för att hitta sidnamnet, som i det här fallet är **vangeluw-OCUC** (som är projektnamnet för demowebbplatsen).

![Adobe Experience Platform Data Collection Setup](./images/hook4.png)

Om du nu navigerar på webbplatsen kommer du att se ytterligare nätverksförfrågningar bli tillgängliga på den här anpassade webbkroken i realtid.

![Adobe Experience Platform Data Collection Setup](./images/hook5.png)

Du har nu konfigurerat vidarebefordran på serversidan av Web SDK/XDM-nyttolaster till en extern anpassad webkrok. I nästa övning kommer du att konfigurera ett liknande tillvägagångssätt, och du kommer att skicka samma data till Google- och AWS-miljöer.

Nästa steg: [2.5.4 Skapa och konfigurera en Google Cloud-funktion](./ex4.md)

[Gå tillbaka till modul 2.5](./aep-data-collection-ssf.md)

[Gå tillbaka till Alla moduler](./../../../overview.md)
