---
title: Bootcamp - Mixing physical and digital - Test your travel - Brazil
description: Bootcamp - Mixing physical and digital - Test your travel - Brazil
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
source-git-commit: 75a878ba596078e6d013b65062606931402302dd
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# 3.4 Testa din resa

Om du vill testa din resa måste du använda händelse-ID:t för händelsen som du skapade i övning 3.2, som ser ut så här.

![ACOP](./images/payloadeventID.png)

Händelse-ID är det som måste skickas till Adobe Experience Platform för att utlösa resan. I det här exemplet är eventID:
`e76c0bf0c77c3517e5b6f4c457a0754ebaf5f1f6b9357d74e0d8e13ae517c3d5`.

Öppna mobilappen och gå till hemsidan. Klicka på **Inställningar** ikon.

![DSN](./images/appsett.png)

Klistra in ditt eventID i fältet **Beacon EventID** och klicka **Spara**.

![DSN](./images/beacon1.png)

Öppna den här webbsidan på datorn innan du fortsätter: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html)

Då ser du det här:

![DSN](./images/screen1.png)

Gå sedan tillbaka till hemsidan. Klicka på **beacon** ikon.

![DSN](./images/app23.png)

Du kommer då att se det här. Välj först **Bootcamp Screen Beacon** och klicka sedan på **entry** -knappen. På så sätt kan du simulera ett fynd.

![DSN](./images/app21.png)

Titta nu på butiksskärmen. Där visas den senaste produkten du visade inom fem sekunder.

![DSN](./images/beacon3.png)

Du har också fått ditt push-meddelande.

![DSN](./images/beacon2.png)

Du har nu avslutat den här övningen.

[Gå tillbaka till användarflöde 3](./uc3.md)

[Gå tillbaka till Alla moduler](../../overview.md)
