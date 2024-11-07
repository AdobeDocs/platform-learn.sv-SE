---
title: Segmentaktivering till Microsoft Azure Event Hub - Konfigurera Event Hub i Azure
description: Segmentaktivering till Microsoft Azure Event Hub - Konfigurera Event Hub i Azure
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---

# 2.4.1 Konfigurera din Microsoft Azure EventHub-miljö

Azure Event Hubs är en mycket skalbar publiceringsprenumerationstjänst som kan importera miljontals händelser per sekund och strömma dem till flera program. På så sätt kan du bearbeta och analysera den enorma mängd data som produceras av dina anslutna enheter och program.

## 2.4.1.1 Vad är Azure Event Hubs?

Azure Event Hubs är en stor dataströmningsplattform och en tjänst för händelsehantering. Den kan ta emot och bearbeta miljontals händelser per sekund. Data som skickas till ett händelsehubb kan omformas och lagras med hjälp av alla realtidsanalysleverantörer eller batchnings-/lagringsadaptrar.

Händelsehubbar representerar **ytterdörren** för en händelsepipeline, som ofta kallas händelseinsättare i lösningsarkitekturer. En händelseinsättare är en komponent eller tjänst som är placerad mellan händelseutgivare (som Adobe Experience Platform RTCDP) och händelsekonsumenter för att frigöra produktionen av en händelseström från förbrukningen av dessa händelser. Event Hubs utgör en enhetlig direktuppspelningsplattform med en buffert för tidsbevarande, som frigör händelseproducenter från händelsekonsumenter.

## 2.4.1.2 Skapa namnutrymmet Event Hubs

Gå till [https://portal.azure.com/#home](https://portal.azure.com/#home) och välj **Skapa en resurs**.

![1-01-open-azure-portal.png](./images/1-01-open-azure-portal.png)

Ange **Händelse** i sökfältet på resursskärmen och välj **Händelsehubbar** i listrutan:

![1-02-search-event-hubs.png](./images/1-02-search-event-hubs.png)

Klicka på **Skapa**:

![1-03-event-hub-create.png](./images/1-03-event-hub-create.png)

Om det här är första gången du skapar en resurs i Azure måste du skapa en ny **resursgrupp**. Om du redan har en resursgrupp kan du markera den (eller skapa en ny).

Välj **Skapa ny** och ge gruppen namnet `--aepUserLdap---aep-enablement`.

![1-04-create-resource-group.png](./images/1-04-create-resource-group.png)

Utför testet av fälten enligt följande:

- Namnområde: Definiera namnområdet, det måste vara unikt, använd följande mönster `--aepUserLdap---aep-enablement`
- Plats: **Västeuropa** refererar till Azure-datacenter i Amsterdam
- Prisnivå: **Grundläggande**
- Genomströmningsenheter: **1**

![1-05-create-namespace.png](./images/1-05-create-namespace.png)

Klicka på **Granska + skapa**.

![1-06-namespace-review-create.png](./images/1-06-namespace-review-create.png)

Klicka på **Skapa**.

![1-07-namespace-create.png](./images/1-07-namespace-create.png)

Distributionen av resursgruppen kan ta 1-2 minuter, och följande skärm visas när den är klar:

![1-08-namespace-deploy.png](./images/1-08-namespace-deploy.png)

## 2.4.1.3 Konfigurera händelsehubben i Azure

Gå till [https://portal.azure.com/#home](https://portal.azure.com/#home) och välj **Alla resurser**.

![1-09-all-resources.png](./images/1-09-all-resources.png)

Välj ditt `--aepUserLdap---aep-enablement`-namnområde i resurslistan:

![1-10-list-resources.png](./images/1-10-list-resources.png)

Välj **Händelsehubbar** på `--aepUserLdap---aep-enablement`-detaljskärmen:

![1-11-even-thub-namespace.png](./images/1-11-eventhub-namespace.png)

Klicka på **+ Händelsehubben**.

![1-12-add-event-hub.png](./images/1-12-add-event-hub.png)

Använd `--aepUserLdap---aep-enablement-event-hub` som namn och klicka på **Skapa**.

![1-13-create-event-hub.png](./images/1-13-create-event-hub.png)

Klicka på **Händelsehubbar** i händelsehubbens namnutrymme. Du bör nu se din **händelsehubb** i listan. I så fall kan du gå vidare till nästa övning.

![1-14-event-hub-list.png](./images/1-14-event-hub-list.png)

## 2.4.1.4 Konfigurera ditt Azure Storage-konto

Om du vill felsöka din Azure Event Hub-funktion i senare övningar måste du tillhandahålla ett Azure Storage-konto som en del av projektkonfigurationen för Visual Studio Code. Du skapar nu det Azure Storage-kontot.

Gå till [https://portal.azure.com/#home](https://portal.azure.com/#home) och välj **Skapa en resurs**.

![1-15-event-hub-storage.png](./images/1-15-event-hub-storage.png)

Ange **lagring** i sökningen och välj **Lagringskonto** i listan.

![1-16-event-hub-search-storage.png](./images/1-16-event-hub-search-storage.png)

Välj **Skapa**.

![1-17-event-hub-create-storage.png](./images/1-17-event-hub-create-storage.png)

Ange din **resursgrupp** (skapad i början av den här övningen), använd `--aepUserLdap--aepstorage` som lagringskontonamn, välj **Lokalt redundant lagring (LRS)** och klicka sedan på **Granska + skapa**.

![1-18-event-hub-create-review-storage.png](./images/1-18-event-hub-create-review-storage.png)

Klicka på **Skapa**.

![1-19-event-hub-submit-storage.png](./images/1-19-event-hub-submit-storage.png)

Det tar några sekunder att skapa ditt lagringskonto:

![1-20-event-hub-deploy-storage.png](./images/1-20-event-hub-deploy-storage.png)

När skärmen är klar visas knappen **Gå till resurs**.

Klicka på **Microsoft Azure**.

![1-21-event-hub-deploy-ready-storage.png](./images/1-21-event-hub-deploy-ready-storage.png)

Ditt lagringskonto visas nu under **Senaste resurser**.

![1-22-event-hub-deploy-resources-list.png](./images/1-22-event-hub-deploy-resources-list.png)

Nästa steg: [2.4.2 Konfigurera Azure Event Hub-målet i Adobe Experience Platform](./ex2.md)

[Gå tillbaka till modul 2.4](./segment-activation-microsoft-azure-eventhub.md)

[Gå tillbaka till Alla moduler](./../../../overview.md)
