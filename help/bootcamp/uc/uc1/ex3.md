---
title: Bootcamp - kundprofil i realtid - Skapa ett segment - användargränssnitt
description: Bootcamp - kundprofil i realtid - Skapa ett segment - användargränssnitt
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Segments
exl-id: 37d4a5e8-e2bc-4c8c-a74f-09f74ea79962
source-git-commit: ee5c0af17c12f1d90774a3a4150c9788e2368e39
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 2%

---

# 1.3 Skapa ett segment - användargränssnitt

I den här övningen skapar du ett segment genom att använda Adobe Experience Platform Segment Builder.

## Artikel

Gå till [Adobe Experience Platform](https://experience.adobe.com/platform). När du har loggat in loggar du in på Adobe Experience Platform hemsida.

![Inmatning av data](./images/home.png)

Innan du fortsätter måste du välja en **sandlåda**. Sandlådan som ska markeras har namnet ``Bootcamp``. Du kan göra detta genom att klicka på texten **[!UICONTROL Production Prod]** i den blå linjen ovanför skärmen. När du har valt lämplig [!UICONTROL sandbox]kommer du att se skärmändringen och nu är du med på din [!UICONTROL sandbox].

![Inmatning av data](./images/sb1.png)

På menyn till vänster går du till **Segment**. På den här sidan visas en översikt över alla befintliga segment. Klicka på **+ Skapa segment** för att börja skapa ett nytt segment.

![Segmentering](./images/menuseg.png)

När du är i segmentbyggaren märker du omedelbart **Attribut** menyalternativ och **Individuell XDM-profil** referens.

![Segmentering](./images/segmentationui.png)

Eftersom XDM är det språk som används i upplevelseverksamheten är XDM även grunden för segmentbyggaren. Alla data som är inkapslade i Platform ska mappas mot XDM, och som sådana blir alla data en del av samma datamodell oavsett varifrån dessa data kommer. Detta ger en stor fördel när du skapar segment, eftersom ni från det här segmentbyggargränssnittet kan kombinera data från vilket ursprung som helst i samma arbetsflöde. Segment som byggts i Segment Builder kan skickas till lösningar som Adobe Target, Adobe Campaign och Adobe Audience Manager för aktivering.

Nu måste ni skapa ett segment av alla kunder som har tittat på produkten **Real-Time CDP**.

Om du vill bygga ut det här segmentet måste du lägga till en Experience Event. Du kan hitta alla Experience Events genom att klicka på **Händelser** ikonen i **Fält** menyraden.

![Segmentering](./images/findee.png)

Nu kommer du att se den översta nivån, **XDM ExperienceEvents** nod. Klicka på **XDM ExperienceEvent**.

![Segmentering](./images/see.png)

Gå till **Produktlisteobjekt**.

![Segmentering](./images/plitems.png)

Välj **Namn** och dra och släpp **Namn** objekt från den vänstra menyn på segmentbyggarbetsytan i **Händelser** -avsnitt. Då ser du det här:

![Segmentering](./images/eewebpdtlname.png)

Jämförelseparametern ska vara **är lika med** och i inmatningsfältet anger du **CDP i realtid**.

![Segmentering](./images/pv.png)

Varje gång du lägger till ett element i segmentverktyget kan du klicka på **Uppdatera offert** för att få en ny uppskattning av populationen i ditt segment.

![Segmentering](./images/refreshest.png)

Som **Utvärderingsmetod**, markera **Kant**.

![Segmentering](./images/evedge.png)

Till sist ger vi segmentet ett namn och sparar det.

Använd följande som namnkonvention:

- `yourLastName - Interest in Real-Time CDP`

Klicka sedan på **Spara och stäng** för att spara segmentet.

![Segmentering](./images/segmentname.png)

Du kommer nu tillbaka till sidan för segmentöversikt där du får en förhandsgranskning av kundprofiler som är kvalificerade för ditt segment.

![Segmentering](./images/savedsegment.png)

Du kan nu fortsätta med nästa övning och använda ditt segment med Adobe Target.

Nästa steg: [1.4 Take Action: send your segment to Adobe Target](./ex4.md)

[Gå tillbaka till användarflöde 1](./uc1.md)

[Gå tillbaka till Alla moduler](../../overview.md)
