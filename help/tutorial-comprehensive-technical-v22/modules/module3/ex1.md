---
title: Foundation - kundprofil i realtid - Från okänd till känd på webbplatsen
description: Foundation - kundprofil i realtid - Från okänd till känd på webbplatsen
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: 065d79c5-8979-4992-afb1-4da47bbff74b
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 0%

---

# 3.1 Från okänd till känd på webbplatsen

## Kontext

Resan från okänd till känd är en av de viktigaste ämnena bland varumärken nuförtiden, liksom kundresan från förvärv till lojalitet.

Adobe Experience Platform spelar en mycket viktig roll på den här resan. Plattformen är hjärnan för kommunikation,&quot;upplevelsesystemet för register&quot;.

Plattform är en miljö där ordet kund är bredare än bara de kända kunderna. En okänd besökare på webbplatsen är också en kund ur plattformens perspektiv, och som sådan skickas även allt beteende som en okänd besökare till Platform. Tack vare den metoden kan ett varumärke, när besökaren till slut blir en känd kund, även visualisera det som hände före det ögonblicket. Detta bidrar till att optimera attribuering och upplevelser.

## Kundreseflöde

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

![Demo](../module2/images/pv1.png)

Ta en titt på panelen Profilvisningsprogram och kundprofilen i realtid med **Experience Cloud ID** som primär identifierare för den här okända kunden.

![Demo](../module2/images/pv2.png)

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

### Navigera i mobilappen

Efter att ha blivit en känd kund är det dags att börja använda mobilappen. Öppna mobilappen på din iPhone och logga sedan in på appen.

Om du inte har installerat appen längre eller om du inte kommer ihåg hur du installerar den kan du titta här: [0.5 Använda mobilappen](../module0/ex5.md)

När du har installerat appen enligt instruktionerna ser du landningssidan för appen med Luma-märket inläst. Klicka på kontoikonen i skärmens övre vänstra del.

![Demo](./images/app_hp.png)

På inloggningsskärmen loggar du in med den e-postadress du använde på datorwebbplatsen. Klicka **Inloggning**.

![Demo](./images/app_acc.png)

Gå till appens startskärm och klicka för att öppna valfri produkt.

![Demo](./images/app_hp.png)

Då visas informationssidan för produkten.

![Demo](./images/app_carst.png)

Gå till startskärmen i appen och svep åt vänster på skärmen för att visa panelen Profilvisningsprogram. Du kommer då att se produkten du just visade i **Experience Events** tillsammans med alla produktvyer från webbplatssessionen tidigare.

![Demo](./images/app_after_carst.png)

Gå tillbaka till din stationära dator och uppdatera hemsidan. Sedan visas produkten också där.

![Demo](./images/lb_x_aftermobile.png)

Du har nu importerat data till Adobe Experience Platform och du har länkat dessa data till identifierare som ECID och e-postadresser. Målet med den här övningen var att förstå affärskontexten för det du ska göra. Ni har nu effektivt byggt upp en kundprofil för olika enheter i realtid. I nästa övning ska du visualisera din profil i Adobe Experience Platform.

Nästa steg: [3.2 Visualisera din egen kundprofil i realtid - användargränssnitt](./ex2.md)

[Gå tillbaka till modul 3](./real-time-customer-profile.md)

[Gå tillbaka till Alla moduler](../../overview.md)
