---
title: Foundation - konfigurera Adobe Experience Platform Data Collection och Web SDK-tillägget - XDM-schemakrav i Adobe Experience Platform
description: Foundation - konfigurera Adobe Experience Platform Data Collection och Web SDK-tillägget - XDM-schemakrav i Adobe Experience Platform
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 8e17129c-633d-45bd-aa70-78cc3d3a2108
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---

# 1.7 XDM-schemakrav i Adobe Experience Platform

För att säkerställa att Web SDK och alloy.js kan importera data till Adobe Experience Platform finns det ett krav på att en specifik XDM-mixin ska ingå i XDM-schemat i Adobe Experience Platform.

Gå till [https://experience.adobe.com/platform](https://experience.adobe.com/platform) och logga in.

![AEP Debugger](./images/exp1.png)

När du har loggat in väljer du lämplig sandlåda genom att klicka på texten **Produktionsprodukt** i den blå linjen ovanför skärmen. Markera sandlådan `--aepSandboxId--`.

När du har valt sandlådan ser du skärmändringen och nu befinner du dig i sandlådan.

![AEP Debugger](./images/exp2.png)

Gå till den vänstra menyn **Scheman** och öppna **Demonstrationssystem - händelseschema för webbplats (Global v1.1)** Schema.

![AEP Debugger](./images/exp3.png)

I det schemat ser du att fältgruppen **AEP Web SDK ExperienceEvent Mixin** har lagts till. Den här fältgruppen lägger till alla minimalt obligatoriska fält i schemat. Alla Experience Event Schema i Adobe Experience Platform som ska användas av Web SDK kräver alltid att fältgruppen är en del av schemat.

![AEP Debugger](./images/exp4.png)

I [Modul 2](./../module2/data-ingestion.md) du får lära dig hur du lägger till fältgrupper i scheman.

Nästa steg: [Sammanfattning och fördelar](./summary.md)

[Gå tillbaka till modul 1](./data-ingestion-launch-web-sdk.md)

[Gå tillbaka till Alla moduler](./../../overview.md)
