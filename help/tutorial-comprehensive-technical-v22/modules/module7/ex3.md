---
title: Modul 7 Uppdatera ditt konfigurations-ID och testa din resa
description: Uppdatera ditt konfigurations-ID och testa din resa
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
exl-id: d3ceb676-d7f5-4f52-85a4-deaa5ef24034
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 0%

---

# 7.3 Uppdatera din datainsamlingsegenskap och testa din resa

## 7.3.1 Uppdatera din datainsamlingsegenskap

Gå till [Adobe Experience Platform Data Collection](https://experience.adobe.com/launch/) och markera **Taggar**.

Det här är egenskapssidan för Adobe Experience Platform Data Collection som du såg tidigare.

![Egenskapssida](../module1/images/launch1.png)

I modul 0 skapade Demo System två klientegenskaper: en för webbplatsen och en för mobilappen. Hitta dem genom att söka efter `--demoProfileLdap--` i **[!UICONTROL Sök]** box. Klicka för att öppna **Webb** -egenskap.

![Sökruta](../module1/images/property6.png)

Du kommer då att se det här.

![Starta installationen](./images/rule1.png)

Gå till den vänstra menyn **Regler** och söka efter regeln **Registrera profil**. Klicka på regeln **Registrera profil** för att öppna den.

![Starta installationen](./images/rule2.png)

Då ser du detaljerna om den här regeln. Klicka för att öppna funktionsmakrot **Skicka&quot;Registreringshändelse&quot; till AEP - utlösande JO**.

![Starta installationen](./images/rule3.png)

Du kommer då att se att när den här åtgärden utlöses används ett specifikt dataelement för att definiera XDM-datastrukturen. Du måste uppdatera det dataelementet och definiera **Händelse-ID** av händelsen som du konfigurerade i [Utövning 7.1](./ex1.md).

![Starta installationen](./images/rule4.png)

Du måste nu uppdatera dataelementet **XDM - Registreringshändelse**. Om du vill göra det går du till **Dataelement**. Sök efter **XDM - Registreringshändelse** och klicka för att öppna det dataelementet.

![Starta installationen](./images/rule5.png)

Då ser du det här:

![Starta installationen](./images/rule6.png)

Navigera till fältet `_experience.campaign.orchestration.eventID`. Ta bort det aktuella värdet och klistra in ditt eventID där.

Händelse-ID:t finns i Adobe Journey Optimizer under **Konfigurationer > Händelser** och du hittar händelse-ID:t i exempelnyttolasten för din even, som ser ut så här: `"eventID": "227402c540eb8f8855c6b2333adf6d54d7153d9d7d56fa475a6866081c574736"`.

![ACOP](./images/payloadeventID.png)

När du har klistrat in ditt eventID bör skärmen se ut så här. Klicka på **Spara** eller **Spara i bibliotek**.

![Starta installationen](./images/rule7.png)

Slutligen måste du publicera ändringarna. Gå till **Publiceringsflöde** i den vänstra menyn.

![Starta installationen](./images/rule8.png)

Klicka **Lägg till alla ändrade resurser** och sedan klicka **Spara och bygg till utveckling**.

![Starta installationen](./images/rule9.png)

Biblioteket uppdateras sedan och efter 1-2 minuter kan du testa konfigurationen.

## 7.3.2 Testa din resa

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

1 minut efter att du har skapat ditt konto får du ett e-postmeddelande från Adobe Journey Optimizer om att du har skapat kontot.

![Starta installationen](./images/email.png)

Nästa steg: [Sammanfattning och fördelar](./summary.md)

[Gå tillbaka till modul 7](./journey-orchestration-create-account.md)

[Gå tillbaka till Alla moduler](../../overview.md)
