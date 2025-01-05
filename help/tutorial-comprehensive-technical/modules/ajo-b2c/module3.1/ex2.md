---
title: Journey Optimizer - Skapa dina fragment
description: Journey Optimizer - Skapa dina fragment
kt: 5342
doc-type: tutorial
exl-id: 81810b3a-7eca-436f-a5dc-48c46cb33980
source-git-commit: 9865b5697abe2d344fb530636a1afc3f152a9e8f
workflow-type: tm+mt
source-wordcount: '1056'
ht-degree: 0%

---

# 3.1.2 Skapa fragment som ska användas i ditt meddelande

I den här övningen ska du konfigurera 2 fragment, 1 för ett återanvändbart sidhuvud och 1 för en återanvändbar sidfot.

Logga in på Adobe Journey Optimizer på [Adobe Experience Cloud](https://experience.adobe.com). Klicka på **Journey Optimizer**.

![ACOP](./images/acophome.png)

Du omdirigeras till vyn **Hem** i Journey Optimizer. Kontrollera först att du använder rätt sandlåda. Sandlådan som ska användas kallas `--aepSandboxName--`.

![ACOP](./images/acoptriglp.png)

## 3.1.2.1 Skapa rubrikfragment

Klicka på **Fragment** på den vänstra menyn. Ett fragment är en återanvändbar komponent i Journey Optimizer, som undviker dubbletter och underlättar framtida ändringar som påverkar alla meddelanden, till exempel ändringar i ett sidhuvud eller en sidfot i ett e-postmeddelande.

Klicka på **Skapa fragment**.

![ACOP](./images/fragm1.png)

Ange namnet `--aepUserLdap-- - CitiSignal - Header` och välj **Typ: Visual Fragment**. Klicka på **Skapa**.

![ACOP](./images/fragm2.png)

Då ser du det här. På den vänstra menyn hittar du de strukturkomponenter som du kan använda för att definiera e-postmeddelandets struktur (rader och kolumner).

Dra och släpp en **1:1-kolumn** från menyn på arbetsytan. Detta blir platshållare för logotypbilden.

![Journey Optimizer](./images/fragm3.png)

Sedan kan du använda Innehållskomponenter för att lägga till innehåll i dessa block. Dra och släpp en **bild**-komponent i den första cellen på den första raden. Klicka på **Bläddra**.

![Journey Optimizer](./images/fragm4.png)

Då visas ett popup-fönster där du ser AEM Assets Media Library. Gå till mappen **citi-signal-images**, klicka för att markera bilden **CitiSignal-Logo-White.png** och klicka på **Välj**.

>[!NOTE]
>
>Om du inte ser Citi Signal-bilderna i ditt AEM Assets-bibliotek hittar du dem [här](../../../assets/ajo/CitiSignal-images.zip). Hämta dem till skrivbordet, skapa mappen **citi-signal-images** och överför alla bilder i mappen.

![Journey Optimizer](./images/fragm5.png)

Då ser du det här. Bilden är vit och visas inte än. Nu bör du definiera en bakgrundsfärg så att bilden visas korrekt. Klicka på **Stilar** och sedan på rutan **Bakgrundsfärg** .

![Journey Optimizer](./images/fragm6.png)

Ändra färgkoden **Hex** till **#8821F4** på popup-menyn och ändra sedan fokus genom att klicka i fältet **100%** . Sedan ser du den nya färgen som används på bilden.

![Journey Optimizer](./images/fragm7.png)

Bilden är också lite för stor just nu. Vi ändrar bredden genom att skjuta **Breddväxlaren** till **40%**.

![Journey Optimizer](./images/fragm8.png)

Ditt rubrikfragment är nu klart. Klicka på **Spara** och sedan på pilen för att gå tillbaka till föregående skärm.

![Journey Optimizer](./images/fragm9.png)

Ditt fragment måste publiceras innan det kan användas. Klicka på **Publish**.

![Journey Optimizer](./images/fragm10.png)

Efter några minuter ser du att ditt fragments status har ändrats till **Live**.
Sedan bör du skapa ett nytt fragment för sidfoten i dina e-postmeddelanden. Klicka på **Skapa fragment**.

![Journey Optimizer](./images/fragm11.png)

## 3.1.2.2 Skapa sidfotsavsnittet

Klicka på **Skapa fragment**.

![Journey Optimizer](./images/fragm11.png)

Ange namnet `--aepUserLdap-- - CitiSignal - Footer` och välj **Typ: Visual Fragment**. Klicka på **Skapa**.

![Journey Optimizer](./images/fragm12.png)

Då ser du det här. På den vänstra menyn hittar du de strukturkomponenter som du kan använda för att definiera e-postmeddelandets struktur (rader och kolumner).

Dra och släpp en **1:1-kolumn** från menyn på arbetsytan. Det här blir platshållare för sidfotsinnehållet.

![Journey Optimizer](./images/fragm13.png)

Sedan kan du använda Innehållskomponenter för att lägga till innehåll i dessa block. Dra och släpp en **HTML** -komponent i den första cellen på den första raden. Klicka på komponenten för att markera den och klicka sedan på ikonen **&lt;/>** för att redigera HTML-källkoden.

![Journey Optimizer](./images/fragm14.png)

Då ser du det här.

![Journey Optimizer](./images/fragm15.png)

Kopiera kodfragmentet nedan och klistra in det i fönstret **Redigera HTML** i Journey Optimizer.

```html
<!--[if mso]><table cellpadding="0" cellspacing="0" border="0" width="100%"><tr><td style="text-align: center;" ><![endif]-->
<table style="width: auto; display: inline-block;">
  <tbody>
    <tr class="component-social-container">
      <td style="padding: 5px">
        <a style="text-decoration: none;" href="https://www.facebook.com" data-component-social-icon-id="facebook">
        
        </a>
      </td>
      <td style="padding: 5px">
        <a style="text-decoration: none;" href="https://x.com" data-component-social-icon-id="twitter">
        
        </a>
      </td>
      <td style="padding: 5px">
        <a style="text-decoration: none;" href="https://www.instagram.com" data-component-social-icon-id="instagram">
         
        </a>
      </td>
    </tr>
  </tbody>
</table>
<!--[if mso]></td></tr></table><![endif]-->
```

Du får den här då. På raderna 7, 12 och 17 måste du nu infoga en bildfil med hjälp av resurserna i ditt AEM Assets-bibliotek.

![Journey Optimizer](./images/fragm16.png)

Se till att markören är placerad på rad 7 och klicka sedan på **Assets** i den vänstra menyn. Klicka på **Öppna resursväljaren** för att välja bilden.

![Journey Optimizer](./images/fragm17.png)

Öppna mappen **citi-signal-images** och klicka för att välja bilden **Icon_Facebook.png**. Klicka på **Markera**.

![Journey Optimizer](./images/fragm18.png)

Se till att markören är placerad på rad 12 och klicka sedan på **Öppna resursväljaren** för att markera bilden.

![Journey Optimizer](./images/fragm19.png)

Öppna mappen **citi-signal-images** och klicka för att välja bilden **Icon_X.png**. Klicka på **Markera**.

![Journey Optimizer](./images/fragm20.png)

Se till att markören är placerad på rad 17 och klicka sedan på **Öppna resursväljaren** för att markera bilden.

![Journey Optimizer](./images/fragm21.png)

Öppna mappen **citi-signal-images** och klicka för att välja bilden **Icon_Instagram.png**. Klicka på **Markera**.

![Journey Optimizer](./images/fragm22.png)

Då ser du det här. Klicka på **Spara**.

![Journey Optimizer](./images/fragm23.png)

Du kommer då tillbaka i redigeraren. Dina ikoner är inte synliga än eftersom bakgrunden och bildfilerna är helt vita. Om du vill ändra bakgrundsfärgen går du till **Stilar** och klickar i kryssrutan **Bakgrundsfärg** .

![Journey Optimizer](./images/fragm24.png)

Ändra färgkoden **Hex** till **#00000**.

![Journey Optimizer](./images/fragm25.png)

Ändra justeringen till centrerad.

![Journey Optimizer](./images/fragm26.png)

Låt oss lägga till några andra delar till sidfoten. Dra och släpp en **bild**-komponent ovanför HTML-komponenten som du just skapade. Klicka på **Bläddra**.

![Journey Optimizer](./images/fragm27.png)

Klicka för att markera bildfilen **`CitiSignal_Footer_Logo.png`** och klicka på **Välj**.

![Journey Optimizer](./images/fragm28.png)

Gå till **Stilar** och klicka i kryssrutan **Bakgrundsfärg** så ändrar vi den till svart igen. Ändra färgkoden **Hex** till **#00000**.

![Journey Optimizer](./images/fragm29.png)

Ändra bredden till **20%** och kontrollera att justeringen är inställd på centrering.

![Journey Optimizer](./images/fragm30.png)

Dra och släpp en **Text** -komponent under den HTML-komponent som du skapade. Klicka på **Bläddra**.

![Journey Optimizer](./images/fragm31.png)

Kopiera och klistra in texten nedan genom att ersätta platshållartexten.

```
1234 N. South Street, Anywhere, US 12345

Unsubscribe

©2024 CitiSignal, Inc and its affiliates. All rights reserved.
```

Ange att **textjusteringen** ska centreras.

![Journey Optimizer](./images/fragm32.png)

Ändra **teckenfärgen** till vit, **#FFFFFF**.

![Journey Optimizer](./images/fragm33.png)

Ändra **bakgrundsfärgen** till svart, **#00000**.

![Journey Optimizer](./images/fragm34.png)

Markera texten **Avsluta prenumeration** i sidfoten och klicka på ikonen **Länk** i menyraden. Ange **Type** till **External Opt-out/Unsubscription** och ange URL:en till **https://aepdemo.net/unsubscribe.html** (det får inte finnas en tom URL för länken för att avbryta prenumerationen).

![Journey Optimizer](./images/fragm35.png)

Du får den här då. Sidfoten är nu klar. Klicka på **Spara** och sedan på pilen för att gå tillbaka till föregående sida.

![Journey Optimizer](./images/fragm36.png)

Klicka på **Publish** om du vill publicera sidfoten så att den kan användas i ett e-postmeddelande.

![Journey Optimizer](./images/fragm37.png)

Efter några minuter ser du att sidfotens status har ändrats till **Live**.

![Journey Optimizer](./images/fragm38.png)

Du har nu avslutat den här övningen.

Nästa steg: [3.1.3 Skapa din resa och ditt e-postmeddelande](./ex3.md)

[Gå tillbaka till modul 3.1](./journey-orchestration-create-account.md)

[Gå tillbaka till Alla moduler](../../../overview.md)
