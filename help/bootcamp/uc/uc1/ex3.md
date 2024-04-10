---
title: Bootcamp - kundprofil i realtid - Skapa en målgrupp - användargränssnitt
description: Bootcamp - kundprofil i realtid - Skapa en målgrupp - användargränssnitt
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Audiences
exl-id: 37d4a5e8-e2bc-4c8c-a74f-09f74ea79962
source-git-commit: 0474808b42925bf95529e10a42a0563f0ecc43b8
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 2%

---

# 1.3 Skapa en målgrupp - användargränssnitt

I den här övningen skapar du en publik genom att använda Adobe Experience Platform Audience Builder.

## Artikel

Gå till [Adobe Experience Platform](https://experience.adobe.com/platform). När du har loggat in loggar du in på Adobe Experience Platform hemsida.

![Inmatning av data](./images/home.png)

Innan du fortsätter måste du välja en **sandlåda**. Sandlådan som ska markeras har namnet ``Bootcamp``. Du kan göra detta genom att klicka på texten **[!UICONTROL Production Prod]** i den blå linjen ovanför skärmen. När du har valt lämplig [!UICONTROL sandbox]kommer du att se skärmändringen och nu är du med på din [!UICONTROL sandbox].

![Inmatning av data](./images/sb1.png)

På menyn till vänster går du till **Målgrupper**. På den här sidan visas Dashboards med viktig information om **Målgrupp** prestanda.

![Segmentering](./images/menuseg.png)

Klicka på **Bläddra** för att få en översikt över alla befintliga målgrupper. Klicka på **+ Skapa målgrupper** för att börja skapa en ny publik.


![Segmentering](./images/segmentationui.png)

Ett popup-fönster visas där du tillfrågas om du vill **&#39;Disponera målgrupp&#39;** eller **&#39;Skapa regel&#39;**. Välj **&#39;Skapa regel&#39;** för att fortsätta och klicka **skapa**.

![Segmentering][def]

När ni väl är med i målgruppsbyggaren märker ni omedelbart **Attribut** menyalternativ och **Individuell XDM-profil** referens.


Eftersom XDM är det språk som driver upplevelseverksamheten är XDM också grunden för målgruppsbyggaren. Alla data som är inkapslade i Platform ska mappas mot XDM, och som sådana blir alla data en del av samma datamodell oavsett varifrån dessa data kommer. Detta ger er en stor fördel när ni bygger målgrupper, och från det här användargränssnittet för målgruppsbyggaren kan ni kombinera data från vilket ursprung som helst i samma arbetsflöde. Publiker som byggts i Audience Builder kan skickas till lösningar som Adobe Target, Adobe Campaign eller någon annan aktiveringskanal.

Nu måste ni skapa en målgrupp med alla kunder som har tittat på produkten **Real-Time CDP**.

Om ni vill bygga ut den här målgruppen måste ni lägga till en Experience Event. Du kan hitta alla Experience Events genom att klicka på **Händelser** ikonen i **Fält** menyraden.

![Segmentering](./images/findee.png)

Nu kommer du att se den översta nivån, **XDM ExperienceEvents** nod. Klicka på **XDM ExperienceEvent**.

![Segmentering](./images/see.png)

Gå till **Produktlisteobjekt**.

![Segmentering](./images/plitems.png)

Välj **Namn** och dra och släpp **Namn** objekt från den vänstra menyn till målgruppsarbetsytan i **Händelser** -avsnitt. Då ser du det här:

![Segmentering](./images/eewebpdtlname.png)

Jämförelseparametern ska vara **är lika med** och i inmatningsfältet anger du **CDP i realtid**.

![Segmentering](./images/pv.png)

Varje gång du lägger till ett element i målgruppsverktyget kan du klicka på **Uppdatera offert** för att få en ny uppskattning av populationen i er målgrupp.

![Segmentering](./images/refreshest.png)

Som **Utvärderingsmetod**, markera **Kant**.

![Segmentering](./images/evedge.png)

Till sist ger vi publiken ett namn och sparar det.

Använd följande som namnkonvention:

- `yourLastName - Interest in Real-Time CDP`

Klicka sedan på **Spara och stäng** för att rädda publiken.

![Segmentering](./images/segmentname.png)

Du kommer nu tillbaka till målgruppsöversikten där du ser en förhandsgranskning av kundprofiler som passar just er målgrupp.

![Segmentering](./images/savedsegment.png)

Du kan nu fortsätta med nästa övning och använda din publik med Adobe Target.

Nästa steg: [1.4 Take Action: send your audition to Adobe Target](./ex4.md)

[Gå tillbaka till användarflöde 1](./uc1.md)

[Gå tillbaka till Alla moduler](../../overview.md)


[def]: ./images/segmentationpopup.png
