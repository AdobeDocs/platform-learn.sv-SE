---
title: Skapa en kampanj med AJO Translation Services
description: Skapa en kampanj med AJO Translation Services
kt: 5342
doc-type: tutorial
source-git-commit: 3b3c62499bfed86ab13a657a816424879cab4f42
workflow-type: tm+mt
source-wordcount: '1644'
ht-degree: 0%

---

# 3.2.2 Skapa en kampanj

Gå till [https://experience.adobe.com/](https://experience.adobe.com/). Klicka på **Journey Optimizer**.

![Översättningar](./images/ajolp1.png)

Du omdirigeras till vyn **Hem** i Journey Optimizer. Kontrollera först att du använder rätt sandlåda. Sandlådan som ska användas kallas `--aepSandboxName--`.

![ACOP](./images/ajolp2.png)

## 3.2.2.1 Skapa rubrikfragment

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

## 3.2.2.2 Skapa sidfotsavsnittet

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

## 3.2.2.3 Skapa fiberresa

Nu ska du skapa en resa. Till skillnad från händelsebaserade resor som bygger på inkommande upplevelsehändelser, fokuserar den här resan på att läsa en befintlig målgrupp och riktar sig till en hel målgrupp en gång med unikt innehåll som nyhetsbrev, engångskampanjer eller specifika kampanjer.

Gå till **Resor** på menyn och klicka på **Skapa resa**.

![Journey Optimizer](./images/campaign1.png)

Ange **Namn** till `--aepUserLdap-- - Fiber` på skärmen där resan skapas. Klicka på **Spara**.

![Journey Optimizer](./images/campaign2.png)

Dra och släpp objektet **Läs målgrupp** på arbetsytan på menyn **Orchestration** .

![Journey Optimizer](./images/campaign2a.png)

Klicka på ikonen **redigera** för att välja en målgrupp.

![Journey Optimizer](./images/campaign2b.png)

För **målgruppen** väljer du målgruppen som du skapade i föregående steg, `--aepUserLdap-- - CitiSignal Eligible for Fiber`. Klicka på **Spara**.

![Journey Optimizer](./images/campaign2c.png)

Du borde se det här då. Ange **Namespace** som **Email**. Klicka på **Spara**.

![Journey Optimizer](./images/campaign3.png)

Under **Åtgärder** drar och släpper du åtgärden **E-post** på arbetsytan.

![Journey Optimizer](./images/campaign4.png)

Ange **kategori** som **marknadsföring** och välj en **konfiguration** för **e-post**. Klicka på **Redigera innehåll**.

![Journey Optimizer](./images/campaign5.png)

Då ser du det här. Klicka på ikonen **redigera** bredvid **Ämnesraden**.

![Journey Optimizer](./images/campaign6.png)

Ställ in ämnesraden på:

```
{{profile.person.name.firstName}}, here's your Fiber offer!
```

Klicka på **Spara**.

![Journey Optimizer](./images/campaign5a.png)

Du borde se det här då. Klicka sedan på **Redigera e-postbrödtext**.

![Journey Optimizer](./images/campaign5b.png)

Välj **Design från grunden**.

![Journey Optimizer](./images/campaign7.png)

Då ser du det här. På den vänstra menyn hittar du de strukturkomponenter som du kan använda för att definiera e-postmeddelandets struktur (rader och kolumner).

Dra och släpp två gånger en **1:1-kolumn** på arbetsytan, vilket bör ge dig den här strukturen:

![Journey Optimizer](./images/campaign8.png)

Gå till **Fragment** på den vänstra menyn. Dra sidhuvudet du skapade tidigare till den första komponenten på arbetsytan. Dra sidfoten som du skapade tidigare till den sista komponenten på arbetsytan.

![Journey Optimizer](./images/campaign9.png)

Klicka på ikonen **+** i den vänstra menyn. Gå till **Innehåll** för att börja lägga till innehåll på arbetsytan.

![Journey Optimizer](./images/campaign10.png)

Dra och släpp en **Text**-komponent på den andra raden.

![Journey Optimizer](./images/campaign11.png)

Markera standardtexten i komponenten **Skriv texten här.** och ersätt den med texten nedan. Ändra justeringen till **Centrera**.

```javascript
Hi {{profile.person.name.firstName}}

As a CitiSignal member, you're part of a dynamic community that's constantly evolving to meet your needs. We're committed to delivering innovative solutions that enhance your digital lifestyle and keep you ahead of the curve.

Stay connected.
```

![Journey Optimizer](./images/campaign12.png)

Dra och släpp en **bild**-komponent på den tredje och fjärde raden. Klicka på **Bläddra** på den tredje raden.

![Journey Optimizer](./images/campaign13.png)

Öppna mappen **citi-signal-images**, klicka för att markera bilden **Offer_AirPods.jpg** och klicka på **Select**.

![Journey Optimizer](./images/campaign14.png)

Klicka på **Bläddra** på bildplatshållaren på den fjärde raden.

![Journey Optimizer](./images/campaign15.png)

Öppna mappen **citi-signal-images**, klicka för att markera bilden **Offer_Phone.jpg** och klicka på **Select**.

![Journey Optimizer](./images/campaign16.png)

Dra och släpp en **Text** -komponent på den tredje och fjärde raden.

![Journey Optimizer](./images/campaign17.png)

Markera standardtexten i komponenten på den tredje raden **Skriv texten här.** och ersätt den med texten nedan.

```javascript
Get AirPods for free:

Experience seamless connectivity like never before with CitiSignal. Sign up for select premium plans and receive a complimentary pair of Apple AirPods. Stay connected in style with our unbeatable offer.
```

Markera standardtexten i komponenten på den fjärde raden **Skriv texten här.** och ersätt den med texten nedan.

```javascript
We'll pay off your phone:

Make the switch to CitiSignal and say goodbye to phone payments! Switching to CitiSignal has never been more rewarding. Say farewell to hefty phone bills as we help pay off your phone, up to 800$!
```

![Journey Optimizer](./images/campaign18.png)

Ditt enkla nyhetsbrev är nu klart. Klicka på **Spara**.

Gå tillbaka till kontrollpanelen för kampanjer genom att klicka på **pilen** bredvid texten för ämnesraden i det övre vänstra hörnet.

![Journey Optimizer](./images/campaign19.png)

Klicka på **Granska för att aktivera**.

![Journey Optimizer](./images/campaign20.png)

Du kan då få det här felet. Om så är fallet kan du behöva vänta i upp till 24 timmar tills målgruppen har utvärderats och sedan försöka aktivera kampanjen igen. Du kan också behöva uppdatera schemat för din kampanj så att den körs vid ett senare tillfälle.

Klicka på **Aktivera**.

![Journey Optimizer](./images/campaign21.png)

När kampanjen är aktiverad kommer den att köras.

![Journey Optimizer](./images/campaign22.png)

Din kampanj är nu aktiverad. E-postmeddelandet med nyhetsbrevet skickas så som du har definierat det i ditt schema, och kampanjen stoppas så snart som det senaste e-postmeddelandet har skickats.

Du bör också få e-postadressen till den demoprofil du skapade tidigare.

![Journey Optimizer](./images/campaign23.png)

Du har gjort klart den här övningen.

## Nästa steg

Gå till [3.2.3 ...](./ex3.md)

Gå tillbaka till [Modul 3.2](./ajotranslationsvcs.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../overview.md){target="_blank"}
