---
title: CDP för realtid - Bygg ett segment och vidta åtgärder - Konfigurera ett Advertising-mål som Google DV360
description: CDP för realtid - Bygg ett segment och vidta åtgärder - Konfigurera ett Advertising-mål som Google DV360
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 0%

---

# 2.3.2 Konfigurera ett Advertising-mål som Google DV360

>[!IMPORTANT]
>
>Innehållet nedan är avsett som FYI - du behöver **INTE** konfigurera ett nytt mål för DV360. Målet har redan skapats och du kan använda det i nästa övning.

Gå till [Adobe Experience Platform](https://experience.adobe.com/platform). När du har loggat in loggar du in på Adobe Experience Platform hemsida.

![Datainmatning](./../../../modules/datacollection/module1.2/images/home.png)

Innan du fortsätter måste du välja en **sandlåda**. Sandlådan som ska markeras har namnet ``--aepSandboxName--``. Du kan göra detta genom att klicka på texten **[!UICONTROL Production Prod]** i den blå raden ovanför skärmen. När du har valt rätt [!UICONTROL sandbox] visas skärmändringen och nu är du i din dedikerade [!UICONTROL sandbox].

![Datainmatning](./../../../modules/datacollection/module1.2/images/sb1.png)

Gå till **Destinationer** på den vänstra menyn och gå sedan till **Katalog**. Därefter visas **målkatalogen**.

![RTCDP](./images/rtcdp.png)

I **Destinationer** klickar du på **Google Display &amp; Video 360** och sedan på **+ Set Up** (Konfigurera).

![RTCDP](./images/rtcdpgoogle.png)

Då ser du det här. Klicka på **Anslut till mål**.

![RTCDP](./images/rtcdpgooglecreate1.png)

På nästa skärm kan du konfigurera ditt mål till Google DV360.

![RTCDP](./images/rtcdpgooglecreatedest.png)

Ange ett värde i fälten **Namn** och **Beskrivning**.

Fältet **Konto-ID** är **Advertiser-ID** för DV360-kontot. Här hittar du:

![RTCDP](./images/rtcdpgoogledv360advid.png)

**Kontotypen** ska anges till **Bjud in annonsörer**.

Nu har du den här. Klicka på **Nästa**.

![RTCDP](./images/rtcdpgoogldv360new.png)

>[!NOTE]
>
>Google måste tillåta Adobe för att Adobe Experience Platform ska kunna skicka data till Google DV360. Kontakta din kontohanterare för Google för att aktivera det här dataflödet.

När du har skapat målet visas det här. Du kan också välja en datastyrningspolicy. Klicka sedan på **Spara och avsluta**.

![RTCDP](./images/rtcdpcreatedest1.png)

Då visas en lista med tillgängliga destinationer.
I nästa övning ska du koppla segmentet som du skapade i föregående övning till Google DV360-målet.

Nästa steg: [2.3.3 Vidta åtgärd: skicka segmentet till DV360](./ex3.md)

[Gå tillbaka till modul 2.3](./real-time-cdp-build-a-segment-take-action.md)

[Gå tillbaka till Alla moduler](../../../overview.md)
