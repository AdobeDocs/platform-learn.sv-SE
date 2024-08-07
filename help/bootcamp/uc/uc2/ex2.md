---
title: Bootcamp - Journey Optimizer Create your event
description: Bootcamp - Journey Optimizer Create your event
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Events
exl-id: 89db40ab-d4c5-4310-aca6-cb64828e7bc9
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 0%

---

# 2.2 Skapa en aktivitet

Logga in på Adobe Journey Optimizer på [Adobe Experience Cloud](https://experience.adobe.com). Klicka på **Journey Optimizer**.

![ACOP](./images/acophome.png)

Du omdirigeras till vyn **Hem** i Journey Optimizer. Kontrollera först att du använder rätt sandlåda. Sandlådan som ska användas kallas `Bootcamp`. Om du vill ändra från en sandlåda till en annan klickar du på **Prod** och väljer sandlådan i listan. I det här exemplet heter sandlådan **Bootcamp**. Du kommer sedan att vara i vyn **Hem** i din sandlåda `Bootcamp`.

![ACOP](./images/acoptriglp.png)

Bläddra nedåt på den vänstra menyn och klicka på **Konfigurationer**. Klicka sedan på knappen **Hantera** under **Händelser**.

![ACOP](./images/acopmenu.png)

Därefter visas en översikt över alla tillgängliga händelser. Klicka på **Skapa händelse** för att börja skapa en egen händelse.

![ACOP](./images/emptyevent.png)

Ett nytt, tomt händelsefönster öppnas sedan.

![ACOP](./images/emptyevent1.png)

Först och främst ger du evenemanget ett namn som detta: `yourLastNameAccountCreationEvent` och lägger till en beskrivning som denna `Account Creation Event`.

![ACOP](./images/eventdescription.png)

Kontrollera sedan att **Type** är inställd på **Unitary** och välj **System Generated** för **Event ID Type** -markeringen.

![ACOP](./images/eventidtype.png)

Nästa steg är schemavalet. Ett schema förbereddes för den här övningen. Använd schemat `Demo System - Event Schema for Website (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

När du har valt schemat visas ett antal fält som markeras i avsnittet **Fält**. Nu bör du hovra över avsnittet **Fält** så visas 3 ikoner-popup. Klicka på ikonen **Redigera** .

![ACOP](./images/eventpayload.png)

Du kommer att se en popup-meny i fönstret **Fält** där du måste markera några fält som vi behöver för att anpassa e-postmeddelandet.  Vi väljer andra profilattribut senare med de data som redan finns i Adobe Experience Platform.

![ACOP](./images/eventfields.png)

I objektet `_experienceplatform.demoEnvironment` måste du markera fälten **brandLogo** och **brandName**.

![ACOP](./images/eventpayloadbr.png)

Markera fältet **email** i objektet `_experienceplatform.identification.core`.

![ACOP](./images/eventpayloadbrid.png)

Klicka på **OK** om du vill spara ändringarna.

![ACOP](./images/saveok.png)

Du borde se det här då. Klicka på **Spara** en gång till för att spara ändringarna.

![ACOP](./images/eventsave.png)

Din händelse är nu konfigurerad och sparad.

![ACOP](./images/eventdone.png)

Klicka på aktiviteten igen för att öppna skärmen **Redigera händelse** igen. Håll pekaren över **Fält** igen om du vill se de tre ikonerna igen. Klicka på ikonen **Visa nyttolast** .

![ACOP](./images/viewevent.png)

Nu visas ett exempel på den förväntade nyttolasten.
Händelsen har ett unikt ID för Orchestration-händelse som du kan hitta genom att rulla nedåt i nyttolasten tills du ser `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

Händelse-ID:t är det som måste skickas till Adobe Experience Platform för att utlösa den resa som du ska bygga i någon av de kommande övningarna. Kom ihåg detta eventID, som du kanske behöver det senare.
`"eventID": "19cab7852cdef99d25b6d5f1b6503da39d1f486b1d585743f97ed2d1e6b6c74f"`

Klicka på **OK** och sedan på **Avbryt**.

Du har nu avslutat den här övningen.

Nästa steg: [2.3 Skapa ditt e-postmeddelande](./ex3.md)

[Gå tillbaka till användarflöde 2](./uc2.md)

[Gå tillbaka till Alla moduler](../../overview.md)
