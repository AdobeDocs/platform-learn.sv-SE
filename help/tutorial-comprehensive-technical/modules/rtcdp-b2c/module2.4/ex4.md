---
title: Segmentaktivering till Microsoft Azure Event Hub - Aktivera segment
description: Segmentaktivering till Microsoft Azure Event Hub - Aktivera segment
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---

# 2.4.4 Aktivera segment

## 2.4.4.1 Lägg till segment till Azure Event Hub-målet

I den här övningen ska du lägga till ditt segment `--aepUserLdap-- - Interest in Equipment` i ditt `--aepUserLdap---aep-enablement` Azure Event Hub-mål.

Logga in på Adobe Experience Platform via följande URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

När du har loggat in loggar du in på Adobe Experience Platform hemsida.

![Datainmatning](./../../../modules/datacollection/module1.2/images/home.png)

Innan du fortsätter måste du välja en **sandlåda**. Sandlådan som ska markeras har namnet ``--aepSandboxName--``. Du kan göra detta genom att klicka på texten **[!UICONTROL Production Prod]** i den blå raden ovanför skärmen. När du har valt rätt sandlåda ser du skärmändringen och nu befinner du dig i din dedikerade sandlåda.

![Datainmatning](./../../../modules/datacollection/module1.2/images/sb1.png)

Gå till **Destinationer** och klicka sedan på **Bläddra**. Då ser du alla tillgängliga destinationer. Leta upp målet och klicka på ikonen **+** enligt nedan.

![5-01-select-destination.png](./images/5-01-select-destination.png)

Då ser du det här. Sök efter ditt segment med hjälp av din ldap och välj `--aepUserLdap-- - Interest in Equipment` i listan med segment.

Klicka på **Nästa**.

![5-04-select-segment.png](./images/5-04-select-segment.png)

Adobe Experience Platform CDP i realtid kan leverera en nyttolast till två typer av destinationer, segmentdestinationer och profildestinationer.

Segmentdestinationer får en fördefinierad segmentkvalificeringsnyttolast som kommer att diskuteras senare. En sådan nyttolast innehåller **alla** segmentkvalifikationerna för en viss profil. Även för segment som inte finns med i målets aktiveringslista. Ett exempel på ett sådant segmentmål är **Azure Event Hubs** och **AWS Kinesis**.

Profilbaserade mål gör att du kan välja valfritt attribut (firstName, lastName, ...) från XDM-profilens unionsschema och inkludera det i aktiveringsnyttolasten. Ett exempel på en sådan destination är **E-postmarknadsföring**.

Eftersom din Azure Event Hub-destination är ett **segment**-mål väljer du till exempel fältet `--aepTenantId--.identification.core.ecid`.

Klicka på **Lägg till nytt fält**, klicka på Bläddra schema och markera fältet `--aepTenantId--identification.core.ecid` (ta bort alla andra fält som skulle visas automatiskt).

Klicka på **Nästa**.

![5-05-select-attributes.png](./images/5-05-select-attributes.png)

Klicka på **Slutför**.

![5-06-destination-finish.png](./images/5-06-destination-finish.png)

Ditt segment är nu aktiverat mot din Microsoft Event Hub-destination.

![5-07-destination-segment-added.png](./images/5-07-destination-segment-added.png)

Nästa steg: [2.4.5 Skapa ditt Microsoft Azure-projekt](./ex5.md)

[Gå tillbaka till modul 2.4](./segment-activation-microsoft-azure-eventhub.md)

[Gå tillbaka till Alla moduler](./../../../overview.md)
