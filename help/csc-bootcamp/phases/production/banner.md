---
title: CSC Bootcamp - Skapa produktstartsidesbanderoll
description: CSC Bootcamp - Skapa produktstartsidesbanderoll
doc-type: multipage-overview
exl-id: c78b6ba2-1a1a-4e95-a8ab-1b572fa2d8b1
source-git-commit: 143da6340b932563a3309bb46c1c7091e0ab2ee2
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 0%

---

# Skapa produktstartsidans banderoll

## Banderollens produktion

Med innehållsautomatisering får marknadsförarna tillgång till kraften i Adobe Creative Cloud i Experience Manager Assets och kan automatisera materialproduktionen i stor skala, vilket dramatiskt snabbar upp framtagningen av variationer. Låt oss använda de här funktionerna för att skapa en banderoll som ska användas på hemsidan!

- Gå till AEM författare på [https://author-p105462-e991028.adobeaemcloud.com/](https://author-p105462-e991028.adobeaemcloud.com/) och logga in med de autentiseringsuppgifter som vi har angett.

- Gå till Verktyg \> Assets \> Bearbetningsprofiler på startsidan.

![Verktyg > Assets > Bearbeta profiler](./images/prod-processing-profiles.png)

- I gränssnittet visas alla befintliga bearbetningsprofiler. De kan användas för att möjliggöra vissa automatiseringar.

![lista med bearbetningsprofiler](./images/prod-profile-list.png)


- Följande är intressanta:
   - Adobe-cykelbanderoll mörk: skapar en Adobe-banderoll med en mörk övertäckning, baserat på den valda resursen
     ![mörk banderoll](./images/prod-banner-dark.jpg)
   - Adobe Cycle Banner Light: skapar en Adobe-banderoll med lätt övertäckning, baserat på vald mediefil
     ![ljusbanderoll](./images/prod-banner-light.jpg)
   - Adobe-cykelbanderollgrön: skapar en Adobe-banderoll med en grön övertäckning som baseras på den valda resursen
     ![grön banderoll](./images/prod-banner-green.jpg)

- När du har valt vilken typ av banderoll du vill skapa markerar du den bearbetningsprofilen och väljer sedan &quot;Använd profil för mapp(ar)&quot;.

![använd profil för mappen](./images/prod-apply-profile.png)

- På nästa skärm går du till teamets mapp i AEM Assets. Välj sedan knappen &quot;Skapa&quot; längst upp till vänster för att skapa en ny mapp och ge den ett beskrivande namn, till exempel &quot;Skapa mörk banderoll&quot;.

![skapa mapp](./images/prod-create-profile-folder.png)

![skapa mappinformation](./images/prod-profile-folder-details.png)

- När du har skapat mappen markerar du rutan bredvid dess namn och klickar sedan på knappen &quot;Använd&quot; längst upp till höger.

![gäller för skapad mapp](./images/prod-select-profile-folder.png)

Nu när vi har gjort den nödvändiga konfigurationen ska vi skapa vår banderoll.

- Klicka på AEM logotyp i det övre vänstra hörnet för att öppna navigeringen och navigera sedan till Navigering \> Assets \>-filer.

![aem home screen](./images/prod-select-assets.png)
![aem assets screen](./images/prod-select-assets-2.png)

- Gå till mappen&quot;Generated Adobe Cycle Assets&quot; och öppna den genom att klicka på kortet. Här visas de genererade bannerarna.

![genererade adocycle-resurser](./images/prod-generated-banners.png)

- Öppna en ny flik och gå till AEM Assets igen. Navigera sedan till mappen som vi tillämpade bearbetningsprofilen på.

- I mappen överför du bilden som du vill skapa en banderoll för genom att dra och släppa den i webbläsaren, eller genom att klicka på Skapa \> filer i det övre högra hörnet av gränssnittet.

![överföring genom dra och släpp](./images/prod-drag-drop-banner.png)

![ladda upp med Skapa fil](./images/prod-create-file.png)


- Vänta en stund tills resursen bearbetas och läs sedan in skärmen igen. Om du ser resursen i läget &quot;Nytt&quot; vet du att den har bearbetats.

![resurs i nytt läge](./images/prod-asset-processed.png)

- Gå tillbaka till föregående flik och läs in skärmen igen här. Du bör lägga märke till en ny resurs i läget &quot;Nytt&quot;. Det här är vår banderoll, allt från DAM! Ser du den inte än? Vänta en minut till och läs sedan in skärmen igen.

![genererad banner](./images/prod-new-banner.png)

>[!NOTE]
>
> Är du inte nöjd med resultatet? Du kan använda en annan bearbetningsprofil för mappen och överföra resursen på nytt för att generera en annan banderoll (eller överföra en annan resurs, förstås). Under den nya överföringen frågar systemet dig vad du vill göra med den befintliga resursen och väljer&quot;Ersätt&quot;.
> ![ersätt befintlig](./images/prod-replace-asset.png)

Vi har nu en banderoll som vi kan använda senare under lanseringen av vår kampanj. Var noga med att publicera banderollen genom att markera den och sedan klicka på Snabb-Publish på menyfliksområdet.

![publicera resurs](./images/prod-publish-banner.png)

## Uppföljning i Workfront

Om ni behöver en formell och kontrollerbar granskning och godkännande av er Assets är Workfront den rätta platsen.

>[!NOTE]
>
> Även om vi uttryckligen nämner det här, är det avsikten att uppdatera uppgifterna i Workfront när du är klar med dem. Du bör alltid sträva efter ett Skapa > Granska > Godkänn-flöde.

- Vi går tillbaka till vårt projekt och expanderar dragspelsfönstret&quot;Go/No Go Banner Review&quot; för att öppna den här uppgiften genom att klicka på den:

![banner go/no-go](./images/banner-gonogo.png)

- Klicka på dokumentdelen av uppgiften (den vänstra kolumnen) och klicka sedan på den länkade AEM Assets-mappen &quot;Slutlig&quot;. Välj resursen genom att klicka på dess zon och klicka på Skapa korrektur. Ett bevis är möjligheten att korrekturläsa innehåll, t.ex. bild, text, video, webbplats, osv., på ett strukturerat och samarbetsbaserat sätt, där kommentarer, korrigeringar, ändringar av berörda intressenter samlas in, versioner och resultat kan jämföras och slutligt godkännas med ett enda klick.

![skapa korrektur](./images/wf-create-proof.png)

- Välj Avancerat korrektur när vi vill ha en detaljerad godkännandeprocess.

![avancerat korrektur](./images/wf-advanced-proof.png)

>[!NOTE]
>
> Vi kommer att besluta manuellt vem som ska granska och/eller godkänna våra bevis i det här bootlägret. I de flesta fall skulle vi använda en förinställd mall för godkännandeflöden som redan definierats för varje typ av korrektur.

- Som standard är vi i arbetsflödestypen&quot;grundläggande&quot; och vi ska välja din Workfront Bootcamp-specialist som granskare och godkännare. Skriv ditt namn på Bootcamp Workfront-specialist där det står &#39;Skriv kontaktnamn eller e-postadress för att lägga till en mottagare:

![tilldela korrektur](./images/wf-proof-assign.png)

![tilldela korrektur](./images/wf-assign-proof-2.png)

- Ange dem som &#39;Granskare och godkännare&#39;:

![granskare och godkännare](./images/wf-review-approve.png)

- Klicka på Skapa korrektur. Workfront kommer att ta en stund att generera beviset:

![genererar korrektur](./images/wf-generating-proof.png)

- Din Workfront-specialist kommer nu att få ett nytt meddelande som informerar dem om att de har ett bevis för att granska och/eller godkänna:

![arbetsyteuppgift](./images/wf-proof-task.png)

- När de har klickat på meddelandet kommer de att få ditt korrektur och kunna kommentera och/eller godkänna det här korrekturet.

   - De kan klicka på&quot;Lägg till kommentar&quot; högst upp på skärmen om de har kommentarer:

  ![Lägg till kommentar](./images/wf-proof-add-comment.png)

   - De kan då inte bara lägga in kommentarer utan även använda verktygsfältet med pekare för att tydligt definiera vilket område som behöver ändras.

  ![Fästpunktskommentar](./images/wf-proof-comment.png)

   - Genom att lägga till kommentaren kan de tala om för dig att du behöver göra lite extra arbete med en ny version av korrekturet. Uppdatera Workfront-fliken så får du ett nytt meddelande som talar om det. När du vet vilka ändringar du måste göra kan du göra AEM och sedan ladda upp den nya versionen här:

  ![ladda upp ny version](./images/wf-upload-version.png)

   - Välj den uppdaterade resursen (om inga ändringar behövs i Bootcamp-scenariot, överför bara samma resurs igen) och klicka på Länk:

  ![länkresurs](./images/wf-link-new-asset.png)

   - Klicka sedan på Skapa korrektur till höger.

  ![skapa korrektur](./images/create-new-proof.png)

   - När beviset har skapats (detta kan ta en stund) får din Workfront-specialist ett meddelande om detta och kommer att kunna granska och godkänna den nya versionen.  Genom att till exempel använda knappen för korrekturjämförelse kan de se en jämförelse sida vid sida av V1 och V2 med alla kommentarer som har gjorts.

  ![jämför korrektur](./images/wf-proof-compare.png)

  ![fatta beslut](./images/make-decision-proof.png)

  ![godkänd](./images/approved.png)

Vi har nu ett formellt godkännande av användningen av vår banderoll. Det är enkelt att följa med i den process vi är och de uppdateringar du gör automatiskt aktiverar meddelanden så att du kan arbeta på ett så effektivt sätt som möjligt.

Nästa steg: [Fas 2 - Produktion: Skapa annons för sociala medier](./social.md)

[Gå tillbaka till fas 1 - Planering: Annat förarbete](../planning/prework.md)

[Gå tillbaka till Alla moduler](../../overview.md)
