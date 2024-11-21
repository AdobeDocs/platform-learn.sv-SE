---
title: Segmentaktivering till Microsoft Azure Event Hub - Konfigurera Event Hub i Azure
description: Segmentaktivering till Microsoft Azure Event Hub - Konfigurera Event Hub i Azure
kt: 5342
doc-type: tutorial
exl-id: 0c2e94ec-00e8-4f47-add7-ca3a08151225
source-git-commit: 216914c9d97827afaef90e21ed7d4f35eaef0cd3
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 0%

---

# 2.4.2 Konfigurera din Microsoft Azure EventHub-miljö

Azure Event Hubs är en mycket skalbar publiceringsprenumerationstjänst som kan importera miljontals händelser per sekund och strömma dem till flera program. På så sätt kan du bearbeta och analysera den enorma mängd data som produceras av dina anslutna enheter och program.

## Vad är Azure Event Hubs?

Azure Event Hubs är en stor dataströmningsplattform och en tjänst för händelsehantering. Den kan ta emot och bearbeta miljontals händelser per sekund. Data som skickas till ett händelsehubb kan omformas och lagras med hjälp av alla realtidsanalysleverantörer eller batchnings-/lagringsadaptrar.

Händelsehubbar representerar **ytterdörren** för en händelsepipeline, som ofta kallas händelseinsättare i lösningsarkitekturer. En händelseinsättare är en komponent eller tjänst som är placerad mellan händelseutgivare (som Adobe Experience Platform RTCDP) och händelsekonsumenter för att frigöra produktionen av en händelseström från förbrukningen av dessa händelser. Event Hubs utgör en enhetlig direktuppspelningsplattform med en buffert för tidsbevarande, som frigör händelseproducenter från händelsekonsumenter.

## Skapa ett namnutrymme för händelsehubbar

Gå till [https://portal.azure.com/#home](https://portal.azure.com/#home) och välj **Skapa en resurs**.

![1-01-open-azure-portal.png](./images/101openazureportal.png)

Ange **Händelse** i sökfältet på resursskärmen. Leta reda på **Event Hubs**-kortet, klicka på **Skapa** och klicka sedan på **Event Hubs**.

![1-02-search-event-hubs.png](./images/102searcheventhubs.png)

Om det här är första gången du skapar en resurs i Azure måste du skapa en ny **resursgrupp**. Om du redan har en resursgrupp kan du markera den (eller skapa en ny).

Klicka på **Skapa ny** och ge gruppen ett namn `--aepUserLdap---aep-enablement`. Klicka sedan på **OK**.

![1-04-create-resource-group.png](./images/104createresourcegroup.png)

Fyll i resten av fälten enligt följande:

- Namnområde: Definiera namnområdet, det måste vara unikt, använd följande mönster `--aepUserLdap---aep-enablement`
- Plats: välj en plats
- Prisnivå: **Grundläggande**
- Genomströmningsenheter: **1**

Klicka på **Granska + skapa**.

![1-05-create-namespace.png](./images/105createnamespace.png)

Klicka på **Skapa**.

![1-07-namespace-create.png](./images/107namespacecreate.png)

Distributionen av resursgruppen kan ta 1-2 minuter, och följande skärm visas när den är klar:

![1-08-namespace-deploy.png](./images/108namespacedeploy.png)

## Konfigurera händelsehubben i Azure

Gå till [https://portal.azure.com/#home](https://portal.azure.com/#home) och välj **Alla resurser**.

![1-09-all-resources.png](./images/109allresources.png)

Klicka på `--aepUserLdap---aep-enablement`-händelsehubbens namnområde i resurslistan:

![1-10-list-resources.png](./images/110listresources.png)

Gå till **Enheter** på skärmen `--aepUserLdap---aep-enablement` och klicka på **Händelsehubbar**:

![1-11-even-thub-namespace.png](./images/111eventhubnamespace.png)

Klicka på **+ Händelsehubben**.

![1-12-add-event-hub.png](./images/112addeventhub.png)

Använd `--aepUserLdap---aep-enablement-event-hub` som namn och klicka på **Granska + skapa**.

![1-13-create-event-hub.png](./images/113createeventhub.png)

Klicka på **Skapa**.

![1-13-create-event-hub.png](./images/113createeventhub1.png)

I **Händelsehubbar** under händelsehubbens namnutrymme visas nu din **händelsehubb** i listan.

![1-14-event-hub-list.png](./images/114eventhublist.png)

## Konfigurera ditt Azure Storage-konto

Om du vill felsöka din Azure Event Hub-funktion i senare övningar måste du tillhandahålla ett Azure Storage-konto som en del av projektkonfigurationen för Visual Studio Code. Du skapar nu det Azure Storage-kontot.

Gå till [https://portal.azure.com/#home](https://portal.azure.com/#home) och välj **Skapa en resurs**.

![1-15-event-hub-storage.png](./images/115eventhubstorage.png)

Ange **lagringskontot** i sökningen, sök efter kortet för **lagringskontot** och klicka på **lagringskontot**.

![1-16-event-hub-search-storage.png](./images/116eventhubsearchstorage.png)

Ange din **resursgrupp** (skapades i början av den här övningen), använd `--aepUserLdap--aepstorage` som lagringskontonamn och välj **Lokalt redundant lagring (LRS)** och klicka sedan på **Granska + skapa**.

![1-18-event-hub-create-review-storage.png](./images/118eventhubcreatereviewstorage.png)

Klicka på **Skapa**.

![1-19-event-hub-submit-storage.png](./images/119eventhubsubmitstorage.png)

Det tar några sekunder att skapa ditt lagringskonto:

![1-20-event-hub-deploy-storage.png](./images/120eventhubdeploystorage.png)

När skärmen är klar visas knappen **Gå till resurs**.

Klicka på **Hem**.

![1-21-event-hub-deploy-ready-storage.png](./images/121eventhubdeployreadystorage.png)

Ditt lagringskonto visas nu under **Senaste resurser**.

![1-22-event-hub-deploy-resources-list.png](./images/122eventhubdeployresourceslist.png)

Nästa steg: [2.4.3 Konfigurera Azure Event Hub-målet i Adobe Experience Platform](./ex3.md)

[Gå tillbaka till modul 2.4](./segment-activation-microsoft-azure-eventhub.md)

[Gå tillbaka till Alla moduler](./../../../overview.md)
