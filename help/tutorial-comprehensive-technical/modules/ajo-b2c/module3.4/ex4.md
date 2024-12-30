---
title: Adobe Journey Optimizer - Konfigurera och använda push-meddelanden för iOS
description: Installera och använda push-meddelanden för iOS
kt: 5342
doc-type: tutorial
exl-id: a49fa91c-5235-4814-94c1-8dcdec6358c5
source-git-commit: c531412a2c0a5c216f49560e01fb26b9b7e71869
workflow-type: tm+mt
source-wordcount: '1800'
ht-degree: 0%

---

# 3.4.4 Konfigurera och använda push-meddelanden för iOS

Om du vill använda push-meddelanden med Adobe Journey Optimizer finns det ett antal inställningar att kontrollera och känna till.

Här följer alla inställningar som ska verifieras:

- Datauppsättningar och scheman i Adobe Experience Platform
- Datastream för mobiler
- Datainsamlingsegenskap för mobil
- Appyta för push-certifikat
- Testa din push-konfiguration med AEP Assurance

Vi granskar dem en i taget.

Logga in på Adobe Journey Optimizer på [Adobe Experience Cloud](https://experience.adobe.com). Klicka på **Journey Optimizer**.

![ACOP](./../../../modules/ajo-b2c/module3.1/images/acophome.png)

Du omdirigeras till vyn **Hem** i Journey Optimizer. Kontrollera först att du använder rätt sandlåda. Sandlådan som ska användas kallas `--aepSandboxName--`. Du kommer sedan att vara i vyn **Hem** i din sandlåda `--aepSandboxName--`.

![ACOP](./../../../modules/ajo-b2c/module3.1/images/acoptriglp.png)

## 3.4.4.1 Push datasets

Adobe Journey Optimizer använder datauppsättningar för att lagra saker som push-tokens från mobila enheter eller interaktioner med push-meddelanden (till exempel meddelande som skickas, meddelande som öppnas) i en datauppsättning i Adobe Journey Optimizer.

Du kan hitta de här datauppsättningarna genom att gå till **[!UICONTROL Datasets]** på menyn till vänster på skärmen. Om du vill visa systemdatauppsättningar klickar du på filterikonen.

![Datainmatning](./images/menudsjo.png)

Aktivera alternativet **Visa systemdatauppsättningar** och sök efter **AJO**. Du kommer då att se de datauppsättningar som används för push-meddelanden.

![Datainmatning](./images/menudsjo1.png)

## 3.4.4.2 Datastream för mobiler

Gå till [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/).

Gå till **[!UICONTROL Datastream]** på den vänstra menyn och sök efter det datastream som du skapade i [Exercise 0.2](./../../../modules/gettingstarted/gettingstarted/ex2.md), som har namnet `--aepUserLdap-- - Demo System Datastream (Mobile)`. Klicka för att öppna den.

![Klicka på Datastream-ikonen i den vänstra navigeringen](./images/edgeconfig1a.png)

Klicka på **Redigera** på tjänsten **Adobe Experience Platform**.

![Klicka på Datastream-ikonen i den vänstra navigeringen](./images/edgeconfig1.png)

Du kommer då att se de datastream-inställningar som har definierats och i vilka datamängdshändelser och profilattribut lagras.

![Namnge dataströmmen och spara](./images/edgeconfig2.png)

Inga ändringar behövs. Datastream är nu klar att användas i din datainsamling-klientegenskap för Mobile.

## 3.4.4.3 Granska din datainsamlingsegenskap för mobiler

Gå till [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/). Som en del av [övningen 0.1](./../../../modules/gettingstarted/gettingstarted/ex1.md) skapades två datainsamlingsegenskaper.
Du har redan använt dessa egenskaper för datainsamlingsklienten som en del av tidigare moduler.

Klicka för att öppna datainsamlingsegenskapen för mobilen.

![DSN](./images/launchprop.png)

Gå till **Tillägg** i din datainsamlingsegenskap. Du kommer då att se de olika tillägg som behövs för mobilappen. Klicka för att öppna tillägget **Adobe Experience Platform Edge Network**.

![Adobe Experience Platform-datainsamling](./images/launchprop1.png)

Du kommer då att se att ditt datastream för mobilen är länkat här. Klicka sedan på **Avbryt** för att gå tillbaka till översikten över dina tillägg.

![Adobe Experience Platform-datainsamling](./images/launchprop2.png)

Du kommer då tillbaka hit. Tillägget för **AEP Assurance** visas. AEP Assurance hjälper er att inspektera, bevisa, simulera och validera hur ni samlar in data eller levererar upplevelser i er mobilapp. Du kan läsa mer om AEP Assurance och Project Griffon här [https://aep-sdks.gitbook.io/docs/beta/project-griffon](https://aep-sdks.gitbook.io/docs/beta/project-griffon).

![Adobe Experience Platform-datainsamling](./images/launchprop8.png)

Klicka sedan på **Konfigurera** för att öppna tillägget **Adobe Journey Optimizer**.

![Adobe Experience Platform-datainsamling](./images/launchprop9.png)

Du kommer då att se att det är här som datauppsättningen för spårning av push-händelser är länkad.

![Adobe Experience Platform-datainsamling](./images/launchprop10.png)

Du behöver inte göra några ändringar i din datainsamlingsegenskap.

## 3.4.4.4 Granska konfigurationen av appytan

Gå till [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/). Gå till **Appytor** på den vänstra menyn och öppna appytan för **DX Demo App APNS**.

![Adobe Experience Platform-datainsamling](./images/appsf.png)

Sedan visas den konfigurerade appytan för iOS och Android.

![Adobe Experience Platform-datainsamling](./images/appsf1.png)

## 3.4.4.5 Testa konfigurationen av push-meddelanden med AEP Assurance.

När appen har installerats hittar du den på enhetens hemskärm. Klicka på ikonen för att öppna programmet.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/mobileappn1.png)

När du använder appen första gången ombeds du logga in med din Adobe ID. Slutför inloggningsprocessen.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/mobileappn2.png)

När du har loggat in visas ett meddelande som ber dig att skicka meddelanden. Vi skickar meddelanden som en del av självstudiekursen, så klicka på **Tillåt**.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/mobileappn3.png)

Då ser du appens hemsida. Gå till **Inställningar**.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/mobileappn4.png)

I inställningarna ser du att ett **offentligt projekt** har lästs in i appen. Klicka på **Eget projekt**.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/mobileappn5.png)

Du kan nu läsa in ett anpassat projekt. Klicka på QR-koden för att enkelt läsa in ditt projekt.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/mobileappn6.png)

Efter träning 0.1 fick du det här resultatet. Klicka för att öppna det **Mobile Retail-projekt** som skapades för dig.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/dsn5b.png)

Om du av misstag har stängt webbläsarfönstret, eller för framtida demonstrations- eller aktiveringssessioner, kan du även komma åt webbplatsprojektet genom att gå till [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). När du har loggat in med din Adobe ID ser du det här. Klicka på ditt mobilappsprojekt för att öppna det.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web8a.png)

Då ser du det här. Klicka på **Integrationer**.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web8aa.png)

Du måste välja datainsamlingsegenskapen för mobilen som skapades i övning 0.1. Klicka sedan på **Kör**.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web8b.png)

Då visas den här popup-rutan som innehåller en QR-kod. Skanna QR-koden inifrån mobilappen.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web8c.png)

Sedan visas ditt projekt-ID i appen. Sedan kan du klicka på **Spara**.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/mobileappn7.png)

Gå tillbaka till **Hem** i appen. Ditt program är nu klart att användas.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/mobileappn8.png)

Nu måste du skanna en QR-kod för att ansluta den mobila enheten till AEP Assurance-sessionen.

Om du vill starta en AEP Assurance-session går du till [https://experience.adobe.com/#/@experienceplatform/griffon](https://experience.adobe.com/#/@experienceplatform/griffon). Klicka på **Skapa session**.

![Adobe Experience Platform-datainsamling](./images/griffon3.png)

Klicka på **Start**.

![Adobe Experience Platform-datainsamling](./images/griffon5.png)

Fyll i värdena:

- Sessionsnamn: använd `--aepUserLdap-- - push debugging` och ersätt ldap med din ldap
- Bas-URL: använd **dxdemo://default**

Klicka på **Nästa**.

![Adobe Experience Platform-datainsamling](./images/griffon4.png)

Sedan visas en QR-kod på skärmen som du bör skanna med din iOS-enhet.

![Adobe Experience Platform-datainsamling](./images/griffon6.png)

Öppna kameramappen på din mobila enhet och skanna QR-koden som visas av AEP Assurance.

![Adobe Experience Platform-datainsamling](./images/ipadPushTest8a.png)

Då visas en popup-skärm där du ombeds ange PIN-koden. Kopiera PIN-koden från AEP Assurance-skärmen och klicka på **Anslut**.

![Adobe Experience Platform-datainsamling](./images/ipadPushTest9.png)

Då ser du det här.

![Adobe Experience Platform-datainsamling](./images/ipadPushTest11.png)

I AEP Assurance ser du nu att en enhet går till AEP Assurance-sessionen.

![Adobe Experience Platform-datainsamling](./images/griffon7.png)

Gå till **Push Debug**. Du kommer att se något liknande.

![Adobe Experience Platform-datainsamling](./images/griffon10.png)

Förklaring:

- I den första kolumnen, **Klient**, visas tillgängliga identifierare på din iOS-enhet. Du ser ett ECID och en push-token.
- I den andra kolumnen visas **profilinformation**, med ytterligare information om vilken plattform Push-token finns i (APNS eller APNSSandbox). Om du klickar på knappen **Inspect-profil** dirigeras du till Adobe Experience Platform och du ser hela kundprofilen i realtid.
- I den tredje kolumnen visas **App Configuration** som konfigurerades som en del av övningen **3.4.5.4 Create App Configuration i Launch**

Klicka på knappen **Skicka push-meddelande** om du vill testa push-konfigurationsinställningarna.

![Adobe Experience Platform-datainsamling](./images/griffon11.png)

Du måste kontrollera att appen **DX Demo** inte är öppen när du klickar på knappen **Skicka push-meddelande** . Om appen är öppen kan push-meddelandet tas emot i bakgrunden och inte visas.

Du kommer då att se ett sådant här push-meddelande på din mobila enhet.

![Adobe Experience Platform-datainsamling](./images/ipadPush2.png)

Om du har fått ett push-meddelande betyder det att konfigurationen är korrekt och fungerar som den ska.

## 3.4.4.6 Skapa en ny händelse

Gå till **Reseadministration** på menyn och klicka på **Hantera** under **Händelser**.

![ACOP](./images/acopmenu.png)

På skärmen **Händelser** ser du en liknande vy. Klicka på **Skapa händelse**.

![ACOP](./images/add.png)

Därefter visas en tom händelsekonfiguration.

![ACOP](./images/emptyevent.png)

Först och främst ger du evenemanget ett namn som detta: `--aepUserLdap--StoreEntryEvent` och anger beskrivningen till `Store Entry Event`.

![ACOP](./images/eventname.png)

Nästa steg är markeringen **Händelsetyp**. Välj **Enhet**.

![ACOP](./images/eventidtype1.png)

Nästa steg är **Typ av händelse-ID**. Välj **Systemgenererad**

![ACOP](./images/eventidtype.png)

Nästa steg är schemavalet. Ett schema förbereddes för den här övningen. Använd schemat `Demo System - Event Schema for Mobile App (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

När du har valt schemat visas ett antal fält som markeras i avsnittet **Nyttolast**. Din händelse är nu helt konfigurerad.

![ACOP](./images/eventpayload.png)

Du borde se det här då. Klicka på **Spara**.

![ACOP](./images/eventsave.png)

Händelsen är nu konfigurerad och sparad. Klicka på aktiviteten igen för att öppna skärmen **Redigera händelse** igen.

![ACOP](./images/eventdone.png)

Håll muspekaren över fältet **Nyttolast** och klicka på ikonen **Visa nyttolast** .

![ACOP](./images/hover.png)

Nu visas ett exempel på den förväntade nyttolasten.

![ACOP](./images/fullpayload.png)

Händelsen har ett unikt ID för Orchestration-händelse som du kan hitta genom att rulla nedåt i nyttolasten tills du ser `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

Händelse-ID är det som måste skickas till Adobe Experience Platform för att utlösa den resa som du ska bygga i nästa steg. Skriv ned detta eventID, som du behöver det i nästa steg.
`"eventID": "e3a8f0bdc0b609667cd96a72a6b1e5aafa0ddaf6ccf121c574e6a2030860a633"`

Klicka på **OK**, följt av **Avbryt**.

## 3.4.4.7 Skapa en resa

Gå till **Resor** på menyn och klicka på **Skapa resa**.

![DSN](./images/sjourney1.png)

Då ser du det här. Ge resan ett namn. Använd `--aepUserLdap-- - Store Entry journey`. Klicka på **OK**.

![DSN](./images/sjourney3.png)

Först måste du lägga till din händelse som startpunkt för din resa. Sök efter din händelse `--aepUserLdap--StoreEntryEvent` och dra och släpp den på arbetsytan. Klicka på **OK**.

![DSN](./images/sjourney4.png)

Under **Åtgärder** söker du efter åtgärden **Push**.
Dra och släpp åtgärden **Tryck** på arbetsytan.

![DSN](./images/sjourney5.png)

Ange **kategorin** till **Marknadsföring** och välj en push-yta som gör att du kan skicka push-meddelanden. I det här fallet är e-postytan som ska väljas **Push-iOS-Android**.

![ACOP](./images/journeyactions1push.png)

Nästa steg är att skapa ett meddelande. Det gör du genom att klicka på **Redigera innehåll**.

![ACOP](./images/journeyactions2push.png)

Då ser du det här. Klicka på ikonen **personalisering** för fältet **Titel**.

![Tryck](./images/bp5.png)

Då ser du det här. Du kan nu välja valfritt profilattribut direkt i kundprofilen i realtid.

![Tryck](./images/bp6.png)

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

Klicka på **OK** för att stänga din push-åtgärd.

![DSN](./images/sjourney8.png)

Klicka på **Publish**.

![DSN](./images/sjourney10.png)

Klicka på **Publish** igen.

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

![DSN](./images/demo2.png)

Efter några sekunder visas meddelandet.

![DSN](./images/demo3.png)

Du har gjort klart den här övningen.

Nästa steg: [3.4.5 Skapa en affärshändelseresa](./ex5.md)

[Gå tillbaka till modul 3.4](./journeyoptimizer.md)

[Gå tillbaka till Alla moduler](../../../overview.md)
