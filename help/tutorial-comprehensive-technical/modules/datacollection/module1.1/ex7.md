---
title: Foundation - konfigurera Adobe Experience Platform Data Collection och Web SDK-tillägget - XDM-schemakrav i Adobe Experience Platform
description: Foundation - konfigurera Adobe Experience Platform Data Collection och Web SDK-tillägget - XDM-schemakrav i Adobe Experience Platform
kt: 5342
doc-type: tutorial
exl-id: 3fc4a1d6-4130-464e-98c0-5b9cac8051a0
source-git-commit: 0dbcda0cfc9f199a44c845c1b5caf00a8d740251
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# 1.1.7 XDM-schemakrav i Adobe Experience Platform

För att säkerställa att Web SDK och alloy.js kan importera data till Adobe Experience Platform finns det ett krav på att en specifik XDM-mixin ska ingå i XDM-schemat i Adobe Experience Platform.

Gå till [https://experience.adobe.com/platform](https://experience.adobe.com/platform) och logga in.

![AEP-felsökning](./images/exp1.png)

När du har loggat in väljer du lämplig sandlåda genom att klicka på texten **Produktionsprodukt** på den blå raden ovanför skärmen. Markera sandlådan `--aepSandboxName--`.

När du har valt sandlådan ser du skärmändringen och nu befinner du dig i sandlådan.

![AEP-felsökning](./images/exp2.png)

Gå till **Scheman** på den vänstra menyn och öppna **Demo System - Event Schema för webbplats (Global v1.1)** Schema.

![AEP-felsökning](./images/exp3.png)

I det schemat ser du att fältgruppen **AEP Web SDK ExperienceEvent** har lagts till. Den här fältgruppen lägger till alla minimalt obligatoriska fält i schemat. Alla Experience Event Schema i Adobe Experience Platform som ska användas av Web SDK kräver alltid att fältgruppen är en del av schemat.

![AEP-felsökning](./images/exp4.png)

I [Modul 1.2](./../module1.2/data-ingestion.md) får du lära dig att lägga till fältgrupper i scheman.

Nästa steg: [Sammanfattning och förmåner](./summary.md)

[Gå tillbaka till modul 1.1](./data-ingestion-launch-web-sdk.md)

[Gå tillbaka till Alla moduler](./../../../overview.md)
