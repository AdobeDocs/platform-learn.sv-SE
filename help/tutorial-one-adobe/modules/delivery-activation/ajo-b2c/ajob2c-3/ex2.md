---
title: Konfigurera en resa med push-meddelanden
description: Konfigurera en resa med push-meddelanden
kt: 5342
doc-type: tutorial
exl-id: 63d7ee24-b6b5-4503-b104-a345c2b26960
source-git-commit: fb14ba45333bdd5834ff0c6c2dc48dda35cfe85f
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 0%

---

# 3.3.2 Konfigurera en resa med push-meddelanden

Logga in på Adobe Journey Optimizer på [Adobe Experience Cloud](https://experience.adobe.com). Klicka på **Journey Optimizer**.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Du omdirigeras till vyn **Hem** i Journey Optimizer. Kontrollera först att du använder rätt sandlåda. Sandlådan som ska användas kallas `--aepSandboxName--`. Du kommer sedan att vara i vyn **Hem** i din sandlåda `--aepSandboxName--`.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

## 3.3.2.1 Skapa en ny händelse

Gå till **Konfigurationer** på den vänstra menyn och klicka på **Hantera** under **Händelser**.

![ACOP](./images/acopmenu.png)

På skärmen **Händelser** ser du en liknande vy. Klicka på **Skapa händelse**.

![ACOP](./images/add.png)

Därefter visas en tom händelsekonfiguration.
Först och främst ger du evenemanget ett namn som detta: `--aepUserLdap--StoreEntryEvent` och anger beskrivningen till `Store Entry Event`.
Nästa steg är markeringen **Händelsetyp**. Välj **Enhet**.
Nästa steg är **Typ av händelse-ID**. Välj **Systemgenererad**.

![ACOP](./images/eventname.png)

Nästa steg är schemavalet. Ett schema förbereddes för den här övningen. Använd schemat `Demo System - Event Schema for Mobile App (Global v1.1) v.1`.

När du har valt schemat visas ett antal fält som markeras i avsnittet **Nyttolast**. Kontrollera att fältet **Namespace** har värdet **ECID**. Din händelse är nu helt konfigurerad.

Klicka på **Spara**.

![ACOP](./images/eventschema.png)

Din händelse är nu konfigurerad och sparad. Klicka på aktiviteten igen för att öppna skärmen **Redigera händelse** igen.

![ACOP](./images/eventdone.png)

Håll muspekaren över fältet **Nyttolast** och klicka på ikonen **Visa nyttolast** .

![ACOP](./images/hover.png)

Nu visas ett exempel på den förväntade nyttolasten.

Händelsen har ett unikt ID för Orchestration-händelse som du kan hitta genom att rulla nedåt i nyttolasten tills du ser `_experience.campaign.orchestration.eventID`.

Händelse-ID är det som måste skickas till Adobe Experience Platform för att utlösa den resa som du ska bygga i nästa steg. Skriv ned detta eventID, som du behöver det i nästa steg.
`"eventID": "aa895251f76831e6440f169f1bb9d2a4388f0696d8e2782cfab192a275817dfa"`

Klicka på **OK**.

![ACOP](./images/payloadeventID.png)

Klicka på **Avbryt**.

![ACOP](./images/payloadeventIDa.png)

## 3.3.2.2 Skapa en resa

Gå till **Resor** på den vänstra menyn och klicka på **Skapa resa**.

![DSN](./images/sjourney1.png)

Då ser du det här. Ge din resa ett namn: `--aepUserLdap-- - Store Entry journey`. Klicka på **Spara**.

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

## 3.3.2.3 Uppdatera din datainsamlingsegenskap för mobilen

I **Getting Started** skapade Demo System sedan taggegenskaper åt dig: en för webbplatsen och en för mobilappen. Sök efter dem genom att söka efter `--aepUserLdap--` i rutan **Sök**. Klicka för att öppna egenskapen **Mobile**.

![DSN](./images/pushpoi1.png)

Du borde se det här då.

![DSN](./images/pushpoi2.png)

Gå till **Regler** på den vänstra menyn och klicka för att öppna regeln **Platspost**.

![DSN](./images/pushpoi3.png)

Du borde se det här då. Klicka på åtgärden **Mobile Core - Attach Data**.

![DSN](./images/pushpoi4.png)

Du borde se det här då.

![DSN](./images/pushpoi5.png)

Klistra in eventID för din händelse `--aepUserLdap--StoreEntryEvent` i fönstret **JSON Payload**. Klicka på **Behåll ändringar**.

![DSN](./images/pushpoi6.png)

Klicka på **Spara** eller **Spara i bibliotek**.

![DSN](./images/pushpoi7.png)

Gå till **Publiceringsflöde** och klicka för att öppna biblioteket **Huvudsida**.

![DSN](./images/pushpoi8.png)

Klicka på **Lägg till alla ändrade resurser** och sedan på **Spara och skapa i utveckling**.

![DSN](./images/pushpoi9.png)

## 3.3.2.4 Testa din resa och skicka ett push-meddelande

Öppna **DSN Mobile**-programmet.

![DSN](./images/dxdemo1.png)

Gå till sidan **Store Locator**.

![DSN](./images/dxdemo2.png)

Klicka på **Simulera POI-post**.

![DSN](./images/dxdemo3.png)

Efter några sekunder visas ett push-meddelande.

![DSN](./images/dxdemo4.png)

## Nästa steg

Gå till [3.3.3 Konfigurera en kampanj med meddelanden i appen](./ex3.md){target="_blank"}

Gå tillbaka till [Adobe Journey Optimizer: Push och In-app Messages](ajopushinapp.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../../overview.md){target="_blank"}