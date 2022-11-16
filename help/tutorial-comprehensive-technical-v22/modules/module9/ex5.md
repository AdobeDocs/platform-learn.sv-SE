---
title: offer decisioning - Använd ditt beslut i ett e-postmeddelande
description: Använd ditt beslut i ett e-postmeddelande
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 0fb8c244-1025-479f-b82e-374d1aa5e4dc
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 0%

---

# 9.5 Använd ditt beslut i ett e-postmeddelande

I den här övningen använder du ditt beslut för att anpassa leveransen av ett e-postmeddelande och ett SMS.

Gå till **Resor**. Hitta den resa du skapade i övning 7.2, som heter `--demoProfileLdap-- - Account Creation Journey`. Klicka på resan för att öppna den.

![Journey Optimizer](./images/emailoffer1.png)

Du kommer då att se det här. Klicka **Skapa en ny version**.

![Journey Optimizer](./images/journey1.png)

Klicka **Skapa en ny version**.

![Journey Optimizer](./images/journey2.png)

Klicka på **E-post** och sedan klicka **Redigera innehåll**.

![Journey Optimizer](./images/journey3.png)

Då visas meddelandepanelen. Klicka **E-postdesigner**.

![Journey Optimizer](./images/emailoffer2.png)

Du kommer då att se det här.

![Journey Optimizer](./images/emailoffer5.png)

Du kommer då att se det här. Dra en ny **1:1-kolumn** strukturkomponent på arbetsytan.

![Journey Optimizer](./images/emailoffer6.png)

Gå till menyn **Innehållskomponenter**. Välj **Beslut om erbjudandet** och dra och släpp den här komponenten i e-postmeddelandets innehållserbjudandeplatshållare enligt vad som anges. Klicka sedan på **Lägg till**.

![Journey Optimizer](./images/emailoffer7.png)

Välj den typ av placering som du vill ta med i e-postmeddelandet. I **Placeringar** listrutemeny välja **E-post - bild** väljer du sedan ditt beslut `--demoProfileLdap-- - Luma Decision`. Klicka **Lägg till**.

![Journey Optimizer](./images/emailoffer8.png)

Nu ser du alla personaliserade erbjudanden och reserverbjudandet visualiseras inuti e-postdesignern. Klicka  **Simulera innehåll** för att förhandsgranska e-postmeddelandet med en riktig kundprofil.

![Journey Optimizer](./images/emailoffer9.png)

Börja med att identifiera vilken profil du vill använda för förhandsgranskningen. Välj **e-post** och ange e-postadressen till en kundprofil som du har skapat på demowebbplatsen. Klicka på **Förhandsgranska**.

![Journey Optimizer](./images/emailoffer10.png)

När e-postmeddelandet har visats och erbjudandet visas korrekt klickar du på **Stäng** -knappen.

![Journey Optimizer](./images/emailoffer11.png)

Klicka slutligen **Spara**.

![Journey Optimizer](./images/emailoffer12.png)

Klicka på pilen för att gå tillbaka till föregående skärm.

![Journey Optimizer](./images/emailoffer13.png)

Du kommer då att se det här. Klicka på pilen i det övre vänstra hörnet för att gå tillbaka till din resa.

![Journey Optimizer](./images/emailoffer14.png)

Klicka **OK** för att stänga **E-post** åtgärd.

![Journey Optimizer](./images/emailoffer14a.png)

Klicka **Publicera** för att publicera din uppdaterade resa.

![Journey Optimizer](./images/emailoffer14b.png)

Bekräfta genom att klicka **Publicera** igen.

![Journey Optimizer](./images/emailoffer15.png)

Meddelandet har publicerats.

![Journey Optimizer](./images/emailoffer16.png)

När du skapar ett nytt konto på demowebbplatsen får du nu det här e-postmeddelandet:

![Journey Optimizer](./images/emailoffer17.png)

Du har gjort klart den här övningen.

Nästa steg: [9.6 Testa ditt beslut med API:t](./ex6.md)

[Gå tillbaka till modul 9](./offer-decisioning.md)

[Gå tillbaka till Alla moduler](./../../overview.md)
