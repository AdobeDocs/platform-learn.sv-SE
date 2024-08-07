---
title: Bootcamp - kundprofil i realtid - Från okänd till känd på webbplatsen
description: Bootcamp - kundprofil i realtid - Från okänd till känd på webbplatsen
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Profiles
exl-id: 32a084a3-4c04-4367-947e-f7151fdad73b
source-git-commit: cd59a41f4533f18a54d80298ee9faf3a8ba3c6e7
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---

# 1.1 Från okänd till känd på webbplatsen

## Kontext

Resan från okänd till känd är en av de viktigaste ämnena bland varumärken nuförtiden, liksom kundresan från förvärv till lojalitet.

Adobe Experience Platform spelar en mycket viktig roll på den här resan. Plattformen är hjärnan för kommunikation, **upplevelsesystemet för posten**.

Plattform är en miljö där ordet kund är bredare än bara de kända kunderna. En okänd besökare på webbplatsen är också en kund ur plattformens perspektiv, och som sådan skickas även allt beteende som en okänd besökare till Platform. Tack vare den metoden kan ett varumärke, när besökaren till slut blir en känd kund, även visualisera det som hände före det ögonblicket. Detta bidrar till att optimera attribuering och upplevelser.

## Kundreseflöde

Gå till [https://bootcamp.aepdemo.net](https://publish9122.adobedemo.com/content/aep-bootcamp-experience/language-masters/en.html). Klicka på **Tillåt alla**.

![DSN](./images/web8.png)

Klicka på logotypikonen för Adobe i det övre vänstra hörnet av skärmen för att öppna profilvisningsprogrammet.

![Demo](./images/pv1.png)

Ta en titt på panelen Profilvisningsprogram och kundprofilen i realtid med **Experience Cloud ID** som primär identifierare för den okända kunden.

![Demo](./images/pv2.png)

Ni kan också se alla upplevelsehändelser som samlats in baserat på kundens beteende. Listan är för närvarande tom, men den ändras snart.

![Demo](./images/pv3.png)

Gå till menyalternativet **Programtjänster** och klicka på produkten **Real-Time CDP**.

![Demo](./images/pv4.png)

Då visas informationssidan för produkten. En upplevelsehändelse av typen **Produktvy** har nu skickats till Adobe Experience Platform med den Web SDK-implementering som du granskade i modul 1. Öppna panelen Profilvisningsprogram och titta på dina **Experience Events**.

![Demo](./images/pv5.png)

Gå till menyalternativet **Programtjänster** och klicka på produkten **Adobe Journey Optimizer**. En annan Experience Event har skickats till Adobe Experience Platform.

![Demo](./images/pv7.png)

Öppna panelen Profilvisningsprogram. Nu visas 2 Experience Events av typen **Product View**. Medan beteendet är anonymt spåras och lagras varje klick i Adobe Experience Platform. När den anonyma kunden blir känd kan vi automatiskt sammanfoga alla anonyma beteenden med kunskapsprofilen.

![Demo](./images/pv8.png)

Nu ska vi analysera kundprofilen och sedan använda ditt beteende för att personalisera kundupplevelsen på webbplatsen.

Nästa steg: [1.2 Visa din egen kundprofil i realtid - användargränssnitt](./ex2.md)

[Gå tillbaka till användarflöde 1](./uc1.md)

[Gå tillbaka till Alla moduler](../../overview.md)
