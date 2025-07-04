---
title: Foundation - kundprofil i realtid - Från okänd till känd på webbplatsen
description: Foundation - kundprofil i realtid - Från okänd till känd på webbplatsen
kt: 5342
doc-type: tutorial
exl-id: f33a7448-e1b9-47e7-97c7-509ad36cf991
source-git-commit: 2264f26a0778c2570c36abe1bae4d6a1dc3a465c
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 0%

---

# 2.1.1 Från okänd till känd på webbplatsen

## Kontext

Resan från okänd till känd är en av de viktigaste ämnena bland varumärken nuförtiden, liksom kundresan från förvärv till lojalitet.

Adobe Experience Platform spelar en mycket viktig roll på den här resan. Plattformen är hjärnan för kommunikation,&quot;upplevelsesystemet för register&quot;.

Plattform är en miljö där ordet kund är bredare än bara de kända kunderna. En okänd besökare på webbplatsen är också en kund ur plattformens perspektiv, och som sådan skickas även allt beteende som en okänd besökare till Platform. Tack vare den metoden kan ett varumärke, när besökaren till slut blir en känd kund, även visualisera det som hände före det ögonblicket. Detta bidrar till att optimera attribuering och upplevelser.

## Kundreseflöde

Gå till [https://dsn.adobe.com](https://dsn.adobe.com). När du har loggat in med din Adobe ID ser du det här. Klicka på de tre punkterna **..** i webbplatsprojektet och klicka sedan på **Kör** för att öppna det.

![DSN](./../../datacollection/dc1.1/images/web8.png)

Du kommer då att se din demowebbplats öppnas. Markera URL-adressen och kopiera den till Urklipp.

![DSN](../../../getting-started/gettingstarted/images/web3.png)

Öppna ett nytt inkognito-webbläsarfönster.

![DSN](../../../getting-started/gettingstarted/images/web4.png)

Klistra in webbadressen till demowebbplatsen, som du kopierade i föregående steg. Du ombeds sedan logga in med din Adobe ID.

![DSN](../../../getting-started/gettingstarted/images/web5.png)

Välj kontotyp och slutför inloggningsprocessen.

![DSN](../../../getting-started/gettingstarted/images/web6.png)

Därefter visas webbplatsen i ett inkognitivt webbläsarfönster. För varje övning måste du använda ett nytt, inkognitivt webbläsarfönster för att läsa in webbadressen till demowebbplatsen.

![DSN](../../../getting-started/gettingstarted/images/web7.png)

Klicka på ikonen för Adobe logotyp i det övre vänstra hörnet av skärmen för att öppna profilvisningsprogrammet.

![Demo](../../datacollection/dc1.2/images/pv1.png)

Ta en titt på panelen Profilvisningsprogram och kundprofilen i realtid med **Experience Cloud-id** som primär identifierare för den okända kunden.

![Demo](../../datacollection/dc1.2/images/pv2.png)

Ni kan också se alla upplevelsehändelser som samlats in baserat på kundens beteende. Listan är för närvarande tom, men den ändras snart.

![Demo](../../datacollection/dc1.2/images/pv3.png)

Gå till produktkategorin **Telefoner och enheter**. Klicka sedan på produkten **iPhone 16 Pro**.

![Demo](../../datacollection/dc1.2/images/pv4.png)

Då visas informationssidan för produkten. En händelse av typen **Produktvy** har nu skickats till Adobe Experience Platform med den Web SDK-implementering som du granskade i modul 1.

![Demo](../../datacollection/dc1.2/images/pv5.png)

Öppna panelen Provile Viewer och titta på dina **Events**.

![Demo](../../datacollection/dc1.2/images/pv6.png)

Gå tillbaka till kategorisidan **Telefoner och enheter** och klicka på en annan produkt. En annan Experience Event har skickats till Adobe Experience Platform. Öppna panelen Profilvisningsprogram. Nu visas två händelser av typen **Produktvy**. Beteendet är anonymt, men med rätt medgivande kan du spåra varje klick och lagra det i Adobe Experience Platform. När den anonyma kunden blir känd kan vi automatiskt sammanfoga alla anonyma beteenden med kunskapsprofilen.

Klicka på **Logga in**.

![Demo](../../datacollection/dc1.2/images/pv7.png)

Klicka på **Skapa ett konto**.

![Demo](../../datacollection/dc1.2/images/pv8.png)

Fyll i dina uppgifter och klicka på **Registrera**. Sedan dirigeras du om till föregående sida.

![Demo](../../datacollection/dc1.2/images/pv9.png)

Öppna profilvisarpanelen och gå till kundprofilen i realtid. På panelen Profilvisningsprogram ska du se alla dina personuppgifter visas, som dina nya e-post- och telefonidentifierare.

![Demo](../../datacollection/dc1.2/images/pv10.png)

Gå till Experience Events på panelen Profilvisningsprogram. Du kan se de två produkterna som du har visat tidigare på panelen Profilvisningsprogram. Båda dessa händelser är nu också anslutna till din&quot;kända&quot; profil.

![Demo](../../datacollection/dc1.2/images/pv11.png)

Du har nu importerat data till Adobe Experience Platform och du har länkat dessa data till identifierare som ECID och e-postadresser. Målet med detta är att förstå affärssammanhanget för det ni ska göra. I nästa övning kommer du att börja konfigurera allt du behöver för att göra all den dataimporten möjlig.

### Navigera i mobilappen

Efter att ha blivit en känd kund är det dags att börja använda mobilappen. Öppna mobilappen på din iPhone och logga sedan in på appen.

Om du inte har installerat appen längre eller om du inte kommer ihåg hur du installerar den kan du titta här: [Använd mobilappen](../../../getting-started/gettingstarted/ex5.md)

När du har installerat appen enligt instruktionerna ser du landningssidan för appen med Citi Signal-märket inläst. Klicka på kontoikonen i skärmens övre vänstra del.

![Demo](./images/app_hpz.png)

På inloggningsskärmen loggar du in med den e-postadress som du använde på datorwebbplatsen. Klicka på **Logga in**.

![Demo](./images/app_acc.png)

Du får då en bekräftelse på att du är inloggad.

![Demo](./images/app_acc1.png)

Gå till appens startskärm och gå till sidan **Telefoner och enheter**.

![Demo](./images/app_hp1.png)

Klicka på en produkt på sidan.

![Demo](./images/app_hp2.png)

Då visas informationssidan för produkten.

![Demo](./images/app_galaxy.png)

Gå till startskärmen i appen och klicka på ikonen Adobe för att visa profilvisningsprogrampanelen. Du kommer då att se vyn **Profilattribut**, som nu visar en kombinerad vy över din webb- och mobilappsaktivitet. Gå till **Händelser**

![Demo](./images/app_hp3.png)

Du kommer då att se produkten som du just visade i avsnittet **Experience Events**, tillsammans med alla produktvyer från webbplatssessionen tidigare.

>[!NOTE]
>
>Det kan ta några minuter innan du ser den konsoliderade vyn i appen och på webbplatsen.

![Demo](./images/app_after_galaxy.png)

Gå tillbaka till din stationära dator och uppdatera hemsidan. Sedan visas produkten också där.

>[!NOTE]
>
>Det kan ta några minuter innan du ser den konsoliderade vyn i appen och på webbplatsen.

![Demo](./images/web_x_aftermobile.png)

Du har nu importerat data till Adobe Experience Platform och du har länkat dessa data till identifierare som ECID och e-postadresser. Målet med den här övningen var att förstå affärskontexten för det du ska göra. Ni har nu effektivt byggt upp en kundprofil för olika enheter i realtid. I nästa övning ska du visualisera din profil i Adobe Experience Platform.

## Nästa steg

Gå till [2.1.2 Visa din egen kundprofil i realtid - användargränssnitt](./ex2.md){target="_blank"}

Gå tillbaka till [Kundprofil i realtid](./real-time-customer-profile.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../../overview.md){target="_blank"}
