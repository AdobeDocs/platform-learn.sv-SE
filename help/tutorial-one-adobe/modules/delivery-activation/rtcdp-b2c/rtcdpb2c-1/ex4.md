---
title: Foundation - kundprofil i realtid - Skapa en målgrupp - användargränssnitt
description: Foundation - kundprofil i realtid - Skapa en målgrupp - användargränssnitt
kt: 5342
doc-type: tutorial
exl-id: 4870ea42-810b-400b-8285-ab1f89c6a018
source-git-commit: 9c4d585d99920f0cdfd9de083c3f020f0d8171ab
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 2%

---

# 2.1.4 Skapa en målgrupp - användargränssnitt

I den här övningen skapar du en publik genom att använda Adobe Experience Platform Audience Builder.

Gå till [Adobe Experience Platform](https://experience.adobe.com/platform). När du har loggat in loggar du in på Adobe Experience Platform hemsida.

![Datainmatning](./../../../../modules/delivery-activation/datacollection/dc1.2/images/home.png)

Innan du fortsätter måste du välja en **sandlåda**. Sandlådan som ska markeras har namnet ``--aepSandboxName--``. När du har valt rätt [!UICONTROL sandbox] visas skärmändringen och nu är du i din dedikerade [!UICONTROL sandbox].

![Datainmatning](./../../../../modules/delivery-activation/datacollection/dc1.2/images/sb1.png)

Gå till **Publiker** på menyn till vänster. På den här sidan visas en översikt över alla befintliga målgrupper. Klicka på knappen **+ Skapa målgrupp** för att börja skapa en ny målgrupp.

![Segmentering](./images/menuseg.png)

Välj **Skapa regel** och klicka på **Skapa**.

![Segmentering](./images/menusegbr.png)

När du är i målgruppsverktyget lägger du omedelbart märke till menyalternativet **Attribut** och referensen **XDM Individual Profile** .

![Segmentering](./images/segmentationui.png)

Eftersom XDM är det språk som driver upplevelseverksamheten är XDM också grunden för målgruppsbyggaren. Alla data som är inkapslade i Platform ska mappas mot XDM, och som sådana blir alla data en del av samma datamodell oavsett varifrån dessa data kommer. Detta ger er en stor fördel när ni bygger målgrupper, och från det här användargränssnittet för målgruppsbyggaren kan ni kombinera data från vilket ursprung som helst i samma arbetsflöde. Publiker som skapats i målgruppsbyggaren kan skickas till lösningar som Adobe Target, Adobe Campaign och Adobe Audience Manager för aktivering.

Låt oss skapa en målgrupp som innehåller alla **manliga** kunder.

För att komma till könsattributet måste du förstå och känna till XDM.

Kön är ett attribut till Person, som finns under Attribut. För att komma dit börjar du med att klicka på **XDM Individual Profile**. Då ser du det här. I fönstret **XDM Individual Profile** väljer du **Person**.

![Segmentering](./images/person.png)

Då ser du det här. I **Person** hittar du attributet **Kön**. Dra könsattributet till målgruppsverktyget.

![Segmentering](./images/gender.png)

Nu kan du välja ett specifikt kön bland de förifyllda alternativen. I det här fallet väljer vi **Man**.

![Segmentering](./images/genderselection.png)

När du har valt **Handbok** kan du få en uppskattning av målgruppens population genom att trycka på knappen **Uppdatera uppskattning** . Detta är mycket användbart för en affärsanvändare, så att de kan se effekten av vissa attribut på målgruppens storlek.

![Segmentering](./images/segmentpreview.png)

Du kommer då att se en uppskattning som den nedan:

![Segmentering](./images/segmentpreviewest.png)

Därefter bör ni förfina er målgrupp lite. Du måste skapa en målgrupp med alla manliga kunder som har tittat på produkten **iPhone 15 Pro**.

Om ni vill bygga ut den här målgruppen måste ni lägga till en Experience Event. Du kan hitta alla Experience Events genom att klicka på ikonen **Händelser** i menyfältet **Fält** . Därefter visas noden **XDM ExperienceEvents** på den översta nivån. Klicka på **XDM ExperienceEvent**.

![Segmentering](./images/findee.png)

Gå till **Produktlisteobjekt**.

![Segmentering](./images/plitems.png)

Markera **Namn** och dra och släpp objektet **Namn** från den vänstra menyn på målgruppsarbetsytan i avsnittet **Händelser**.

![Segmentering](./images/eeweb.png)

Då ser du det här:

![Segmentering](./images/eewebpdtlname.png)

Jämförelseparametern ska vara **lika med** och i indatafältet anger du **iPhone 15 Pro**.

![Segmentering](./images/pv.png)

Ange tidsvillkoret för ditt segment till **Under de senaste 24 timmarna**.

![Segmentering](./images/pv1.png)

Varje gång du lägger till ett element i målgruppsverktyget kan du klicka på knappen **Uppdatera uppskattning** för att få en ny uppskattning av målgruppspopulationen.

Hittills har ni bara använt användargränssnittet för att skapa er målgrupp, men det finns också ett kodalternativ för att skapa en målgrupp.

När du skapar en målgrupp komponerar du faktiskt en Profile Query Language-fråga (PQL). Om du vill visualisera PQL-koden kan du klicka på **kodvyn** i det övre högra hörnet i målgruppsverktyget.

![Segmentering](./images/codeview.png)

Nu kan du se hela PQL-satsen:

```sql
person.gender in ["male"] and CHAIN(xEvent, timestamp, [C0: WHAT(productListItems.exists(name.equals("iPhone 15 Pro", false)))])
```

Du kan också förhandsgranska ett exempel på kundprofiler som är en del av den här målgruppen genom att klicka på **Visa profiler**.

![Segmentering](./images/previewprofilesdtl.png)

Äntligen får ni ett namn
Ange **Utvärderingsmetoden** till **Edge** och klicka på **Publicera**.

Använd följande som namnkonvention:

- `--aepUserLdap-- - Male customers with interest in iPhone 15 Pro`

![Segmentering](./images/segmentname.png)

Du kommer tillbaka till sidan Audience overview.

![Segmentering](./images/savedsegment.png)

## Nästa steg

Gå till [2.1.5 Se hur kundprofilen i realtid fungerar i Call Center](./ex5.md){target="_blank"}

Gå tillbaka till [Kundprofil i realtid](./real-time-customer-profile.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../../overview.md){target="_blank"}
