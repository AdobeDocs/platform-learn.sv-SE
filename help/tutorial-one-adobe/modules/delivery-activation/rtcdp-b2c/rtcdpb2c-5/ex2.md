---
title: Adobe Experience Platform Data Collection & Servervidarebefordring i realtid - Uppdatera ditt dataflöde och gör data tillgängliga för din Adobe Experience Platform Data Collection Server-egenskap
description: Uppdatera ditt datastream för att göra data tillgängliga för din Adobe Experience Platform Data Collection Server-egenskap
kt: 5342
doc-type: tutorial
exl-id: f4bb0673-d553-4027-8bfd-53d2608efaf5
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# 2.5.2 Uppdatera ditt dataflöde så att data blir tillgängliga för din Adobe Experience Platform Data Collection Server-egenskap

## Uppdatera ditt dataflöde

I [Komma igång](./../../../getting-started/gettingstarted/ex2.md) har du skapat en egen **[!UICONTROL Datastream]**. Du använde sedan namnet `--aepUserLdap-- - Demo System Datastream`.

I den här övningen måste du konfigurera **[!UICONTROL Datastream]** så att den fungerar med din **Data Collection Server-egenskap**.

Gå till [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/) om du vill göra det. Då ser du det här. Klicka på **[!UICONTROL Datastreams]** på den vänstra menyn.

I skärmens övre högra hörn väljer du namnet på sandlådan, som ska vara `--aepSandboxName--`.

![Klicka på ikonen Edge-konfiguration i den vänstra navigeringen](./images/edgeconfig1b.png)

Sök efter din **[!UICONTROL Datastream]**, som har namnet `--aepUserLdap-- - Demo System Datastream`. Klicka på din **[!UICONTROL Datastream]** för att öppna den.

![WebSDK](./images/websdk0.png)

Då ser du det här. Klicka på **[!UICONTROL + Add Service]**.

![WebSDK](./images/websdk3.png)

Välj tjänsten **Händelsevidarebefordran**. Då visas ytterligare två inställningar. Välj egenskapen för vidarebefordran av händelser, som du skapade i föregående övning och som har namnet `--aepUserLdap-- - Demo System (DD/MM/YYYY) (Edge)`. Välj sedan **Utveckling** under **Miljö**. Klicka på **Spara**.

![WebSDK](./images/websdk4.png)

Din datastream har uppdaterats och är klar att användas.

![WebSDK](./images/websdk8a.png)

Din datastream är nu klar att fungera med din **[!DNL Event Forwarding property]**.

## Nästa steg

Gå till [2.5.3 Skapa och konfigurera en anpassad webkrok](./ex3.md){target="_blank"}

Gå tillbaka till [Real-Time CDP-anslutningar: Händelsevidarebefordran](./aep-data-collection-ssf.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../../overview.md){target="_blank"}
