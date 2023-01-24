---
title: Bootcamp - Real-time Customer Profile - Visualize your own Real-time Customer Profile - UI - Brazil
description: Bootcamp - Real-time Customer Profile - Visualize your own Real-time Customer Profile - UI - Brazil
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
source-git-commit: 75a878ba596078e6d013b65062606931402302dd
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 0%

---

# 1.2 Visualisera din egen kundprofil i realtid - användargränssnitt

I den här övningen loggar du in på Adobe Experience Platform och visar din egen kundprofil i realtid i användargränssnittet.

## Artikel

I kundprofilen i realtid visas alla profildata tillsammans med händelsedata samt befintliga segmentmedlemskap. De data som visas kan komma var som helst, från Adobe-program och externa lösningar. Det här är den mest kraftfulla vyn i Adobe Experience Platform, det verkliga upplevelsesystemet.

## 1.2.1 Använda kundprofilvyn i Adobe Experience Platform

Gå till [Adobe Experience Platform](https://experience.adobe.com/platform). När du loggat in kommer du till Adobe Experience Platform hemsida.

![Dataintag](./images/home.png)

Innan du fortsätter måste du välja en **sandlåda**. Sandlådan som ska markeras har namnet ``Bootcamp``. Du kan göra detta genom att klicka på texten **[!UICONTROL Produktionsprodukt]** i den blå linjen ovanför skärmen. När du har valt lämplig [!UICONTROL sandlåda]kommer du att se skärmändringen och nu är du med på din [!UICONTROL sandlåda].

![Dataintag](./images/sb1.png)

Gå till den vänstra menyn **Profiler** och till **Bläddra**.

![Kundprofil](./images/homemenu.png)

På panelen Profilvisningsprogram på webbplatsen finns en översikt över identiteten. Alla identiteter är länkade till ett namnutrymme.

![Kundprofil](./images/identities.png)

På profilvisarpanelen ser du den här identiteten:

| Namnutrymme | Identitet |
|:-------------:| :---------------:|
| Experience Cloud ID (ECID) | 19428085896177382402834560825640259081 |

Med Adobe Experience Platform är alla ID:n lika viktiga. Tidigare var ECID det viktigaste ID:t i Adobe-kontexten och alla andra ID:n länkades till ECID i en hierarkisk relation. I Adobe Experience Platform är detta inte längre fallet och varje ID kan betraktas som en primär identifierare.

Vanligtvis beror den primära identifieraren på sammanhanget. Om du frågar ditt samtalscenter, **Vilket är det viktigaste ID:t?** de kommer antagligen att svara, **telefonnumret!** Men om ni frågar CRM-teamet får de svar **E-postadressen!**  Adobe Experience Platform förstår detta och hanterar det åt dig. Alla program, oavsett om de är ett program från Adobe eller ett program som inte är Adobe, kommer att tala med Adobe Experience Platform genom att hänvisa till det ID som de anser vara primärt. Och det fungerar bara.

För fältet **Namnutrymme för identitet**, markera **ECID** och för fältet **Identitetsvärde** Ange det ECID som du hittar på panelen Profilvisningsprogram på webbplatsen för bootlägret. Klicka **Visa**. Då visas din profil i listan. Klicka på **Profil-ID** för att öppna din profil.

![Kundprofil](./images/popupecid.png)

Nu ser du en översikt över några viktiga **Profilattribut** av er kundprofil.

![Kundprofil](./images/profile.png)

Gå till **Händelser**, där du kan se poster för varje upplevelsehändelse som är länkad till din profil.

![Kundprofil](./images/profileee.png)

Till sist går du till menyalternativet **Segmentmedlemskap**. Nu visas alla segment som är kvalificerade för den här profilen.

![Kundprofil](./images/profileseg.png)

Nu ska vi skapa ett nytt segment som gör att ni kan personalisera kundupplevelsen för en anonym eller välkänd kund.

Nästa steg: [1.3 Skapa ett segment - användargränssnitt](./ex3.md)

[Gå tillbaka till användarflöde 1](./uc1.md)

[Gå tillbaka till Alla moduler](../../overview.md)
