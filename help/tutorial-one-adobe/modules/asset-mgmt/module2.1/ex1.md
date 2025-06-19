---
title: Skapa ett Cloud Manager-program
description: Skapa ett Cloud Manager-program
kt: 5342
doc-type: tutorial
exl-id: fda247eb-1865-4936-b46e-84128ccab357
source-git-commit: 1bcc5123f16dbde30877662159e06d61d75e7287
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 2%

---

# 1.1.1 Skapa ett Cloud Manager-program

Gå till [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. Organisationen som du bör välja är `--aepImsOrgName--`. Då ser du något sådant här. Klicka på **Lägg till program**.

![AEMCS](./images/aemcs1.png)

Använd `--aepUserLdap-- - CitiSignal` för **programnamnet**. Välj alternativet **Konfigurera en sandlåda**. Klicka på **Fortsätt**.

![AEMCS](./images/aemcs2.png)

Kontrollera att följande alternativ är markerade:

- Webbplatser
- Forms
- Resurser

Klicka på pilen för **Assets** för att öppna listan med alternativ.

![AEMCS](./images/aemcs3.png)

Kontrollera att följande alternativ är markerade:

- Content Hub

Rulla ned i listan.

![AEMCS](./images/aemcs3a.png)

Kontrollera att följande alternativ är markerade:

- Edge-leveranstjänster
- Dynamiska medier

Klicka på **Skapa**.

![AEMCS](./images/aemcs3b.png)

Det kan ta 10-20 minuter att skapa miljön.

![AEMCS](./images/aemcs4.png)

Under tiden du väntar kan du redan börja med övning [1.1.2 Skapa din dokumentbaserade webbplats](./ex2.md){target="_blank"}.

När miljöerna har skapats och är klara att användas får du en bekräftelse via e-post, varefter du kan komma tillbaka hit.

![AEMCS](./images/aemcs5.png)

När du har fått din e-postbekräftelse går du tillbaka till [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. Du kommer då att se att status för ditt program har ändrats till **Ready**. Klicka på programmet för att öppna det.

![AEMCS](./images/aemcs6.png)

Ta en titt på fliken **Pipelines**. Klicka på de tre punkterna **..** och sedan på **Kör**.

![AEMCS](./images/aemcs7.png)

Klicka på **Kör**.

![AEMCS](./images/aemcs8.png)

Klicka sedan på de 3 punkterna **..** på fliken **Miljö** och klicka på **Visa detaljer**.

![AEMCS](./images/aemcs9.png)

Du kommer då att se din miljöinformation, inklusive URL:en för din **författarmiljö** som du behöver i nästa övning.

![AEMCS](./images/aemcs10.png)

När din pipeline är klar kan du fortsätta med nästa övning.

Nästa steg: [1.1.2 Skapa en dokumentbaserad webbplats](./ex2.md){target="_blank"}

Gå tillbaka till [Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./aemcs.md){target="_blank"}

[Gå tillbaka till alla moduler](./../../../overview.md){target="_blank"}
