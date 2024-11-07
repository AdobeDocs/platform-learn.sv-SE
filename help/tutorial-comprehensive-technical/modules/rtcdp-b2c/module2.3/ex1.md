---
title: CDP i realtid - Bygg ett segment och agera - Bygg ett segment
description: CDP i realtid - Bygg ett segment och agera - Bygg ett segment
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 1%

---

# 2.3.1 Skapa ett segment

I den här övningen skapar du ett segment genom att använda Adobe Experience Platform segmentbyggare.

## 2.3.1.1 Sammanhang

I dagens värld måste kundens beteende i realtid hanteras. Ett sätt att svara på kundbeteenden i realtid är att använda ett segment, förutsatt att segmentet kvalificeras i realtid. I den här övningen måste ni bygga ut ett segment, med hänsyn tagen till den verkliga aktiviteten på webbplatsen som vi har använt.

## 2.3.1.2 Identifiera det beteende du vill reagera på

Gå till [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). När du har loggat in med din Adobe ID ser du det här. Klicka på webbplatsprojektet för att öppna det.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web8.png)

Nu kan du följa nedanstående flöde för att komma åt webbplatsen. Klicka på **Integrationer**.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web1.png)

På sidan **Integrationer** måste du välja den datainsamlingsegenskap som skapades i övning 0.1.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web2.png)

Du kommer då att se din demowebbplats öppnas. Markera URL-adressen och kopiera den till Urklipp.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web3.png)

Öppna ett nytt inkognito-webbläsarfönster.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web4.png)

Klistra in webbadressen till demowebbplatsen, som du kopierade i föregående steg. Du ombeds sedan logga in med din Adobe ID.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web5.png)

Välj kontotyp och slutför inloggningsprocessen.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web6.png)

Därefter visas webbplatsen i ett inkognitivt webbläsarfönster. För varje demonstration måste du använda ett nytt, inkognitivt webbläsarfönster för att läsa in webbadressen till demowebbplatsen.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web7.png)

I det här exemplet vill du svara en viss kund som tittar på en viss produkt.
Gå till **Män** på hemsidan **Luma** och klicka på produkten **PROTEUS FITNESS JACKSHIRT**.

![Datainmatning](./images/homenadia.png)

Så när någon besöker produktsidan för **PROTEUS FITNESS JACKSHIRT** vill du kunna vidta åtgärder. Det första du måste göra är att definiera ett segment.

![Datainmatning](./images/homenadiapp.png)

## 2.3.1.3 Skapa segmentet

Gå till [Adobe Experience Platform](https://experience.adobe.com/platform). När du har loggat in loggar du in på Adobe Experience Platform hemsida.

![Datainmatning](./../../../modules/datacollection/module1.2/images/home.png)

Innan du fortsätter måste du välja en **sandlåda**. Sandlådan som ska markeras har namnet ``--aepSandboxName--``. Du kan göra detta genom att klicka på texten **[!UICONTROL Production Prod]** i den blå raden ovanför skärmen. När du har valt rätt [!UICONTROL sandbox] visas skärmändringen och nu är du i din dedikerade [!UICONTROL sandbox].

![Datainmatning](./../../../modules/datacollection/module1.2/images/sb1.png)

Gå till **Segment** på menyn till vänster och gå sedan till **Bläddra** där du kan se en översikt över alla befintliga segment. Klicka på knappen **Skapa segment** för att börja skapa ett nytt segment.

![Segmentering](./images/menuseg.png)

Som nämnts ovan måste du skapa ett segment av alla kunder som har tittat på produkten **PROTEUS FITNESS JACKSHIRT**.

Om du vill bygga ut det här segmentet måste du lägga till en händelse. Du kan hitta alla händelser genom att klicka på ikonen **Händelser** i menyraden **Segment** .

Därefter visas noden **XDM ExperienceEvent** på den översta nivån.

Om du vill hitta kunder som har besökt **PROTEUS FITNESS JACKSHIRT** klickar du på **XDM ExperienceEvent**.

![Segmentering](./images/findee.png)

Bläddra nedåt till **Produktlisteobjekt** och klicka på den.

![Segmentering](./images/see.png)

Välj **Namn** och dra och släpp objektet **Namn** från den vänstra menyn **Produktlisteobjekt** på segmentbyggarbetsytan till avsnittet **Händelser** .

![Segmentering](./images/eewebpdtlname1.png)

Jämförelseparametern ska vara **lika med** och ange `PROTEUS FITNESS JACKSHIRT` i indatafältet.

![Segmentering](./images/pv.png)

**Händelsereglerna** bör nu se ut så här. Varje gång du lägger till ett element i segmentbyggaren kan du klicka på knappen **Uppdatera uppskattning** för att få en ny uppskattning av populationen i ditt segment.

![Segmentering](./images/ldap4.png)

Till sist ger vi segmentet ett namn och sparar det.

Använd följande som namnkonvention:

- `--aepUserLdap-- - Interest in PROTEUS FITNESS JACKSHIRT`

Segmentnamnet ska se ut så här:
`vangeluw - Interest in PROTEUS FITNESS JACKSHIRT`

Klicka sedan på knappen **Spara och stäng** för att spara segmentet.

![Segmentering](./images/segmentname.png)

Du kommer nu tillbaka till sidan Segmentöversikt.

![Segmentering](./images/savedsegment.png)

Nästa steg: [2.3.2 Granska hur du konfigurerar DV360-mål med hjälp av mål](./ex2.md)

[Gå tillbaka till modul 2.3](./real-time-cdp-build-a-segment-take-action.md)

[Gå tillbaka till Alla moduler](../../../overview.md)
