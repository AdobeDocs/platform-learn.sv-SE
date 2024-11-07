---
title: Segmentaktivering till Microsoft Azure Event Hub - Skapa ett strömningssegment
description: Segmentaktivering till Microsoft Azure Event Hub - Skapa ett strömningssegment
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---

# 2.4.3 Skapa ett segment

## 2.4.3.1 Inledning

Du skapar ett enkelt segment:

- **Intresse för utrustning** som kundprofiler är kvalificerade för när de besöker sidan **Utrustning** på webbplatsen för Luma-demo.

### Bra att veta

CDP-aktivering i realtid utlöser en aktivering till ett mål när du kvalificerar dig för ett segment som ingår i målets aktiveringslista. I så fall kommer den segmentkvalificeringsnyttolast som skickas till det målet att innehålla **alla segment som din profil kvalificerar** för.

Målet med den här modulen är att visa att kundprofilens segmentkvalificering skickas till **ditt**-händelsehubbsmål i realtid.

### Segmentstatus

En segmentkvalificering i Adobe Experience Platform har alltid en **status**-egenskap och kan vara något av följande:

- **realiserat**: Detta anger att ett nytt segment kvalificerats
- **befintlig**: Detta indikerar en befintlig segmentkvalificering
- **avslutad**: Detta anger att profilen inte längre är kvalificerad för segmentet

## 2.4.3.2 Bygg segmentet

I [Modul 2.3](./../../../modules/rtcdp-b2c/module2.3/real-time-cdp-build-a-segment-take-action.md) förklaras i detalj hur du skapar ett segment.

### Skapa segment

Logga in på Adobe Experience Platform via följande URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

När du har loggat in loggar du in på Adobe Experience Platform hemsida.

![Datainmatning](./../../../modules/datacollection/module1.2/images/home.png)

Innan du fortsätter måste du välja en **sandlåda**. Sandlådan som ska markeras har namnet ``--aepSandboxName--``. Du kan göra detta genom att klicka på texten **[!UICONTROL Production Prod]** i den blå raden ovanför skärmen. När du har valt rätt sandlåda ser du skärmändringen och nu befinner du dig i din dedikerade sandlåda.

![Datainmatning](./../../../modules/datacollection/module1.2/images/sb1.png)

Gå till **Segment**. Klicka på knappen **+ Skapa segment**.

![Datainmatning](./images/seg.png)

Namnge ditt segment `--aepUserLdap-- - Interest in Equipment` och lägg till händelsen för sidnamnsupplevelsen:

Klicka på **Händelser** och dra och släpp **XDM ExperienceEvent > Webb > Information om webbsidor > Namn**. Ange **utrustning** som värde:

![4-05-create-ee-2.png](./images/4-05-create-ee-2.png)

Dra och släpp **XDM ExperienceEvent > `--aepTenantId--` > DemoEnvironment > brandName**. Ange `--aepUserLdap--` som värde, ställ in jämförelseparametern på **contains** och klicka på **Save**:

![4-05-create-ee-2-brand.png](./images/4-05-create-ee-2-brand.png)

### PQL Definition

PQL i ditt segment ser ut som:

```code
CHAIN(xEvent, timestamp, [C0: WHAT(web.webPageDetails.name.equals("equipment", false) and _experienceplatform.demoEnvironment.brandName.contains("--aepUserLdap--", false))])
```

Nästa steg: [2.4.4 Aktivera segment](./ex4.md)

[Gå tillbaka till modul 2.4](./segment-activation-microsoft-azure-eventhub.md)

[Gå tillbaka till Alla moduler](./../../../overview.md)
