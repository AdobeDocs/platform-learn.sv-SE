---
title: Komma igång med Workfront
description: Komma igång med Workfront
kt: 5342
doc-type: tutorial
exl-id: 0867d7fd-4d12-46d8-a5ae-bb8db1575635
source-git-commit: a63c01ebe81df39569981d62b85d0461119ecf66
workflow-type: tm+mt
source-wordcount: '1099'
ht-degree: 0%

---

# 1.2.1 Integrering av Workfront + AEM Assets CS-metadata

>[!IMPORTANT]
>
>För att slutföra den här övningen måste du ha tillgång till en fungerande AEM Assets CS-redigeringsmiljö.
>
>Det finns två alternativ:
>
>- Om du deltar i GenStudio för CSC Technical Enablement har dina lärare skapat en AEM Assets CS Author-miljö åt dig. Kontrollera med dem vad namnet är och hur du fortsätter.
>
>- Om du följer den fullständiga sökvägen till en Adobe-självstudiekurs går du till [Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./../../../modules/asset-mgmt/module2.1/aemcs.md){target="_blank"}. Följ instruktionerna där så får du tillgång till en sådan miljö.

>[!IMPORTANT]
>
>Om du tidigare har konfigurerat ett AEM CS-program med en AEM Assets CS-miljö kan det bero på att din AEM CS-sandlåda är i viloläge. Eftersom det tar 10-15 minuter att dölja en sådan sandlåda, är det en bra idé att starta separationsprocessen nu så att du inte behöver vänta på den vid ett senare tillfälle.

## 1.2.1.1 Workfront Workflow Terminology

Följande är de viktigaste Workfront-objekten och -begreppen:

| Namn | Senaste uppdatering |
| ---------------------- | ------------ | 
| Portfolio | En samling projekt som har enhetliga egenskaper. Dessa projekt konkurrerar vanligtvis om samma resurser, budget eller tidskortplats. |
| Program | En delmängd inom en portfölj, där liknande projekt kan grupperas tillsammans för att uppnå en väldefinierad fördel. |
| Projekt | En stor mängd arbete som måste slutföras inom en viss tidsram och som måste använda en viss budget och ett visst antal resurser. För att projektet ska bli hanterbart delar du upp det i en serie uppgifter. När du slutför alla uppgifter slutförs projektet. |
| Projektmall | Du kan använda projektmallar för att hämta in de flesta repeterbara processer, information och inställningar som är kopplade till projekten i organisationen. När du har skapat mallar kan du bifoga dem till befintliga projekt eller använda dem för att skapa nya projekt. |
| Uppgift | En aktivitet som måste utföras som ett steg mot att uppnå ett slutligt mål (att slutföra projektet). Aktiviteter kan aldrig finnas oberoende. De ingår alltid i ett projekt. |
| Tilldelning | En användare, en jobbroll eller ett team som har tilldelats ett ärende eller en uppgift. Projekt, portföljer eller program kan inte ha tilldelningar. |
| Dokument/version | Alla filer som är kopplade till ett objekt i Workfront. Varje gång samma dokument överförs till samma objekt tilldelas det ett versionsnummer. Användare kan visa och ändra flera alternativ för en tidigare version av ett dokument. |
| Godkännande | En viss arbetsuppgift, till exempel en uppgift, ett dokument eller en tidrapport, kan kräva att en ansvarig eller annan användare signerar arbetsposten. Den här processen med att signera kallas för godkännande. |


Gå till [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Klicka för att öppna **Workfront**.

![Workfront Planning](./../module1.1/images/wfpl1.png)

Då ser du det här.

![WF](./images/wfb1.png)

## 1.2.1.1 Konfigurera din AEM Assets-integrering

Klicka på ikonen **menu** och välj sedan **Konfigurera**.

![WF](./images/wfb2.png)

Bläddra nedåt till **Dokument** på den vänstra menyn och klicka sedan på **Experience Manager Assets**. Klicka på **+ Lägg till Experience Manager-integrering**.

![WF](./images/wfb3.png)

Använd `--aepUserLdap-- - CitiSignal AEM` för integreringens namn.

Öppna listrutan **Experience Manager-databas** och välj din AEM CS-instans, som bör ha namnet `--aepUserLdap-- - CitiSignal`.

![WF](./images/wfb5.png)

Konfigurera följande mappning under **Metadata**:

| Workfront Field | Experience Manager Assets |
| --------------- | ------------------------------ | 
| **Dokument** > **Namn** | **wm:documentName** |
| **Projekt** > **Namn** | **wm:projectName** |
| **Projekt** > **Beskrivning** | **wm:projectDescription** |
| **Dokumentbegäran** > **Status** | **wm:wm:documentStatus** |
| **Aktivitet** > **Namn** | **wm:taskName** |
| **Aktivitet** > **Beskrivning** | **wm:taskDescription** |
| **Projekt** > **ID** | **wm:projectId** |

Aktivera växeln för **Synkronisera objektmetadata**.

Klicka på **Spara**.

![WF](./images/wfb6.png)

Din integrering från Workfront till AEM Assets CS är nu konfigurerad.

![WF](./images/wfb7.png)

## 1.2.1.2 Konfigurera metadataintegrering med AEM Assets

Därefter måste du konfigurera AEM Assets CS så att metadatafälten från resursen i Workfront delas med AEM Assets CS.

Gå till [https://experience.adobe.com/](https://experience.adobe.com/) om du vill göra det. Klicka på **Experience Manager Assets**.

![WF](./images/wfbaem1.png)

Klicka för att välja din AEM Assets-miljö, som ska få namnet `--aepUserLdap-- - CitiSignal dev`.

![WF](./images/wfbaem2.png)

Du borde se det här då. Gå till **Assets** på den vänstra menyn.

![WF](./images/wfbaem3.png)

Klicka sedan på **Skapa mapp**.

![WF](./images/wfbaem3a.png)

Namnge mappen `--aepUserLdap-- - CitiSignal Fiber Launch Assets` och klicka på **Skapa**.

![WF](./images/wfbaem4.png)

Gå sedan till **Metadata Forms** i den vänstra menyn och klicka på **Skapa**.

![WF](./images/wfbaem5.png)

Använd namnet `--aepUserLdap-- - Metadata Form` och klicka på **Skapa**.

![WF](./images/wfbaem6.png)

Lägg till 7 nya **enkelradiga textfält** i formuläret och markera det första fältet. Klicka sedan på ikonen **Schema** bredvid fältet **Metadata-egenskap** för det första fältet.

![WF](./images/wfbaem7.png)

Du kommer då att se den här popup-rutan. Ange `wm:project` i sökfältet och markera sedan fältet **Projektnamn**. Klicka på **Markera**.

![WF](./images/wfbaem11.png)

Ändra fältets etikett till `Project Name`. Klicka på **Spara**.

![WF](./images/wfbaem12.png)

Gå till det andra fältet och klicka på ikonen **Schema** bredvid fältet **Metadataegenskap** .

![WF](./images/wfbaem12a.png)

Ange `wm:project` i sökfältet och markera sedan fältet **Projektbeskrivning**. Klicka på **Markera**.

![WF](./images/wfbaem8.png)

Ändra fältets etikett till `Project Description`.

![WF](./images/wfbaem9.png)

Markera sedan det tredje fältet och klicka på ikonen **Schema** bredvid fältet **Metadataegenskap** igen.

![WF](./images/wfbaem10b.png)

Du kommer då att se den här popup-rutan igen. Ange `wm:project` i sökfältet och markera sedan fältet **Projekt-ID**. Klicka på **Markera**.

![WF](./images/wfbaem10.png)

Ändra fältets etikett till `Project ID`.

![WF](./images/wfbaem10a.png)

Markera sedan det fjärde fältet och klicka på ikonen **Schema** bredvid fältet **Metadataegenskap** igen.

![WF](./images/wfbaem11a.png)

Du kommer då att se den här popup-rutan igen. Ange `wm:document` i sökfältet och markera sedan fältet **Projekt-ID**. Klicka på **Markera**.

![WF](./images/wfbaem101.png)

Ändra fältets etikett till `Document Status`.

![WF](./images/wfbaem102.png)

Markera sedan det femte fältet och klicka på ikonen **Schema** bredvid fältet **Metadataegenskap** igen.

![WF](./images/wfbaem103.png)

Du kommer då att se den här popup-rutan igen. Ange `wm:document` i sökfältet och markera sedan fältet **Projekt-ID**. Klicka på **Markera**.

![WF](./images/wfbaem104.png)

Ändra fältets etikett till `Document Name`.

![WF](./images/wfbaem105.png)

Markera sedan det sjätte fältet och klicka på ikonen **Schema** bredvid fältet **Metadataegenskap** igen.

![WF](./images/wfbaem106.png)

Du kommer då att se den här popup-rutan igen. Ange `wm:task` i sökfältet och markera sedan fältet **Uppgiftsnamn**. Klicka på **Markera**.

![WF](./images/wfbaem107.png)

Ändra fältets etikett till `Task Name`.

![WF](./images/wfbaem108.png)

Markera sedan det sjunde fältet och klicka på ikonen **Schema** bredvid fältet **Metadataegenskap** igen.

![WF](./images/wfbaem109.png)

Du kommer då att se den här popup-rutan igen. Ange `wm:task` i sökfältet och markera sedan fältet **Aktivitetsbeskrivning**. Klicka på **Markera**.

![WF](./images/wfbaem110.png)

Ändra fältets etikett till `Task Description`.

![WF](./images/wfbaem111.png)

Ändra **fliknamnet** i formuläret till `--aepUserLdap-- - Workfront Metadata`.

![WF](./images/wfbaem13.png)

Klicka på **Spara** och **Stäng**.

![WF](./images/wfbaem13a.png)

**Metadataformuläret** har konfigurerats.

![WF](./images/wfbaem14.png)

Därefter måste du tilldela metadataformuläret till mappen som du skapade tidigare. Markera kryssrutan för ditt metadataformulär och klicka på **Tilldela till mapp(ar)**.

![WF](./images/wfbaem15.png)

Välj din mapp som ska ha namnet `--aepUserLdap-- - CitiSignal Fiber Launch Assets`. Klicka på **Tilldela**.

![WF](./images/wfbaem16.png)

Metadataformuläret har nu tilldelats mappen.

![WF](./images/wfbaem17.png)

Nästa steg: [1.2.2 Korrektur med Workfront](./ex2.md){target="_blank"}

Gå tillbaka till [Arbetsflödeshantering med Adobe Workfront](./workfront.md){target="_blank"}

[Gå tillbaka till alla moduler](./../../../overview.md){target="_blank"}
