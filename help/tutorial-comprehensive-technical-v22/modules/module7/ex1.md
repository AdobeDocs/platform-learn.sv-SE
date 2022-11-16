---
title: Journey Optimizer Create your event
description: Journey Optimizer Create your event
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
exl-id: e35d2357-21f9-4566-b2a1-cc0cf0c64956
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# 7.1 Skapa en aktivitet

Logga in på Adobe Journey Optimizer genom att gå till [Adobe Experience Cloud](https://experience.adobe.com). Klicka **Journey Optimizer**.

![ACOP](./images/acophome.png)

Du omdirigeras till **Startsida**  i Journey Optimizer. Kontrollera först att du använder rätt sandlåda. Sandlådan som ska användas anropas `--aepSandboxId--`. Om du vill ändra från en sandlåda till en annan klickar du på **PRODUKTIONSprodukt (VA7)** och välj sandlådan i listan. I det här exemplet heter sandlådan **AEP-aktivering FY22**. Då är du i **Startsida** vy över din sandlåda `--aepSandboxId--`.

![ACOP](./images/acoptriglp.png)

Bläddra nedåt i den vänstra menyn och klicka på **Konfigurationer**. Klicka sedan på **Hantera** knapp under **Händelser**.

![ACOP](./images/acopmenu.png)

Därefter visas en översikt över alla tillgängliga händelser. Klicka **Skapa händelse** för att börja skapa en egen händelse.

![ACOP](./images/emptyevent.png)

Ett nytt, tomt händelsefönster öppnas sedan.

![ACOP](./images/emptyevent1.png)

Först och främst ger du evenemanget ett namn som detta: `--demoProfileLdap--AccountCreationEvent`.

![ACOP](./images/eventname.png)

Lägg sedan till en sådan beskrivning `Account Creation Event`.

![ACOP](./images/eventdescription.png)

Kontrollera sedan att **Typ** är inställd på **Unitary** och för **Typ av händelse-ID** markering, markera **Systemgenererat**.

![ACOP](./images/eventidtype.png)

Nästa steg är schemavalet. Ett schema förbereddes för den här övningen. Använd schemat `Demo System - Event Schema for Website (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

När du har valt schemat visas ett antal fält i **Nyttolast** -avsnitt. Nu ska du hovra över **Nyttolast** så visas tre popup-fönster med ikoner. Klicka på **Redigera** ikon.

![ACOP](./images/eventpayload.png)

Du får se en **Fält** fönsterpopup, där du måste markera några av de fält som vi behöver för att anpassa e-postmeddelandet.  Vi väljer andra profilattribut senare med de data som redan finns i Adobe Experience Platform.

![ACOP](./images/eventfields.png)

I objektet `--aepTenantId--.demoEnvironment`måste du markera fälten **brandLogo** och **brandName**.

![ACOP](./images/eventpayloadbr.png)

I objektet `--aepTenantId--.identification.core`måste du markera fältet **e-post**.

![ACOP](./images/eventpayloadbrid.png)

Klicka **OK** för att spara ändringarna.

![ACOP](./images/saveok.png)

Du bör då se det här:

![ACOP](./images/eventsave.png)

Klicka **Spara** ännu en gång för att spara ändringarna.

![ACOP](./images/save1.png)

Din händelse är nu konfigurerad och sparad.

![ACOP](./images/eventdone.png)

Klicka på aktiviteten igen för att öppna **Redigera händelse** skärm igen. Hovra över **Nyttolast** om du vill visa de tre ikonerna igen. Klicka på **Visa nyttolast** ikon.

![ACOP](./images/viewevent.png)

Nu visas ett exempel på den förväntade nyttolasten.

![ACOP](./images/fullpayload.png)

Händelsen har ett unikt ID för Orchestration-händelse som du kan hitta genom att rulla nedåt i nyttolasten tills du ser `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

Händelse-ID är det som måste skickas till Adobe Experience Platform för att utlösa den resa som du bygger i Exercise 7.2. Kom ihåg detta eventID, som du behöver det i Exercise 7.3.
`"eventID": "227402c540eb8f8855c6b2333adf6d54d7153d9d7d56fa475a6866081c574736"`

Klicka **OK**, följt av att klicka **Avbryt**.

Du har nu avslutat den här övningen.

Nästa steg: [7.2 Journey Optimizer: Skapa en resa och ett e-postmeddelande](./ex2.md)

[Gå tillbaka till modul 7](./journey-orchestration-create-account.md)

[Gå tillbaka till Alla moduler](../../overview.md)
