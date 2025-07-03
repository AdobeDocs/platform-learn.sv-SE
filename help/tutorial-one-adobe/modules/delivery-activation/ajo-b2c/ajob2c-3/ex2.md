---
title: Konfigurera en resa med push-meddelanden
description: Konfigurera en resa med push-meddelanden
kt: 5342
doc-type: tutorial
source-git-commit: 203590e3289d2e5342085bf8b6b4e3cd11859539
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 0%

---

# 3.3.2 Konfigurera en resa med push-meddelanden


## 3.4.4.6 Skapa en ny händelse

Gå till **Journey Optimizer**. Gå till **Konfigurationer** på den vänstra menyn och klicka på **Hantera** under **Händelser**.

![ACOP](./images/acopmenu.png)

På skärmen **Händelser** ser du en liknande vy. Klicka på **Skapa händelse**.

![ACOP](./images/add.png)

Därefter visas en tom händelsekonfiguration.
Först och främst ger du evenemanget ett namn som detta: `--aepUserLdap--StoreEntryEvent` och anger beskrivningen till `Store Entry Event`.
Nästa steg är markeringen **Händelsetyp**. Välj **Enhet**.
Nästa steg är **Typ av händelse-ID**. Välj **Systemgenererad**.

![ACOP](./images/eventname.png)

Nästa steg är schemavalet. Ett schema förbereddes för den här övningen. Använd schemat `Demo System - Event Schema for Mobile App (Global v1.1) v.1`.

När du har valt schemat visas ett antal fält som markeras i avsnittet **Nyttolast**. Din händelse är nu helt konfigurerad.

Klicka på **Spara**.

![ACOP](./images/eventschema.png)

Händelsen är nu konfigurerad och sparad. Klicka på aktiviteten igen för att öppna skärmen **Redigera händelse** igen.

![ACOP](./images/eventdone.png)

Håll muspekaren över fältet **Nyttolast** och klicka på ikonen **Visa nyttolast** .

![ACOP](./images/hover.png)

Nu visas ett exempel på den förväntade nyttolasten.

Händelsen har ett unikt ID för Orchestration-händelse som du kan hitta genom att rulla nedåt i nyttolasten tills du ser `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

Händelse-ID är det som måste skickas till Adobe Experience Platform för att utlösa den resa som du ska bygga i nästa steg. Skriv ned detta eventID, som du behöver det i nästa steg.
`"eventID": "89acd341ec2b7d1130c9a73535029debf2ac35f486bc99236b1a5091d6f4bc68"`

Klicka på **OK**, följt av **Avbryt**.

## 3.4.4.7 Skapa en resa

Gå till **Resor** på menyn och klicka på **Skapa resa**.

![DSN](./images/sjourney1.png)

Då ser du det här. Ge resan ett namn. Använd `--aepUserLdap-- - Store Entry journey`. Klicka på **Spara**.

![DSN](./images/sjourney3.png)

Först måste du lägga till din händelse som startpunkt för din resa. Sök efter din händelse `--aepUserLdap--StoreEntryEvent` och dra och släpp den på arbetsytan. Klicka på **Spara**.

![DSN](./images/sjourney4.png)

Under **Åtgärder** söker du efter åtgärden **Push**. Dra och släpp åtgärden **Tryck** på arbetsytan.

Ange **kategorin** till **Marknadsföring** och välj en push-yta som gör att du kan skicka push-meddelanden. I det här fallet är e-postytan som ska väljas **Push-iOS-Android**.

>[!NOTE]
>
>Det måste finnas en kanal i Journey Optimizer som använder **appytan** som granskats tidigare.

![ACOP](./images/journeyactions1push.png)

Nästa steg är att skapa ett meddelande. Det gör du genom att klicka på **Redigera innehåll**.

![ACOP](./images/journeyactions2push.png)

Då ser du det här. Klicka på ikonen **personalisering** för fältet **Titel**.

![Tryck](./images/bp5.png)

Då ser du det här. Du kan nu välja valfritt profilattribut direkt i kundprofilen i realtid.

Sök efter fältet **Förnamn** och klicka sedan på ikonen **+** bredvid fältet **Förnamn**. Du kommer då att se personaliseringstoken för förnamn som läggs till: **{{profile.person.name.firstName}}**.

![Tryck](./images/bp9.png)

Lägg sedan till texten **, välkommen till vår butik!** bakom **{{profile.person.name.firstName}}**.

Klicka på **Spara**.

![Tryck](./images/bp10.png)

Du har den här nu. Klicka på ikonen **personalisering** för fältet **Brödtext**.

![Tryck](./images/bp11.png)

Ange den här texten **Klicka här för att få 10 % rabatt när du köper idag!** och klicka på **Spara**.

![Tryck](./images/bp12.png)

Du får den här då. Klicka på pilen i det övre vänstra hörnet för att gå tillbaka till din resa.

![Journey Optimizer](./images/bp12a.png)

Klicka på **Spara** för att stänga din push-åtgärd.

![DSN](./images/sjourney8.png)

Klicka på **Publicera**.

![DSN](./images/sjourney10.png)

Klicka på **Publicera** igen.

![DSN](./images/sjourney10a.png)

Din resa är nu publicerad.

![DSN](./images/sjourney11.png)

## 3.4.4.8 Testa din resa och skicka ett push-meddelande

Gå till skärmen **Inställningar** i ditt DX Demo 2.0-mobilprogram. Klicka på knappen **Butikspost**.

>[!NOTE]
>
>Knappen **Butikspost** implementeras. Du hittar det inte i appen än.

![DSN](./images/demo1b.png)

Stäng appen omedelbart efter att du klickat på ikonen **Store Entry** (Store-post), annars visas inte push-meddelandet.

Efter några sekunder visas meddelandet.

![DSN](./images/demo2.png)

Du har gjort klart den här övningen.

## Nästa steg

Gå till [3.3.3 Konfigurera en kampanj med meddelanden i appen](./ex3.md){target="_blank"}

Gå tillbaka till [Adobe Journey Optimizer: Push och In-app Messages](ajopushinapp.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../../overview.md){target="_blank"}
