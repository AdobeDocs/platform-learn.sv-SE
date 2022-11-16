---
title: Adobe Journey Optimizer - Använd personalisering i ett e-postmeddelande
description: Den här övningen förklarar hur du använder segmentpersonalisering i ett e-postinnehåll
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 573ecfba-4f1d-4242-8358-1d33109aaea3
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 0%

---

# 10.3 Använda personalisering i ett e-postmeddelande

Logga in på Adobe Experience Cloud genom att gå till [Adobe Experience Cloud](https://experience.adobe.com). Klicka **Adobe Journey Optimizer**.

![ACOP](../module7/images/acophome.png)

Du omdirigeras till **Startsida** i Journey Optimizer. Innan du fortsätter måste du välja en **sandlåda**. Sandlådan som ska markeras har namnet ``--aepTenantId--``. Du kan göra detta genom att klicka på texten **[!UICONTROL Produktionsprodukt]** i den blå linjen ovanför skärmen.

![ACOP](../module7/images/acoptriglp.png)

## 10.3.1 Segmentbaserad personalisering

I den här övningen kommer du att förbättra ditt nyhetsbrev via e-post med en personlig text baserad på segmentmedlemskap.

Gå till **Resor**. Hitta den nyhetsbrevsresa du har skapat i föregående övning. Sök efter `--demoProfileLdap-- - Newsletter`. Klicka på resan för att öppna den.

![Journey Optimizer](./images/sbp1.png)

Du kommer då att se det här. Klicka **Duplicera**.

![Journey Optimizer](./images/sbp2.png)

Klicka på ** Duplicera**.

![Journey Optimizer](./images/sbp3.png)

Välj **E-post** och klicka **Redigera innehåll**.

![Journey Optimizer](./images/sbp3a.png)

Klicka **E-postdesigner**.

![Journey Optimizer](./images/sbp4.png)

Du kommer då att se det här.

![Journey Optimizer](./images/sbp5.png)

Öppna **Innehållskomponenter** och dra en **Text** under det aktuella nyhetsbrevet.

![Journey Optimizer](./images/sbp6.png)

Markera hela standardtexten och ta bort den. Klicka sedan på **Lägg till personalisering** i verktygsfältet.

![Journey Optimizer](./images/sbp7.png)

Då ser du det här:

![Journey Optimizer](./images/seg1.png)

Klicka på **Segmentmedlemskap**.

![Journey Optimizer](./images/seg2.png)

>[!NOTE]
>
>Om du inte hittar ditt segment i den här listan kan du bläddra nedåt och hitta instruktioner om hur du hämtar segmentets ID manuellt.

Markera segmentet `Luma - Women's Category Interest` och klicka på **+** -ikonen, som ska se ut så här:

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

Klicka **Validera** för att säkerställa att koden är korrekt. Klicka **Spara**.

![Journey Optimizer](./images/sbp8.png)

Du kan nu spara det här meddelandet genom att klicka på **Spara** i det övre högra hörnet. Klicka sedan på **Simulera innehåll**.

![Journey Optimizer](./images/sbp9.png)

Välj en av profilerna som du skapade som en del av kursen och klicka på **Förhandsgranska**. Resultatet av konfigurationen visas då.

![Journey Optimizer](./images/sbp10.png)

Du kommer då att se det här. Klicka sedan på **Stäng**.

![Journey Optimizer](./images/sbp10fff.png)

Gå tillbaka till meddelandekontrollpanelen genom att klicka på **pil** bredvid texten på ämnesraden i det övre vänstra hörnet.

![Journey Optimizer](./images/sbp11.png)

Klicka på pilen i det övre vänstra hörnet för att gå tillbaka till din resa.

![Journey Optimizer](./images/oc79afff.png)

Klicka **OK** för att stänga e-poståtgärden.

![Journey Optimizer](./images/oc79bfff.png)

Ändra dina **Schema** till **En gång** och definiera **Datum/tid**. Klicka **OK**.

>[!NOTE]
>
>Datum och tid för sändning av meddelande måste vara inom mer än en timme.

![Journey Optimizer](./images/sbp18.png)

Klicka på **Publicera** på resan.

![Journey Optimizer](./images/sbp19.png)

I popup-fönstret klickar du på **Publicera** igen.

![Journey Optimizer](./images/sbp20.png)

Din grundläggande nyhetsbrevsresa är nu publicerad. E-postmeddelandet med nyhetsbrevet skickas baserat på ditt schema och din resa avbryts så snart som det senaste e-postmeddelandet har skickats.

![Journey Optimizer](./images/sbp20fff.png)

Du har gjort klart den här övningen.

Nästa steg: [10.4 Konfigurera och använda push-meddelanden för iOS](./ex4.md)

[Gå tillbaka till modul 10](./journeyoptimizer.md)

[Gå tillbaka till Alla moduler](../../overview.md)
