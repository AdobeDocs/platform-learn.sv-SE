---
title: Kundens AI - Instrumentpanel för bedömning och segmentering (predikt & Take Action)
description: Kundens AI - Instrumentpanel för bedömning och segmentering (predikt & Take Action)
kt: 5342
doc-type: tutorial
exl-id: a6df3ff1-f907-4185-8189-f0b39c67c943
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# 2.2.3 Kundens AI - Instrumentpanel för bedömning och segmentering (predikt &amp; Take Action)

När kundens AI-instans har slutfört en modellkörning kan ni visualisera den benägenhetspoäng som utvärderas för att förutsäga att kunden genomför ett köp inom 30 dagar.

![AI](./images/caiinstancesummary1.png)

>[!NOTE]
>
>Det är bara en kunds-AI-instans med statusen **Slutfört** som du kan förhandsgranska tjänstens insikter.

## Förutsägelse av känslighet

Nu ska vi granska den förväntade benägenheten som genereras av kundens AI-instansmodell. Klicka på instansnamnet för att visa kontrollpanelen.

![AI](./images/caimodels1.png)

Kundens AI-instrumentpanel visar sammanfattningen om poäng, fördelning av populationen och de faktorer som påverkar modellen.

![AI-beskrivning](./images/caidescription.png)

Håll muspekaren över de inflytelserika faktorerna för att se hur datafördelningen kan fördelas ytterligare.

![Påverkansfaktorer](./images/caiinfluencefactors.png)

## Affärsåtgärder

### Segmentera kunder

Med kundens AI-panel kan du definiera segment med ett enda klick. Klicka på knappen **Skapa segment** på benägenhetskorten.

![Skapa ett segment](./images/caiinfluencefactors1.png)

Du ser att en segmentdefinition skapas automatiskt.

![Segmentregel](./images/caicreatesegment.png)

Ge segmentet ett namn enligt följande namnkonvention: `--aepUserLdap-- - Customer AI High Propensity`. Klicka på **Publicera**.

![Segmentregel](./images/caicreatesegment1.png)

Du kan nu använda det här segmentet för målinriktning med till exempel CDP i realtid, Journey Optimizer och Adobe Target.

## Rensa

För att säkerställa att inga onödiga demodata sparas i din miljö måste du ta bort datauppsättningen `--aepUserLdap-- - Demo System - Customer Experience Event Dataset` när du har slutfört den här övningen. Om du inte tar bort demodata kommer det att påverka AEP-instansen negativt.

![Profil](./images/cleanup.png)

## Nästa steg

Gå till [Sammanfattning och förmåner](./summary.md){target="_blank"}

Gå tillbaka till [Intelligenta tjänster](./intelligent-services.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../../overview.md){target="_blank"}
