---
title: Bootcamp - Blanda fysiska och digitala - Använd mobilappen och utlösa ett fyr-inträde
description: Bootcamp - Blanda fysiska och digitala - Använd mobilappen och utlösa ett fyr-inträde
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: c33c973b-db8a-49ce-bd6c-a6c4fbe579a0
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 0%

---

# 3.1 Använda mobilappen och utlösa en fyndighetsinmatning

## Installera mobilappen

Innan du installerar programmet måste du aktivera **Spårning** på din iOS-enhet. Om du vill göra det går du till **Inställningar** > **Integritet och säkerhet** > **Spårning** och se till att alternativet **Tillåt att appar begär att spåras**.

![DSN](./../uc3/images/app4.png)

Gå till Apple App Store och sök efter `aepmobile-bootcamp`. Klicka **Installera** eller **Hämta**.

![DSN](./../uc3/images/app1.png)

När appen är installerad klickar du på **Öppna**.

![DSN](./../uc3/images/app2.png)

Klicka **OK**.

![DSN](./../uc3/images/app9.png)

Klicka **Tillåt**.

![DSN](./../uc3/images/app3.png)

Klicka **Jag håller med**.

![DSN](./../uc3/images/app7.png)

Klicka **Tillåt när appen används**.

![DSN](./../uc3/images/app8.png)

Klicka **Tillåt**.

![DSN](./../uc3/images/app5.png)

Du är nu med i appen, på hemsidan, redo att gå igenom kundresan.

![DSN](./../uc3/images/app12.png)

## Kundreseflöde

Först och främst måste du logga in. Klicka **Inloggning**.

![DSN](./images/app13.png)

När du skapat ditt konto i de tidigare övningarna såg du detta på webbplatsen. Du måste nu återanvända e-postadressen för kontot som du skapade i appen för att logga in.

![Demo](./images/pv1.png)

Ange den e-postadress du använde på webbplatsen här och klicka på **Inloggning**.

![DSN](./images/app14.png)

Du får då en bekräftelse på att du är inloggad och du får ett push-meddelande.

![DSN](./images/app15.png)

Gå tillbaka till startsidan i appen så visas fler funktioner.

![DSN](./images/app17.png)

Först, gå till **Produkter**. Klicka på valfri produkt, i det här exemplet **Kaffe att gå**.

![DSN](./images/app19.png)

Du kommer att se **Kaffe att gå** produktsida i appen.

![DSN](./images/app20.png)

Du simulerar nu en händelse för att lägga in en signal i en offlinebutik. Målet med att simulera detta är att personalisera kundupplevelsen på butiksskärmar. För att visualisera butiksupplevelsen har en sida skapats som dynamiskt visar den information som är relevant för kunden som just har kommit in i butiken.

Öppna den här webbsidan på datorn innan du fortsätter: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html)

Då ser du det här:

![DSN](./images/screen1.png)

Gå sedan tillbaka till hemsidan. Klicka på **beacon** ikon.

![DSN](./images/app23.png)

Du kommer då att se det här. Välj först **Bootcamp Screen Beacon** och klicka sedan på **entry** -knappen. På så sätt kan du simulera ett fynd.

![DSN](./images/app21.png)

Titta nu på butiksskärmen. Där visas den senaste produkten du visade inom fem sekunder.

![DSN](./images/screen2.png)

Gå sedan tillbaka till **Produkter**. Klicka på valfri produkt, i det här exemplet **Strandfilt Tan**.

![DSN](./images/app22.png)

Gå sedan tillbaka till hemsidan. Klicka på **beacon** ikon.

![DSN](./images/app23.png)

Du kommer då att se det här. Välj först **Bootcamp Screen Beacon** och klicka sedan på **entry** igen. På så sätt kan du simulera ett fynd.

![DSN](./images/app21.png)

Titta nu på butiksskärmen igen. Där visas den senaste produkten du visade inom fem sekunder.

![DSN](./images/screen3.png)

Nu ska vi också titta på din profilvisare på webbplatsen. Där finns många händelser som lagts till för att visa att all interaktion med en kund samlas in och lagras i Adobe Experience Platform.

![DSN](./images/screen4.png)

I nästa övning kommer du att konfigurera och testa din egen neoningresa.

Nästa steg: [3.2 Skapa en aktivitet](./ex2.md)

[Gå tillbaka till användarflöde 3](./uc3.md)

[Gå tillbaka till Alla moduler](../../overview.md)
