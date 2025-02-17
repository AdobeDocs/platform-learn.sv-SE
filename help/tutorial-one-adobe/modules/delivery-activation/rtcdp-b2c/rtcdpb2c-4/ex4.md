---
title: Audience Activation till Microsoft Azure Event Hub - Skapa en målgrupp
description: Audience Activation till Microsoft Azure Event Hub - Skapa en målgrupp
kt: 5342
doc-type: tutorial
exl-id: d9450e18-7c9b-4a6c-8317-19baf99d43a3
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%

---

# 2.4.4 Skapa en målgrupp

## Introduktion

Du kommer att skapa en enkel publik:

- **Intresse för planer** som kunder är kvalificerade för när de besöker sidan **Planer** på demowebbplatsen CitiSignal.

### Bra att veta

CDP-aktivering i realtid utlöser en aktivering till ett mål när ni kvalificerar er för en målgrupp som ingår i målets aktiveringslista. I så fall kommer målgruppsklassificeringsnyttolasten som skickas till det målet att innehålla **alla målgrupper som din kundprofil kvalificerar** för.

Målet med den här modulen är att visa att kundprofilens målgruppskvalifikation skickas till din Event Hub-destination i nära realtid.

### Målgruppsstatus

En målgruppsklassificering i Adobe Experience Platform har alltid en **status**-egenskap och kan vara något av följande:

- **realiserat**: Detta indikerar en ny publikkvalificering
- **avslutad**: Detta anger att profilen inte längre är kvalificerad för målgruppen

## Bygg publiken

Logga in på Adobe Experience Platform via följande URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

När du har loggat in loggar du in på Adobe Experience Platform hemsida.

![Datainmatning](./../../../../modules/delivery-activation/datacollection/dc1.2/images/home.png)

Innan du fortsätter måste du välja en **sandlåda**. Sandlådan som ska markeras har namnet ``--aepSandboxName--``. När du har valt rätt sandlåda ser du skärmändringen och nu befinner du dig i din dedikerade sandlåda.

![Datainmatning](./../../../../modules/delivery-activation/datacollection/dc1.2/images/sb1.png)

Gå till **Publiker**. Klicka på knappen **+ Skapa målgrupp**.

![Datainmatning](./images/seg.png)

Välj **Skapa regel** och klicka på **Skapa**.

![Datainmatning](./images/seg1.png)

Namnge målgruppen `--aepUserLdap-- - Interest in Plans`, ange utvärderingsmetoden till **Edge** och lägg till sidnamnet från upplevelsehändelsen.

Klicka på **Händelser** och dra och släpp **XDM ExperienceEvent > Webb > Information om webbsidor > Namn**. Ange **planer** som värde:

![4-05-create-ee-2.png](./images/405createee2.png)

Dra och släpp **XDM ExperienceEvent > `--aepTenantId--` > DemoEnvironment > brandName**. Ange `--aepUserLdap--` som värde, ställ in jämförelseparametern på **contains** och klicka på **Publish**:

![4-05-create-ee-2-brand.png](./images/405createee2brand.png)

Din publik är nu publicerad.

![4-05-create-ee-2-brand.png](./images/405createee2brand1.png)

## Nästa steg

Gå till [2.4.5 Aktivera din målgrupp](./ex5.md){target="_blank"}

Gå tillbaka till [Real-Time CDP: Audience Activation till Microsoft Azure Event Hub](./segment-activation-microsoft-azure-eventhub.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../../overview.md){target="_blank"}
