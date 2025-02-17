---
title: Foundation - konfigurera Adobe Experience Platform Data Collection och Web SDK-tillägget - XDM-schemakrav i Adobe Experience Platform
description: Foundation - konfigurera Adobe Experience Platform Data Collection och Web SDK-tillägget - XDM-schemakrav i Adobe Experience Platform
kt: 5342
doc-type: tutorial
exl-id: 124c9c54-27f1-4784-9a5c-2c9d8ba620d5
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---

# 1.1.7 XDM-schemakrav i Adobe Experience Platform

För att säkerställa att Web SDK kan importera data till Adobe Experience Platform måste en viss XDM-blandning ingå i XDM-schemat i Adobe Experience Platform.

Gå till [https://experience.adobe.com/platform](https://experience.adobe.com/platform) och logga in.

![AEP-felsökning](./images/exp1.png)

När du har loggat in väljer du lämplig sandlåda genom att klicka på texten **Produktionsprodukt** på den blå raden ovanför skärmen. Markera sandlådan `--aepSandboxName--`.

När du har valt sandlådan ser du skärmändringen och nu befinner du dig i sandlådan.

![AEP-felsökning](./images/exp2.png)

Gå till **Scheman** på den vänstra menyn och öppna **Demo System - Event Schema för webbplats (Global v1.1)** Schema.

![AEP-felsökning](./images/exp3.png)

I det schemat ser du att fältgruppen **AEP Web SDK ExperienceEvent** har lagts till. Den här fältgruppen lägger till alla minimalt obligatoriska fält i schemat. Alla Experience Event Schema i Adobe Experience Platform som ska användas av Web SDK kräver alltid att fältgruppen är en del av schemat.

![AEP-felsökning](./images/exp4.png)

I [Modul 1.2 Datainmatning](./../dc1.2/data-ingestion.md) får du lära dig hur du lägger till fältgrupper i scheman.

Nästa steg:

## Nästa steg

Gå till [Sammanfattning och förmåner](./summary.md){target="_blank"}

Gå tillbaka till [Konfigurera Adobe Experience Platform Data Collection och taggtillägget Web SDK](./data-ingestion-launch-web-sdk.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../../overview.md){target="_blank"}
