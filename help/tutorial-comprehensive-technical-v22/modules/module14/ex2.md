---
title: Adobe Experience Platform Data Collection & Servervidarebefordring i realtid - Uppdatera ditt datastream för att göra data tillgängliga för din Adobe Experience Platform Data Collection Server-egenskap
description: Uppdatera ditt datastream för att göra data tillgängliga för din Adobe Experience Platform Data Collection Server-egenskap
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 0c42350c-c38a-410e-bdab-41aff6024f81
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---

# 14.2 Uppdatera ditt datastream så att data blir tillgängliga för din Adobe Experience Platform Data Collection Server-egenskap

## 14.2.1 Uppdatera ditt datastream

I [Utövning 0.2](./../../modules/module0/ex2.md)har du skapat en egen **[!UICONTROL Datastream]**. Du använde sedan namnet `--demoProfileLdap-- - Demo System Datastream`.

I den här övningen måste du konfigurera att **[!UICONTROL Datastream]** att arbeta med **[!DNL Data Collection Server property]**.

Om du vill göra det går du till [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/). Du kommer då att se det här. Klicka på **[!UICONTROL Datastreams]**.

I skärmens övre högra hörn väljer du namnet på sandlådan, som bör vara `--aepSandboxId--`.

![Klicka på ikonen Edge Configuration (Kantkonfiguration) i den vänstra navigeringen](./images/edgeconfig1b.png)

Sök efter **[!UICONTROL Datastream]**, som har namnet `--demoProfileLdap-- - Demo System Datastream`. Klicka på **[!UICONTROL Datastream]** för att öppna den.

![WebSDK](./images/websdk0.png)

Du kommer då att se det här. Klicka **[!UICONTROL + Lägg till tjänst]**.

![WebSDK](./images/websdk3.png)

Välj tjänsten **Vidarebefordran av händelser**. Då visas ytterligare två inställningar. Välj egenskapen för vidarebefordring av händelser, som du skapade i föregående övning och som har namnet `--demoProfileLdap-- - Demo System (DD/MM/YYYY) (Edge)`. Välj sedan **Utveckling** under **Miljö**. Klicka **Spara**.

![WebSDK](./images/websdk4.png)

Din datastream har uppdaterats och är klar att användas.

![WebSDK](./images/websdk8a.png)

Din datastream är nu klar att fungera med din **[!DNL Event Forwarding property]**.

Nästa steg: [14.3 Skapa och konfigurera en anpassad webkrok](./ex3.md)

[Gå tillbaka till modul 14](./aep-data-collection-ssf.md)

[Gå tillbaka till Alla moduler](./../../overview.md)
