---
title: Bootcamp - CDP i realtid - Skapa en målgrupp och vidta åtgärder - Skicka din målgrupp till DV360
description: Bootcamp - CDP i realtid - Bygg en målgrupp och vidta åtgärder - Skicka din målgrupp till DV360
jira: KT-5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
feature: Destinations
exl-id: 31f46e37-f1c0-4730-8520-1ccd98df6501
source-git-commit: 5876de5015e4c8c337c235c24cc28b0a32e274dd
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# 1.5 Take Action: send your audition to Facebook

Gå till [Adobe Experience Platform](https://experience.adobe.com/platform). När du har loggat in loggar du in på Adobe Experience Platform hemsida.

![Datainmatning](./images/home.png)

Innan du fortsätter måste du välja en **sandlåda**. Sandlådan som ska markeras har namnet ``Bootcamp``. Du kan göra detta genom att klicka på texten **[!UICONTROL Production Prod]** i den blå raden ovanför skärmen. När du har valt rätt [!UICONTROL sandbox] visas skärmändringen och nu är du i din dedikerade [!UICONTROL sandbox].

![Datainmatning](./images/sb1.png)

Gå till **Destinationer** på den vänstra menyn och gå sedan till **Katalog**. Därefter visas **målkatalogen**. I **Destinationer** klickar du på **Aktivera målgrupper** på kortet **Facebook Custom Audience** .

![RTCDP](./images/rtcdpgoogleseg.png)

Markera målet **bootcamp-facebook** och klicka på **Next**.

![RTCDP](./images/rtcdpcreatedest2.png)

I listan över tillgängliga målgrupper väljer du den målgrupp du skapade i föregående övning. Klicka på **Nästa**.

![RTCDP](./images/rtcdpcreatedest3.png)

Kontrollera att kryssrutan **Använd omformning** är aktiverad på sidan **Mappning**. Klicka på **Nästa**.

![RTCDP](./images/rtcdpcreatedest4a.png)

På sidan **Målgruppsplan** väljer du **Publiken** som har sin ursprung och anger **Direkt från kunderna**. Klicka på **Nästa**.

![RTCDP](./images/rtcdpcreatedest4.png)

Klicka slutligen på **Slutför** på sidan **Granska**.

![RTCDP](./images/rtcdpcreatedest5.png)

Din målgrupp är nu länkad till Facebook anpassade målgrupper. Varje gång en kund kvalificerar sig för den här målgruppen skickas en signal till Facebook på serversidan om att inkludera den kunden i Custom Audience på Facebook sida.

I Facebook hittar du målgrupper från Adobe Experience Platform under Anpassade målgrupper:

![RTCDP](./images/rtcdpcreatedest5b.png)

Nu kan du se hur din anpassade målgrupp visas i Facebook:

![RTCDP](./images/rtcdpcreatedest5a.png)

[Gå tillbaka till användarflöde 1](./uc1.md)

[Gå tillbaka till Alla moduler](../../overview.md)
