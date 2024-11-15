---
title: Adobe Journey Optimizer - External Weather API, SMS Action med mera - Trigga din orkestrerade kundresa
description: Adobe Journey Optimizer - External Weather API, SMS Action med mera - Trigga din orkestrerade kundresa
kt: 5342
doc-type: tutorial
exl-id: 068c8be4-2e9e-4d38-9c0e-f769ac927b57
source-git-commit: 0dbcda0cfc9f199a44c845c1b5caf00a8d740251
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 0%

---

# 3.2.5 Utlösa din resa

I den här övningen ska du testa och utlösa den resa du konfigurerade i den här modulen.

## 3.2.5.1 Uppdatera konfigurationen för geofence-händelsen

Gå till [Adobe Experience Platform Data Collection](https://experience.adobe.com/launch/) och välj **Taggar**.

Det här är egenskapssidan för Adobe Experience Platform Data Collection som du såg tidigare.

![Sidan Egenskaper](./../../../modules/datacollection/module1.1/images/launch1.png)

I modul 0 skapade Demo System två klientegenskaper åt dig: en för webbplatsen och en för mobilappen. Sök efter dem genom att söka efter `--aepUserLdap--` i rutan **[!UICONTROL Search]**. Klicka för att öppna egenskapen **Webb**.

![Sökruta](./../../../modules/datacollection/module1.1/images/property6.png)

Då ser du det här.

![Starta installationsprogrammet](./images/rule1.png)

Gå till **Regler** på den vänstra menyn och sök efter regeln **Geofence-händelse**. Klicka på regeln **Geofence-händelse** för att öppna den.

![Starta installationsprogrammet](./images/rule2.png)

Då ser du detaljerna om den här regeln. Klicka för att öppna åtgärden **Skicka&quot;geofence-händelse&quot; till AEP - utlösa JO**.

![Starta installationsprogrammet](./images/rule3.png)

Du kommer då att se att när den här åtgärden utlöses används ett specifikt dataelement för att definiera XDM-datastrukturen. Du måste uppdatera det dataelementet och du måste definiera **händelse-ID** för händelsen som du konfigurerade i [övning 8.1](./ex1.md).

![Starta installationsprogrammet](./images/rule4.png)

Du måste nu uppdatera dataelementet **XDM - Geofence-händelse**. Gå till **Dataelement** om du vill göra det. Sök efter **XDM - Geofence Event** och öppna dataelementet genom att klicka.

![Starta installationsprogrammet](./images/rule5.png)

Då ser du det här:

![Starta installationsprogrammet](./images/rule6.png)

Navigera till fältet `_experience.campaign.orchestration.eventID`. Ta bort det aktuella värdet och klistra in ditt eventID där.

Händelse-ID:t finns i Adobe Journey Optimizer under **Konfigurationer > Händelser** och du hittar händelse-ID:t i exempelnyttolasten för din jämna, som ser ut så här: `"eventID": "fa42ab7982ba55f039eacec24c1e32e5c51b310c67f0fa559ab49b89b63f4934"`.

![ACOP](./images/payloadeventID.png)

Därefter bör du definiera din stad i det här dataelementet. Gå till **placeContext > geo > city** och ange en valfri ort. Klicka sedan på **Spara** eller **Spara i bibliotek**.

![ACOP](./images/payloadeventIDgeo.png)

Slutligen måste du publicera ändringarna. Gå till **Publiceringsflöde** på den vänstra menyn.

![Starta installationsprogrammet](./images/rule8.png)

Klicka på **Lägg till alla ändrade resurser** och sedan på **Spara och skapa i utveckling**.

![Starta installationsprogrammet](./images/rule9.png)

## 3.2.5.2 Utlösa din resa

Gå till [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). När du har loggat in med din Adobe ID ser du det här. Klicka på webbplatsprojektet för att öppna det.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web8.png)

Du kommer då att se din demowebbplats öppnas. Markera URL-adressen och kopiera den till Urklipp.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web3.png)

Öppna ett nytt inkognito-webbläsarfönster.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web4.png)

Klistra in webbadressen till demowebbplatsen, som du kopierade i föregående steg. Du ombeds sedan logga in med din Adobe ID.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web5.png)

Välj kontotyp och slutför inloggningsprocessen.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web6.png)

Därefter visas webbplatsen i ett inkognitivt webbläsarfönster. För varje demonstration måste du använda ett nytt, inkognitivt webbläsarfönster för att läsa in webbadressen till demowebbplatsen.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web7.png)

Klicka på logotypikonen för Adobe i det övre vänstra hörnet av skärmen för att öppna profilvisningsprogrammet.

![Demo](./../../../modules/datacollection/module1.2/images/pv1.png)

Ta en titt på panelen Profilvisningsprogram och kundprofilen i realtid med **Experience Cloud ID** som primär identifierare för den okända kunden.

![Demo](./../../../modules/datacollection/module1.2/images/pv2.png)

Gå till sidan Register/Login. Klicka på **SKAPA ETT KONTO**.

![Demo](./../../../modules/datacollection/module1.2/images/pv9.png)

Fyll i dina uppgifter och klicka på **Registrera**. Sedan dirigeras du om till föregående sida.

![Demo](./../../../modules/datacollection/module1.2/images/pv10.png)

Öppna profilvisarpanelen och gå till kundprofilen i realtid. På panelen Profilvisningsprogram ska du se alla dina personuppgifter visas, som dina nya e-post- och telefonidentifierare.

![Demo](./../../../modules/datacollection/module1.2/images/pv11.png)

Klicka på **VERKTYG** på panelen Profilvisningsprogram. Ange `geofenceevent` och klicka på **Skicka**.

![Demo](./images/smsdemo1.png)

Några sekunder senare får du ett SMS från Adobe Journey Optimizer.

![Demo](./images/smsdemo4.png)

Nästa steg: [Sammanfattning och förmåner](./summary.md)

[Gå tillbaka till modul 3.2](journey-orchestration-external-weather-api-sms.md)

[Gå tillbaka till Alla moduler](../../../overview.md)
