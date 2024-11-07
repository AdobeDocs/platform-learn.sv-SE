---
title: Journey Optimizer Create your event
description: Journey Optimizer Create your event
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# 3.1.1 Skapa en händelse

Logga in på Adobe Journey Optimizer på [Adobe Experience Cloud](https://experience.adobe.com). Klicka på **Journey Optimizer**.

![ACOP](./images/acophome.png)

Du omdirigeras till vyn **Hem** i Journey Optimizer. Kontrollera först att du använder rätt sandlåda. Sandlådan som ska användas kallas `--aepSandboxName--`. Om du vill ändra från en sandlåda till en annan klickar du på **PRODUKTIONSprodukt (VA7)** och väljer sandlådan i listan. I det här exemplet heter sandlådan **AEP Enablement FY22**. Du kommer sedan att vara i vyn **Hem** i din sandlåda `--aepSandboxName--`.

![ACOP](./images/acoptriglp.png)

Bläddra nedåt på den vänstra menyn och klicka på **Konfigurationer**. Klicka sedan på knappen **Hantera** under **Händelser**.

![ACOP](./images/acopmenu.png)

Därefter visas en översikt över alla tillgängliga händelser. Klicka på **Skapa händelse** för att börja skapa en egen händelse.

![ACOP](./images/emptyevent.png)

Ett nytt, tomt händelsefönster öppnas sedan.

![ACOP](./images/emptyevent1.png)

Först och främst ger du evenemanget ett namn som detta: `--aepUserLdap--AccountCreationEvent`.

![ACOP](./images/eventname.png)

Lägg sedan till en beskrivning som denna `Account Creation Event`.

![ACOP](./images/eventdescription.png)

Kontrollera sedan att **Type** är inställd på **Unitary** och välj **System Generated** för **Event ID Type** -markeringen.

![ACOP](./images/eventidtype.png)

Nästa steg är schemavalet. Ett schema förbereddes för den här övningen. Använd schemat `Demo System - Event Schema for Website (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

När du har valt schemat visas ett antal fält som markeras i avsnittet **Nyttolast**. Du bör nu hovra över avsnittet **Nyttolast** så visas 3 ikoner-popup. Klicka på ikonen **Redigera** .

![ACOP](./images/eventpayload.png)

Du kommer att se en popup-meny i fönstret **Fält** där du måste markera några fält som vi behöver för att anpassa e-postmeddelandet.  Vi väljer andra profilattribut senare med de data som redan finns i Adobe Experience Platform.

![ACOP](./images/eventfields.png)

I objektet `--aepTenantId--.demoEnvironment` måste du markera fälten **brandLogo** och **brandName**.

![ACOP](./images/eventpayloadbr.png)

Markera fältet **email** i objektet `--aepTenantId--.identification.core`.

![ACOP](./images/eventpayloadbrid.png)

Klicka på **OK** om du vill spara ändringarna.

![ACOP](./images/saveok.png)

Du bör då se det här:

![ACOP](./images/eventsave.png)

Klicka på **Spara** en gång till för att spara ändringarna.

![ACOP](./images/save1.png)

Din händelse är nu konfigurerad och sparad.

![ACOP](./images/eventdone.png)

Klicka på aktiviteten igen för att öppna skärmen **Redigera händelse** igen. Håll pekaren över fältet **Nyttolast** igen för att se de tre ikonerna igen. Klicka på ikonen **Visa nyttolast** .

![ACOP](./images/viewevent.png)

Nu visas ett exempel på den förväntade nyttolasten.

![ACOP](./images/fullpayload.png)

Händelsen har ett unikt ID för Orchestration-händelse som du kan hitta genom att rulla nedåt i nyttolasten tills du ser `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

Händelse-ID är det som måste skickas till Adobe Experience Platform för att utlösa den resa som du bygger i Exercise 7.2. Kom ihåg detta eventID, som du behöver det i Exercise 7.3.
`"eventID": "227402c540eb8f8855c6b2333adf6d54d7153d9d7d56fa475a6866081c574736"`

Klicka på **OK** och sedan på **Avbryt**.

Du har nu avslutat den här övningen.

Nästa steg: [3.1.2 Journey Optimizer: Skapa din resa och ditt e-postmeddelande](./ex2.md)

[Gå tillbaka till modul 3.1](./journey-orchestration-create-account.md)

[Gå tillbaka till Alla moduler](../../../overview.md)
