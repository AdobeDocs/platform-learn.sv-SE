---
title: Firefly API för anpassade modeller
description: Arbeta med Firefly API för anpassade modeller
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 330f4492-d0df-4298-9edc-4174b0065c9a
source-git-commit: b083a817700320e8e45645702c2868423c1fae99
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 0%

---

# 1.1.4 API för anpassade Firefly-modeller

## 1.1.4.1 Konfigurera din anpassade modell

Gå till [https://firefly.adobe.com/](https://firefly.adobe.com/). Klicka på **Egna modeller**.

![Anpassade Firefly-modeller](./images/ffcm1.png){zoomable="yes"}

Du kanske ser det här meddelandet. Om du gör det klickar du på **Godkänn** för att fortsätta.

![Anpassade Firefly-modeller](./images/ffcm2.png){zoomable="yes"}

Du borde se det här då. Klicka på **Utbilda en modell**.

![Anpassade Firefly-modeller](./images/ffcm3.png){zoomable="yes"}

Konfigurera följande fält:

- **Namn**: använd `--aepUserLdap-- - Citi Signal Router Model`
- **Utbildningsläge**: välj **Ämne (förhandsversion av tekniker)**
- **Koncept**: ange `router`
- **Spara i**: öppna listrutan och klicka på **+ Skapa nytt projekt**

![Anpassade Firefly-modeller](./images/ffcm4.png){zoomable="yes"}

Ge det nya projektet ett namn: `--aepUserLdap-- - Custom Models`. Klicka på **Skapa**.

![Anpassade Firefly-modeller](./images/ffcm5.png){zoomable="yes"}

Du borde se det här då. Klicka på **Skapa**.

![Anpassade Firefly-modeller](./images/ffcm6.png){zoomable="yes"}

Du måste nu ange referensbilderna för den anpassade modellen som ska tränas. Klicka på **Välj bilder från datorn**.

![Anpassade Firefly-modeller](./images/ffcm7.png){zoomable="yes"}

Hämta referensbilderna [här](https://tech-insiders.s3.us-west-2.amazonaws.com/CitiSignal_router.zip). Zippa upp den nedladdade filen så får du den här.

![Anpassade Firefly-modeller](./images/ffcm8.png){zoomable="yes"}

Navigera till mappen som innehåller de hämtade bildfilerna. Markera alla och klicka på **Öppna**.

![Anpassade Firefly-modeller](./images/ffcm9.png){zoomable="yes"}

Då ser du att bilderna läses in.

![Anpassade Firefly-modeller](./images/ffcm10.png){zoomable="yes"}

Efter några minuter läses bilderna in korrekt. Det kan bero på att bildtexten inte har genererats eller att bildtexten inte är tillräckligt lång. Granska varje bild med ett fel och ange en bildtext som uppfyller kraven och beskriver bilden.

![Anpassade Firefly-modeller](./images/ffcm11.png){zoomable="yes"}

När alla bilder har bildtexter som uppfyller kraven måste du ändå ange en exempelfråga. Ange en uppmaning som använder ordet router. När du har gjort det kan du börja utbilda din modell. Klicka på **Tåg**.

![Anpassade Firefly-modeller](./images/ffcm12.png){zoomable="yes"}

Då ser du det här. Det kan ta 20-30 minuter eller längre att utbilda modellen.

![Anpassade Firefly-modeller](./images/ffcm13.png){zoomable="yes"}

Efter 20-30 minuter har din modell utbildats och kan publiceras. Klicka på **Publicera**.

![Anpassade Firefly-modeller](./images/ffcm14.png){zoomable="yes"}

Klicka på **Publicera** igen.

![Anpassade Firefly-modeller](./images/ffcm15.png){zoomable="yes"}

Stäng popup-fönstret **Dela anpassad modell**.

![Anpassade Firefly-modeller](./images/ffcm16.png){zoomable="yes"}

## 1.1.4.2 Använda din anpassade modell i användargränssnittet

Gå till [https://firefly.adobe.com/cme/train](https://firefly.adobe.com/cme/train). Klicka på din anpassade modell för att öppna den.

![Anpassade Firefly-modeller](./images/ffcm19.png){zoomable="yes"}

Klicka på **Förhandsgranska och testa**.

![Anpassade Firefly-modeller](./images/ffcm17.png){zoomable="yes"}

Du kommer då att se exempelmeddelandet som du angav innan du kördes.

![Anpassade Firefly-modeller](./images/ffcm18.png){zoomable="yes"}

## 1.1.4.3 Aktivera din anpassade modell för API:t för anpassade Firefly-tjänster

När din anpassade modell har tränats kan den också användas via API:t. I övning 1.1.1 har du redan konfigurerat ditt Adobe I/O-projekt för interaktion med Firefly Services via API:t.

Gå till [https://firefly.adobe.com/cme/train](https://firefly.adobe.com/cme/train). Klicka på din anpassade modell för att öppna den.

![Anpassade Firefly-modeller](./images/ffcm19.png){zoomable="yes"}

Klicka på de tre punkterna **..** och sedan på **Dela**.

![Anpassade Firefly-modeller](./images/ffcm20.png){zoomable="yes"}

Om du vill komma åt en anpassad Firefly-modell måste den anpassade modellen delas med **ID:t för tekniskt konto** i Adobe I/O-projektet.

Gå till [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects) om du vill hämta ditt **tekniska konto-ID**. Klicka för att öppna projektet med namnet `--aepUserLdap-- Firefly`.

![Anpassade Firefly-modeller](./images/ffcm24.png){zoomable="yes"}

Klicka på **OAuth Server-to-Server**.

![Anpassade Firefly-modeller](./images/ffcm25.png){zoomable="yes"}

Klicka för att kopiera ditt **tekniska konto-ID**.

![Anpassade Firefly-modeller](./images/ffcm23.png){zoomable="yes"}

Klistra in ditt **tekniska konto-ID** och klicka på **Bjud in för redigering**.

![Anpassade Firefly-modeller](./images/ffcm21.png){zoomable="yes"}

**ID:t för det tekniska kontot** bör nu kunna komma åt den anpassade modellen.

![Anpassade Firefly-modeller](./images/ffcm22.png){zoomable="yes"}

## 1.1.4.4 Interaktion med Firefly Services API för anpassade modeller

I Exercise 1.1.1 Komma igång med Firefly Services hämtade du den här filen: [postman-ff.zip](./../../../assets/postman/postman-ff.zip) till ditt lokala skrivbord och du importerade sedan samlingen i Postman.

Öppna Postman och gå till mappen **FF - API för anpassade modeller**.

![Anpassade Firefly-modeller](./images/ffcm30.png){zoomable="yes"}

Öppna förfrågan **1. FF - getCustomModels** och klicka på **Skicka**.

![Anpassade Firefly-modeller](./images/ffcm31.png){zoomable="yes"}

Du bör se den anpassade modell som du skapade tidigare, med namnet `--aepUserLdap-- - Citi Signal Router Model`, som en del av svaret. Fältet **assetId** är den unika identifieraren för din anpassade modell, som kommer att refereras i nästa begäran.

![Anpassade Firefly-modeller](./images/ffcm32.png){zoomable="yes"}

Öppna förfrågan **2. Generera bilder asynkront**. I det här exemplet begär du två variationer som ska genereras baserat på din anpassade modell. Du kan uppdatera uppmaningen som i det här fallet är `a white router on a volcano in Africa`.

Klicka på **Skicka**.

![Anpassade Firefly-modeller](./images/ffcm33.png){zoomable="yes"}

Svaret innehåller fältet **jobId**. Jobbet för att generera dessa två bilder körs nu och du kan kontrollera statusen genom att använda nästa begäran.

![Anpassade Firefly-modeller](./images/ffcm34.png){zoomable="yes"}

Öppna förfrågan **3. Hämta CM-status** och klicka på **Skicka**. Du bör då se att statusen är inställd på att köras.

![Anpassade Firefly-modeller](./images/ffcm35.png){zoomable="yes"}

Efter några minuter klickar du på **Skicka** igen för begäran **3. Hämta CM-status**. Du bör då se att statusen har ändrats till **Succas** och du bör se två bild-URL:er som en del av utdata. Klicka för att öppna båda filerna.

![Anpassade Firefly-modeller](./images/ffcm36.png){zoomable="yes"}

Detta är den första bilden som genererades i det här exemplet.

![Anpassade Firefly-modeller](./images/ffcm37.png){zoomable="yes"}

Detta är den andra bilden som genererades i det här exemplet.

![Anpassade Firefly-modeller](./images/ffcm38.png){zoomable="yes"}

Du har nu avslutat den här övningen.

## Nästa steg

Gå till [Sammanfattning och förmåner](./summary.md){target="_blank"}

Gå tillbaka till [Arbeta med Photoshop API:er](./ex3.md){target="_blank"}

Gå tillbaka till [Översikt över Adobe Firefly Services](./firefly-services.md){target="_blank"}
