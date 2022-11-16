---
title: Segmentaktivering till Microsoft Azure Event Hub - Konfigurera Event Hub i Azure
description: Segmentaktivering till Microsoft Azure Event Hub - Konfigurera Event Hub i Azure
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 9434ac83-5554-48bf-838c-7346d571efbf
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# 13.1 Konfigurera din Microsoft Azure EventHub-miljö

Azure Event Hubs är en mycket skalbar publiceringsprenumerationstjänst som kan importera miljontals händelser per sekund och strömma dem till flera program. På så sätt kan du bearbeta och analysera den enorma mängd data som produceras av dina anslutna enheter och program.

## 13.1.1 Vad är Azure Event Hubs?

Azure Event Hubs är en stor dataströmningsplattform och en tjänst för händelsehantering. Den kan ta emot och bearbeta miljontals händelser per sekund. Data som skickas till ett händelsehubb kan omformas och lagras med hjälp av alla realtidsanalysleverantörer eller batchnings-/lagringsadaptrar.

Event Hubs representerar **ytterdörr** för en händelseförlopp, ofta kallat en händelseinsättare i lösningsarkitekturer. En händelseinsättare är en komponent eller tjänst som är placerad mellan händelseutgivare (som Adobe Experience Platform RTCDP) och händelsekonsumenter för att frigöra produktionen av en händelseström från förbrukningen av dessa händelser. Event Hubs utgör en enhetlig direktuppspelningsplattform med en buffert för tidsbevarande, som frigör händelseproducenter från händelsekonsumenter.

## 13.1.2 Skapa ett namnutrymme för händelsehubbar

Gå till [https://portal.azure.com/#home](https://portal.azure.com/#home) och markera **Skapa en resurs**.

![1-01-open-azure-portal.png](./images/1-01-open-azure-portal.png)

På resursskärmen anger du **Händelse** i sökfältet och välj **Händelsehubbar** i listrutan:

![1-02-search-event-hubs.png](./images/1-02-search-event-hubs.png)

Klicka **Skapa**:

![1-03-event-hub-create.png](./images/1-03-event-hub-create.png)

Om det här är första gången du skapar en resurs i Azure måste du skapa en ny **Resursgrupp**. Om du redan har en resursgrupp kan du markera den (eller skapa en ny).

Välj **Skapa nytt**, namnge gruppen `--demoProfileLdap---aep-enablement`.

![1-04-create-resource-group.png](./images/1-04-create-resource-group.png)

Utför testet av fälten enligt följande:

- Namnutrymme: Definiera namnutrymmet, det måste vara unikt, använd följande mönster `--demoProfileLdap---aep-enablement`
- Plats: **Västeuropa** hänvisar till Azure-datacenter i Amsterdam
- Prisnivå: **Grundläggande**
- Genomströmningsenheter: **1**

![1-05-create-namespace.png](./images/1-05-create-namespace.png)

Klicka **Granska och skapa**.

![1-06-namespace-review-create.png](./images/1-06-namespace-review-create.png)

Klicka **Skapa**.

![1-07-namespace-create.png](./images/1-07-namespace-create.png)

Distributionen av resursgruppen kan ta 1-2 minuter, och följande skärm visas när den är klar:

![1-08-namespace-deploy.png](./images/1-08-namespace-deploy.png)

## 13.1.3 Konfigurera händelsehubben i Azure

Gå till [https://portal.azure.com/#home](https://portal.azure.com/#home) och markera **Alla resurser**.

![1-09-all-resources.png](./images/1-09-all-resources.png)

Välj din `--demoProfileLdap---aep-enablement` namnutrymme:

![1-10-list-resources.png](./images/1-10-list-resources.png)

I `--demoProfileLdap---aep-enablement` detaljskärm, välja **Händelsehubbar**:

![1-11-even-thub-namespace.png](./images/1-11-eventhub-namespace.png)

Klicka **+ Händelsehubb**.

![1-12-add-event-hub.png](./images/1-12-add-event-hub.png)

Använd `--demoProfileLdap---aep-enablement-event-hub` som namn och klicka **Skapa**.

![1-13-create-event-hub.png](./images/1-13-create-event-hub.png)

Klicka **Händelsehubbar** i händelsehubbens namnutrymme. Nu bör du se **Händelsehubb** listas. I så fall kan du gå vidare till nästa övning.

![1-14-event-hub-list.png](./images/1-14-event-hub-list.png)

## 13.1.4 Konfigurera ditt Azure Storage-konto

Om du vill felsöka din Azure Event Hub-funktion i senare övningar måste du tillhandahålla ett Azure Storage-konto som en del av projektkonfigurationen för Visual Studio Code. Du skapar nu det Azure Storage-kontot.

Gå till [https://portal.azure.com/#home](https://portal.azure.com/#home) och markera **Skapa en resurs**.

![1-15-event-hub-storage.png](./images/1-15-event-hub-storage.png)

Retur **lagring** i sökningen och välj **Lagringskonto** från listan.

![1-16-event-hub-search-storage.png](./images/1-16-event-hub-search-storage.png)

Välj **Skapa**.

![1-17-event-hub-create-storage.png](./images/1-17-event-hub-create-storage.png)

Ange **Resursgrupp** (skapat i början av övningen), använd `--demoProfileLdap--aepstorage` som ditt lagringskontonamn och välj **Lokalt redundant lagring (LRS)** och sedan klicka **Granska och skapa**.

![1-18-event-hub-create-review-storage.png](./images/1-18-event-hub-create-review-storage.png)

Klicka **Skapa**.

![1-19-event-hub-submit-storage.png](./images/1-19-event-hub-submit-storage.png)

Det tar några sekunder att skapa ditt lagringskonto:

![1-20-event-hub-deploy-storage.png](./images/1-20-event-hub-deploy-storage.png)

När skärmen är klar visas **Gå till resurs** -knappen.

Klicka **Microsoft Azure**.

![1-21-event-hub-deploy-ready-storage.png](./images/1-21-event-hub-deploy-ready-storage.png)

Ditt lagringskonto visas nu under **Senaste resurser**.

![1-22-event-hub-deploy-resources-list.png](./images/1-22-event-hub-deploy-resources-list.png)

Nästa steg: [13.2 Konfigurera Azure Event Hub-målet i Adobe Experience Platform](./ex2.md)

[Gå tillbaka till modul 13](./segment-activation-microsoft-azure-eventhub.md)

[Gå tillbaka till Alla moduler](./../../overview.md)
