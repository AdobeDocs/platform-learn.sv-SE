---
title: Bootcamp - Personalization in the call center - Brazil
description: Bootcamp - Personalization in the call center - Brazil
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
source-git-commit: 75a878ba596078e6d013b65062606931402302dd
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---

# 2.6 Personalisering i call center

Som redan har nämnts flera gånger under bootlägret är personalisering av kundupplevelsen något som bör ske över alla kanaler. Ett callcenter är ofta ganska frånkopplat från resten av kundresan och det leder ofta till frustrerande kundupplevelser, men det behöver inte vara det. Låt oss visa dig ett exempel på hur callcentret enkelt kan anslutas till Adobe Experience Platform i realtid.

## Kundens reseflöde

När du använde mobilappen tidigare köpte du en produkt genom att klicka på **Köp** -knappen.

![DSN](./images/app20.png)

Låt oss anta att du har en fråga om status för din beställning, vad skulle du göra? Vanligtvis ringer du callcenter.

Innan du ringer till callcentret måste du känna till **Förmåns-ID**. Du hittar ditt lojalitets-ID i profilvisningsprogrammet för webbplatsen.

![DSN](./images/cc1.png)

I det här fallet **Förmåns-ID** är **5863105**. Som en del av vår anpassade implementering av funktionen call center i demomiljön måste du lägga till ett prefix i din **Förmåns-ID**. Prefixet är **11373**, så det lojalitets-ID som ska användas i det här exemplet är **11373 5863105**.

Låt oss göra det nu. Använd telefonen och ring numret **+1 (323) 745-1670**.

![DSN](./images/cc2.png)

Du ombeds ange ditt lojalitets-ID följt av **#**. Ange ditt lojalitets-ID.

![DSN](./images/cc3.png)

Då hör du **Hej, förnamn**. Förnamnet hämtas från kundprofilen i realtid i Adobe Experience Platform. Du har sedan tre valmöjligheter. Trycknummer **1**, **Orderstatus**.

![DSN](./images/cc4.png)

När du har hört din orderstatus kan du välja att trycka **1** för att gå tillbaka till huvudmenyn, annars trycker du på 2. Tryck **2**.

![DSN](./images/cc5.png)

Du ombeds sedan betygsätta din samtalscenterupplevelse genom att välja ett nummer mellan 1 och 5, där 1 är lågt och 5 är högt. Gör ditt val.

![DSN](./images/cc6.png)

Ditt samtal till callcenter avslutas nu.

Gå till [Adobe Experience Platform](https://experience.adobe.com/platform). När du loggat in kommer du till Adobe Experience Platform hemsida.

![Dataintag](./images/home.png)

Innan du fortsätter måste du välja en **sandlåda**. Sandlådan som ska markeras har namnet ``Bootcamp``. Du kan göra detta genom att klicka på texten **[!UICONTROL Produktionsprodukt]** i den blå linjen ovanför skärmen. När du har valt lämplig [!UICONTROL sandlåda]kommer du att se skärmändringen och nu är du med på din [!UICONTROL sandlåda].

![Dataintag](./images/sb1.png)

Gå till den vänstra menyn **Profiler** och till **Bläddra**.

![Kundprofil](./images/homemenu.png)

Välj **Namnutrymme för identitet** **E-post** och ange e-postadressen till kundprofilen. Klicka **Visa**. Klicka för att öppna din profil.

![DSN](./images/cc7.png)

Du kommer att se din kundprofil igen. Gå till **Händelser**.

![DSN](./images/cc8.png)

Under händelser visas 2 händelser med eventType för **callCenter**. Den första händelsen är ett resultat av ditt svar på frågan **Betygsätt hur nöjd du är med ditt samtal**.

![DSN](./images/cc9.png)

Bläddra ned en bit så ser du händelsen som spelades in när du valde alternativet att kontrollera **Orderstatus**.

![DSN](./images/cc10.png)

Gå till **Segmentmedlemskap**. Nu kommer du att se att två segment kvalificerar sig för din profil, i realtid, baserat på den interaktion du hade via callcenter. Dessa segmentmedlemskap kan och bör sedan användas för att påverka vad kommunikation och personalisering händer i andra kanaler.

![DSN](./images/cc11.png)

Du har nu avslutat den här övningen.

[Gå tillbaka till användarflöde 2](./uc2.md)

[Gå tillbaka till Alla moduler](../../overview.md)
