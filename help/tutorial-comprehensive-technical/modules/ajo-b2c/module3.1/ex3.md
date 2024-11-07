---
title: Uppdatera ditt konfigurations-ID och testa din resa
description: Uppdatera ditt konfigurations-ID och testa din resa
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 0%

---

# 3.1.3 Uppdatera din datainsamlingsegenskap och testa din resa

## 3.1.3.1 Uppdatera egenskapen för datainsamling

Gå till [Adobe Experience Platform Data Collection](https://experience.adobe.com/launch/) och välj **Taggar**.

Det här är egenskapssidan för Adobe Experience Platform Data Collection som du såg tidigare.

![Sidan Egenskaper](./../../../modules/datacollection/module1.1/images/launch1.png)

I modul 0 skapade Demo System två klientegenskaper åt dig: en för webbplatsen och en för mobilappen. Sök efter dem genom att söka efter `--aepUserLdap--` i rutan **[!UICONTROL Search]**. Klicka för att öppna egenskapen **Webb**.

![Sökruta](./../../../modules/datacollection/module1.1/images/property6.png)

Då ser du det här.

![Starta installationsprogrammet](./images/rule1.png)

Gå till **Regler** på den vänstra menyn och sök efter regeln **Registrera profil**. Klicka på regeln **Registrera profil** för att öppna den.

![Starta installationsprogrammet](./images/rule2.png)

Då ser du detaljerna om den här regeln. Klicka för att öppna åtgärden **Skicka&quot;Registreringshändelse&quot; till AEP - utlösa JO**.

![Starta installationsprogrammet](./images/rule3.png)

Du kommer då att se att när den här åtgärden utlöses används ett specifikt dataelement för att definiera XDM-datastrukturen. Du måste uppdatera det dataelementet och du måste definiera **händelse-ID** för händelsen som du konfigurerade i [övning 7.1](./ex1.md).

![Starta installationsprogrammet](./images/rule4.png)

Du måste nu uppdatera dataelementet **XDM - registreringshändelse**. Gå till **Dataelement** om du vill göra det. Sök efter **XDM - Registreringshändelse** och klicka för att öppna det dataelementet.

![Starta installationsprogrammet](./images/rule5.png)

Då ser du det här:

![Starta installationsprogrammet](./images/rule6.png)

Navigera till fältet `_experience.campaign.orchestration.eventID`. Ta bort det aktuella värdet och klistra in ditt eventID där.

Händelse-ID:t finns i Adobe Journey Optimizer under **Konfigurationer > Händelser** och du hittar händelse-ID:t i exempelnyttolasten för din jämna, som ser ut så här: `"eventID": "227402c540eb8f8855c6b2333adf6d54d7153d9d7d56fa475a6866081c574736"`.

![ACOP](./images/payloadeventID.png)

När du har klistrat in ditt eventID bör skärmen se ut så här. Klicka sedan på **Spara** eller **Spara i bibliotek**.

![Starta installationsprogrammet](./images/rule7.png)

Slutligen måste du publicera ändringarna. Gå till **Publiceringsflöde** på den vänstra menyn.

![Starta installationsprogrammet](./images/rule8.png)

Klicka på **Lägg till alla ändrade resurser** och sedan på **Spara och skapa i utveckling**.

![Starta installationsprogrammet](./images/rule9.png)

Biblioteket uppdateras sedan och efter 1-2 minuter kan du testa konfigurationen.

## 3.1.3.2 Testa din resa

Gå till [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). När du har loggat in med din Adobe ID ser du det här. Klicka på webbplatsprojektet för att öppna det.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web8.png)

Klicka på **Kör** på sidan **Screens**.

![DSN](./../../../modules/datacollection/module1.1/images/web2.png)

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

1 minut efter att du har skapat ditt konto får du ett e-postmeddelande från Adobe Journey Optimizer om att du har skapat kontot.

![Starta installationsprogrammet](./images/email.png)

Nästa steg: [Sammanfattning och förmåner](./summary.md)

[Gå tillbaka till modul 3.1](./journey-orchestration-create-account.md)

[Gå tillbaka till Alla moduler](../../../overview.md)
