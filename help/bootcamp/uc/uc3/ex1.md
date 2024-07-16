---
title: Bootcamp - Blanda fysiska och digitala - Använd mobilappen och utlösa ett fyr-inträde
description: Bootcamp - Blanda fysiska och digitala - Använd mobilappen och utlösa ett fyr-inträde
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Mobile SDK
exl-id: c33c973b-db8a-49ce-bd6c-a6c4fbe579a0
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---

# 3.1 Använda mobilappen och utlösa en fyndighetsinmatning

## Installera mobilappen

Innan du installerar appen måste du aktivera **spårning** på din iOS-enhet. Det gör du genom att gå till **Inställningar** > **Sekretess och säkerhet** > **Spårning** och se till att alternativet **Tillåt appar att begära spårning**.

![DSN](./../uc3/images/app4.png)

Gå till Apple App Store och sök efter `aepmobile-bootcamp`. Klicka på **Installera** eller **Hämta**.

![DSN](./../uc3/images/app1.png)

När appen har installerats klickar du på **Öppna**.

![DSN](./../uc3/images/app2.png)

Klicka på **OK**.

![DSN](./../uc3/images/app9.png)

Klicka på **Tillåt**.

![DSN](./../uc3/images/app3.png)

Klicka på **Jag godkänner**.

![DSN](./../uc3/images/app7.png)

Klicka på **Tillåt när appen används**.

![DSN](./../uc3/images/app8.png)

Klicka på **Tillåt**.

![DSN](./../uc3/images/app5.png)

Du är nu med i appen, på hemsidan, redo att gå igenom kundresan.

![DSN](./../uc3/images/app12.png)

## Kundreseflöde

Först och främst måste du logga in. Klicka på **Logga in**.

![DSN](./images/app13.png)

När du skapat ditt konto i de tidigare övningarna såg du detta på webbplatsen. Du måste nu återanvända e-postadressen för kontot som du skapade i appen för att logga in.

![Demo](./images/pv1.png)

Ange den e-postadress som du använde på webbplatsen här och klicka på **Logga in**.

![DSN](./images/app14.png)

Du får sedan en bekräftelse på att du är inloggad och du får ett push-meddelande.

![DSN](./images/app15.png)

Gå tillbaka till startsidan i appen så visas fler funktioner.

![DSN](./images/app17.png)

Gå först till **Produkter**. Klicka på en produkt, i det här exemplet **Kaffe för att gå**.

![DSN](./images/app19.png)

Produktsidan **Kaffe för att gå** visas i appen.

![DSN](./images/app20.png)

Du simulerar nu en händelse för att lägga in en signal i en offlinebutik. Målet med att simulera detta är att personalisera kundupplevelsen på butiksskärmar. För att visualisera butiksupplevelsen har en sida skapats som dynamiskt visar den information som är relevant för kunden som just har kommit in i butiken.

Öppna den här webbsidan på datorn innan du fortsätter: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html)

Då ser du det här:

![DSN](./images/screen1.png)

Gå sedan tillbaka till hemsidan. Klicka på ikonen **fyr** .

![DSN](./images/app23.png)

Då ser du det här. Välj först **Bootlägers skärmfyr** och klicka sedan på knappen **post** . På så sätt kan du simulera ett fynd.

![DSN](./images/app21.png)

Titta nu på butiksskärmen. Där visas den senaste produkten du visade inom fem sekunder.

![DSN](./images/screen2.png)

Gå sedan tillbaka till **Produkter**. Klicka på en produkt, i det här exemplet **Beach filet Tan**.

![DSN](./images/app22.png)

Gå sedan tillbaka till hemsidan. Klicka på ikonen **fyr** .

![DSN](./images/app23.png)

Då ser du det här. Välj först **Beacon för startlägets skärm** och klicka sedan på knappen **post** igen. På så sätt kan du simulera ett fynd.

![DSN](./images/app21.png)

Titta nu på butiksskärmen igen. Där visas den senaste produkten du visade inom fem sekunder.

![DSN](./images/screen3.png)

Nu ska vi också titta på din profilvisare på webbplatsen. Där finns många händelser som lagts till för att visa att all interaktion med en kund samlas in och lagras i Adobe Experience Platform.

![DSN](./images/screen4.png)

I nästa övning kommer du att konfigurera och testa din egen neoningresa.

Nästa steg: [3.2 Skapa din aktivitet](./ex2.md)

[Gå tillbaka till användarflöde 3](./uc3.md)

[Gå tillbaka till Alla moduler](../../overview.md)
