---
title: Komma igång med push-meddelanden
description: Komma igång med push-meddelanden
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
exl-id: b46e0205-b0a1-4a14-95f6-9afe21cd2b5e
source-git-commit: fb14ba45333bdd5834ff0c6c2dc48dda35cfe85f
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 0%

---

# 3.3.1 Komma igång med push-meddelanden

Om du vill använda push-meddelanden med Adobe Journey Optimizer finns det ett antal inställningar att kontrollera och känna till.

Här följer alla inställningar som ska verifieras:

- Datauppsättningar och scheman i Adobe Experience Platform
- Datastream för mobiler
- Datainsamlingsegenskap för mobil
- Appyta för push-certifikat
- Testa push-konfigurationen med AEP Assurance

Vi granskar dem en i taget.

Logga in på Adobe Journey Optimizer på [Adobe Experience Cloud](https://experience.adobe.com). Klicka på **Journey Optimizer**.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Du omdirigeras till vyn **Hem** i Journey Optimizer. Kontrollera först att du använder rätt sandlåda. Sandlådan som ska användas kallas `--aepSandboxName--`. Du kommer sedan att vara i vyn **Hem** i din sandlåda `--aepSandboxName--`.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

## 3.3.1.1 push-datauppsättning

Adobe Journey Optimizer använder datauppsättningar för att lagra saker som push-tokens från mobila enheter eller interaktioner med push-meddelanden (till exempel meddelande som skickas, meddelande som öppnas) i en datauppsättning i Adobe Journey Optimizer.

Du kan hitta de här datauppsättningarna genom att gå till **Datauppsättningar** på menyn till vänster på skärmen. Om du vill visa systemdatauppsättningar klickar du på ikonen **Aktivera filter** .

Aktivera alternativet för **System** och sök efter **AJO**. Du kommer då att se de datauppsättningar som används för push-meddelanden.

![Datainmatning](./images/menudsjo1.png)

## 3.3.1.2 Datastream för mobilen

Gå till [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/).

Gå till **Datastreams** på den vänstra menyn och sök efter datastream som du skapade i [Komma igång](./../../../../modules/getting-started/gettingstarted/ex2.md), som har namnet `--aepUserLdap-- - One Adobe Datastream (Mobile)`. Klicka för att öppna den.

![Datastreams](./images/edgeconfig1a.png)

Klicka på **Redigera** på tjänsten **Adobe Experience Platform**.

![Datastreams](./images/edgeconfig1.png)

Du kommer då att se de datastream-inställningar som har definierats och i vilka datamängdshändelser och profilattribut lagras.

Du bör även aktivera följande alternativ om de inte är aktiverade än:

- **Offer Decisioning**
- **Personalization Destinations**
- **Adobe Journey Optimizer**

Klicka på **Spara**.

![Namnge dataströmmen och spara](./images/edgeconfig2.png)

## 3.3.1.3 Granska din datainsamlingsegenskap för Mobile

Gå till [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/), till **Taggar**. Som en del av [Komma igång](./../../../../modules/getting-started/gettingstarted/ex1.md)-modulen skapades taggegenskaper för datainsamling.

Du har redan använt dessa taggegenskaper för datainsamling som en del av tidigare moduler.

Klicka för att öppna datainsamlingsegenskapen för mobilen.

![DSN](./images/launchprop.png)

Gå till **Tillägg** i din datainsamlingsegenskap. Du kommer då att se de olika tillägg som behövs för mobilappen. Klicka för att markera tillägget **Adobe Experience Platform Edge Network** och välj sedan **Konfigurera**.

![Adobe Experience Platform-datainsamling](./images/launchprop1.png)

Du kommer då att se att ditt datastream för mobilen är länkat här. Klicka sedan på **Avbryt** för att gå tillbaka till översikten över tillägg.

![Adobe Experience Platform-datainsamling](./images/launchprop2.png)

Du kommer då tillbaka hit. Tillägget för **AEP Assurance** visas. AEP Assurance hjälper er att inspektera, bevisa, simulera och validera hur ni samlar in data eller levererar upplevelser i er mobilapp. Du kan läsa mer om AEP Assurance här: [https://experienceleague.adobe.com/sv/docs/experience-platform/assurance/home](https://experienceleague.adobe.com/sv/docs/experience-platform/assurance/home).

![Adobe Experience Platform-datainsamling](./images/launchprop8.png)

Klicka sedan på **Konfigurera** för att öppna tillägget **Adobe Journey Optimizer**. Det här tillägget möjliggör push-meddelanden och mätning av Adobe Journey Optimizer.

![Adobe Experience Platform-datainsamling](./images/launchprop9.png)

Du kommer då att se att det är här som datauppsättningen för spårning av push-händelser är länkad. Du behöver inte göra några ändringar i din datainsamlingsegenskap. Klicka på **Avbryt** för att gå tillbaka till föregående skärm.

![Adobe Experience Platform-datainsamling](./images/launchprop10.png)

## 3.3.1.4 Granska konfigurationen av appytan

Gå till [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/). Gå till **App Surfaces** på den vänstra menyn och öppna appytan för **DX Demo App APNS**.

![Adobe Experience Platform-datainsamling](./images/appsf.png)

Sedan visas den konfigurerade appytan för iOS och Android.

![Adobe Experience Platform-datainsamling](./images/appsf1.png)

## 3.3.1.5 Testa konfigurationen av push-meddelanden med AEP Assurance.

Du har redan installerat mobilprogrammet **DX Demo** som en del av modulen **Komma igång** . När appen har installerats hittar du den på enhetens hemskärm. Klicka på ikonen för att öppna programmet.

![DSN](./../../../../modules/getting-started/gettingstarted/images/mobileappn1.png)

När du har loggat in visas ett meddelande som ber dig att skicka meddelanden. Vi skickar meddelanden som en del av självstudiekursen, så klicka på **Tillåt**.

![DSN](./../../../modules/../getting-started/gettingstarted/images/mobileappn2.png)

Då ser du appens hemsida. Gå till **Inställningar**.

![DSN](./../../../modules/../getting-started/gettingstarted/images/mobileappn3.png)

I inställningarna ser du att ett **offentligt projekt** har lästs in i appen. Klicka på **Eget projekt**.

![DSN](./../../../modules/../getting-started/gettingstarted/images/mobileappn4.png)

Du kan nu läsa in ett anpassat projekt. Klicka på QR-koden för att enkelt läsa in ditt projekt.

![DSN](./../../../modules/../getting-started/gettingstarted/images/mobileappn5.png)

När du gått igenom avsnittet **Komma igång** fick du det här resultatet. Klicka för att öppna det **Mobile Retail-projekt** som skapades för dig.

![DSN](./../../../modules/../getting-started/gettingstarted/images/dsn5b.png)

Om du av misstag har stängt webbläsarfönstret, eller för framtida demonstrations- eller aktiveringssessioner, kan du även komma åt webbplatsprojektet genom att gå till [https://dsn.adobe.com/projects](https://dsn.adobe.com/projects). När du har loggat in med din Adobe ID ser du det här. Klicka på ditt mobilappsprojekt för att öppna det.

![DSN](./../../../modules/../getting-started/gettingstarted/images/web8a.png)

Klicka sedan på **Kör**.

![DSN](./images/web8b.png)

Då visas den här popup-rutan som innehåller en QR-kod. Skanna QR-koden inifrån mobilappen.

![DSN](./../../../modules/../getting-started/gettingstarted/images/web8c.png)

Du kommer då att se ditt projekt-ID i appen, och därefter kan du klicka på **Byt**.

![DSN](./../../../modules/../getting-started/gettingstarted/images/mobileappn7.png)

Ditt program är nu klart att användas.

![DSN](./../../../modules/../getting-started/gettingstarted/images/mobileappn8.png)

Nu måste du skanna en QR-kod för att ansluta den mobila enheten till din Assurance-session.

Om du vill starta en AEP Assurance-session går du till [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/). Klicka på **Assurance** i den vänstra menyn. Klicka sedan på **Skapa session**.

![Adobe Experience Platform-datainsamling](./images/griffon3.png)

Välj **Djupanslutning** och klicka sedan på **Start**.

![Adobe Experience Platform-datainsamling](./images/griffon5.png)

Fyll i värdena:

- Sessionsnamn: `--aepUserLdap-- - Push Debugging`
- Bas-URL: `dxdemo://default`

Klicka på **Nästa**.

![Adobe Experience Platform-datainsamling](./images/griffon4.png)

Sedan visas en QR-kod på skärmen som du bör skanna med din iOS-enhet.

![Adobe Experience Platform-datainsamling](./images/griffon6.png)

Öppna kameramappen på din mobila enhet och skanna QR-koden som visas av Assurance.

![Adobe Experience Platform-datainsamling](./images/ipadPushTest8a.png)

Då visas en popup-skärm där du ombeds ange PIN-koden. Kopiera PIN-koden från AEP Assurance-skärmen och klicka på **Anslut**.

![Adobe Experience Platform-datainsamling](./images/ipadPushTest9.png)

Då ser du det här.

![Adobe Experience Platform-datainsamling](./images/ipadPushTest11.png)

I Assurance ser du nu att en klientenhet är ansluten till Assurance-sessionen. Klicka sedan på **Konfigurera**.

![Adobe Experience Platform-datainsamling](./images/griffon7.png)

Bläddra ned till **Push Debug**. Klicka på ikonen **+** och sedan på **Spara**.

![Adobe Experience Platform-datainsamling](./images/griffon7a.png)

Gå till **Push Debug**. Du borde se det här.

![Adobe Experience Platform-datainsamling](./images/griffon10.png)

Förklaring:

- I den första kolumnen, **Klient**, visas tillgängliga identifierare på din iOS-enhet. Du ser ett ECID och en push-token.
- I den andra kolumnen visas **App Store-autentiseringsuppgifter och konfiguration**
- I den andra kolumnen visas **profilinformation**, med ytterligare information om vilken plattform Push-token finns i (APNS eller APNSSandbox). Om du klickar på knappen **Inspektera profil** dirigeras du till Adobe Experience Platform och du ser hela kundprofilen i realtid.

Om du vill testa push-konfigurationsinställningarna går du till knappen **Skicka testpush-inställningar** . Klicka på **Skicka push-meddelande om testning**

![Adobe Experience Platform-datainsamling](./images/griffon11.png)

Du måste kontrollera att appen **DX Demo** inte är öppen när du klickar på knappen **Skicka push-meddelande** . Om appen är öppen kan push-meddelandet tas emot i bakgrunden och inte visas.

Du kommer då att se ett sådant här push-meddelande på din mobila enhet.

![Adobe Experience Platform-datainsamling](./images/ipadPush2.png)

Om du har fått ett push-meddelande betyder det att konfigurationen är korrekt och fungerar bra och att du nu kan skapa en verklig resa som resulterar i att du skickar ett push-meddelande från Journey Optimizer.

## Nästa steg

Gå till [3.3.2 Konfigurera en resa med push-meddelanden](./ex2.md){target="_blank"}

Gå tillbaka till [Adobe Journey Optimizer: Push och In-app Messages](ajopushinapp.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../../overview.md){target="_blank"}
