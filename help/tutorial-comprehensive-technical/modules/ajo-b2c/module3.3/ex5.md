---
title: Offer decisioning - Använd ditt beslut via e-post
description: Använd ditt beslut i ett e-postmeddelande
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---

# 3.3.5 Använd ditt beslut i ett e-postmeddelande

I den här övningen använder du ditt beslut för att anpassa leveransen av ett e-postmeddelande och SMS.

Gå till **Resor**. Hitta den resa du skapade i övning 7.2, som heter `--aepUserLdap-- - Account Creation Journey`. Klicka på resan för att öppna den.

![Journey Optimizer](./images/emailoffer1.png)

Då ser du det här. Klicka på **Skapa en ny version**.

![Journey Optimizer](./images/journey1.png)

Klicka på **Skapa en ny version**.

![Journey Optimizer](./images/journey2.png)

Klicka på åtgärden **E-post** och sedan på **Redigera innehåll**.

![Journey Optimizer](./images/journey3.png)

Då visas meddelandepanelen. Klicka på **E-posta Designer**.

![Journey Optimizer](./images/emailoffer2.png)

Då ser du det här.

![Journey Optimizer](./images/emailoffer5.png)

Då ser du det här. Dra en ny **1:1-kolumnstrukturkomponent** till arbetsytan.

![Journey Optimizer](./images/emailoffer6.png)

Gå till **Innehållskomponenter** på menyn. Välj komponenten **Erbjudandebeslut** och dra och släpp den här komponenten i e-postmeddelandets platshållare för innehållserbjudanden enligt vad som anges. Klicka sedan på **Lägg till**.

![Journey Optimizer](./images/emailoffer7.png)

Välj den typ av placering som du vill ta med i e-postmeddelandet. Välj **E-post - bild** i listrutan **Placeringar** och välj sedan ditt beslut `--aepUserLdap-- - Luma Decision`. Klicka på **Lägg till**.

![Journey Optimizer](./images/emailoffer8.png)

Nu ser du alla personaliserade erbjudanden och reserverbjudandet visualiseras inuti e-postdesignern. Klicka på **Simulera innehåll** om du vill förhandsgranska e-postmeddelandet med en riktig kundprofil.

![Journey Optimizer](./images/emailoffer9.png)

Börja med att identifiera vilken profil du vill använda för förhandsgranskningen. Markera namnområdet **email** och ange e-postadressen för en kundprofil som du har skapat på demowebbplatsen. Klicka sedan på **Förhandsgranska**.

![Journey Optimizer](./images/emailoffer10.png)

När e-postmeddelandet har visats och erbjudandet visas korrekt klickar du på knappen **Stäng** .

![Journey Optimizer](./images/emailoffer11.png)

Klicka slutligen på **Spara**.

![Journey Optimizer](./images/emailoffer12.png)

Klicka på pilen för att gå tillbaka till föregående skärm.

![Journey Optimizer](./images/emailoffer13.png)

Då ser du det här. Klicka på pilen i det övre vänstra hörnet för att gå tillbaka till din resa.

![Journey Optimizer](./images/emailoffer14.png)

Klicka på **OK** för att stänga din **e-post**-åtgärd.

![Journey Optimizer](./images/emailoffer14a.png)

Klicka på **Publish** för att publicera den uppdaterade resan.

![Journey Optimizer](./images/emailoffer14b.png)

Bekräfta genom att klicka på **Publish** igen.

![Journey Optimizer](./images/emailoffer15.png)

Meddelandet har publicerats.

![Journey Optimizer](./images/emailoffer16.png)

När du skapar ett nytt konto på demowebbplatsen får du nu det här e-postmeddelandet:

![Journey Optimizer](./images/emailoffer17.png)

Du har gjort klart den här övningen.

Nästa steg: [3.3.6 Testa ditt beslut med API:t](./ex6.md)

[Gå tillbaka till modul 3.3](./offer-decisioning.md)

[Gå tillbaka till Alla moduler](./../../../overview.md)
