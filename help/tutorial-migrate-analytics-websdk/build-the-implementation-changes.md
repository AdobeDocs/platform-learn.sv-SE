---
title: Bygg implementeringsändringarna i utvecklingsbiblioteket
description: Lär dig hur du skapar ändringar som du har gjort i utvecklingsbiblioteket i taggegenskapen, så att du kan testa resultaten på utvecklingswebbplatsen.
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16762
source-git-commit: 7ae56d997884cf1558e72c0ad553df1c5d43c081
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---


# Bygg implementeringsändringarna i utvecklingsbiblioteket

Lär dig hur du skapar ändringar som du har gjort i utvecklingsbiblioteket i taggegenskapen, så att du kan testa resultaten på utvecklingswebbplatsen.

När du går vidare i den här självstudiekursen, eller när du vill göra ändringar i implementeringen, måste du skapa/publicera dessa ändringar för att kunna se dem på dina utvecklings-, staging- eller produktionsplatser. Jag är säker på att du har gjort det här förut, eftersom det är ett migreringsdokument och inte ett första implementeringsdokument. I själva verket vill ni göra detta ganska ofta, när ni utför varje funktion och vill testa den och se till att den fungerar som den ska, och skicka rätt data till Analytics.

Därför kommer det att finnas några påminnelser i den här självstudiekursen om hur du skapar eller publicerar dina ändringar. Om du vill kan du lägga ett bokmärke på den här sidan och inte blyga för att bygga i ditt utvecklingsbibliotek. Du kan göra det när som helst.

Låt oss bygga det vi har gjort hittills. Förresten, vi kan ibland växla&quot;skapa&quot; och&quot;publicera&quot; i den här självstudiekursen. Det viktigaste är att veta om man &quot;bygger&quot; till ett utvecklings- eller staging-bibliotek, eller om man &quot;publicerar&quot; till produktionsbiblioteket och miljön, oavsett vilket ord vi använder.

## Bygg migreringsändringar av utvecklingen i Experience Platform-taggar

1. När du är i egenskapen Experience Platform väljer du **Publiceringsflöde** i den vänstra navigeringen och lägger sedan till ett nytt bibliotek.

   ![Publiceringsflöde](assets/publishing-flow-new-library.jpg)

1. Namnge biblioteket vad du vill, till exempel **Inledande migrering av SDK för webben**.
1. Välj miljön **Utveckling**.
1. Välj **Lägg till alla ändrade resurser** om du vill lägga till alla objekt som du har arbetat med.

   ![Nytt bibliotek](assets/new-library-websdk-migration.jpg)

1. Spara och bygg till utveckling

   ![Spara och bygg till dev](assets/save-and-build-to-dev.jpg)

1. När bygget är klart kan du se om bygget lyckades. För musen över den gröna punkten till vänster om det nya biblioteket i ditt publiceringsflöde, och om den är grön kommer den att ha slutförts utan problem, och du kommer att få veta det.

   ![Publiceringen har slutförts](assets/successful-publish.jpg)

### Välj ett arbetsbibliotek

Här är en bra genväg när du gör ändringar i taggar. Istället för att gå igenom hela publiceringsflödet varje gång du gör en ändring kan du välja ett arbetsbibliotek och spara och bygga med en enkel musklickning. Gör det. Du kommer att tacka mig senare.

1. I stort sett var som helst i tagggränssnittet klickar du på Välj ett arbetsbibliotek längst upp till höger i användargränssnittet och väljer det du vill ha. I den här självstudiekursen väljer du Inledande migrering av SDK för webben.

   ![Välj arbetsbibliotek](assets/select-working-library.jpg)

