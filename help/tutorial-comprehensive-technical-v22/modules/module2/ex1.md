---
title: Foundation - datainmatning - från okänd till känd på webbplatsen
description: Foundation - datainmatning - från okänd till känd på webbplatsen
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 683c7dd9-af69-456e-ab75-2a694588e3b3
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '735'
ht-degree: 0%

---

# 2.1 - Från okänd till känd på webbplatsen

## Kontext

Resan från okänd till känd är en av de viktigaste ämnena bland varumärken nuförtiden, liksom kundresan från förvärv till lojalitet.

Adobe Experience Platform spelar en mycket viktig roll på den här resan. Plattformen är hjärnan för kommunikation, det upplevelsesystem som finns.

Plattformen är en miljö där ordet **kund** är bredare än bara **känd**-customers. Detta är mycket viktigt att nämna när man talar till varumärken: En okänd besökare på webbplatsen är också en kund ur plattformens perspektiv, och som sådan skickas även allt beteende som en okänd besökare till Platform. Tack vare den metoden kan ett varumärke, när kunden så småningom blir en känd kund, även visualisera det som hände före den tidpunkten. Detta bidrar till att optimera attribuering och upplevelser.

## Vad ska du göra?

Du kommer nu att importera data till Adobe Experience Platform och dessa data kommer att länkas till identifierare som ECID och e-postadresser. Målet med detta är att förstå företagssammanhanget för vad du ska göra ur ett konfigurationsperspektiv. I nästa övning kommer du att börja konfigurera allt du behöver för att göra all datainmatning möjlig i din egen sandlådemiljö.

### Kundreseflöde

Gå till [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). När du har loggat in med din Adobe ID ser du det här. Klicka på webbplatsprojektet för att öppna det.

![DSN](../module0/images/web8.png)

På **Skärmar** sida, klicka **Kör**.

![DSN](../module1/images/web2.png)

Du kommer då att se din demowebbplats öppnas. Markera URL-adressen och kopiera den till Urklipp.

![DSN](../module0/images/web3.png)

Öppna ett nytt inkognito-webbläsarfönster.

![DSN](../module0/images/web4.png)

Klistra in webbadressen till demowebbplatsen, som du kopierade i föregående steg. Du ombeds sedan logga in med din Adobe ID.

![DSN](../module0/images/web5.png)

Välj kontotyp och slutför inloggningsprocessen.

![DSN](../module0/images/web6.png)

Därefter visas webbplatsen i ett inkognitivt webbläsarfönster. För varje demonstration måste du använda ett nytt, inkognitivt webbläsarfönster för att läsa in webbadressen till demowebbplatsen.

![DSN](../module0/images/web7.png)

Klicka på logotypikonen för Adobe i det övre vänstra hörnet av skärmen för att öppna profilvisningsprogrammet.

![Demo](./images/pv1.png)

Ta en titt på panelen Profilvisningsprogram och kundprofilen i realtid med **Experience Cloud ID** som primär identifierare för den här okända kunden.

![Demo](./images/pv2.png)

Ni kan också se alla upplevelsehändelser som samlats in baserat på kundens beteende. Listan är för närvarande tom, men den ändras snart.

![Demo](../module2/images/pv3.png)

Gå till **Män** produktkategori. Klicka sedan på produkten **Montana Wind Jacket**.

![Demo](../module2/images/pv4.png)

Då visas informationssidan för produkten. En upplevelsehändelse av typen **Produktvy** har nu skickats till Adobe Experience Platform med den Web SDK-implementering som du granskade i modul 1.

![Demo](../module2/images/pv5.png)

Öppna Provile Viewer-panelen och titta på **Experience Events**.

![Demo](../module2/images/pv6.png)

Gå tillbaka till **Kvinnor** kategorisida och klicka på en annan produkt. En annan Experience Event har skickats till Adobe Experience Platform.

![Demo](../module2/images/pv7.png)

Öppna panelen Profilvisningsprogram. Nu visas 2 upplevelsehändelser av typen **Produktvy**. Beteendet är anonymt, men vi kan spåra varje klick och lagra det i Adobe Experience Platform. När den anonyma kunden blir känd kan vi automatiskt sammanfoga alla anonyma beteenden med kunskapsprofilen.

![Demo](../module2/images/pv8.png)

Gå till sidan Register/Login. Klicka **SKAPA ETT KONTO**.

![Demo](../module2/images/pv9.png)

Fyll i detaljerna och klicka **Registrera** därefter omdirigeras du till föregående sida.

![Demo](../module2/images/pv10.png)

Öppna profilvisarpanelen och gå till kundprofilen i realtid. På panelen Profilvisningsprogram ska du se alla dina personuppgifter visas, som dina nya e-post- och telefonidentifierare.

![Demo](../module2/images/pv11.png)

Gå till Experience Events på panelen Profilvisningsprogram. Du kan se de två produkterna som du har visat tidigare på panelen Profilvisningsprogram. Båda dessa händelser är nu också anslutna till din&quot;kända&quot; profil.

![Demo](../module2/images/pv12.png)

Du har nu importerat data till Adobe Experience Platform och du har länkat dessa data till identifierare som ECID och e-postadresser. Målet med detta är att förstå affärssammanhanget för det ni ska göra. I nästa övning kommer du att börja konfigurera allt du behöver för att göra all den dataimporten möjlig.

Nästa steg: [2.2 Konfigurera scheman och ange identifierare](./ex2.md)

[Gå tillbaka till modul 2](./data-ingestion.md)

[Gå tillbaka till Alla moduler](../../overview.md)
