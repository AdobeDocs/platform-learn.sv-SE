---
title: Korrektur med Workfront
description: Korrektur med Workfront
kt: 5342
doc-type: tutorial
exl-id: 5feb9486-bdb4-4d59-941c-09fc2e38163b
source-git-commit: 19291afe2d8101fead734fa20212a3db76369522
workflow-type: tm+mt
source-wordcount: '810'
ht-degree: 0%

---

# 1.2.2 Korrektur med Workfront

>[!IMPORTANT]
>
>Om du tidigare har konfigurerat ett AEM CS-program med en AEM Assets CS-miljö kan det bero på att din AEM CS-sandlåda är i viloläge. Eftersom det tar 10-15 minuter att dölja en sådan sandlåda, är det en bra idé att starta separationsprocessen nu så att du inte behöver vänta på den vid ett senare tillfälle.

## 1.2.2.1 Skapa ett nytt godkännandeflöde

Gå tillbaka till **Adobe Workfront**. Klicka på ikonen **menu** och välj **Korrektur**.

![WF](./images/wfp1.png)

Gå till **Arbetsflöden**, klicka på **+ Ny** och välj sedan **Ny mall**.

![WF](./images/wfp2.png)

Ange **mallnamnet** till `--aepUserLdap-- - Approval Workflow` och ställ in **mallägaren** till dig själv.

![WF](./images/wfp3.png)

Bläddra nedåt och under **Steg** > **Steg 1** lägger du till dig själv med **rollen** i **Granskare och godkännare**.

Klicka på **Skapa**.

![WF](./images/wfp4.png)

Ditt grundläggande arbetsflöde för godkännande är nu klart att användas.

![WF](./images/wfp5.png)

## 1.2.2.2 Skapa ett nytt projekt

Öppna **menyn** och gå till **Program**.

![WF](./images/wfp6a.png)

Klicka på det program du skapade tidigare, med namnet `--aepUserLdap-- CitiSignal Fiber Launch`.

>[!NOTE]
>
>Du skapade ett program som en del av övningen på [Workfront Planning](./../module1.1/ex1.md) med den automatisering du skapade och körde. Om du inte har gjort det än kan du hitta instruktionerna där.

![WF](./images/wfp6b.png)

Gå till **Projekt** i ditt program. Klicka på **+ Nytt projekt** och välj sedan **Nytt projekt**.

![WF](./images/wfp6.png)

Du borde se det här då. Ändra namnet till `--aepUserLdap-- - CitiSignal Fiber Launch`.

![WF](./images/wfp6c.png)

Gå till **Projektinformation**. Klicka på **+Lägg till** under **Beskrivning**.

![WF](./images/wfp6d.png)

Ange beskrivningen till `The CitiSignal Fiber Launch project is used to plan the upcoming launch of CitiSignal Fiber.`

Klicka på **Spara ändringar**.

![WF](./images/wfp6e.png)

Ditt projekt har skapats.

![WF](./images/wfp7.png)

## 1.2.2.3 Skapa en ny aktivitet

Gå till **Åtgärder** och klicka på **+ Ny aktivitet**.

![WF](./images/wfp7a.png)

Ange det här namnet för din uppgift: `Create assets for Fiber campaign`.

Ställ in fältet **Beskrivning** till: `This task is used to track the progress of the creation of the assets for the CitiSignal Fiber Launch Campaign.`

Klicka på **Skapa uppgift**.

![WF](./images/wfp8.png)

Du borde se det här då.

![WF](./images/wfp9.png)

Lägg till ditt namn i kolumnen **Tilldelning**.

![WF](./images/wfp9a.png)

Uppgiften tilldelas sedan till dig.

![WF](./images/wfp9b.png)

## 1.2.2.4 Lägg till ett nytt dokument i din uppgift via godkännandeflödet

Klicka på **Workfront**-logotypen för att gå tillbaka till översiktssidan. Du bör då se projektet som du just skapade visas i översikten. Klicka på projektet för att öppna det.

![WF](./images/wfp9c.png)

Öppna uppgiften genom att klicka i **Aktiviteter**.

![WF](./images/wfp9d.png)

Gå till **Dokument**. Klicka på **+ Lägg till ny** och välj sedan **Dokument**.

![WF](./images/wfp10.png)

Hämta [den här filen](./images/2048x2048.png) till skrivbordet.

![WF](./images/2048x2048.png){width="50px" align="left"}

Markera filen **2048x2048.png** och klicka på **Öppna**.

![WF](./images/wfp12.png)

Du borde ha den här då. Håll muspekaren över det överförda dokumentet. Klicka på **Skapa korrektur** och välj sedan **Avancerat korrektur**.

![WF](./images/wfp13.png)

Välj **Automatiserad** i fönstret **Nytt korrektur** och välj sedan den arbetsflödesmall som du skapade tidigare, som ska ha namnet `--aepUserLdap-- - Approval Workflow`. Klicka på **Skapa bevis**.

![WF](./images/wfp14.png)

Klicka på **Arbeta med den**.

![WF](./images/wfp17.png)

Klicka på **Öppna korrektur**

![WF](./images/wfp18.png)

Nu kan du granska korrekturet. Välj **Lägg till kommentar** om du vill lägga till en kommentar som kräver att dokumentet ändras.

![WF](./images/wfp19.png)

Ange din kommentar och klicka på **Publicera**. Klicka på **Stäng**.

![WF](./images/wfp20.png)

Därefter måste du ändra din roll från **Granskare** till **Granskare och godkännare**. Om du vill göra det går du tillbaka till din uppgift och klickar på **Korrektur**.

![WF](./images/wfp21.png)

Ändra din roll från **Granskare** till **Granskare och godkännare**.

![WF](./images/wfp22.png)

Gå tillbaka till Uppgiften och öppna korrekturet igen. Nu visas en ny knapp, **Fatta beslut**. Klicka på den.

![WF](./images/wfp23.png)

Välj **Ändringar krävs** och klicka på **Fatta beslut**.

![WF](./images/wfp24.png)

Gå tillbaka till din **aktivitet** och **dokumentet**. Nu måste du ladda upp en andra bild som tar hänsyn till de kommentarer som lämnats.

![WF](./images/wfp25.png)

Hämta [den här filen](./images/2048x2048_buynow.png) till skrivbordet.

![den här filen](./images/2048x2048_buynow.png){width="50px" align="left"}

Välj den gamla bildfilen som inte godkänts i aktivitetsvyn. Klicka sedan på **+ Lägg till ny**, markera **Version** och välj sedan **Dokument**.

![WF](./images/wfp26.png)

Markera filen **2048x2048_buynow.png** och klicka på **Öppna**.

![WF](./images/wfp27.png)

Du borde ha den här då. Klicka på **Skapa korrektur** och välj sedan **Avancerat korrektur** igen.

![WF](./images/wfp28.png)

Då ser du det här. **Arbetsflödesmallen** är nu förvald eftersom Workfront antar att det tidigare arbetsflödet för godkännande fortfarande är giltigt. Klicka på **Skapa bevis**.

![WF](./images/wfp29.png)

Välj **Öppna korrektur**.

![WF](./images/wfp30.png)

Nu kan du se två versioner av filen bredvid varandra.

![WF](./images/wfp31.png)

Klicka på **Fatta beslut**, välj **Godkänd** och klicka på **Fatta beslut** igen.

![WF](./images/wfp32.png)

Klicka på **Aktivitetsnamnet** för att gå tillbaka till aktivitetsöversikten.

![WF](./images/wfp33.png)

Du kommer sedan tillbaka i aktivitetsvyn med en godkänd resurs. Materialet måste nu delas med AEM Assets.

![WF](./images/wfp34.png)

Välj det godkända dokumentet. Klicka på ikonen **Dela-pil** och välj den AEM Assets-integrering som ska ha namnet `--aepUserLdap-- - CitiSignal AEM`.

![WF](./images/wfp35.png)

Dubbelklicka på mappen som du skapade tidigare, som bör ha namnet `--aepUserLdap-- - CitiSignal Fiber Launch Assets`.

![WF](./images/wfp36.png)

Klicka på **Välj mapp**.

![WF](./images/wfp37.png)

Efter 1-2 minuter publiceras dokumentet nu i AEM Assets. En AEM-ikon visas bredvid dokumentnamnet.

![WF](./images/wfp37a.png)

## 1.2.2.5 Visa filen i AEM Assets

Gå till din mapp i AEM Assets CS med namnet `--aepUserLdap-- - CitiSignal Fiber Launch Assets`.

![WF](./images/wfppaem1.png)

Markera bilden och välj sedan **Detaljer**.

![WF](./images/wfppaem2.png)

Du kommer då att se metadataformuläret som du skapade tidigare, med värden som fyllts i automatiskt genom integrationen mellan Workfront och AEM Assets.

![WF](./images/wfppaem3.png)

Gå tillbaka till [Arbetsflödeshantering med Adobe Workfront](./workfront.md){target="_blank"}

[Gå tillbaka till alla moduler](./../../../overview.md){target="_blank"}
