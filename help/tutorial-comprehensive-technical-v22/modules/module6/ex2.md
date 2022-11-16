---
title: CDP för realtid - Bygg ett segment och vidta åtgärder - Konfigurera ett annonsmål som Google DV360
description: CDP för realtid - Bygg ett segment och vidta åtgärder - Konfigurera ett annonsmål som Google DV360
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 40441815-428a-48dc-a12e-91220d4ba307
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 0%

---

# 6.2 Konfigurera ett reklammål som Google DV360

>[!IMPORTANT]
>
>Innehållet nedan är avsett som FYI - det gör du **NOT** måste konfigurera ett nytt mål för DV360. Målet har redan skapats och du kan använda det i nästa övning.

Gå till [Adobe Experience Platform](https://experience.adobe.com/platform). När du loggat in kommer du till Adobe Experience Platform hemsida.

![Dataintag](../module2/images/home.png)

Innan du fortsätter måste du välja en **sandlåda**. Sandlådan som ska markeras har namnet ``--aepSandboxId--``. Du kan göra detta genom att klicka på texten **[!UICONTROL Produktionsprodukt]** i den blå linjen ovanför skärmen. När du har valt lämplig [!UICONTROL sandlåda]kommer du att se skärmändringen och nu är du med på din [!UICONTROL sandlåda].

![Dataintag](../module2/images/sb1.png)

Gå till den vänstra menyn **Destinationer** och sedan gå till **Katalog**. Då ser du **Målkatalog**.

![RTCDP](./images/rtcdp.png)

I **Destinationer**, klicka på **Google Display &amp; Video 360** och sedan klicka **+ Ställ in uppåt**.

![RTCDP](./images/rtcdpgoogle.png)

Du kommer då att se det här. Klicka **Anslut till mål**.

![RTCDP](./images/rtcdpgooglecreate1.png)

På nästa skärm kan du konfigurera ditt mål till Google DV360.

![RTCDP](./images/rtcdpgooglecreatedest.png)

Ange ett värde i fälten **Namn** och **Beskrivning**.

Fältet **Konto-ID** är **Annonsörs-ID** av DV360-kontot. Här hittar du:

![RTCDP](./images/rtcdpgoogledv360advid.png)

The **Kontotyp** ska anges till **Bjud in annonsör**.

Nu har du den här. Klicka på **Nästa**.

![RTCDP](./images/rtcdpgoogldv360new.png)

>[!NOTE]
>
>Google måste tillåta Adobe för att Adobe Experience Platform ska kunna skicka data till Google DV360. Kontakta kontohanteraren för Google för att aktivera det här dataflödet.

När du har skapat målet visas det här. Du kan också välja en datastyrningspolicy. Klicka på **Spara och avsluta**.

![RTCDP](./images/rtcdpcreatedest1.png)

Då visas en lista med tillgängliga destinationer.
I nästa övning ska du koppla segmentet som du skapade i föregående övning till Google DV360-målet.

Nästa steg: [6.3 Vidta åtgärder: skicka segmentet till DV360](./ex3.md)

[Gå tillbaka till modul 6](./real-time-cdp-build-a-segment-take-action.md)

[Gå tillbaka till Alla moduler](../../overview.md)
