---
title: Offer decisioning - Testa ditt beslut med demowebbplatsen
description: Testa ditt beslut med demowebbplatsen
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 0%

---

# 3.3.4 Kombinera Adobe Target och Offer decisioning

## 3.3.4.1 Samla in länken till ditt demoprojekt

För att kunna läsa in demonstrationswebbplatsprojektet i Adobe Target måste du först samla in en speciell länk som gör att Adobe Target kan läsa in ditt projekt för demowebbplatser.

Gå till [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects) om du vill göra det. När du har loggat in med din Adobe ID ser du det här. Klicka på webbplatsprojektet för att öppna det.

![RTCDP](./images/builder1.png)

Du kommer att se det här. Klicka på **Dela**.

![RTCDP](./images/builder2.png)

Klicka på **Skapa länk** och kopiera sedan länken till Urklipp.

![RTCDP](./images/builder3.png)

Gå till [https://bitly.com](https://bitly.com), klistra in länken som du kopierade och klicka på **Förkorta**. Du får nu en förkortad länk som ser ut så här: `https://bit.ly/3JxN7aG`. Du kommer att behöva den länken i nästa övning.

![RTCDP](./images/builder4.png)

## 3.3.4.2 Samla in

Gå till Adobe Experience Cloud hemsida på [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/). Klicka på **Mål**.

![RTCDP](./../../../modules/rtcdp-b2c/module2.3/images/excl.png)

På startsidan för **Adobe Target** visas alla befintliga aktiviteter.

![RTCDP](./../../../modules/rtcdp-b2c/module2.3/images/exclatov.png)

Klicka på **+ Skapa aktivitet** för att skapa en ny aktivitet.

![RTCDP](./../../../modules/rtcdp-b2c/module2.3/images/exclatcr.png)

Välj **Experience Targeting**.

![RTCDP](./images/exclatcrxt.png)

Välj **Visuell** och klistra in den förkortade länken i fältet **Ange aktivitets-URL**. Klicka på **Nästa**.

![RTCDP](./images/exclatcrxt1.png)

Du kommer då att se hur ditt demonstrationswebbplatsprojekt läses in i Visuel Experience Composer.

![RTCDP](./images/vec1.png)

Gå till **bläddringsläget** och klicka på **Tillåt alla** på popup-fönstret för cookie-samtycke.

![RTCDP](./images/vec2.png)

Klicka i området som innehåller texten **Aktuella kategorier**. Klicka på **Infoga före** och välj sedan **Erbjudandebeslut**.

![RTCDP](./images/vec3.png)

Du kommer då att se den här popup-rutan. Markera sandlådan `--aepSandboxName--` och välj sedan placeringen **Webb - bild**.

![RTCDP](./images/vec4.png)

Välj sedan ditt beslut `--aepUserLdap-- - Luma Decision`. Klicka på **Spara**.

![RTCDP](./images/vec5.png)

Då ser du det här. Kontrollera att den extra mallregeln **URL** **innehåller** **ditt-project-name**. Klicka på **Spara**.

![RTCDP](./images/vec6.png)

Då ser du det här. Klicka på **Nästa**.

![RTCDP](./images/vec7.png)

Ange ett namn för erbjudandet. Använd det här namnet: `--aepUserLdap-- - XT with Offers (VEC)`. Klicka på **Nästa**.

![RTCDP](./images/vec8.png)

Då ser du det här. Definiera **målmåttet** enligt vad som anges. Klicka på **Spara och stäng**.

![RTCDP](./images/vec9.png)

Erbjudandet har skapats och publiceras.

![RTCDP](./images/vec10.png)

När erbjudandet har publicerats kan du aktivera det.

Nästa steg: [3.3.5 Använd ditt beslut i ett e-postmeddelande och SMS](./ex5.md)

[Gå tillbaka till modul 3.3](./offer-decisioning.md)

[Gå tillbaka till Alla moduler](./../../../overview.md)
