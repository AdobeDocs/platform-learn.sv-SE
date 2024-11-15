---
title: Foundation - Installation av Adobe Experience Platform Data Collection och Web SDK-tillägget - Implementera Adobe Target
description: Foundation - Installation av Adobe Experience Platform Data Collection och Web SDK-tillägget - Implementera Adobe Target
kt: 5342
doc-type: tutorial
exl-id: 475e9a34-c80e-41e4-9660-61c79f26922d
source-git-commit: 0dbcda0cfc9f199a44c845c1b5caf00a8d740251
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# 1.1.6 Implementera Adobe Target

## 1.1.6.1 Uppdatera ditt datastream för att använda Adobe Target

Följ de här stegen om du vill skicka data som samlats in av Web SDK till Adobe Target och få ett svar från Adobe Target med en personaliserad upplevelse för varje kund.

Gå till [https://experience.adobe.com/launch/](https://experience.adobe.com/launch/) och gå till **Datastreams**.

I skärmens övre högra hörn väljer du namnet på sandlådan, som ska vara `--aepSandboxName--`. Öppna den specifika datastream som heter `--aepUserLdap-- - Demo System Datastream`.

![Klicka på ikonen Edge-konfiguration i den vänstra navigeringen](./images/edgeconfig1b.png)

Då ser du det här. Om du vill aktivera Adobe Target klickar du på **+Lägg till tjänst**.

![AEP-felsökning](./images/aa2.png)

Då ser du det här. Välj tjänsten **Adobe Target**, varefter du kan ange ytterligare information om du vill. Klicka på **Spara**.

![AEP-felsökning](./images/at1.png)

Nästa steg: [1.1.7 XDM-schemakrav i Adobe Experience Platform](./ex7.md)

[Gå tillbaka till modul 1.1](./data-ingestion-launch-web-sdk.md)

[Gå tillbaka till Alla moduler](./../../../overview.md)
