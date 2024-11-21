---
title: Konfigurera HTTP API-slutpunkt i Adobe Experience Platform
description: Konfigurera HTTP API-slutpunkt i Adobe Experience Platform
kt: 5342
doc-type: tutorial
exl-id: a29dd01d-4415-45d6-ad52-7f14aef60565
source-git-commit: acb941e4ee668248ae0767bb9f4f42e067c181ba
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# 2.6.3 Konfigurera slutpunkten för HTTP API-direktuppspelning i Adobe Experience Platform

Innan du kan konfigurera Adobe Experience Platform Sink Connector i Kafka måste du skapa en HTTP API Source Connector i Adobe Experience Platform. Slutpunkts-URL:en för HTTP-API-direktuppspelning krävs för att konfigurera Adobe Experience Platform Sink Connector.

Om du vill skapa en HTTP API Source Connector loggar du in på Adobe Experience Platform genom att gå till följande URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

När du har loggat in loggar du in på Adobe Experience Platform hemsida.

![Datainmatning](./../../../modules/datacollection/module1.2/images/home.png)

Innan du fortsätter måste du välja en **sandlåda**. Sandlådan som ska markeras har namnet ``--aepSandboxName--``. När du har valt rätt sandlåda ser du skärmändringen och nu befinner du dig i din dedikerade sandlåda.

![Datainmatning](./../../../modules/datacollection/module1.2/images/sb1.png)

Gå till **Källor** på den vänstra menyn och rulla nedåt i **Källkatalogen** tills du ser **HTTP API**. Klicka på **Lägg till data**.

![Datainmatning](./images/kaep1.png)

Klicka på **Nytt konto**. Använd `--aepUserLdap-- - Kafka` som namn för din HTTP API-anslutning, i det här fallet **vangeluw - Kafka**. Aktivera kryssrutan för **XDM-kompatibel**. Klicka på **Anslut till källa**.

![Datainmatning](./images/kaep2.png)

Du kommer då att se detta, klicka på **Nästa**.

![Datainmatning](./images/kaep3.png)

Välj **Befintlig datauppsättning** och öppna listrutan. Sök efter och välj datauppsättningen **Demo System - Event Dataset for Call Center (Global v1.1)**.

![Datainmatning](./images/kaep4.png)

Klicka på **Nästa**.

![Datainmatning](./images/kaep6.png)

Klicka på **Nästa**.

![Datainmatning](./images/kaep7.png)

Klicka på **Slutför**.

![Datainmatning](./images/kaep8.png)

Därefter visas en översikt över den HTTP API Source Connector som du nyss skapade.

![Datainmatning](./images/kaep9.png)

Du måste kopiera URL:en för **direktuppspelningsslutpunkten**, som ser ut som den nedan, precis som du behöver den i nästa övning.

`https://dcs.adobedc.net/collection/d282bbfc8a540321341576275a8d052e9dc4ea80625dd9a5fe5b02397cfd80dc`

Du har gjort klart den här övningen.

Nästa steg: [2.6.4 Installera och konfigurera Kafka Connect och Adobe Experience Platform Sink Connector](./ex4.md)

[Gå tillbaka till modul 2.6](./aep-apache-kafka.md)

[Gå tillbaka till Alla moduler](../../../overview.md)
