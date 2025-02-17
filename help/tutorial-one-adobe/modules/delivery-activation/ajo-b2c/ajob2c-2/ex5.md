---
title: Adobe Journey Optimizer - Externa datakällor och anpassade åtgärder
description: Adobe Journey Optimizer - Externa datakällor och anpassade åtgärder
kt: 5342
doc-type: tutorial
exl-id: 5c8cbec6-58c1-4992-a0c7-1a2b7c34e5b6
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 0%

---

# 3.2.5 Utlösa din resa

I den här övningen ska du testa och utlösa den resa du konfigurerade i den här modulen.

## 3.2.5.1 Uppdatera konfigurationen för geofence-händelsen

Gå till [Adobe Experience Platform Data Collection](https://experience.adobe.com/launch/) och välj **Taggar**.

Det här är egenskapssidan för Adobe Experience Platform Data Collection som du såg tidigare.

![Sidan Egenskaper](./../../../../modules/delivery-activation/datacollection/dc1.1/images/launch1.png)

I **Komma igång** skapade Demo System två klientegenskaper åt dig: en för webbplatsen och en för mobilappen. Sök efter dem genom att söka efter `--aepUserLdap--` i rutan **[!UICONTROL Search]**. Klicka för att öppna egenskapen **Webb**.

![Sökruta](./../../../../modules/delivery-activation/datacollection/dc1.1/images/property6.png)

Då ser du det här.

![Starta installationsprogrammet](./images/rule1.png)

Gå till **Regler** på den vänstra menyn och sök efter regeln **Geofence-händelse**. Klicka på regeln **Geofence-händelse** för att öppna den.

![Starta installationsprogrammet](./images/rule2.png)

Då ser du detaljerna om den här regeln. Klicka för att öppna åtgärden **Adobe Experience Platform Web SDK - skicka händelse**.

![Starta installationsprogrammet](./images/rule3.png)

Du kommer då att se att när den här åtgärden utlöses används ett specifikt dataelement för att definiera XDM-datastrukturen. Du måste uppdatera det dataelementet och du måste definiera **händelse-ID** för händelsen som du konfigurerade i [Exercise 3.2.1](./ex1.md).

![Starta installationsprogrammet](./images/rule4.png)

Du måste nu uppdatera dataelementet **XDM - Geofence-händelse**. Gå till **Dataelement** om du vill göra det. Sök efter **XDM - Geofence Event** och öppna dataelementet genom att klicka.

![Starta installationsprogrammet](./images/rule5.png)

Då ser du det här:

![Starta installationsprogrammet](./images/rule6.png)

Navigera till fältet `_experience.campaign.orchestration.eventID`. Ta bort det aktuella värdet och klistra in ditt eventID där.

Händelse-ID:t finns i Adobe Journey Optimizer under **Konfigurationer > Händelser** och du hittar händelse-ID:t i exempelnyttolasten för din jämna, som ser ut så här: `"eventID": "4df8dc10731eba7b0c37af83a9db38d4de7aa6aebcce38196d9d47929b9c598e"`.

![ACOP](./images/payloadeventID.png)

Därefter bör du definiera din stad i det här dataelementet. Gå till **placeContext > geo > city** och ange en valfri ort. Klicka sedan på **Spara** eller **Spara i bibliotek**.

![ACOP](./images/payloadeventIDgeo.png)

Slutligen måste du publicera ändringarna. Gå till **Publiceringsflöde** på den vänstra menyn och klicka på **Man** för att öppna biblioteket.

![Starta installationsprogrammet](./images/rule8.png)

Klicka på **Lägg till alla ändrade resurser** och sedan på **Spara och skapa i utveckling**.

![Starta installationsprogrammet](./images/rule9.png)

## 3.2.5.2 Utlösa din resa

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

Öppna profilvisarpanelen och gå till kundprofilen i realtid. På panelen Profilvisningsprogram ska du se alla dina personuppgifter visas, som dina nya e-post- och telefonidentifierare.

![Demo](./images/pv2.png)

Klicka på **VERKTYG** på panelen Profilvisningsprogram. Ange `geofenceevent` och klicka på **Skicka**.

>[!NOTE]
>
>Om du inte har möjlighet att skicka en direktanropshändelse på panelen Profilvisningsprogram kan du skicka en händelse manuellt genom att öppna utvecklarvyn i din webbläsare och gå till **Konsol** och sedan klistra in och skicka det här kommandot: `_satellite.track('geofenceevent')`.

Några sekunder senare visas meddelandet från Adobe Journey Optimizer i Slack-kanalen.

![Demo](./images/smsdemo4.png)

## Nästa steg

Gå till [Sammanfattning och förmåner](./summary.md){target="_blank"}

Gå tillbaka till [Adobe Journey Optimizer: Externa datakällor och anpassade åtgärder](journey-orchestration-external-weather-api-sms.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../../overview.md){target="_blank"}
