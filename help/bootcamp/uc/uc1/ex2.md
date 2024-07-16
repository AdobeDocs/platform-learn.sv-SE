---
title: Bootcamp - Real-time Customer Profile - Visualize your own Real-time Customer Profile - UI
description: Bootcamp - Real-time Customer Profile - Visualize your own Real-time Customer Profile - UI
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Profiles
exl-id: 4c810767-00ab-4cae-baa9-97b0cb9bf2df
source-git-commit: 5876de5015e4c8c337c235c24cc28b0a32e274dd
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---

# 1.2 Visualisera din egen kundprofil i realtid - användargränssnitt

I den här övningen loggar du in på Adobe Experience Platform och visar din egen kundprofil i realtid i användargränssnittet.

## Artikel

I kundprofilen i realtid visas alla profildata tillsammans med händelsedata samt befintliga målgruppsmedlemskap. De data som visas kan komma var som helst, från Adobe-program och externa lösningar. Det här är den mest kraftfulla vyn i Adobe Experience Platform, det verkliga upplevelsesystemet.

## 1.2.1 Använda kundprofilvyn i Adobe Experience Platform

Gå till [Adobe Experience Platform](https://experience.adobe.com/platform). När du har loggat in loggar du in på Adobe Experience Platform hemsida.

![Datainmatning](./images/home.png)

Innan du fortsätter måste du välja en **sandlåda**. Sandlådan som ska markeras har namnet ``Bootcamp``. Du kan göra detta genom att klicka på texten **[!UICONTROL Production Prod]** i den blå raden ovanför skärmen. När du har valt rätt [!UICONTROL sandbox] visas skärmändringen och nu är du i din dedikerade [!UICONTROL sandbox].



Gå till **Profiler** och till **Bläddra** på den vänstra menyn.

![Kundprofil](./images/homemenu.png)

På panelen Profilvisningsprogram på webbplatsen finns en översikt över identiteten. Alla identiteter är länkade till ett namnutrymme.

![Kundprofil](./images/identities.png)




Med Adobe Experience Platform är alla ID:n lika viktiga. Tidigare var ECID det viktigaste ID:t i Adobe-kontexten och alla andra ID:n länkades till ECID i en hierarkisk relation. I Adobe Experience Platform är detta inte längre fallet och varje ID kan betraktas som en primär identifierare.

Vanligtvis beror den primära identifieraren på sammanhanget. **Vad är det viktigaste ID:t om du frågar ditt samtalscenter?** kommer antagligen att svara, **telefonnumret!** Men om du frågar ditt CRM-team kommer de att svara **E-postadressen!** Adobe Experience Platform förstår den här komplexiteten och hanterar den åt dig. Alla program, oavsett om de är ett program från Adobe eller ett program som inte är Adobe, kommer att tala med Adobe Experience Platform genom att hänvisa till det ID som de anser vara primärt. Och det fungerar bara.

För fältet **Identitetsnamnområde** väljer du **ECID** och för fältet **Identitetsvärde** anger du det ECID som du hittar på panelen Profilvisningsprogram på webbplatsen för bootlägret. Klicka på **Visa**. Då visas din profil i listan. Klicka på **profil-ID** för att öppna din profil.

![Kundprofil](./images/popupecid.png)

Nu visas en översikt över några viktiga **profilattribut** för din kundprofil.

![Kundprofil](./images/profile.png)

Gå till **Händelser**, där du kan se poster för varje upplevelsehändelse som är länkad till din profil.

![Kundprofil](./images/profileee.png)

Till sist går du till menyalternativet **Målgruppsmedlemskap**. Nu ser du alla målgrupper som är kvalificerade för den här profilen.

![Kundprofil](./images/profileseg.png)

Nu ska vi skapa en ny målgrupp som gör att ni kan personalisera kundupplevelsen för en anonym eller välkänd kund.

Nästa steg: [1.3 Skapa en målgrupp - användargränssnitt](./ex3.md)

[Gå tillbaka till användarflöde 1](./uc1.md)

[Gå tillbaka till Alla moduler](../../overview.md)
