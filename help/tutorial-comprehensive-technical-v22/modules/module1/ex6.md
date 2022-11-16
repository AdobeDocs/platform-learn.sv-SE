---
title: Foundation - Installation av Adobe Experience Platform Data Collection och Web SDK-tillägget - Implementera Adobe Target
description: Foundation - Installation av Adobe Experience Platform Data Collection och Web SDK-tillägget - Implementera Adobe Target
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 4aee8ae2-38ca-49a3-8f1b-57713d16f5b5
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# 1.6 Implementera Adobe Target

## 1.6. Uppdatera ditt datastream för att använda Adobe Target

Följ de här stegen om du vill skicka data som samlats in av Web SDK till Adobe Target och få ett svar från Adobe Target med en personaliserad upplevelse för varje kund.

Gå till [https://experience.adobe.com/launch/](https://experience.adobe.com/launch/) och gå till **Datastreams**.

I skärmens övre högra hörn väljer du namnet på sandlådan, som bör vara `--aepSandboxId--`. Öppna en specifik datastream med namnet `--demoProfileLdap-- - Demo System Datastream`.

![Klicka på ikonen Edge Configuration (Kantkonfiguration) i den vänstra navigeringen](./images/edgeconfig1b.png)

Du kommer då att se det här. Om du vill aktivera Adobe Target klickar du på **+Lägg till tjänst**.

![AEP Debugger](./images/aa2.png)

Du kommer då att se det här. Välj tjänsten **Adobe Target** därefter kan du ange ytterligare information. För tillfället behöver du inte spara det här, så klicka på **Avbryt**.

![AEP Debugger](./images/at1.png)

Nästa steg: [1.7 XDM-schemakrav i Adobe Experience Platform](./ex7.md)

[Gå tillbaka till modul 1](./data-ingestion-launch-web-sdk.md)

[Gå tillbaka till Alla moduler](./../../overview.md)
