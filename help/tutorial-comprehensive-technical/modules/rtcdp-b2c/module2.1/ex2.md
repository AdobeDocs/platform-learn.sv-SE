---
title: Foundation - kundprofil i realtid - Visa din egen kundprofil i realtid - användargränssnitt
description: Foundation - kundprofil i realtid - Visa din egen kundprofil i realtid - användargränssnitt
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 0%

---

# 2.1.2 Visualisera din egen kundprofil i realtid - användargränssnitt

I den här övningen loggar du in på Adobe Experience Platform och visar din egen kundprofil i realtid i användargränssnittet.

## Artikel

I kundprofilen i realtid visas alla profildata tillsammans med händelsedata samt befintliga segmentmedlemskap. De data som visas kan komma var som helst, från Adobe-program och externa lösningar. Det här är den mest kraftfulla vyn i Adobe Experience Platform, det verkliga upplevelsesystemet.

## 2.1.2.1 Använda kundprofilvyn i Adobe Experience Platform

Gå till [Adobe Experience Platform](https://experience.adobe.com/platform). När du har loggat in loggar du in på Adobe Experience Platform hemsida.

![Datainmatning](../../datacollection/module1.2/images/home.png)

Innan du fortsätter måste du välja en **sandlåda**. Sandlådan som ska markeras har namnet ``--aepSandboxName--``. Du kan göra detta genom att klicka på texten **[!UICONTROL Production Prod]** i den blå raden ovanför skärmen. När du har valt rätt [!UICONTROL sandbox] visas skärmändringen och nu är du i din dedikerade [!UICONTROL sandbox].

![Datainmatning](../../datacollection/module1.2/images/sb1.png)

Gå till **Profiler** och till **Bläddra** på den vänstra menyn.

![Kundprofil](./images/homemenu.png)

På panelen Profilvisningsprogram på webbplatsen kan du hitta flera identiteter. Alla identiteter är länkade till ett namnutrymme.

![Kundprofil](./images/identities.png)

På panelen Profilvisningsprogram kan du se följande kombinationer av ID:n och namnutrymmen:

| Identitet | Namnutrymme |
|:-------------:| :---------------:|
| Experience Cloud ID (ECID) | 12507560687324495704459439363261812234 |
| E-post-ID | woutervangeluwe+06022022-01@gmail.com |
| Mobilnummer-ID | +32473622044+06022022-01 |

Med Adobe Experience Platform är alla ID:n lika viktiga. Tidigare var ECID det viktigaste ID:t i Adobe-kontexten och alla andra ID:n länkades till ECID i en hierarkisk relation. I Adobe Experience Platform är detta inte längre fallet och varje ID kan betraktas som en primär identifierare.

Vanligtvis beror den primära identifieraren på sammanhanget. **Vad är det viktigaste ID:t om du frågar ditt samtalscenter?** kommer antagligen att svara, **telefonnumret!** Men om du frågar ditt CRM-team kommer de att svara **E-postadressen!** Adobe Experience Platform förstår den här komplexiteten och hanterar den åt dig. Alla program, oavsett om de är ett program från Adobe eller ett program som inte är Adobe, kommer att tala med Adobe Experience Platform genom att hänvisa till det ID som de anser vara primärt. Och det fungerar bara.

För fältet **Identitetsnamnområde** väljer du **E-post** och för fältet **Identitetsvärde** anger du den e-postadress som du använde för att registrera i föregående övning. Klicka på **Visa**. Då visas din profil i listan. Klicka på **profil-ID** för att öppna din profil.

![Kundprofil](./images/popupecid.png)

Nu visas en översikt över några viktiga **profilattribut** för din kundprofil.

![Kundprofil](./images/profile.png)

Om du vill se alla tillgängliga profilattribut för din profil går du till **Attribut**.

![Kundprofil](./images/profilattr.png)

Gå till **Händelser**, där du kan se poster för varje upplevelsehändelse som är länkad till din profil.

![Kundprofil](./images/profileee.png)

Till sist går du till menyalternativet **Segmentmedlemskap**. Nu visas alla segment som är kvalificerade för den här profilen.

![Kundprofil](./images/profileseg.png)

Nu när du har lärt dig att se kundens realtidsprofil genom att använda Adobe Experience Platform användargränssnitt kan vi göra samma sak med API:erna genom att använda Postman och Adobe I/O för att fråga mot Adobe Experience Platform API:er.

Nästa steg: [2.1.3 Visa din egen kundprofil i realtid - API](./ex3.md)

[Gå tillbaka till modul 2.1](./real-time-customer-profile.md)

[Gå tillbaka till Alla moduler](../../../overview.md)
