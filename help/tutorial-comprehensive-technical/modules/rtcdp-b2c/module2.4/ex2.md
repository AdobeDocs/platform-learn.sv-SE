---
title: Segmentaktivering till Microsoft Azure Event Hub - Konfigurera Event Hub RTCDP-målet i Adobe Experience Platform
description: Segmentaktivering till Microsoft Azure Event Hub - Konfigurera Event Hub RTCDP-målet i Adobe Experience Platform
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 0%

---

# 2.4.2 Konfigurera Azure Event Hub-målet i Adobe Experience Platform

## 2.4.2.1 Identifiera obligatoriska Azure Connection-parametrar

Om du vill definiera en Event Hub-destination i Adobe Experience Platform behöver du din

- Namnutrymme för händelsehubbar
- Händelsehubb
- Azure SAS-nyckelnamn
- Azure SAS-nyckel

Händelsehubben och EventHub-namnutrymmet har definierats i den föregående övningen: [Utgång 1 - Konfigurera händelsehubben i Azure](./ex1.md)

### Namnutrymme för händelsehubbar

Om du vill söka efter ovanstående information i Azure Portal går du till [https://portal.azure.com/#home](https://portal.azure.com/#home). Kontrollera att du använder rätt Azure-konto.

Välj **Alla resurser** i Azure Portal:

![2-01-azure-all-resources.png](./images/2-01-azure-all-resources.png)

### Händelsehubb

Leta efter en resurs med resurstypen **Event Hubs Namespace**. Om du följt namnkonventionerna som användes i den tidigare övningen kommer du att använda Event Hubs Namespace `--aepUserLdap---aep-enablement`. Observera att du kommer att behöva det i nästa övning.

![2-02-select-event-hubs-namespace.png](./images/2-02-select-event-hubs-namespace.png)

Klicka på namnet på händelsehubbens namnområde för att få mer information:

![2-03-select-event-hub.png](./images/2-03-select-event-hub.png)

Välj **Händelsehubbar** om du vill visa en lista över händelsehubbar som har definierats i namnutrymmet för händelsehubbar. Om du följde namnkonventionerna som användes i den föregående övningen hittar du en händelsehubb med namnet `--aepUserLdap---aep-enablement-event-hub`. Observera att du kommer att behöva det i nästa övning.

![2-04-event-hub-selected.png](./images/2-04-event-hub-selected.png)

### SAS-nyckelnamn

Välj **Principer för delad åtkomst** för **namnområdet för händelsehubbar**

![2-05-select-sas.png](./images/2-05-select-sas.png)

Du ser en lista över principer för delad åtkomst. SAS-nyckeln som vi letar efter är **RootManageSharedAccessKey**. Detta är namnet på SAS-nyckeln. Skriv ner det.

![2-06-sas-overview.png](./images/2-06-sas-overview.png)

### SAS-nyckelvärde

Klicka på **RootManageSharedAccessKey** för att hämta SAS-nyckelvärdet. Tryck på ikonen **Kopiera till Urklipp** för att kopiera **primärnyckeln**:

![2-07-sas-key-value.png](./images/2-07-sas-key-value.png)

### Sammanfattning av målvärden

Nu bör du ha identifierat alla värden som behövs för att definiera Azure Event Hub-målet i Adobe Experience Platform CDP i realtid.

| Namn på målattribut | Värde för målattribut | Exempelvärde |
|---|---|---|
| sasKeyName | SAS-nyckelnamn | RootHanteraDeladÅtkomstnyckel |
| sasKey | SAS-nyckelvärde | srREx9ShJG1Rv7f/... |
| namespace | Namnutrymme för händelsehubbar | `--aepUserLdap---aep-enablement` |
| eventHubName | Händelsehubb | `--aepUserLdap---aep-enablement-event-hub` |

## 2.4.2.2 Skapa Azure Event Hub-mål i Adobe Experience Platform

Logga in på Adobe Experience Platform via följande URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

När du har loggat in loggar du in på Adobe Experience Platform hemsida.

![Datainmatning](./../../../modules/datacollection/module1.2/images/home.png)

Innan du fortsätter måste du välja en **sandlåda**. Sandlådan som ska markeras har namnet ``--aepSandboxName--``. Du kan göra detta genom att klicka på texten **[!UICONTROL Production Prod]** i den blå raden ovanför skärmen. När du har valt rätt sandlåda ser du skärmändringen och nu befinner du dig i din dedikerade sandlåda.

![Datainmatning](./../../../modules/datacollection/module1.2/images/sb1.png)

Gå till **Destinationer** och gå sedan till **Katalog**.

![Datainmatning](./images/sb2a.png)

Välj **molnlagring** och gå till **Azure Event Hubs** och klicka på **Konfigurera** eller **Konfigurera**:

![2-08-list-destination.png](./images/2-08-list-destinations.png)

Fyll i de målvärden som du har samlat in i föregående övning. Klicka sedan på **Anslut till mål**.

![2-09-destination-values.png](./images/2-09-destination-values.png)

Om dina autentiseringsuppgifter är korrekta visas en bekräftelse: **Ansluten**.

![2-09-destination-values.png](./images/2-09-destination-valuesa.png)

Du måste nu ange namn och beskrivning i formatet `--aepUserLdap---aep-enablement`. Ange **eventHubName** (se föregående övning, den ser ut så här: `--aepUserLdap---aep-enablement-event-hub`) och klicka på **Nästa**.

![2-10-create-destination.png](./images/2-10-create-destination.png)

Klicka på **Spara och avsluta**.

![2-11-save-exit-activation.png](./images/2-11-save-exit-activation.png)

Målet har nu skapats och är tillgängligt i Adobe Experience Platform.

![2-12-destination-created.png](./images/2-12-destination-created.png)

Nästa steg: [2.4.3 Skapa ett segment](./ex3.md)

[Gå tillbaka till modul 2.4](./segment-activation-microsoft-azure-eventhub.md)

[Gå tillbaka till Alla moduler](./../../../overview.md)
