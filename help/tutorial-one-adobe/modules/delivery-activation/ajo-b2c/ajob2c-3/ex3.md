---
title: Offer Decisioning - Testa ditt beslut
description: Offer Decisioning - Testa ditt beslut
kt: 5342
doc-type: tutorial
exl-id: c40b9b8c-9717-403c-bf02-6b8f42a59c05
source-git-commit: 2e856759e1a9b5509ad0632e28b269bcfc4ae861
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---

# 3.3.3 Konfigurera en kampanj med meddelanden i appen

Logga in på Adobe Journey Optimizer på [Adobe Experience Cloud](https://experience.adobe.com). Klicka på **Journey Optimizer**.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Du omdirigeras till vyn **Hem** i Journey Optimizer. Kontrollera först att du använder rätt sandlåda. Sandlådan som ska användas kallas `--aepSandboxName--`. Du kommer sedan att vara i vyn **Hem** i din sandlåda `--aepSandboxName--`.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

## Kanalkonfiguration för meddelanden i appen 3.3.3.1

Gå till **Kanaler** på den vänstra menyn och välj sedan **Kanalkonfigurationer**. Klicka på **Skapa kanalkonfiguration**.

![InApp](./images/inapp1.png)

Ange namnet: `--aepUserLdap--_In-app_Messages`, markera kanalen **Meddelanden i appen** och aktivera sedan plattformarna **Webb**, **iOS** och **Android**.

![InApp](./images/inapp2.png)

Bläddra ned, du borde se det här.

![InApp](./images/inapp3.png)

Kontrollera att **En sida** är aktiverad.

För **Webben** anger du URL-adressen till webbplatsen som skapades tidigare som en del av modulen **Komma igång** som ser ut så här: `https://dsn.adobe.com/web/--aepUserLdap---XXXX`. Glöm inte att ändra **XXXX** till webbplatsens unika kod.

Ange **för** iOS **och** Android`com.adobe.dsn.dxdemo`.

![InApp](./images/inapp4.png)

Bläddra uppåt och klicka på **Skicka**.

![InApp](./images/inapp5.png)

Kanalkonfigurationen är nu klar att användas.

![InApp](./images/inapp6.png)

## 3.3.3.2 Konfigurera en schemalagd kampanj för meddelanden i appen

Gå till **Kampanjer** på den vänstra menyn och klicka sedan på **Skapa kampanj**.

![InApp](./images/inapp7.png)

Välj **Schemalagd - Markering** och klicka sedan på **Skapa**.

![InApp](./images/inapp8.png)

Ange namnet `--aepUserLdap-- - CitiSignal Fiber Max` och klicka sedan på **Åtgärder**.

![InApp](./images/inapp9.png)

Klicka på **+ Lägg till åtgärd** och välj sedan **Meddelande i programmet**.

![InApp](./images/inapp10.png)

Välj den konfiguration av meddelandekanal i appen som du skapade i föregående steg, med namnet: `--aepUserLdap--_In-app_Messages`. Klicka på **Redigera innehåll**.

![InApp](./images/inapp11.png)

Du borde se det här då. Klicka på **Modal**.

![InApp](./images/inapp12.png)

Klicka på **Ändra layout**.

![InApp](./images/inapp13.png)

Klicka på ikonen **Media URL** om du vill välja en resurs från AEM Assets.

![InApp](./images/inapp14.png)

Gå till mappen **citisign-images** och välj bildfilen **neon-rabbit.jpg**. Klicka på **Markera**.

![InApp](./images/inapp15.png)

Använd **för texten** Header`CitiSignal Fiber Max`.
Använd **för texten** Brödtext`Conquer lag with Fiber Max`.

![InApp](./images/inapp16.png)

Ställ in texten **Knapp 1** på: `Go to Plans`.
Ange **target** till `com.adobe.dsn.dxdemo://plans`.

Klicka på **Granska för att aktivera**.

![InApp](./images/inapp17.png)

Klicka på **Aktivera**.

![InApp](./images/inapp18.png)

Statusen för din kampanj är nu inställd på **Aktivera**. Det kan ta några minuter innan kampanjen är aktiv.

![InApp](./images/inapp19.png)

När statusen har ändrats till **Live** kan du testa din kampanj.

![InApp](./images/inapp20.png)

## 3.3.3.3 Testa din kampanj för meddelanden i appen på mobilen

Öppna appen på din mobila enhet. Det nya meddelandet i appen visas när du har startat appen. Klicka på knappen **Gå till planer**.

![InApp](./images/inapp21.png)

Du dirigeras sedan till sidan **Planer**.

![InApp](./images/inapp22.png)

## Nästa steg

Gå till [Sammanfattning och förmåner](./summary.md){target="_blank"}

Gå tillbaka till [Adobe Journey Optimizer: Push och In-app Messages](ajopushinapp.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../../overview.md){target="_blank"}
