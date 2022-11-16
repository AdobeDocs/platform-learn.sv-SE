---
title: Segmentaktivering till Microsoft Azure Event Hub - Aktivera segment
description: Segmentaktivering till Microsoft Azure Event Hub - Aktivera segment
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 250f8536-b6bd-4c64-a552-80d5c6fb6358
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 1%

---

# 13.4 Aktivera segment

## 13.4.1 Lägg till segment i Azure Event Hub-målet

I den här övningen ska du lägga till ditt segment `--demoProfileLdap-- - Interest in Equipment` till `--demoProfileLdap---aep-enablement` Azure Event Hub-mål.

Logga in på Adobe Experience Platform genom att gå till denna URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

När du loggat in kommer du till Adobe Experience Platform hemsida.

![Dataintag](../module2/images/home.png)

Innan du fortsätter måste du välja en **sandlåda**. Sandlådan som ska markeras har namnet ``--aepSandboxId--``. Du kan göra detta genom att klicka på texten **[!UICONTROL Produktionsprodukt]** i den blå linjen ovanför skärmen. När du har valt rätt sandlåda ser du skärmändringen och nu befinner du dig i din dedikerade sandlåda.

![Dataintag](../module2/images/sb1.png)

Gå till **Destinationer** och sedan klicka **Bläddra**. Då ser du alla tillgängliga destinationer. Leta upp målet och klicka på **+** ikonen enligt nedan.

![5-01-select-destination.png](./images/5-01-select-destination.png)

Du kommer då att se det här. Sök efter ditt segment med hjälp av din ldap och välj `--demoProfileLdap-- - Interest in Equipment` i listan över segment.

Klicka på **Nästa**.

![5-04-select-segment.png](./images/5-04-select-segment.png)

Adobe Experience Platform CDP i realtid kan leverera en nyttolast till två typer av destinationer, segmentdestinationer och profildestinationer.

Segmentdestinationer får en fördefinierad segmentkvalificeringsnyttolast som kommer att diskuteras senare. En sådan nyttolast innehåller **alla** Segmentkvalifikationer för en viss profil. Även för segment som inte finns med i målets aktiveringslista. Ett exempel på ett sådant segmentmål är **Azure Event Hubs** och **AWS Kinesis**.

Profilbaserade mål gör att du kan välja valfritt attribut (firstName, lastName, ...) från XDM-profilens unionsschema och inkludera det i aktiveringsnyttolasten. Ett exempel på en sådan destination är **E-postmarknadsföring**.

Eftersom din Azure Event Hub-destination är en **segment** mål, välj till exempel fältet `--aepTenantId--.identification.core.ecid`.

Klicka **Lägg till nytt fält**, klicka på bläddra i schemat och markera fältet `--aepTenantId--identification.core.ecid` (ta bort alla andra fält som visas automatiskt).

Klicka på **Nästa**.

![5-05-select-attributes.png](./images/5-05-select-attributes.png)

Klicka **Slutför**.

![5-06-destination-finish.png](./images/5-06-destination-finish.png)

Ditt segment är nu aktiverat mot din Microsoft Event Hub-destination.

![5-07-destination-segment-added.png](./images/5-07-destination-segment-added.png)

Nästa steg: [13.5 Skapa ditt Microsoft Azure-projekt](./ex5.md)

[Gå tillbaka till modul 13](./segment-activation-microsoft-azure-eventhub.md)

[Gå tillbaka till Alla moduler](./../../overview.md)
