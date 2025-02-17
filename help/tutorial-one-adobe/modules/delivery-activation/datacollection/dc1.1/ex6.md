---
title: Foundation - Installation av Adobe Experience Platform Data Collection och Web SDK-tillägget - Implementera Adobe Target
description: Foundation - Installation av Adobe Experience Platform Data Collection och Web SDK-tillägget - Implementera Adobe Target
kt: 5342
doc-type: tutorial
exl-id: 31cdde2f-011d-442d-8e47-15a318a6c89d
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---

# 1.1.6 Implementera Adobe Target

## Uppdatera ditt datastream för att använda Adobe Target

Följ de här stegen om du vill skicka data som samlats in av Web SDK till Adobe Target och få svar från Adobe Target med en personlig upplevelse för varje kund.

Gå till [https://experience.adobe.com/launch/](https://experience.adobe.com/launch/) och gå till **Datastreams**.

I skärmens övre högra hörn väljer du namnet på sandlådan, som ska vara `--aepSandboxName--`. Öppna den specifika datastream som heter `--aepUserLdap-- - Demo System Datastream`.

![Klicka på ikonen Edge-konfiguration i den vänstra navigeringen](./images/edgeconfig1b.png)

Då ser du det här. Klicka på **Lägg till tjänst** om du vill aktivera Adobe Target.

![AEP-felsökning](./images/aa2.png)

Då ser du det här. Välj tjänsten **Adobe Target**, varefter du kan ange ytterligare information om du vill. Klicka på **Spara**.

![AEP-felsökning](./images/at1.png)

## Nästa steg

Gå till [1.1.7 XDM-schemakrav i Adobe Experience Platform](./ex7.md){target="_blank"}

Gå tillbaka till [Konfigurera Adobe Experience Platform Data Collection och taggtillägget Web SDK](./data-ingestion-launch-web-sdk.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../../overview.md){target="_blank"}
