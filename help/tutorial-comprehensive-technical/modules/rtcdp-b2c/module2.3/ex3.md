---
title: CDP i realtid - Bygg ett segment och vidta åtgärder - Skicka segmentet till DV360
description: CDP i realtid - Bygg ett segment och vidta åtgärder - Skicka segmentet till DV360
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---

# 2.3.3 Vidta åtgärd: skicka segmentet till DV360

Gå till [Adobe Experience Platform](https://experience.adobe.com/platform). När du har loggat in loggar du in på Adobe Experience Platform hemsida.

![Datainmatning](./../../../modules/datacollection/module1.2/images/home.png)

Innan du fortsätter måste du välja en **sandlåda**. Sandlådan som ska markeras har namnet ``--aepSandboxName--``. Du kan göra detta genom att klicka på texten **[!UICONTROL Production Prod]** i den blå raden ovanför skärmen. När du har valt rätt [!UICONTROL sandbox] visas skärmändringen och nu är du i din dedikerade [!UICONTROL sandbox].

![Datainmatning](./../../../modules/datacollection/module1.2/images/sb1.png)

Gå till **Destinationer** på den vänstra menyn och gå sedan till **Katalog**. Därefter visas **målkatalogen**.

![RTCDP](./images/rtcdpmenudest.png)

I **Destinationer** klickar du på **Aktivera segment** på **Google Display &amp; Video 360** -kortet.

![RTCDP](./images/rtcdpgoogleseg.png)

Välj ditt mål och klicka på **Nästa**.

![RTCDP](./images/rtcdpcreatedest2.png)

I listan med tillgängliga segment väljer du det segment som du skapade i föregående övning. Klicka på **Nästa**.

![RTCDP](./images/rtcdpcreatedest3.png)

Klicka på **Nästa** på sidan **Segmentschema**.

![RTCDP](./images/rtcdpcreatedest4.png)

Klicka slutligen på **Slutför** på sidan **Granska**.

![RTCDP](./images/rtcdpcreatedest5.png)

Ditt segment är nu länkat till Google DV360. Varje gång en kund kvalificerar sig för det här segmentet skickas en signal till Google DV360 för att inkludera den kunden i målgruppen på Google DV360-sidan.

Nästa steg: [2.3.4 Vidta åtgärd: skicka segmentet till ett S3-mål](./ex4.md)

[Gå tillbaka till modul 2.3](./real-time-cdp-build-a-segment-take-action.md)

[Gå tillbaka till Alla moduler](../../../overview.md)
