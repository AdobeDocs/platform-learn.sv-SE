---
title: Korrektur med Workfront
description: Korrektur med Workfront
kt: 5342
doc-type: tutorial
exl-id: 5feb9486-bdb4-4d59-941c-09fc2e38163b
source-git-commit: 6b93c7ed76ef38dda8903d63f4800a98f4e46e1d
workflow-type: tm+mt
source-wordcount: '1319'
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

Bläddra nedåt och ändra rollen **Korrekturskapare** till **Granskare och godkännare** under **Steg** > **Steg 1**. Du kan även lägga till andra, så som till exempel lägga till dig själv genom att markera användaren och ange **rollen** för **Granskare och godkännare**.

Klicka på **Skapa**.

![WF](./images/wfp4.png)

Ditt grundläggande arbetsflöde för godkännande är nu klart att användas.

![WF](./images/wfp5.png)

## 1.2.2.2 Aktivera Workfront Blueprint

I nästa steg skapar du ett nytt projekt med hjälp av en mall. Adobe Workfront tillhandahåller ett antal ritningar som bara behöver aktiveras.

För CitiSignals användningsfall är den **integrerade kampanjkörningen** den du behöver använda.

Om du vill installera den översikten öppnar du menyn och väljer **utkast**.

![WF](./images/blueprint1.png)

Välj filtret **Marknadsföring** och bläddra sedan nedåt för att hitta den **integrerade kampanjkörningen**. Klicka på **Installera**.

![WF](./images/blueprint2.png)

Klicka på **Fortsätt**.

![WF](./images/blueprint3.png)

Klicka på **Installera som..**.

![WF](./images/blueprint4.png)

Du borde se det här då. Installationen kan ta några minuter.

![WF](./images/blueprint5.png)

Efter några minuter installeras ritningen.

![WF](./images/blueprint6.png)

## 1.2.2.3 Skapa ett nytt projekt

Öppna **menyn** och gå till **Program**.

![WF](./images/wfp6a.png)

Klicka på det program du skapade tidigare, med namnet `--aepUserLdap-- CitiSignal Fiber Launch`.

>[!NOTE]
>
>Du skapade ett program som en del av övningen på [Workfront Planning](./../module1.1/ex1.md) med den automatisering du skapade och körde. Om du inte har gjort det än kan du hitta instruktionerna där.

![WF](./images/wfp6b.png)

Gå till **Projekt** i ditt program. Klicka på **+ Nytt projekt** och välj sedan **Nytt projekt från mall**.

![WF](./images/wfp6.png)

Välj mallen **Integrerad kampanjkörning** och klicka på **Använd mall**.

![WF](./images/wfp6g.png)

Du borde se det här då. Ändra namnet till `--aepUserLdap-- - CitiSignal Fiber Launch Winter 2026` och klicka på **Skapa projekt**.

![WF](./images/wfp6c.png)

Ditt projekt har skapats. Gå till **Projektinformation**.

![WF](./images/wfp6h.png)

Gå till **Projektinformation**. Klicka för att markera den aktuella texten under **Beskrivning**.

![WF](./images/wfp6d.png)

Ange beskrivningen till `The CitiSignal Fiber Launch project is used to plan the upcoming launch of CitiSignal Fiber.`

Klicka på **Spara ändringar**.

![WF](./images/wfp6e.png)

Ditt projekt är nu klart att användas.

![WF](./images/wfp7.png)

Aktiviteter och beroenden i projektet har skapats baserat på den mall du valde och du har angetts som. projektägare. Projektets status har angetts till **Planering**. Du kan ändra projektets status genom att välja ett annat värde i listan.

![WF](./images/wfp7z.png)

## 1.2.2.4 Skapa en ny aktivitet

Hovra över aktiviteten **Börja skapa designmallar** och klicka på de tre punkterna **..**.

![WF](./images/wfp7a.png)

Välj alternativet **Infoga aktivitet nedan**.

![WF](./images/wfp7x.png)

Ange det här namnet för din uppgift: `Create layout using approved assets and copy`.

Ställ in fältet **Uppdrag** till rollen **Designer**.
Ange fältet **Varaktighet** till **5 dagar**.
Ställ in fältets föregångare till **9**.
Ange ett datum för fälten **Börja den** och **Förfaller den**.

Klicka någon annanstans på skärmen för att spara den nya uppgiften.

![WF](./images/wfp8.png)

Du borde se det här då. Klicka på uppgiften för att öppna den.

![WF](./images/wfp9.png)

Gå till **aktivitetsinformation** och ställ in fältet **Beskrivning** på: `This task is used to track the progress of the creation of the assets for the CitiSignal Fiber Launch Campaign.`

Klicka på **Spara ändringar**.

![WF](./images/wfp9a.png)

Du borde se det här då. Klicka på fältet **Projekt** för att gå tillbaka till ditt projekt.

![WF](./images/wfp9b.png)

Gå till **Utjämning av arbetsbelastning** i vyn **Projekt**.

![WF](./images/wfpwlb1.png)

Klicka på **Gruppera tilldelningar**.

![WF](./images/wfpwlb2.png)

Markera **rolltilldelningen** för **Designer** och klicka sedan i fältet **Användare för att tilldela**. Detta visar alla användare som har en **Designer**-roll i din Workfront-instans. I det här fallet väljer du den fiktiva användaren **Melissa Jenkins**.

![WF](./images/wfpwlb3.png)

Klicka på **Tilldela**. Användaren du valde tilldelas nu till aktiviteterna i projektet som är länkade till rollen **Designer**.

![WF](./images/wfpwlb4.png)

Uppgifterna har nu tilldelats. Klicka på **Åtgärder** för att gå tillbaka till översiktssidan för **Åtgärder**.

![WF](./images/wfpwlb5.png)

Klicka på den uppgift du skapade, med namnet
**Skapa layout med godkända resurser och kopiera**.

![WF](./images/wfpwlb6.png)

Du kommer nu att börja arbeta med den här uppgiften som en del av den här övningen. Du ser att Melissa Jenkins är tilldelad den här uppgiften just nu. Om du vill ändra det för dig själv klickar du på fältet **Tilldelningar** och väljer **Tilldela mig**.

![WF](./images/wfpwlb7.png)

Klicka på **Spara**.

![WF](./images/wfpwlb8.png)

Klicka på **Arbeta med den**.

![WF](./images/wfpwlb9.png)

Du borde se det här då.

![WF](./images/wfpwlb10.png)

Som en del av detta måste du skapa en ny bild och sedan överföra den som ett dokument i Workfront. Nu kan du själv skapa resursen med Adobe Express.

## 1.2.2.5 Lägg till ett nytt dokument i din uppgift och starta godkännandeflödet

För den här övningen måste du hämta och använda den här resursen: [tidslinjen.png](./images/timetravelnow.png)

![WF](./images/timetravelnow.png)

Gå tillbaka till skärmen **Uppgiftsinformation**. Gå till **Dokument**. Klicka på **+ Lägg till ny** och välj sedan din AEM Assets CS-databas, som ska ha namnet `--aepUserLdap-- - CitiSignal`.

![WF](./images/wfp10.png)

Dubbelklicka för att öppna mappen `--aepUserLdap-- CitiSignal Fiber Campaign`.

![WF](./images/wfp10a.png)

Markera filen som du skapade i föregående steg, som heter **CitiSignal - Neonkanin - Timeravel Now!.png**. Klicka på **Markera**.

![WF](./images/2048x2048.png){width="50px" align="left"}

Du borde ha den här då. Håll muspekaren över det överförda dokumentet. Klicka på **Skapa korrektur** och välj sedan **Avancerat korrektur**.

![WF](./images/wfp13.png)

Välj **Automatiserad** i fönstret **Nytt korrektur** och välj sedan den arbetsflödesmall som du skapade tidigare, som ska ha namnet `--aepUserLdap-- - Approval Workflow`. Klicka på **Skapa bevis**.

![WF](./images/wfp14.png)

Klicka på **Öppna korrektur**

![WF](./images/wfp18.png)

Nu kan du granska korrekturet. Välj **Lägg till kommentar** om du vill lägga till en kommentar som kräver att dokumentet ändras.

![WF](./images/wfp19.png)

Ange din kommentar och klicka på **Publicera**. Klicka sedan på **Fatta ett beslut**.

![WF](./images/wfp20.png)

Välj **Ändringar krävs** och klicka på **Fatta beslut**.

![WF](./images/wfp24.png)

Gå tillbaka till din **aktivitet** och **dokumentet**. Texten **Ändringar som krävs** visas också där.

![WF](./images/wfp25.png)

Nu måste du göra designändringar, som du gör i Adobe Express.

## 1.2.2.6 Lägg till en ny version av dokumentet i din uppgift

För den här övningen måste du hämta och använda resursen: [getonboard.png](./images/getonboard.png)

![WF](./images/getonboard.png)

I uppgiftsvyn i Adobe Workfront väljer du den gamla bildfilen som inte godkänts. Klicka sedan på **+ Lägg till ny**, markera **Version** och välj sedan din AEM Assets CS-databas, som ska ha namnet `--aepUserLdap-- - CitiSignal`.

![WF](./images/wfp26.png)

Navigera till mappen `--aepUserLdap-- CitiSignal Fiber Campaign` och markera filen `CitiSignal - Neon Rabit - Get On Board Now!.png`. Klicka på **Markera**.

![WF](./images/wfp26a.png)

Du borde ha den här då. Klicka på **Skapa korrektur** och välj sedan **Avancerat korrektur** igen.

![WF](./images/wfp28.png)

Då ser du det här. **Arbetsflödesmallen** är nu förvald eftersom Workfront antar att det tidigare arbetsflödet för godkännande fortfarande är giltigt. Klicka på **Skapa bevis**.

![WF](./images/wfp29.png)

Välj **Öppna korrektur**.

![WF](./images/wfp30.png)

Nu kan du se två versioner av filen bredvid varandra. Klicka på knappen **Jämför korrektur**.

![WF](./images/wfp31.png)

Du bör sedan se båda versionerna av bilden bredvid varandra. Klicka på **Fatta beslut**.

![WF](./images/wfp32.png)

Välj **Godkänd** och klicka på **Fatta beslut** igen.

![WF](./images/wfp32a.png)

Stäng vyn **Jämför korrektur** genom att stänga den vänstra versionen av bilden. Klicka på **Aktivitetsnamnet** för att gå tillbaka till aktivitetsöversikten.

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

Klicka på **Markera som slutförd** om du vill slutföra den här uppgiften.

![WF](./images/wfp37b.png)

Du borde se det här då.

![WF](./images/wfp37c.png)

## 1.2.2.7 Visa filen i AEM Assets

Gå till din mapp i AEM Assets CS med namnet `--aepUserLdap-- - CitiSignal Fiber Launch Assets`.

![WF](./images/wfppaem1.png)

Markera bilden och välj sedan **Detaljer**.

![WF](./images/wfppaem2.png)

Du kommer då att se metadataformuläret som du skapade tidigare, med värden som fyllts i automatiskt genom integrationen mellan Workfront och AEM Assets.

![WF](./images/wfppaem3.png)

Gå tillbaka till [Arbetsflödeshantering med Adobe Workfront](./workfront.md){target="_blank"}

[Gå tillbaka till alla moduler](./../../../overview.md){target="_blank"}
