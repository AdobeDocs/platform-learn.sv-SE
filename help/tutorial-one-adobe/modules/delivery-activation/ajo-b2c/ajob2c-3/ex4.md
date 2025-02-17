---
title: Offer Decisioning - Testa ditt beslut med demowebbplatsen
description: Testa ditt beslut med demowebbplatsen
kt: 5342
doc-type: tutorial
exl-id: ecfcdcc7-fc26-48f7-b3f8-6e97f8e1eee3
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 0%

---

# 3.3.4 Kombinera Adobe Target och Offer Decisioning

## 3.3.4.1 Samla in länken till ditt demoprojekt

För att kunna läsa in demonstrationswebbplatsprojektet i Adobe Target måste du först samla in en speciell länk som gör att Adobe Target kan läsa in ditt projekt för demowebbplatser.

Gå till [https://dsn.adobe.com/projects](https://builder.adobedemo.com/projects) om du vill göra det. När du har loggat in med din Adobe ID ser du det här. Klicka på webbplatsprojektet för att öppna det.

![RTCDP](./images/builder1.png)

Du kommer att se det här. Gå till **Dela**. Klicka på **Skapa länk** och kopiera sedan länken till Urklipp.

![RTCDP](./images/builder2.png)

Gå till [https://bitly.com](https://bitly.com), klistra in länken som du kopierade och klicka på **Skapa länken**.

![RTCDP](./images/builder4.png)

Du får nu en förkortad länk som ser ut så här: `https://adobe.ly/3PpGcFk`. Du kommer att behöva den länken i nästa övning.

![RTCDP](./images/builder5.png)

## 3.3.4.2 Samla in

Gå till Adobe Experience Cloud hemsida på [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/). Klicka på **Mål**.

![RTCDP](./../../../../modules/delivery-activation/rtcdp-b2c/rtcdpb2c-3/images/excl.png)

På startsidan för **Adobe Target** visas alla befintliga aktiviteter. Klicka på **Skapa aktivitet** och sedan på **Upplevelsemål**.

![RTCDP](./../../../../modules/delivery-activation/rtcdp-b2c/rtcdpb2c-3/images/exclatov.png)

Välj **Visuell** och klistra in den förkortade länken i fältet **Ange aktivitets-URL**. Klicka på **Skapa**.

![RTCDP](./images/exclatcrxt1.png)

Du kommer då att se hur ditt demonstrationswebbplatsprojekt läses in i Visuel Experience Composer.

>[!NOTE]
>
>Om webbplatsen inte läses in korrekt installerar och aktiverar du det här Chrome-tillägget: **Adobe Target VEC Helper** från Chrome Web Store och försöker sedan igen.

![RTCDP](./images/vec1.png)

Klicka på det område som innehåller Disney+-erbjudandet. Se till att du väljer den fullständiga **behållaren**. Klicka på **Infoga före** och välj sedan **Erbjudandebeslut**.

![RTCDP](./images/vec3.png)

Du kommer då att se den här popup-rutan. Markera sandlådan `--aepSandboxName--` och välj sedan placeringen **Webb - bild**.

![RTCDP](./images/vec4.png)

Välj sedan ditt beslut `--aepUserLdap-- - CitiSignal Decision`. Klicka på **Spara**.

![RTCDP](./images/vec5.png)

Då ser du det här. Klicka på **Granskningsregel**.

![RTCDP](./images/vec5a.png)

Kontrollera att den extra mallregeln **URL** **innehåller** **ditt-project-name**. Klicka på **Spara**.

![RTCDP](./images/vec6.png)

Då ser du det här. Klicka på **Nästa**.

![RTCDP](./images/vec7.png)

Ange ett namn för erbjudandet. Använd det här namnet: `--aepUserLdap-- - XT with Offers (VEC)`. Klicka på **Nästa**.

![RTCDP](./images/vec8.png)

Då ser du det här. Definiera **målmåttet** enligt vad som anges. Klicka på **Spara och stäng**.

![RTCDP](./images/vec9.png)

Erbjudandet har skapats och publiceras. När erbjudandet har publicerats kan du aktivera det.

![RTCDP](./images/vec11.png)

## Nästa steg

Gå till [3.3.5 Använd ditt beslut i ett e-postmeddelande och SMS](./ex5.md){target="_blank"}

Gå tillbaka till [Offer Decisioning](offer-decisioning.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../../overview.md){target="_blank"}
