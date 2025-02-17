---
title: Uppdatera ditt konfigurations-ID och testa din resa
description: Uppdatera ditt konfigurations-ID och testa din resa
kt: 5342
doc-type: tutorial
exl-id: da018975-7421-4d70-b04d-ad8b0597f460
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '631'
ht-degree: 0%

---

# 3.1.3 Uppdatera din datainsamlingsegenskap och testa din resa

## 3.1.3.1 Uppdatera egenskapen för datainsamling

Gå till [Adobe Experience Platform Data Collection](https://experience.adobe.com/launch/) och välj **Taggar**.

![Sidan Egenskaper](./../../../../modules/delivery-activation/datacollection/dc1.1/images/launch1.png)

I **Komma igång** skapade Demo System två klientegenskaper åt dig: en för webbplatsen och en för mobilappen. Sök efter dem genom att söka efter `--aepUserLdap--` i rutan **[!UICONTROL Search]**. Klicka för att öppna egenskapen **Webb**.

![Sökruta](./../../../../modules/delivery-activation/datacollection/dc1.1/images/property6.png)

Då ser du det här.

![Starta installationsprogrammet](./images/rule1.png)

Gå till **Regler** på den vänstra menyn och sök efter regeln **Skapa konto**. Klicka på regeln **Skapa konto** för att öppna den.

![Starta installationsprogrammet](./images/rule2.png)

Då ser du detaljerna om den här regeln. Klicka för att öppna åtgärden **Skicka händelse för registrering**.

![Starta installationsprogrammet](./images/rule3.png)

Du kommer då att se att när den här åtgärden utlöses används ett specifikt dataelement för att definiera XDM-datastrukturen. Du måste uppdatera det dataelementet, och du måste definiera **händelse-ID** för händelsen som du konfigurerade i [övning 3.1.1](./ex1.md).

![Starta installationsprogrammet](./images/rule4.png)

Du måste nu uppdatera dataelementet **XDM - registreringshändelse**. Gå till **Dataelement** om du vill göra det. Sök efter **XDM - registrering** och klicka för att öppna det dataelementet.

![Starta installationsprogrammet](./images/rule5.png)

Då ser du det här:

![Starta installationsprogrammet](./images/rule6.png)

Navigera till fältet `_experience.campaign.orchestration.eventID`. Ta bort det aktuella värdet och klistra in ditt eventID där.

Händelse-ID:t finns i Adobe Journey Optimizer under **Konfigurationer > Händelser** och du hittar händelse-ID:t i exempelnyttolasten för din jämna, som ser ut så här: `"eventID": "5ae9b8d3f68eb555502b0c07d03ef71780600c4bd0373a4065c692ae0bfbd34d"`.

![ACOP](./images/payloadeventID.png)

När du har klistrat in ditt eventID bör skärmen se ut så här. Klicka sedan på **Spara** eller **Spara i bibliotek**.

![Starta installationsprogrammet](./images/rule7.png)

Slutligen måste du publicera ändringarna. Gå till **Publiceringsflöde** på den vänstra menyn och klicka för att öppna ditt **huvudbibliotek**.

![Starta installationsprogrammet](./images/rule8.png)

Klicka på **Lägg till alla ändrade resurser** och sedan på **Spara och skapa i utveckling**.

![Starta installationsprogrammet](./images/rule9.png)

Biblioteket uppdateras sedan och efter 1-2 minuter kan du testa konfigurationen.

## 3.1.3.2 Testa din resa

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

![Demo](./../../../../modules/delivery-activation/datacollection/dc1.2/images/pv1.png)

Ta en titt på panelen Profilvisningsprogram och kundprofilen i realtid med **Experience Cloud-id** som primär identifierare för den okända kunden. Klicka på **Logga in**.

![Demo](./../../../../modules/delivery-activation/datacollection/dc1.2/images/pv2.png)

Klicka på **SKAPA ETT KONTO**.

![Demo](./../../../../modules/delivery-activation/datacollection/dc1.2/images/pv9.png)

Fyll i dina uppgifter och klicka på **Registrera**. Sedan dirigeras du om till föregående sida.

![Demo](./../../../../modules/delivery-activation/datacollection/dc1.2/images/pv10.png)

Öppna profilvisarpanelen och gå till kundprofilen i realtid. På panelen Profilvisningsprogram ska du se alla dina personuppgifter visas, som dina nya e-post- och telefonidentifierare.

![Demo](./../../../../modules/delivery-activation/datacollection/dc1.2/images/pv11.png)

1 minut efter att du har skapat ditt konto får du ett e-postmeddelande från Adobe Journey Optimizer om att du har skapat kontot.

![Starta installationsprogrammet](./images/email.png)

Du kommer också att se hur resan fortskrider i Journey Optimizer.

![Starta installationsprogrammet](./images/emaildash.png)

## Nästa steg

Gå till [Sammanfattning och förmåner](./summary.md){target="_blank"}

Gå tillbaka till [Adobe Journey Optimizer: Orchestration](./journey-orchestration-create-account.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../../overview.md){target="_blank"}
