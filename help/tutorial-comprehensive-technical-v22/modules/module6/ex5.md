---
title: CDP i realtid - Bygg ett segment och vidta åtgärder - Skicka ditt segment till Adobe Target
description: CDP i realtid - Bygg ett segment och vidta åtgärder - Skicka ditt segment till Adobe Target
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 7883cfa9-0119-47c2-a300-3ff0f741191a
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1033'
ht-degree: 0%

---

# 6.5 Vidta åtgärder: skicka segmentet till Adobe Target

Gå till [Adobe Experience Platform](https://experience.adobe.com/platform). När du loggat in kommer du till Adobe Experience Platform hemsida.

![Dataintag](../module2/images/home.png)

Innan du fortsätter måste du välja en **sandlåda**. Sandlådan som ska markeras har namnet ``--aepSandboxId--``. Du kan göra detta genom att klicka på texten **[!UICONTROL Produktionsprodukt]** i den blå linjen ovanför skärmen. När du har valt lämplig [!UICONTROL sandlåda]kommer du att se skärmändringen och nu är du med på din [!UICONTROL sandlåda].

![Dataintag](../module2/images/sb1.png)

## 6.5.1 Verifiera ditt datastream

Adobe Target-målet i Real-Time CDP är anslutet till den datastream som används för att importera data till kantnätverket i Adobe. Om du vill ställa in ditt Adobe Target-mål måste du först kontrollera om ditt datastream redan är aktiverat för Adobe Target. Ditt datastram har konfigurerats i [Utövning 0.2 Skapa ditt datastream](./../module0/ex2.md) och har namngetts `--demoProfileLdap-- - Demo System Datastream`.

Gå till [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)och sedan klicka **Datastreams** eller **Datastreams (beta)**.

![Dataintag](./images/atdestds1.png)

I skärmens övre högra hörn väljer du namnet på sandlådan, som bör vara `--aepSandboxId--`.

![Klicka på ikonen Edge Configuration (Kantkonfiguration) i den vänstra navigeringen](./images/edgeconfig1b.png)

I Datastreams söker du efter den datastream som har namnet `--demoProfileLdap-- - Demo System Datastream`. Klicka på ditt datastream för att öppna det.

![Dataintag](./images/atdestds3.png)

Du kommer att se det här, klicka **...** nästa **Adobe Experience Platform** och sedan klicka **Redigera**.

![Dataintag](./images/atdestds4.png)

Markera kryssrutorna för båda **Kantsegmentering** och **Destinationer för personalisering**. Klicka **Spara**.

![Dataintag](./images/atdestds4a.png)

Klicka på **+ Lägg till tjänst**.

![Dataintag](./images/atdestds4b.png)

Välj tjänsten **Adobe Target**. Klicka **Spara**.

![Dataintag](./images/atdestds5.png)

Din datastream är nu konfigurerad för Adobe Target.

![Dataintag](./images/atdestds5a.png)

## 6.5.2 Konfigurera ditt Adobe Target-mål

Adobe Target finns som mål från Real-Time CDP. Om du vill konfigurera Adobe Target-integreringen går du till **Destinationer**, till **Katalog**.

![AT](./images/atdest1.png)

Klicka **Personalisering** i **Kategorier** -menyn. Då ser du **Adobe Target** destinationskort. Klicka **Aktivera segment** (eller **Konfigurera** beroende på din miljö).

![AT](./images/atdest2.png)

Beroende på din miljö kan du behöva klicka **+ Konfigurera nytt mål** för att börja skapa destinationen.

![AT](./images/atdest3.png)

Du kommer då att se det här.

![AT](./images/atdest4.png)

I **Konfigurera nytt mål** måste du konfigurera två saker:

- Namn: använd namnet `--demoProfileLdap-- - Adobe Target (Web)`som ser ut så här: **vangeluw - Adobe Target (webb)**.
- Datastream-ID: du måste välja den datastream som du konfigurerade i [Utövning 0.2 Skapa ditt datastream](./../module0/ex2.md). Namnet på din datastream ska vara: `--demoProfileLdap-- - Demo System Datastream`.

Klicka på **Nästa**.

![AT](./images/atdest5.png)

På nästa skärm kan du välja en policy. Du behöver inte välja någon, i det här fallet behöver du inte välja någon, så klicka **Skapa**.

![AT](./images/atdest6.png)

Målet skapas nu och visas i listan. Välj mål och klicka på **Nästa** för att börja skicka segment till din destination.

![AT](./images/atdest7.png)

I listan med tillgängliga segment väljer du det segment du skapade i [Utgång 6.1 Skapa ett segment](./ex1.md), som har namnet `--demoProfileLdap-- - Interest in PROTEUS FITNESS JACKSHIRT`. Klicka sedan på **Nästa**.

![AT](./images/atdest8.png)

På nästa sida klickar du på **Nästa**.

![AT](./images/atdest9.png)

Klicka **Slutför**.

![AT](./images/atdest10.png)

Ditt segment är nu aktiverat mot Adobe Target.

![AT](./images/atdest11.png)

>[!IMPORTANT]
>
>När du just har skapat Adobe Target-destinationen i Real-Time CDP kan det ta upp till en timme innan destinationen är aktiv. Detta är en engångsväntetid på grund av konfigurationen av serverdelskonfigurationen. När den inledande väntetiden på en timme och backend-konfigurationen är klar, kommer nytillagda kantsegment som skickas till Adobe Target-destinationen att vara tillgängliga för målgruppsanpassning i realtid.

## 6.5.3 Konfigurera din formulärbaserade Adobe Target-aktivitet

Nu när ditt Real-Time CDP-segment är konfigurerat att skickas till Adobe Target kan du konfigurera din Experience Targeting-aktivitet i Adobe Target. I den här övningen ska du konfigurera en formulärbaserad aktivitet.

Gå till Adobe Experience Cloud hemsida genom att gå till [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/). Klicka **Mål** för att öppna den.

![RTCDP](./images/excl.png)

På **Adobe Target** på startsidan ser du alla befintliga aktiviteter.

![RTCDP](./images/exclatov.png)

Klicka **+ Skapa aktivitet** för att skapa en ny aktivitet.

![RTCDP](./images/exclatcr.png)

Välj **Experience Targeting**.

![RTCDP](./images/exclatcrxt.png)

Välj **Formulär** och markera **Inga egenskapsbegränsningar**. Klicka på **Nästa**.

![RTCDP](./images/exclatcrxtdtlform.png)

Du är nu med i den formulärbaserade aktivitetshanteraren.

![RTCDP](./images/atform1.png)

För fältet **PLATS 1**, markera **target-global-mbox**.

![RTCDP](./images/atform2.png)

Standardmålgruppen är för närvarande **Alla besökare**. Klicka på **3 punkter** nästa **Alla besökare** och klicka **Ändra målgrupp**.

![RTCDP](./images/atform3.png)

Du ser nu en lista över tillgängliga målgrupper, och Adobe Experience Platform-segmentet som du skapade tidigare och skickade till Adobe Target ingår nu i listan. Markera det segment som du tidigare har skapat i Adobe Experience Platform. Klicka **Tilldela publik**.

![RTCDP](./images/exclatvecchaud.png)

Ditt Adobe Experience Platform-segment är nu en del av denna Experience Targeting Activity.

![RTCDP](./images/atform4.png)

Nu ska vi ändra Hero Image på webbplatsens hemsida. Klicka för att öppna listrutan bredvid **Standardinnehåll** och klicka **Skapa HTML**.

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

- `--demoProfileLdap-- - RTCDP - XT (Form)`

![RTCDP](./images/atform8.png)

Klicka på **Nästa**.

![RTCDP](./images/exclatvecnamenext.png)

På **Mål och inställningar** - sida, gå till **Målmått**.

![RTCDP](./images/atform9.png)

Ställ in det primära målet på **Engagemang** - **Tid på plats**.

![RTCDP](./images/vec3.png)

Klicka **Spara och stäng**.

![RTCDP](./images/vecsave.png)

Du är nu på **Översikt över aktivitet** sida. Du måste fortfarande aktivera din aktivitet.

![RTCDP](./images/atform10.png)

Klicka på fältet **Inaktiv** och markera **Aktivera**.

![RTCDP](./images/atform11.png)

Sedan får du en visuell bekräftelse på att din aktivitet nu är aktiv.

![RTCDP](./images/atform12.png)

Din aktivitet finns nu tillgänglig och kan testas på demowebbplatsen.

>[!IMPORTANT]
>
>När du just har skapat Adobe Target-destinationen i Real-Time CDP kan det ta upp till en timme innan destinationen är aktiv. Detta är en engångsväntetid på grund av konfigurationen av serverdelskonfigurationen. När den inledande väntetiden på en timme och backend-konfigurationen är klar, kommer nytillagda kantsegment som skickas till Adobe Target-destinationen att vara tillgängliga för målgruppsanpassning i realtid.

Om du nu går tillbaka till din demowebbplats och besöker produktsidan för PROTEUS FITNESS JACKSHIRT, kan du direkt kvalificera dig för det segment du har skapat och du ser Adobe Target-aktiviteten visas på startsidan i realtid.

![RTCDP](./images/atform13.png)

Nästa steg: [6.6 Externa målgrupper](./ex6.md)

[Gå tillbaka till modul 6](./real-time-cdp-build-a-segment-take-action.md)

[Gå tillbaka till Alla moduler](../../overview.md)
