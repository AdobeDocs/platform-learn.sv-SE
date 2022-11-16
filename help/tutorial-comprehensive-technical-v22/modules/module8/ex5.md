---
title: Adobe Journey Optimizer - External Weather API, SMS Action med mera - Trigga din orkestrerade kundresa
description: Adobe Journey Optimizer - External Weather API, SMS Action med mera - Trigga din orkestrerade kundresa
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 4d92877d-8fdc-4902-ad32-7fa068bc1395
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---

# 8.5 Utlösa din resa

I den här övningen ska du testa och utlösa den resa du konfigurerade i den här modulen.

## 8.5.1 Uppdatera konfigurationen för geofence-händelsen

Gå till [Adobe Experience Platform Data Collection](https://experience.adobe.com/launch/) och markera **Taggar**.

Det här är egenskapssidan för Adobe Experience Platform Data Collection som du såg tidigare.

![Egenskapssida](../module1/images/launch1.png)

I modul 0 skapade Demo System två klientegenskaper: en för webbplatsen och en för mobilappen. Hitta dem genom att söka efter `--demoProfileLdap--` i **[!UICONTROL Sök]** box. Klicka för att öppna **Webb** -egenskap.

![Sökruta](../module1/images/property6.png)

Du kommer då att se det här.

![Starta installationen](./images/rule1.png)

Gå till den vänstra menyn **Regler** och söka efter regeln **Geofence-händelse**. Klicka på regeln **Geofence-händelse** för att öppna den.

![Starta installationen](./images/rule2.png)

Då ser du detaljerna om den här regeln. Klicka för att öppna funktionsmakrot **Skicka &quot;geofence event&quot; till AEP - utlösande JO**.

![Starta installationen](./images/rule3.png)

Du kommer då att se att när den här åtgärden utlöses används ett specifikt dataelement för att definiera XDM-datastrukturen. Du måste uppdatera det dataelementet och definiera **Händelse-ID** av händelsen som du konfigurerade i [Utövning 8.1](./ex1.md).

![Starta installationen](./images/rule4.png)

Du måste nu uppdatera dataelementet **XDM - Geofence-händelse**. Om du vill göra det går du till **Dataelement**. Sök efter **XDM - Geofence-händelse** och klicka för att öppna det dataelementet.

![Starta installationen](./images/rule5.png)

Då ser du det här:

![Starta installationen](./images/rule6.png)

Navigera till fältet `_experience.campaign.orchestration.eventID`. Ta bort det aktuella värdet och klistra in ditt eventID där.

Händelse-ID:t finns i Adobe Journey Optimizer under **Konfigurationer > Händelser** och du hittar händelse-ID:t i exempelnyttolasten för din even, som ser ut så här: `"eventID": "fa42ab7982ba55f039eacec24c1e32e5c51b310c67f0fa559ab49b89b63f4934"`.

![ACOP](./images/payloadeventID.png)

Därefter bör du definiera din stad i det här dataelementet. Gå till **placeContext > geo > city** och ange en valfri ort. Klicka på **Spara** eller **Spara i bibliotek**.

![ACOP](./images/payloadeventIDgeo.png)

Slutligen måste du publicera ändringarna. Gå till **Publiceringsflöde** i den vänstra menyn.

![Starta installationen](./images/rule8.png)

Klicka **Lägg till alla ändrade resurser** och sedan klicka **Spara och bygg till utveckling**.

![Starta installationen](./images/rule9.png)

## 8.5.2 Utlösa din resa

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

Gå till sidan Register/Login. Klicka **SKAPA ETT KONTO**.

![Demo](../module2/images/pv9.png)

Fyll i detaljerna och klicka **Registrera** därefter omdirigeras du till föregående sida.

![Demo](../module2/images/pv10.png)

Öppna profilvisarpanelen och gå till kundprofilen i realtid. På panelen Profilvisningsprogram ska du se alla dina personuppgifter visas, som dina nya e-post- och telefonidentifierare.

![Demo](../module2/images/pv11.png)

På profilvisarpanelen klickar du på **VERKSAMHET**. Retur `geofenceevent` och klicka **Skicka**.

![Demo](./images/smsdemo1.png)

Några sekunder senare får du ett SMS från Adobe Journey Optimizer.

![Demo](./images/smsdemo4.png)

Nästa steg: [Sammanfattning och fördelar](./summary.md)

[Gå tillbaka till modul 8](journey-orchestration-external-weather-api-sms.md)

[Gå tillbaka till Alla moduler](../../overview.md)
