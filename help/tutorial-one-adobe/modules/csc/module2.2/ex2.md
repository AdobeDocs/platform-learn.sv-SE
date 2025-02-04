---
title: Korrektur med Workfront
description: Korrektur med Workfront
kt: 5342
doc-type: tutorial
exl-id: 1b5ca13b-2a32-44a1-a3ae-342bccc6baeb
source-git-commit: 5b15d54af26d67b4193a1ac4d5d62f5c62a37362
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 0%

---

# 2.2.2 Korrektur med Workfront

## 2.2.2.1 Skapa ett nytt godkännandeflöde

Gå till [https://experienceplatform.my.workfront.com/](https://experienceplatform.my.workfront.com/){target="_blank"}.

Klicka på ikonen **hamburger** med nio punkter och välj **Korrektur**.

![WF](./images/wfp1.png)

Gå till **Arbetsflöden**, klicka på **+ Ny** och välj sedan **Ny mall**.

![WF](./images/wfp2.png)

Ange **mallnamnet** till `--aepUserLdap-- - Approval Workflow` och ställ in **mallägaren** till dig själv.

![WF](./images/wfp3.png)

Bläddra nedåt och under **Steg** > **Steg 1** lägger du till **Wouter Van Geluwe** med **rollen** för **Granskare och godkännare**.

Klicka på **Skapa**.

![WF](./images/wfp4.png)

Ditt grundläggande arbetsflöde för godkännande är nu klart att användas.

![WF](./images/wfp5.png)

## 2.2.2.2 Skapa ett nytt projekt

Klicka på **Nytt** på fliken **Mina projekt** på startsidan för Workfront. Välj **Tomt projekt**.

![WF](./images/wfp6.png)

Du borde se det här då. Ändra namnet till `--aepUserLdap-- - CitiSignal Fiber Launch`.

![WF](./images/wfp6a.png)

Ditt projekt har skapats.

![WF](./images/wfp7.png)

## 2.2.2.3 Skapa en ny uppgift

Ange det här namnet för din aktivitet: **Skapa resurser för Fibre-kampanj**. Klicka på **Skapa uppgift**.

![WF](./images/wfp8.png)

Du borde se det här då.

![WF](./images/wfp9.png)

## 2.2.2.4 Lägg till ett nytt dokument i din uppgift genom hela godkännandeflödet

Klicka på **+ Lägg till ny** och välj sedan **Dokument**.

![WF](./images/wfp10.png)

Hämta [den här filen](./images/2048x2048.png) till skrivbordet.

![WF](./images/2048x2048.png){width="50px" align="left"}

Markera filen **2048x2048.png** och klicka på **Öppna**.

![WF](./images/wfp12.png)

Du borde ha den här då. Klicka på **Skapa korrektur** och välj sedan **Avancerat korrektur**.

![WF](./images/wfp13.png)

I fönstret **nytt korrektur** väljer du den arbetsflödesmall som du skapade tidigare och som ska ha namnet `--aepuserLdap-- - Approval Workflow`. Klicka på **Skapa bevis**.

![WF](./images/wfp14.png)

Du kommer sedan att vara tillbaka i din uppgift. Klicka på knappen **Tilldela till** och välj **Tilldela till mig**.

![WF](./images/wfp15.png)

Klicka på **Spara**.

![WF](./images/wfp16.png)

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

Du borde vara tillbaka här. Nu måste du ladda upp en andra bild som tar hänsyn till de kommentarer som lämnats.

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

Stäng korrekturförhandsgranskningen.

![WF](./images/wfp33.png)

Du kommer sedan tillbaka i aktivitetsvyn med en godkänd resurs. Materialet måste nu delas med AEM Assets.

![WF](./images/wfp34.png)

Klicka på ikonen **Dela-pil** och välj den AEM Assets-integrering som ska ha namnet `--aepUserLdap-- - Citi Signal AEM`.

![WF](./images/wfp35.png)

Dubbelklicka på mappen som du skapade tidigare, som bör ha namnet `--aepUserLdap-- - Workfront Assets`.

![WF](./images/wfp36.png)

Klicka på **Välj mapp**.

![WF](./images/wfp37.png)

Efter 1-2 minuter publiceras dokumentet nu i AEM Assets. En AEM visas bredvid dokumentnamnet.

![WF](./images/wfp37a.png)

Klicka på **Öppna sammanfattning**.

![WF](./images/wfp38.png)

Gå till **Metadata** och se följande:

![WF](./images/wfp39.png)

Gå till **Översikt** och klicka på **+ Lägg till** för att lägga till en beskrivning.

![WF](./images/wfp40.png)

Ange din beskrivning. Dina korrektur- och dokumentinställningar är nu klara.

![WF](./images/wfp41.png)

## 2.2.2.5 Visa filen i AEM Assets

Gå till din mapp i AEM Assets med namnet `--aepUserLdap-- - Workfront Assets`.

![WF](./images/wfppaem1.png)

Klicka på de tre punkterna under bilden och välj sedan **Detaljer**.

![WF](./images/wfppaem2.png)

Du kommer då att se metadataformuläret som du skapade tidigare, med värden som fyllts i automatiskt genom integrationen mellan Workfront och AEM Assets.

![WF](./images/wfppaem3.png)

[Gå tillbaka till modul 2.2](./workfront.md){target="_blank"}

[Gå tillbaka till alla moduler](./../../../overview.md){target="_blank"}
