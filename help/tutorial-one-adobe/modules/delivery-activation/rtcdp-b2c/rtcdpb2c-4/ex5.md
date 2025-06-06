---
title: Audience Activation till Microsoft Azure Event Hub - Aktivera målgrupp
description: Audience Activation till Microsoft Azure Event Hub - Aktivera målgrupp
kt: 5342
doc-type: tutorial
exl-id: e6bac0ce-4a1e-4458-af3e-3d6ac40b9cb5
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 0%

---

# 2.4.5 Aktivera er målgrupp

## Lägg till målgrupp i Azure Event Hub-målet

I den här övningen lägger du till din målgrupp `--aepUserLdap-- - Interest in Plans` i ditt `--aepUserLdap---aep-enablement` Azure Event Hub-mål.

Logga in på Adobe Experience Platform via följande URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

När du har loggat in loggar du in på Adobe Experience Platform hemsida.

![Datainmatning](./../../../../modules/delivery-activation/datacollection/dc1.2/images/home.png)

Innan du fortsätter måste du välja en **sandlåda**. Sandlådan som ska markeras har namnet ``--aepSandboxName--``. När du har valt rätt sandlåda ser du skärmändringen och nu befinner du dig i din dedikerade sandlåda.

![Datainmatning](./../../../../modules/delivery-activation/datacollection/dc1.2/images/sb1.png)

Gå till **Destinationer** och klicka sedan på **Bläddra**. Då ser du alla tillgängliga destinationer. Leta upp målplatsen och klicka på de 3 punkterna&#x200B;**..** som anges nedan och klicka sedan på **Aktivera målgrupper**.

![5-01-select-destination.png](./images/501selectdestination.png)

Då ser du det här. Sök efter din målgrupp med hjälp av din ldap och välj `--aepUserLdap-- - Interest in Plans` i listan över målgrupper.

Klicka på **Nästa**.

![5-04-select-segment.png](./images/504selectsegment.png)

Klicka på **Lägg till nytt fält**, klicka på Bläddra schema och markera fältet `--aepTenantId--identification.core.ecid` (ta bort alla andra fält som skulle visas automatiskt).

Klicka på **Nästa**.

![5-05-select-attributes.png](./images/505selectattributes.png)

Klicka på **Slutför**.

![5-06-destination-finish.png](./images/506destinationfinish.png)

Din målgrupp är nu aktiverad mot din Microsoft Event Hub-destination.

![5-07-destination-segment-added.png](./images/507destinationsegmentadded.png)

## Nästa steg

Gå till [2.4.6 Skapa ditt Microsoft Azure-projekt](./ex6.md){target="_blank"}

Gå tillbaka till [Real-Time CDP: Audience Activation till Microsoft Azure Event Hub](./segment-activation-microsoft-azure-eventhub.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../../overview.md){target="_blank"}
