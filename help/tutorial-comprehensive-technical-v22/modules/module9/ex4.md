---
title: offer decisioning - Testa ditt beslut med demowebbplatsen
description: Testa ditt beslut med demowebbplatsen
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: cdb2ba7d-bfc3-43ce-b9a1-1f0866322589
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 2%

---

# 9.4 Kombinera Adobe Target och Offer decisioning

## 9.4.1 Samla in länken till ditt demoprojekt

För att kunna läsa in demonstrationswebbplatsprojektet i Adobe Target måste du först samla in en speciell länk som gör att Adobe Target kan läsa in ditt projekt för demowebbplatser.

Om du vill göra det går du till [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). När du har loggat in med din Adobe ID ser du det här. Klicka på webbplatsprojektet för att öppna det.

![RTCDP](./images/builder1.png)

Du kommer att se det här. Klicka **Dela**.

![RTCDP](./images/builder2.png)

Klicka **Generera länk** och sedan kopiera länken till Urklipp.

![RTCDP](./images/builder3.png)

Gå till [https://bitly.com](https://bitly.com), klistra in länken som du kopierade och klicka på **Korta**. Nu får du en förkortad länk som ser ut så här: `https://bit.ly/3JxN7aG`. Du kommer att behöva den länken i nästa övning.

![RTCDP](./images/builder4.png)

## 9.4.2 Samla in

Gå nu till Adobe Experience Cloud hemsida genom att gå till [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/). Klicka **Mål**.

![RTCDP](../module6/images/excl.png)

På **Adobe Target** på startsidan ser du alla befintliga aktiviteter.

![RTCDP](../module6/images/exclatov.png)

Klicka **+ Skapa aktivitet** för att skapa en ny aktivitet.

![RTCDP](../module6/images/exclatcr.png)

Välj **Experience Targeting**.

![RTCDP](./images/exclatcrxt.png)

Välj nu **Visual** och klistra in den förkortade länken i fältet **Ange aktivitets-URL**. Klicka på **Nästa**.

![RTCDP](./images/exclatcrxt1.png)

Du kommer då att se hur ditt demonstrationswebbplatsprojekt läses in i Visuel Experience Composer.

![RTCDP](./images/vec1.png)

Gå till **Bläddra** läge för att klicka **Tillåt alla** på popup-fönstret för cookie-samtycke.

![RTCDP](./images/vec2.png)

Klicka på området som innehåller texten **Kategorier**. Klicka **Infoga före** och sedan markera **Erbjudandebeslut**.

![RTCDP](./images/vec3.png)

Du kommer då att se den här popup-rutan. Välj din sandlåda `--aepSandboxId--` och välj sedan placering **Webb - bild**.

![RTCDP](./images/vec4.png)

Välj sedan ditt beslut `--demoProfileLdap-- - Luma Decision`. Klicka **Spara**.

![RTCDP](./images/vec5.png)

Du kommer då att se det här. Se till att lägga till en extra mallregel **URL** **innehåller** **ditt projektnamn**. CLick **Spara**.

![RTCDP](./images/vec6.png)

Du kommer då att se det här. Klicka på **Nästa**.

![RTCDP](./images/vec7.png)

Ange ett namn för erbjudandet. Använd det här namnet: `--demoProfileLdap-- - XT with Offers (VEC)`. Klicka på **Nästa**.

![RTCDP](./images/vec8.png)

Du kommer då att se det här. Definiera **Målmått** enligt vad som anges. Klicka **Spara och stäng**.

![RTCDP](./images/vec9.png)

Erbjudandet har skapats och publiceras.

![RTCDP](./images/vec10.png)

När erbjudandet har publicerats kan du aktivera det.

Nästa steg: [9.5 Använd ditt beslut i ett e-postmeddelande och i ett sms](./ex5.md)

[Gå tillbaka till modul 9](./offer-decisioning.md)

[Gå tillbaka till Alla moduler](./../../overview.md)
