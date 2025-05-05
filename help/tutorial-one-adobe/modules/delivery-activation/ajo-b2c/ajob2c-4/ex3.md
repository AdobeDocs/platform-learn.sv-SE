---
title: Adobe Journey Optimizer - Använd personalisering i ett e-postmeddelande
description: Den här övningen förklarar hur du använder segmentpersonalisering i ett e-postinnehåll
kt: 5342
doc-type: tutorial
exl-id: a1ad649e-d0c4-4e87-b784-1e2d99f34a2e
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# 3.4.3 Använda segmentbaserad personalisering i ett e-postmeddelande

Logga in på Adobe Experience Cloud på [Adobe Experience Cloud](https://experience.adobe.com). Klicka på **Adobe Journey Optimizer**.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Du omdirigeras till vyn **Hem** i Journey Optimizer. Innan du fortsätter måste du välja en **sandlåda**. Sandlådan som ska markeras har namnet ``--aepTenantId--``.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

## 3.4.3.1 Segmentbaserad personalisering

I den här övningen kommer du att förbättra nyhetsbrevets e-postmeddelande som du skapade i föregående övning med en personlig text baserad på segmentmedlemskap.

Gå till **Kampanjer**. Hitta den nyhetsbrevsresa du har skapat i föregående övning. Sök efter `--aepUserLdap-- - CitiSignal Newsletter`. Högerklicka på de 3 punkterna **..** och klicka på **Duplicera**.

![Journey Optimizer](./images/sbp1.png)

Då ser du det här. Använd det här för **titeln**: `--aepUserLdap-- - CitiSignal Newsletter (SBP)`. Klicka på **Duplicera**.

![Journey Optimizer](./images/sbp2.png)

Klicka på den duplicerade kampanjen för att öppna den.

![Journey Optimizer](./images/sbp3.png)

Klicka på **Redigera** om du vill ändra innehållet.

![Journey Optimizer](./images/sbp3a.png)

Klicka på **Redigera e-postbrödtext**.

![Journey Optimizer](./images/sbp4.png)

Då ser du det här.

![Journey Optimizer](./images/sbp5.png)

Öppna **Innehållskomponenter** och dra en **1:1-kolumn** ovanför erbjudandet för AirPods.

![Journey Optimizer](./images/sbp6.png)

Dra och släpp en **Text** -komponent i den 1:1-kolumnen.

![Journey Optimizer](./images/sbp6a.png)

Markera hela standardtexten och ta bort den. Klicka sedan på knappen **Lägg till anpassning** i verktygsfältet.

![Journey Optimizer](./images/sbp7.png)

Då ser du det här. Klicka på **Publiker** på den vänstra menyn.

![Journey Optimizer](./images/seg1.png)

Markera segmentet `--aepUserLdap-- - Interest in Plans` och klicka på ikonen **+** för att lägga till det på arbetsytan.

![Journey Optimizer](./images/seg3.png)

Sedan lämnar du den första raden som den är och ersätter rad 2 och 3 med den här koden:

&grave;&grave;
    PS: It may be a good idea to check if your plan still meets your needs! Click here to be contacted by one of our experts!
{%else%}
    PS: Thanks for taking the time to read our newsletter. Here is a 10% promo code to use on the website: NEWSLETTER10
{%/if%}
&grave;&grave;

Du får den här då. Klicka på **Spara**.

![Journey Optimizer](./images/seg4.png)

Ändra textjusteringen till **Centrera**.

![Journey Optimizer](./images/sbp9.png)

Du kan nu spara det här meddelandet genom att klicka på knappen **Spara** i det övre högra hörnet. Klicka sedan på **pilen** bredvid texten på ämnesraden i det övre vänstra hörnet.

![Journey Optimizer](./images/sbp9a.png)

Klicka på **Granska för att aktivera**.

![Journey Optimizer](./images/oc79afff.png)

Klicka på **Aktivera**.

![Journey Optimizer](./images/oc79bfff.png)

Ditt nyhetsbrev med segmentbaserad personalisering publiceras nu. E-postmeddelandet med nyhetsbrevet skickas baserat på ditt schema och din resa avbryts så snart som det senaste e-postmeddelandet har skickats.

Om du är berättigad till det segment som användes visas detta i e-postmeddelandet som du får:

![Journey Optimizer](./images/sbp20fff.png)

Du har gjort klart den här övningen.

## Nästa steg

Gå till installationsprogrammet för [3.4.4 och använd push-meddelanden för iOS](./ex4.md){target="_blank"}

Gå tillbaka till [Adobe Journey Optimizer](journeyoptimizer.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../../overview.md){target="_blank"}
