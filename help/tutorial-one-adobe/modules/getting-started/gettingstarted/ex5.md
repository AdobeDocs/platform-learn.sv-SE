---
title: Komma igång - Använd mobilappen
description: Komma igång - Använd mobilappen
kt: 5342
doc-type: tutorial
exl-id: a619dd84-5c9e-4c1e-a753-2d98f50f4cfb
source-git-commit: 53f21d39caa047170811a063ff9d01d57e456626
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---

# Använda mobilappen

## Hämta appen

Gå till [https://dsn.adobe.com/install](https://dsn.adobe.com/install){target="_blank"} på datorn och gå till **Beta Version**. Logga in med din Adobe ID så ser du det här.

![DSN](./images/mobileapp.png)

Använd appen **Camera** på smarttelefonen för att installera mobilappen för operativsystemet på din enhet. För den här aktiveringen måste du installera versionen **0.6.1** (eller senare) som använder Adobe Experience Platform Mobile SDK.

>[!NOTE]
>
>När du har installerat appen för första gången på en iOS-enhet kan du få ett felmeddelande när du försöker öppna appen som säger: **Untrusted Enterprise Developer**. För att kunna åtgärda detta måste du gå till **Inställningar > Allmänt > VPN och enhetshantering > Adobe Systems Inc.** och klicka på **Lita på Adobe Systems Inc.**.

När du har läst in QR-koden väljer du **Installera**.

![DSN](./images/mobileappn0.png)

När appen har installerats hittar du den på enhetens hemskärm. Klicka på ikonen för att öppna programmet.

![DSN](./images/mobileappn1.png)

När du har loggat in visas ett meddelande som ber dig att skicka meddelanden. Vi skickar meddelanden som en del av självstudiekursen, så klicka på **Tillåt**.

![DSN](./images/mobileappn2.png)

Då ser du appens hemsida. Gå till **Inställningar**.

![DSN](./images/mobileappn3.png)

I inställningarna ser du att ett **offentligt projekt** har lästs in i appen. Klicka på **Eget projekt**.

![DSN](./images/mobileappn4.png)

Du kan nu läsa in ett anpassat projekt. Klicka på QR-koden för att enkelt läsa in ditt projekt.

![DSN](./images/mobileappn5.png)

Efter föregående övning fick du det här resultatet. Klicka för att öppna det **Mobile Edge Telco-projekt** som skapades åt dig.

![DSN](./images/dsn5b.png)

Om du av misstag har stängt webbläsarfönstret, eller för framtida demonstrations- eller aktiveringssessioner, kan du även komma åt webbplatsprojektet genom att gå till [https://dsn.adobe.com](https://dsn.adobe.com){target="_blank"}. När du har loggat in med din Adobe ID ser du det här. Klicka på de tre punkterna **..** i ditt mobilappsprojekt och klicka sedan på **Redigera**.

![DSN](./images/web8a.png)

På sidan **Integrationer** måste du välja den datainsamlingsegenskap som skapades i föregående övning. Det gör du genom att klicka på **Välj miljö**.

![DSN](./images/web8aa.png)

Klicka på **Välj** på den datainsamlingsegenskap som skapades i föregående steg med namnet `--aepUserLdap - One Adobe (DD/MM/YYYY) (mobile)`. Klicka sedan på **Spara**.

![DSN](./images/web8b.png)

Då ser du det här. Klicka sedan på **Kör**.

![DSN](./images/web8bb.png)

Då visas den här popup-rutan som innehåller en QR-kod. Skanna QR-koden inifrån mobilappen.

![DSN](./images/web8c.png)

Du kommer då att se att ditt projekt-ID läses in i appen och sedan kan du klicka på **Växla**.

![DSN](./images/mobileappn7.png)

Du bör då se att demovarumärket **CitiSignal** läses in. Ditt program är nu klart att användas.

![DSN](./images/mobileappn8.png)

## Nästa steg

Gå till [Konfigurera ditt Adobe I/O-projekt](./ex6.md){target="_blank"}

Gå tillbaka till [Komma igång](./getting-started.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../overview.md){target="_blank"}