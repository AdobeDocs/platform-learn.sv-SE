---
title: Segmentaktivering till Microsoft Azure Event Hub - Skapa ett strömningssegment
description: Segmentaktivering till Microsoft Azure Event Hub - Skapa ett strömningssegment
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: de3824bd-553c-4281-8edf-29abcc28a8e7
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 0%

---

# 13.3 Skapa ett segment

## 13.3.1 Inledning

Du skapar ett enkelt segment:

- **Intresse av utrustning** för vilka kundprofiler kvalificerar sig när de besöker **Utrustning** på webbplatsen för Luma demo.

### Bra att veta

CDP-aktivering i realtid utlöser en aktivering till ett mål när du kvalificerar dig för ett segment som ingår i målets aktiveringslista. I så fall kommer den segmentkvalificeringsnyttolast som skickas till den destinationen att innehålla **alla segment som din profil är kvalificerad för**.

Målet med den här modulen är att visa att kundprofilens segmentkvalificering skickas till **din** händelsenhetens mål i realtid.

### Segmentstatus

En segmentkvalificering i Adobe Experience Platform har alltid **status**-property och kan vara något av följande:

- **realiserad**: detta anger att ett nytt segment är kvalificerat
- **befintlig**: detta indikerar en befintlig segmentkvalificering
- **avslutad**: detta anger att profilen inte längre är kvalificerad för segmentet

## 13.3.2 Bygg segmentet

Hur man skapar ett segment förklaras i detalj i [Modul 6](../module6/real-time-cdp-build-a-segment-take-action.md).

### Skapa segment

Logga in på Adobe Experience Platform genom att gå till denna URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

När du loggat in kommer du till Adobe Experience Platform hemsida.

![Dataintag](../module2/images/home.png)

Innan du fortsätter måste du välja en **sandlåda**. Sandlådan som ska markeras har namnet ``--aepSandboxId--``. Du kan göra detta genom att klicka på texten **[!UICONTROL Produktionsprodukt]** i den blå linjen ovanför skärmen. När du har valt rätt sandlåda ser du skärmändringen och nu befinner du dig i din dedikerade sandlåda.

![Dataintag](../module2/images/sb1.png)

Gå till **Segment**. Klicka på **+ Skapa segment** -knappen.

![Dataintag](./images/seg.png)

Namnge ditt segment `--demoProfileLdap-- - Interest in Equipment` och lägg till händelsen för sidnamnsupplevelsen:

Klicka på **Händelser** och dra och släppa **XDM ExperienceEvent > Webb > Information om webbsidor > Namn**. Retur **utrustning** som värdet:

![4-05-create-ee-2.png](./images/4-05-create-ee-2.png)

Dra och släpp **XDM ExperienceEvent > `--aepTenantIdSchema--` > demoEnvironment > brandName**. Retur `--demoProfileLdap--` som värdet anger du jämförelseparametern till **innehåller** och klicka **Spara**:

![4-05-create-ee-2-brand.png](./images/4-05-create-ee-2-brand.png)

### PQL-definition

Segmentets PQL ser ut så här:

```code
CHAIN(xEvent, timestamp, [C0: WHAT(web.webPageDetails.name.equals("equipment", false) and _experienceplatform.demoEnvironment.brandName.contains("--demoProfileLdap--", false))])
```

Nästa steg: [13.4 Aktivera segment](./ex4.md)

[Gå tillbaka till modul 13](./segment-activation-microsoft-azure-eventhub.md)

[Gå tillbaka till Alla moduler](./../../overview.md)
