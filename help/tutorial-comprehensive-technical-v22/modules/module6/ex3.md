---
title: CDP i realtid - Bygg ett segment och vidta åtgärder - Skicka segmentet till DV360
description: CDP i realtid - Bygg ett segment och vidta åtgärder - Skicka segmentet till DV360
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 7a78260f-cd25-4ed0-801b-87174babaffe
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 0%

---

# 6.3 Vidta åtgärder: skicka segmentet till DV360

Gå till [Adobe Experience Platform](https://experience.adobe.com/platform). När du loggat in kommer du till Adobe Experience Platform hemsida.

![Dataintag](../module2/images/home.png)

Innan du fortsätter måste du välja en **sandlåda**. Sandlådan som ska markeras har namnet ``--aepSandboxId--``. Du kan göra detta genom att klicka på texten **[!UICONTROL Produktionsprodukt]** i den blå linjen ovanför skärmen. När du har valt lämplig [!UICONTROL sandlåda]kommer du att se skärmändringen och nu är du med på din [!UICONTROL sandlåda].

![Dataintag](../module2/images/sb1.png)

Gå till den vänstra menyn **Destinationer** och sedan gå till **Katalog**. Då ser du **Målkatalog**.

![RTCDP](./images/rtcdpmenudest.png)

I **Destinationer** klickar du på **Aktivera segment** på **Google Display &amp; Video 360** kort.

![RTCDP](./images/rtcdpgoogleseg.png)

Välj mål och klicka på **Nästa**.

![RTCDP](./images/rtcdpcreatedest2.png)

I listan med tillgängliga segment väljer du det segment som du skapade i föregående övning. Klicka på **Nästa**.

![RTCDP](./images/rtcdpcreatedest3.png)

På **Segmentschema** sida, klicka **Nästa**.

![RTCDP](./images/rtcdpcreatedest4.png)

Till sist **Granska** sida, klicka **Slutför**.

![RTCDP](./images/rtcdpcreatedest5.png)

Ditt segment är nu länkat till Google DV360. Varje gång en kund kvalificerar sig för det här segmentet skickas en signal till Google DV360 för att inkludera den kunden i målgruppen på Google DV360-sidan.

Nästa steg: [6.4 Vidta åtgärder: skicka segmentet till en S3-destination](./ex4.md)

[Gå tillbaka till modul 6](./real-time-cdp-build-a-segment-take-action.md)

[Gå tillbaka till Alla moduler](../../overview.md)
