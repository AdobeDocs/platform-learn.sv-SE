---
title: Bootcamp - CDP i realtid - Bygg ett segment och vidta åtgärder - Skicka ditt segment till DV360
description: Bootcamp - CDP i realtid - Bygg ett segment och vidta åtgärder - Skicka ditt segment till DV360
jira: KT-5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
feature: Destinations
exl-id: 31f46e37-f1c0-4730-8520-1ccd98df6501
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 3%

---

# 1.5 Vidta åtgärder: skicka segmentet till Facebook

Gå till [Adobe Experience Platform](https://experience.adobe.com/platform). När du loggat in kommer du till Adobe Experience Platform hemsida.

![Datainmatning](./images/home.png)

Innan du fortsätter måste du välja en **sandlåda**. Sandlådan som ska markeras har namnet ``Bootcamp``. Du kan göra detta genom att klicka på texten **[!UICONTROL Produktionsprodukt]** i den blå linjen ovanför skärmen. När du har valt lämplig [!UICONTROL sandlåda]kommer du att se skärmändringen och nu är du med på din [!UICONTROL sandlåda].

![Datainmatning](./images/sb1.png)

Gå till den vänstra menyn **Destinationer** och sedan gå till **Katalog**. Då ser du **Målkatalog**. I **Destinationer**, klicka **Aktivera segment** på **Facebook Custom Audience** kort.

![RTCDP](./images/rtcdpgoogleseg.png)

Välj mål **bootcamp-facebook** och klicka **Nästa**.

![RTCDP](./images/rtcdpcreatedest2.png)

I listan med tillgängliga segment väljer du det segment som du skapade i föregående övning. Klicka på **Nästa**.

![RTCDP](./images/rtcdpcreatedest3.png)

På **Mappning** se till att **Använd omformning** kryssrutan är aktiverad. Klicka på **Nästa**.

![RTCDP](./images/rtcdpcreatedest4a.png)

På **Segmentschema** väljer du **Målgruppens ursprung** och ange **Direkt från kunderna**. Klicka på **Nästa**.

![RTCDP](./images/rtcdpcreatedest4.png)

Till sist **Granska** sida, klicka **Slutför**.

![RTCDP](./images/rtcdpcreatedest5.png)

Ditt segment är nu länkat till Facebook anpassade målgrupper. Varje gång en kund kvalificerar sig för det här segmentet skickas en signal till Facebook på serversidan för att inkludera den kunden i Custom Audience på Facebook sida.

I Facebook hittar du ditt segment från Adobe Experience Platform under Anpassade målgrupper:

![RTCDP](./images/rtcdpcreatedest5b.png)

Nu kan du se hur din anpassade målgrupp visas i Facebook:

![RTCDP](./images/rtcdpcreatedest5a.png)

[Gå tillbaka till användarflöde 1](./uc1.md)

[Gå tillbaka till Alla moduler](../../overview.md)
