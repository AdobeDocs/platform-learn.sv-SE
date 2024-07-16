---
title: Bootcamp - kundprofil i realtid - Skapa en målgrupp - användargränssnitt
description: Bootcamp - kundprofil i realtid - Skapa en målgrupp - användargränssnitt
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Audiences
exl-id: 37d4a5e8-e2bc-4c8c-a74f-09f74ea79962
source-git-commit: 5876de5015e4c8c337c235c24cc28b0a32e274dd
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 2%

---

# 1.3 Skapa en målgrupp - användargränssnitt

I den här övningen skapar du en publik genom att använda Adobe Experience Platform Audience Builder.

## Artikel

Gå till [Adobe Experience Platform](https://experience.adobe.com/platform). När du har loggat in loggar du in på Adobe Experience Platform hemsida.

![Datainmatning](./images/home.png)

Innan du fortsätter måste du välja en **sandlåda**. Sandlådan som ska markeras har namnet ``Bootcamp``. Du kan göra detta genom att klicka på texten **[!UICONTROL Production Prod]** i den blå raden ovanför skärmen. När du har valt rätt [!UICONTROL sandbox] visas skärmändringen och nu är du i din dedikerade [!UICONTROL sandbox].

![Datainmatning](./images/sb1.png)

Gå till **Publiker** på menyn till vänster. På den här sidan visas instrumentpaneler med viktig information om **målgruppens** prestanda.

![Segmentering](./images/menuseg.png)

Klicka på **Bläddra** om du vill se en översikt över alla befintliga målgrupper. Klicka på knappen **+ Skapa målgrupp** för att börja skapa en ny målgrupp.


![Segmentering](./images/segmentationui.png)

Ett popup-fönster visas där du tillfrågas om du vill **&#39;Disponera målgrupp&#39;** eller **&#39;Build rule&#39;**. Välj **&#39;Skapa regel&#39;** för att fortsätta och klicka på **skapa**.

![Segmentering][def]

När du är i målgruppsverktyget lägger du omedelbart märke till menyalternativet **Attribut** och referensen **XDM Individual Profile** .


Eftersom XDM är det språk som driver upplevelseverksamheten är XDM också grunden för målgruppsbyggaren. Alla data som är inkapslade i Platform ska mappas mot XDM, och som sådana blir alla data en del av samma datamodell oavsett varifrån dessa data kommer. Detta ger er en stor fördel när ni bygger målgrupper, och från det här användargränssnittet för målgruppsbyggaren kan ni kombinera data från vilket ursprung som helst i samma arbetsflöde. Publiker som byggts i Audience Builder kan skickas till lösningar som Adobe Target, Adobe Campaign eller någon annan aktiveringskanal.

Nu måste du skapa en målgrupp med alla kunder som har tittat på produkten **Real-Time CDP**.

Om ni vill bygga ut den här målgruppen måste ni lägga till en Experience Event. Du kan hitta alla Experience Events genom att klicka på ikonen **Händelser** i menyfältet **Fält** .

![Segmentering](./images/findee.png)

Därefter visas noden **XDM ExperienceEvents** på den översta nivån. Klicka på **XDM ExperienceEvent**.

![Segmentering](./images/see.png)

Gå till **Produktlisteobjekt**.

![Segmentering](./images/plitems.png)

Markera **Namn** och dra och släpp objektet **Namn** från den vänstra menyn på målgruppsarbetsytan i avsnittet **Händelser**. Då ser du det här:

![Segmentering](./images/eewebpdtlname.png)

Jämförelseparametern ska vara **lika med** och i indatafältet ska du ange **CDP i realtid**.

![Segmentering](./images/pv.png)

Varje gång du lägger till ett element i målgruppsverktyget kan du klicka på knappen **Uppdatera uppskattning** för att få en ny uppskattning av målgruppspopulationen.

![Segmentering](./images/refreshest.png)

Som **Utvärderingsmetod** väljer du **Edge**.

![Segmentering](./images/evedge.png)

Till sist ger vi publiken ett namn och sparar det.

Använd följande som namnkonvention:

- `yourLastName - Interest in Real-Time CDP`

Klicka sedan på knappen **Spara och stäng** för att spara din publik.

![Segmentering](./images/segmentname.png)

Du kommer nu tillbaka till målgruppsöversikten där du ser en förhandsgranskning av kundprofiler som passar just er målgrupp.

![Segmentering](./images/savedsegment.png)

Du kan nu fortsätta med nästa övning och använda din publik med Adobe Target.

Nästa steg: [1.4 Vidta åtgärd: skicka målgruppen till Adobe Target](./ex4.md)

[Gå tillbaka till användarflöde 1](./uc1.md)

[Gå tillbaka till Alla moduler](../../overview.md)


[def]: ./images/segmentationpopup.png
