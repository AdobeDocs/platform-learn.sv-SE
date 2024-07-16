---
title: Bootcamp - Blanda fysiska och digitala - Journey Optimizer Create your event
description: Bootcamp - Blanda fysiska och digitala - Journey Optimizer Create your event
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Events
exl-id: 3d47c686-c2d8-4961-a05b-0990025392fa
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# 3.2 Skapa en aktivitet

Logga in på Adobe Journey Optimizer på [Adobe Experience Cloud](https://experience.adobe.com). Klicka på **Journey Optimizer**.

![ACOP](./images/acophome.png)

Du omdirigeras till vyn **Hem** i Journey Optimizer. Kontrollera först att du använder rätt sandlåda. Sandlådan som ska användas kallas `Bootcamp`. Om du vill ändra från en sandlåda till en annan klickar du på **Prod** och väljer sandlådan i listan. I det här exemplet heter sandlådan **Bootcamp2**. Du kommer sedan att vara i vyn **Hem** i din sandlåda `Bootcamp`.

![ACOP](./images/acoptriglp.png)

Bläddra nedåt på den vänstra menyn och klicka på **Konfigurationer**. Klicka sedan på knappen **Hantera** under **Händelser**.

![ACOP](./images/acopmenu.png)

Därefter visas en översikt över alla tillgängliga händelser. Klicka på **Skapa händelse** för att börja skapa en egen händelse.

![ACOP](./images/emptyevent.png)

Ett nytt, tomt händelsefönster öppnas sedan.

Först och främst ger du evenemanget ett namn som detta: `yourLastNameBeaconEntryEvent` och lägger till en beskrivning som denna `Beacon Entry Event`.

![ACOP](./images/eventdescription.png)

Kontrollera sedan att **Type** är inställd på **Unitary** och välj **System Generated** för **Event ID Type** -markeringen.

![ACOP](./images/eventidtype.png)

Nästa steg är schemavalet. Ett schema förbereddes för den här övningen. Använd schemat `Demo System - Event Schema for Mobile App (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

När du har valt schemat visas ett antal fält som markeras i avsnittet **Fält**. Nu bör du hovra över avsnittet **Fält** så visas 3 ikoner-popup. Klicka på ikonen **Redigera** .

![ACOP](./images/eventpayload.png)

Du kommer att se en popup-meny i fönstret **Fält** där du måste markera några fält som vi behöver för att anpassa resan.  Vi väljer andra profilattribut senare med de data som redan finns i Adobe Experience Platform.

![ACOP](./images/eventfields.png)

Bläddra nedåt tills du ser objektet `Place context` och markera kryssrutan. På så sätt kommer kundens hela kontext att göras tillgänglig för resan. Klicka på **OK** om du vill spara ändringarna.

![ACOP](./images/eventpayloadbr.png)

Du borde se det här då. Klicka på **Spara** en gång till för att spara ändringarna.

![ACOP](./images/eventsave.png)

Din händelse är nu konfigurerad och sparad.

![ACOP](./images/eventdone.png)

Klicka på aktiviteten igen för att öppna skärmen **Redigera händelse** igen. Håll pekaren över **Fält** igen om du vill se de tre ikonerna. Klicka på ikonen **Visa** .

![ACOP](./images/viewevent.png)

Nu visas ett exempel på den förväntade nyttolasten.
Händelsen har ett unikt ID för Orchestration-händelse som du kan hitta genom att rulla nedåt i nyttolasten tills du ser `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

Händelse-ID:t är det som måste skickas till Adobe Experience Platform för att utlösa den resa som du ska bygga i någon av de kommande övningarna. Kom ihåg detta eventID, som du kanske behöver det senare.
`"eventID": "e76c0bf0c77c3517e5b6f4c457a0754ebaf5f1f6b9357d74e0d8e13ae517c3d5"`

Klicka på **OK** och sedan på **Avbryt**.

Du har nu avslutat den här övningen.

Nästa steg: [3.3 Skapa din resa och push-meddelanden](./ex3.md)

[Gå tillbaka till användarflöde 3](./uc3.md)

[Gå tillbaka till Alla moduler](../../overview.md)
