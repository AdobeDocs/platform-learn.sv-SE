---
title: Bootcamp - Journey Optimizer Create your event
description: Bootcamp - Journey Optimizer Create your event
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
exl-id: 89db40ab-d4c5-4310-aca6-cb64828e7bc9
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---

# 2.2 Skapa en aktivitet

Logga in på Adobe Journey Optimizer genom att gå till [Adobe Experience Cloud](https://experience.adobe.com). Klicka **Journey Optimizer**.

![ACOP](./images/acophome.png)

Du omdirigeras till **Startsida**  i Journey Optimizer. Kontrollera först att du använder rätt sandlåda. Sandlådan som ska användas anropas `Bootcamp`. Om du vill ändra från en sandlåda till en annan klickar du på **Prod** och välj sandlådan i listan. I det här exemplet heter sandlådan **Bootläger**. Då är du i **Startsida** vy över din sandlåda `Bootcamp`.

![ACOP](./images/acoptriglp.png)

Bläddra nedåt i den vänstra menyn och klicka på **Konfigurationer**. Klicka sedan på **Hantera** knapp under **Händelser**.

![ACOP](./images/acopmenu.png)

Därefter visas en översikt över alla tillgängliga händelser. Klicka **Skapa händelse** för att börja skapa en egen händelse.

![ACOP](./images/emptyevent.png)

Ett nytt, tomt händelsefönster öppnas sedan.

![ACOP](./images/emptyevent1.png)

Först och främst ger du evenemanget ett namn som detta: `yourLastNameAccountCreationEvent` och lägg till en beskrivning som denna `Account Creation Event`.

![ACOP](./images/eventdescription.png)

Kontrollera sedan att **Typ** är inställd på **Unitary** och för **Typ av händelse-ID** markering, markera **Systemgenererat**.

![ACOP](./images/eventidtype.png)

Nästa steg är schemavalet. Ett schema förbereddes för den här övningen. Använd schemat `Demo System - Event Schema for Website (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

När du har valt schemat visas ett antal fält i **Fält** -avsnitt. Nu ska du hovra över **Fält** så visas tre popup-fönster med ikoner. Klicka på **Redigera** ikon.

![ACOP](./images/eventpayload.png)

Du får se en **Fält** fönsterpopup, där du måste markera några av de fält som vi behöver för att anpassa e-postmeddelandet.  Vi väljer andra profilattribut senare med de data som redan finns i Adobe Experience Platform.

![ACOP](./images/eventfields.png)

I objektet `_experienceplatform.demoEnvironment`måste du markera fälten **brandLogo** och **brandName**.

![ACOP](./images/eventpayloadbr.png)

I objektet `_experienceplatform.identification.core`måste du markera fältet **e-post**.

![ACOP](./images/eventpayloadbrid.png)

Klicka **OK** för att spara ändringarna.

![ACOP](./images/saveok.png)

Du borde se det här då. Klicka **Spara** ännu en gång för att spara ändringarna.

![ACOP](./images/eventsave.png)

Din händelse är nu konfigurerad och sparad.

![ACOP](./images/eventdone.png)

Klicka på aktiviteten igen för att öppna **Redigera händelse** skärm igen. Hovra över **Fält** igen för att se de tre ikonerna igen. Klicka på **Visa nyttolast** ikon.

![ACOP](./images/viewevent.png)

Nu visas ett exempel på den förväntade nyttolasten.
Händelsen har ett unikt ID för Orchestration-händelse som du kan hitta genom att rulla nedåt i nyttolasten tills du ser `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

Händelse-ID:t är det som måste skickas till Adobe Experience Platform för att utlösa den resa som du ska bygga i någon av de kommande övningarna. Kom ihåg detta eventID, som du kanske behöver det senare.
`"eventID": "19cab7852cdef99d25b6d5f1b6503da39d1f486b1d585743f97ed2d1e6b6c74f"`

Klicka **OK**, följt av att klicka **Avbryt**.

Du har nu avslutat den här övningen.

Nästa steg: [2.3 Skapa ett e-postmeddelande](./ex3.md)

[Gå tillbaka till användarflöde 2](./uc2.md)

[Gå tillbaka till Alla moduler](../../overview.md)
