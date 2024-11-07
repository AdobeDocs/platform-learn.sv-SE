---
title: Adobe Journey Optimizer - Använd personalisering i ett e-postmeddelande
description: Den här övningen förklarar hur du använder segmentpersonalisering i ett e-postinnehåll
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 0%

---

# 3.4.3 Använda personalisering i ett e-postmeddelande

Logga in på Adobe Experience Cloud på [Adobe Experience Cloud](https://experience.adobe.com). Klicka på **Adobe Journey Optimizer**.

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acophome.png)

Du omdirigeras till vyn **Hem** i Journey Optimizer. Innan du fortsätter måste du välja en **sandlåda**. Sandlådan som ska markeras har namnet ``--aepTenantId--``. Du kan göra detta genom att klicka på texten **[!UICONTROL Production Prod]** i den blå raden ovanför skärmen.

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acoptriglp.png)

## 3.4.3.1 Segmentbaserad personalisering

I den här övningen kommer du att förbättra ditt nyhetsbrev via e-post med en personlig text baserad på segmentmedlemskap.

Gå till **Resor**. Hitta den nyhetsbrevsresa du har skapat i föregående övning. Sök efter `--aepUserLdap-- - Newsletter`. Klicka på resan för att öppna den.

![Journey Optimizer](./images/sbp1.png)

Då ser du det här. Klicka på **Duplicera**.

![Journey Optimizer](./images/sbp2.png)

Klicka på **Duplicera**.

![Journey Optimizer](./images/sbp3.png)

Välj åtgärden **E-post** och klicka på **Redigera innehåll**.

![Journey Optimizer](./images/sbp3a.png)

Klicka på **E-posta Designer**.

![Journey Optimizer](./images/sbp4.png)

Då ser du det här.

![Journey Optimizer](./images/sbp5.png)

Öppna **Innehållskomponenter** och dra en **Text** -komponent nedanför det aktuella nyhetsbrevet.

![Journey Optimizer](./images/sbp6.png)

Markera hela standardtexten och ta bort den. Klicka sedan på knappen **Lägg till anpassning** i verktygsfältet.

![Journey Optimizer](./images/sbp7.png)

Då ser du det här:

![Journey Optimizer](./images/seg1.png)

Klicka på **Segmentmedlemskap** på den vänstra menyn.

![Journey Optimizer](./images/seg2.png)

>[!NOTE]
>
>Om du inte hittar ditt segment i den här listan kan du bläddra nedåt och hitta instruktioner om hur du hämtar segmentets ID manuellt.

Markera segmentet `Luma - Women's Category Interest` och klicka på ikonen **+** som ska se ut så här:

![Journey Optimizer](./images/seg3.png)

Sedan lämnar du den första raden som den är och ersätter rad 2 och 3 med den här koden:

``
    Psssst... a private sale in the women category will launch soon, we will keep you posted
{%else%}
    Thanks for taking the time to read our newsletter. Here is a 10% promo code to use on the website: READER10
{%/if%}
``

Då får du den här:

![Journey Optimizer](./images/seg4.png)

Klicka på **Validera** för att kontrollera att koden är korrekt. Klicka på **Spara**.

![Journey Optimizer](./images/sbp8.png)

Du kan nu spara det här meddelandet genom att klicka på knappen **Spara** i det övre högra hörnet. Klicka sedan på **Simulera innehåll**.

![Journey Optimizer](./images/sbp9.png)

Välj en av profilerna som du skapade som en del av den här självstudiekursen och klicka på **Förhandsgranska**. Resultatet av konfigurationen visas då.

![Journey Optimizer](./images/sbp10.png)

Då ser du det här. Klicka sedan på **Stäng**.

![Journey Optimizer](./images/sbp10fff.png)

Gå tillbaka till meddelandekontrollpanelen genom att klicka på **pilen** intill ämnesraden i det övre vänstra hörnet.

![Journey Optimizer](./images/sbp11.png)

Klicka på pilen i det övre vänstra hörnet för att gå tillbaka till din resa.

![Journey Optimizer](./images/oc79afff.png)

Klicka på **OK** för att stänga e-poståtgärden.

![Journey Optimizer](./images/oc79bfff.png)

Ändra ditt **schema** till **En gång** och definiera ett **datum/tid**. Klicka på **OK**.

>[!NOTE]
>
>Datum och tid för sändning av meddelande måste vara inom mer än en timme.

![Journey Optimizer](./images/sbp18.png)

Klicka på knappen **Publish** på resan.

![Journey Optimizer](./images/sbp19.png)

Klicka på **Publish** igen i popup-fönstret.

![Journey Optimizer](./images/sbp20.png)

Din grundläggande nyhetsbrevsresa är nu publicerad. E-postmeddelandet med nyhetsbrevet skickas baserat på ditt schema och din resa avbryts så snart som det senaste e-postmeddelandet har skickats.

![Journey Optimizer](./images/sbp20fff.png)

Du har gjort klart den här övningen.

Nästa steg: [3.4.4 Konfigurera och använd push-meddelanden för iOS](./ex4.md)

[Gå tillbaka till modul 3.4](./journeyoptimizer.md)

[Gå tillbaka till Alla moduler](../../../overview.md)
