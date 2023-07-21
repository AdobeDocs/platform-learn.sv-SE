---
title: Bootcamp - Journey Optimizer Create your travel
description: Bootcamp - Journey Optimizer Create your travel
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Journeys
exl-id: e4464502-60c8-4fba-a429-169b7a4516c8
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# 2.4 Testa din resa

## Kundreseflöde

Öppna ett nytt, rent, inkognitivt webbläsarfönster och gå till [https://bootcamp.aepdemo.net](https://bootcamp.aepdemo.net). Klicka **Tillåt alla**. Beroende på ditt surfbeteende i det tidigare användarflödet kommer personalisering att ske på webbplatsens hemsida.

![DSN](./images/web8a.png)

Klicka på **Profil** i skärmens övre högra hörn.

![Demo](./images/web8b.png)

Klicka **Skapa ett konto**.

![Demo](./images/pv5.png)

Fyll i alla fält i formuläret. Använd ett reellt värde för e-postadress och telefonnummer, eftersom det kommer att användas i senare övningar för att leverera e-post och SMS.

![Demo](./images/pv7a.png)

Bläddra nedåt. Du måste nu ange eventID för din anpassade händelse som du skapade i övning 2.2. Här finns den:

![ACOP](./images/payloadeventID.png)

Händelse-ID är det som måste skickas till Adobe Experience Platform för att utlösa den resa som du har skapat. Detta är eventID i det här exemplet: `19cab7852cdef99d25b6d5f1b6503da39d1f486b1d585743f97ed2d1e6b6c74f`

Fyll i eventID i fältet **Händelse-ID för att skapa ditt konto** och klicka **Registrera**.

![Demo](./images/pv8a.png)

Du kommer då att se det här.

![Demo](./images/pv9.png)

Du får också det här mejlet, som är det e-postmeddelande du själv skapade som en del av övningen.

![Demo](./images/pv10a.png)

Du har nu avslutat den här övningen.

Nästa steg: [2.5 Installera och använda mobilappen](./ex5.md)

[Gå tillbaka till användarflöde 2](./uc2.md)

[Gå tillbaka till Alla moduler](../../overview.md)
