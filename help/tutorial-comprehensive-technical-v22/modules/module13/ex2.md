---
title: Segmentaktivering till Microsoft Azure Event Hub - Konfigurera Event Hub RTCDP-målet i Adobe Experience Platform
description: Segmentaktivering till Microsoft Azure Event Hub - Konfigurera Event Hub RTCDP-målet i Adobe Experience Platform
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: b42b4ccb-1952-480b-b538-c1bd661e29eb
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 0%

---

# 13.2 Konfigurera Azure Event Hub-målet i Adobe Experience Platform

## 13.2.1 Identifiera obligatoriska Azure Connection-parametrar

Om du vill definiera en Event Hub-destination i Adobe Experience Platform behöver du din

- Namnutrymme för händelsehubbar
- Händelsehubb
- Azure SAS-nyckelnamn
- Azure SAS-nyckel

Händelsehubben och EventHub-namnutrymmet har definierats i föregående åtgärd: [Utövning 1 - Konfigurera händelsehubben i Azure](./ex1.md)

### Namnutrymme för händelsehubbar

Om du vill söka efter ovanstående information i Azure Portal går du till [https://portal.azure.com/#home](https://portal.azure.com/#home). Kontrollera att du använder rätt Azure-konto.

Välj **Alla resurser** i Azure Portal:

![2-01-azure-all-resources.png](./images/2-01-azure-all-resources.png)

### Händelsehubb

Sök efter en resurs med resurstyp **Namnutrymme för händelsehubbar** Om du följde namngivningskonventionerna som användes i den föregående övningen kommer du att få namnutrymmet Event Hubs `--demoProfileLdap---aep-enablement`. Observera att du kommer att behöva det i nästa övning.

![2-02-select-event-hubs-namespace.png](./images/2-02-select-event-hubs-namespace.png)

Klicka på namnet på händelsehubbens namnområde för att få mer information:

![2-03-select-event-hub.png](./images/2-03-select-event-hub.png)

Välj **Händelsehubbar** om du vill ha en lista över händelsehubbar som definieras i namnutrymmet för händelsehubbar, och om du följt de namnkonventioner som användes i den föregående övningen, hittar du en händelsehubb med namnet `--demoProfileLdap---aep-enablement-event-hub`. Observera att du kommer att behöva det i nästa övning.

![2-04-event-hub-selected.png](./images/2-04-event-hub-selected.png)

### SAS-nyckelnamn

Välj **Principer för delad åtkomst** för **Namnutrymme för händelsehubbar**

![2-05-select-sas.png](./images/2-05-select-sas.png)

Du ser en lista över principer för delad åtkomst. SAS-nyckeln vi letar efter är **RootHanteraDeladÅtkomstnyckel**. Detta är namnet på SAS-nyckeln. Skriv ner det.

![2-06-sas-overview.png](./images/2-06-sas-overview.png)

### SAS-nyckelvärde

Klicka på **RootHanteraDeladÅtkomstnyckel** för att få SAS-nyckelvärdet. Och tryck på **Kopiera till Urklipp** -ikonen för att kopiera **Primär nyckel**:

![2-07-sas-key-value.png](./images/2-07-sas-key-value.png)

### Sammanfattning av målvärden

Nu bör du ha identifierat alla värden som behövs för att definiera Azure Event Hub-målet i Adobe Experience Platform CDP i realtid.

| Namn på målattribut | Värde för målattribut | Exempelvärde |
|---|---|---|
| sasKeyName | SAS-nyckelnamn | RootHanteraDeladÅtkomstnyckel |
| sasKey | SAS-nyckelvärde | srREx9ShJG1Rv7f/... |
| namespace | Namnutrymme för händelsehubbar | `--demoProfileLdap---aep-enablement` |
| eventHubName | Händelsehubb | `--demoProfileLdap---aep-enablement-event-hub` |

## 13.2.2 Skapa Azure Event Hub-mål i Adobe Experience Platform

Logga in på Adobe Experience Platform genom att gå till denna URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

När du loggat in kommer du till Adobe Experience Platform hemsida.

![Dataintag](../module2/images/home.png)

Innan du fortsätter måste du välja en **sandlåda**. Sandlådan som ska markeras har namnet ``--aepSandboxId--``. Du kan göra detta genom att klicka på texten **[!UICONTROL Produktionsprodukt]** i den blå linjen ovanför skärmen. När du har valt rätt sandlåda ser du skärmändringen och nu befinner du dig i din dedikerade sandlåda.

![Dataintag](../module2/images/sb1.png)

Gå till **Destinationer** och sedan gå till **Katalog**.

![Dataintag](./images/sb2a.png)

Välj **molnlagring** och gå till **Azure Event Hubs** och klicka **Konfigurera** eller **Konfigurera**:

![2-08-list-destination.png](./images/2-08-list-destinations.png)

Fyll i de målvärden som du har samlat in i föregående övning. Klicka på **Anslut till mål**.

![2-09-destination-values.png](./images/2-09-destination-values.png)

Om inloggningsuppgifterna är korrekta visas en bekräftelse: **Ansluten**.

![2-09-destination-values.png](./images/2-09-destination-valuesa.png)

Nu måste du ange namn och beskrivning i formatet `--demoProfileLdap---aep-enablement`. Ange **eventHubName** (se föregående övning ser det ut så här: `--demoProfileLdap---aep-enablement-event-hub`) och klicka på **Nästa**.

![2-10-create-destination.png](./images/2-10-create-destination.png)

Klicka **Spara och avsluta**.

![2-11-save-exit-activation.png](./images/2-11-save-exit-activation.png)

Målet har nu skapats och är tillgängligt i Adobe Experience Platform.

![2-12-destination-created.png](./images/2-12-destination-created.png)

Nästa steg: [13.3 Skapa ett segment](./ex3.md)

[Gå tillbaka till modul 13](./segment-activation-microsoft-azure-eventhub.md)

[Gå tillbaka till Alla moduler](./../../overview.md)
