---
title: CDP i realtid - Bygg ett segment och vidta åtgärder - Skicka ditt segment till Adobe Target
description: CDP i realtid - Bygg ett segment och vidta åtgärder - Skicka ditt segment till Adobe Target
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 0%

---

# 2.3.5 Take Action: send your segment to Adobe Target

Gå till [Adobe Experience Platform](https://experience.adobe.com/platform). När du har loggat in loggar du in på Adobe Experience Platform hemsida.

![Datainmatning](./../../../modules/datacollection/module1.2/images/home.png)

Innan du fortsätter måste du välja en **sandlåda**. Sandlådan som ska markeras har namnet ``--aepSandboxName--``. Du kan göra detta genom att klicka på texten **[!UICONTROL Production Prod]** i den blå raden ovanför skärmen. När du har valt rätt [!UICONTROL sandbox] visas skärmändringen och nu är du i din dedikerade [!UICONTROL sandbox].

![Datainmatning](./../../../modules/datacollection/module1.2/images/sb1.png)

## 2.3.5.1 Verifiera ditt dataflöde

Adobe Target-målet i Real-Time CDP är anslutet till den datastream som används för att importera data till kantnätverket i Adobe. Om du vill ställa in ditt Adobe Target-mål måste du först kontrollera om ditt datastream redan är aktiverat för Adobe Target. Ditt datastram konfigurerades i [övning 0.2 Skapa ditt datastream](./../../../modules/gettingstarted/gettingstarted/ex2.md) och namngavs `--aepUserLdap-- - Demo System Datastream`.

Gå till [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/) och klicka sedan på **Datastreams** eller **Datastreams (Beta)**.

![Datainmatning](./images/atdestds1.png)

I skärmens övre högra hörn väljer du namnet på sandlådan, som ska vara `--aepSandboxName--`.

![Klicka på ikonen Edge-konfiguration i den vänstra navigeringen](./images/edgeconfig1b.png)

Sök efter din datastream med namnet `--aepUserLdap-- - Demo System Datastream` i Datastreams. Klicka på ditt datastream för att öppna det.

![Datainmatning](./images/atdestds3.png)

Du ser sedan detta genom att klicka på **..** bredvid **Adobe Experience Platform** och sedan klicka på **Redigera**.

![Datainmatning](./images/atdestds4.png)

Markera kryssrutorna för både **Edge Segmentation** och **Personalization Destinations**. Klicka på **Spara**.

![Datainmatning](./images/atdestds4a.png)

Klicka sedan på **+ Lägg till tjänst**.

![Datainmatning](./images/atdestds4b.png)

Välj tjänsten **Adobe Target**. Klicka på **Spara**.

![Datainmatning](./images/atdestds5.png)

Din datastream är nu konfigurerad för Adobe Target.

![Datainmatning](./images/atdestds5a.png)

## 2.3.5.2 Konfigurera ditt Adobe Target-mål

Adobe Target finns som mål från Real-Time CDP. Gå till **Destinationer** och **Katalog** om du vill konfigurera din Adobe Target-integrering.

![AT](./images/atdest1.png)

Klicka på **Personalization** på menyn **Kategorier**. Sedan visas **Adobe Target**-målkortet. Klicka på **Aktivera segment** (eller **Konfigurera** beroende på din miljö).

![AT](./images/atdest2.png)

Beroende på din miljö kan du behöva klicka på **+ Konfigurera nytt mål** för att börja skapa ditt mål.

![AT](./images/atdest3.png)

Då ser du det här.

![AT](./images/atdest4.png)

På skärmen **Konfigurera nytt mål** måste du konfigurera två saker:

- Namn: använd namnet `--aepUserLdap-- - Adobe Target (Web)` som ska se ut så här: **vangeluw - Adobe Target (webb)**.
- Datastream-ID: Du måste välja det datastream som du konfigurerade i [Utför 0.2 Skapa ditt datastream](./../../../modules/gettingstarted/gettingstarted/ex2.md). Namnet på din datastream ska vara: `--aepUserLdap-- - Demo System Datastream`.

Klicka på **Nästa**.

![AT](./images/atdest5.png)

På nästa skärm kan du välja en policy. Du behöver inte välja någon, i det här fallet behöver du inte välja någon, så klicka på **Skapa**.

![AT](./images/atdest6.png)

Målet har skapats och kommer att visas i listan. Välj mål och klicka på **Nästa** för att börja skicka segment till målet.

![AT](./images/atdest7.png)

I listan med tillgängliga segment väljer du det segment som du skapade i [Utför 6.1 Skapa ett segment](./ex1.md) med namnet `--aepUserLdap-- - Interest in PROTEUS FITNESS JACKSHIRT`. Klicka sedan på **Nästa**.

![AT](./images/atdest8.png)

På nästa sida klickar du på **Nästa**.

![AT](./images/atdest9.png)

Klicka på **Slutför**.

![AT](./images/atdest10.png)

Ditt segment är nu aktiverat mot Adobe Target.

![AT](./images/atdest11.png)

>[!IMPORTANT]
>
>När du just har skapat Adobe Target-destinationen i Real-Time CDP kan det ta upp till en timme innan destinationen är aktiv. Detta är en engångsväntetid på grund av konfigurationen av serverdelskonfigurationen. När den inledande väntetiden på en timme och backend-konfigurationen är klar, kommer nytillagda kantsegment som skickas till Adobe Target-destinationen att vara tillgängliga för målgruppsanpassning i realtid.

## 2.3.5.3 Konfigurera din formulärbaserade Adobe Target-aktivitet

Nu när ditt Real-Time CDP-segment är konfigurerat att skickas till Adobe Target kan du konfigurera din Experience Targeting-aktivitet i Adobe Target. I den här övningen ska du konfigurera en formulärbaserad aktivitet.

Gå till Adobe Experience Cloud hemsida på [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/). Klicka på **Mål** för att öppna det.

![RTCDP](./images/excl.png)

På startsidan för **Adobe Target** visas alla befintliga aktiviteter.

![RTCDP](./images/exclatov.png)

Klicka på **+ Skapa aktivitet** för att skapa en ny aktivitet.

![RTCDP](./images/exclatcr.png)

Välj **Experience Targeting**.

![RTCDP](./images/exclatcrxt.png)

Välj **Formulär** och välj **Inga egenskapsbegränsningar**. Klicka på **Nästa**.

![RTCDP](./images/exclatcrxtdtlform.png)

Du är nu med i den formulärbaserade aktivitetshanteraren.

![RTCDP](./images/atform1.png)

För fältet **LOCATION 1** väljer du **target-global-mbox**.

![RTCDP](./images/atform2.png)

Standardmålgruppen är **Alla besökare**. Klicka på **3 punkter** bredvid **Alla besökare** och klicka på **Ändra publik**.

![RTCDP](./images/atform3.png)

Du ser nu en lista över tillgängliga målgrupper, och Adobe Experience Platform-segmentet som du skapade tidigare och skickade till Adobe Target ingår nu i den här listan. Markera det segment som du tidigare har skapat i Adobe Experience Platform. Klicka på **Tilldela målgrupp**.

![RTCDP](./images/exclatvecchaud.png)

Ditt Adobe Experience Platform-segment är nu en del av denna Experience Targeting Activity.

![RTCDP](./images/atform4.png)

Nu ska vi ändra Hero Image på webbplatsens hemsida. Klicka för att öppna listrutan bredvid **Standardinnehåll** och klicka på **Skapa HTML-erbjudande**.

![RTCDP](./images/atform5.png)

Klistra in följande kod. Klicka sedan på **Nästa**.

```javascript
<script>document.querySelector("#home > div > div > div > div > div.banner_img.d-none.d-lg-block > img").src="https://parsefiles.back4app.com/hgJBdVOS2eff03JCn6qXXOxT5jJFzialLAHJixD9/ff92fdc3885972c0090ad5419e0ef4d4_Luma - Product - Proteus - Hero Banner.png"; document.querySelector(".banner_text > *").remove()</script>
```

![RTCDP](./images/atform6.png)

Du kommer då att se den nya upplevelsen av den nya bilden för den valda målgruppen.

![RTCDP](./images/atform7.png)

Klicka på aktivitetens titel i det övre vänstra hörnet för att byta namn på den.

![RTCDP](./images/exclatvecname.png)

För namnet, använd:

- `--aepUserLdap-- - RTCDP - XT (Form)`

![RTCDP](./images/atform8.png)

Klicka på **Nästa**.

![RTCDP](./images/exclatvecnamenext.png)

Gå till **Målmått** på sidan **Mål och inställningar** -.

![RTCDP](./images/atform9.png)

Ange som primärt mål **engagemang** - **tid på plats**.

![RTCDP](./images/vec3.png)

Klicka på **Spara och stäng**.

![RTCDP](./images/vecsave.png)

Du finns nu på sidan **Aktivitetsöversikt**. Du måste fortfarande aktivera din aktivitet.

![RTCDP](./images/atform10.png)

Klicka på fältet **Inaktiv** och välj **Aktivera**.

![RTCDP](./images/atform11.png)

Sedan får du en visuell bekräftelse på att din aktivitet nu är aktiv.

![RTCDP](./images/atform12.png)

Din aktivitet finns nu tillgänglig och kan testas på demowebbplatsen.

>[!IMPORTANT]
>
>När du just har skapat Adobe Target-destinationen i Real-Time CDP kan det ta upp till en timme innan destinationen är aktiv. Detta är en engångsväntetid på grund av konfigurationen av serverdelskonfigurationen. När den inledande väntetiden på en timme och backend-konfigurationen är klar, kommer nytillagda kantsegment som skickas till Adobe Target-destinationen att vara tillgängliga för målgruppsanpassning i realtid.

Om du nu går tillbaka till din demowebbplats och besöker produktsidan för PROTEUS FITNESS JACKSHIRT, kan du direkt kvalificera dig för det segment du har skapat och du ser Adobe Target-aktiviteten visas på startsidan i realtid.

![RTCDP](./images/atform13.png)

Nästa steg: [2.3.6 Externa målgrupper](./ex6.md)

[Gå tillbaka till modul 2.3](./real-time-cdp-build-a-segment-take-action.md)

[Gå tillbaka till Alla moduler](../../../overview.md)
