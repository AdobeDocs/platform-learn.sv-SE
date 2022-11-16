---
title: Konfigurera HTTP API-slutpunkt i Adobe Experience Platform
description: Konfigurera HTTP API-slutpunkt i Adobe Experience Platform
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 3346c57b-3a78-40b1-a891-053fc8781659
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 1%

---

# 15.3 Konfigurera slutpunkten för HTTP API-direktuppspelning i Adobe Experience Platform

Innan du kan konfigurera Adobe Experience Platform Sink Connector i Kafka måste du skapa en HTTP API Source Connector i Adobe Experience Platform. Slutpunkts-URL:en för HTTP-API-direktuppspelning krävs för att konfigurera Adobe Experience Platform Sink Connector.

Om du vill skapa en HTTP API Source Connector loggar du in på Adobe Experience Platform genom att gå till den här URL:en: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

När du loggat in kommer du till Adobe Experience Platform hemsida.

![Dataintag](../module2/images/home.png)

Innan du fortsätter måste du välja en **sandlåda**. Sandlådan som ska markeras har namnet ``--aepSandboxId--``. Du kan göra detta genom att klicka på texten **[!UICONTROL Produktionsprodukt]** i den blå linjen ovanför skärmen. När du har valt rätt sandlåda ser du skärmändringen och nu befinner du dig i din dedikerade sandlåda.

![Dataintag](../module2/images/sb1.png)

Gå till den vänstra menyn **Källor** och rulla nedåt i **Källkatalog** tills du ser **HTTP-API**. Klicka **Lägg till data**.

![Dataintag](./images/kaep1.png)

Klicka **Nytt konto**. Använd `--demoProfileLdap-- - Kafka` som namn för HTTP API-anslutningen, i det här fallet **vangeluw - Kafka**. Aktivera kryssrutan för **XDM-kompatibel**. Klicka **Anslut till källa**.

![Dataintag](./images/kaep2.png)

Du kommer att se det här, klicka **Nästa**.

![Dataintag](./images/kaep3.png)

Välj **Befintlig datauppsättning**&#x200B;öppnar du listrutan. Sök efter och markera datauppsättningen **Demo System - händelsedatauppsättning för callcenter (Global v1.1)**.

![Dataintag](./images/kaep4.png)

Klicka på **Nästa**.

![Dataintag](./images/kaep6.png)

Klicka på **Nästa**.

![Dataintag](./images/kaep7.png)

Klicka **Slutför**.

![Dataintag](./images/kaep8.png)

Därefter visas en översikt över HTTP API Source Connector som du nyss skapade.

![Dataintag](./images/kaep9.png)

Du måste kopiera **Slutpunkt för direktuppspelning** URL, som ser ut som den nedan, som du kommer att behöva i nästa övning.

`https://dcs.adobedc.net/collection/d282bbfc8a540321341576275a8d052e9dc4ea80625dd9a5fe5b02397cfd80dc`

Du har gjort klart den här övningen.

Nästa steg: [15.4 Installera och konfigurera Kafka Connect och Adobe Experience Platform Sink Connector](./ex4.md)

[Gå tillbaka till modul 15](./aep-apache-kafka.md)

[Gå tillbaka till Alla moduler](../../overview.md)
