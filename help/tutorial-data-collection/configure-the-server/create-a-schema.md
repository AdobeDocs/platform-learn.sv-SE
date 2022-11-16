---
title: Skapa ett schema
description: Skapa ett schema
exl-id: 0256b358-0c2c-4c59-ab23-5fe0d38880d6
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# Skapa ett schema

Som beskrivs i [Strukturera data](../structuring-your-data.md)måste data som skickas till Adobe Experience Platform vara i XDM. Mer specifikt måste dina data matcha en _schema_. Ett schema är i princip en beskrivning av hur data ska se ut. Den beskriver namnen på fälten och var de ska placeras i data. Den beskriver också vilken typ av värde varje fält ska ha (till exempel ett booleskt värde, en sträng med en längd på 12 tecken, en array med siffror).

Adobe Experience Platform har några färdiga byggstenar, så kallade fältgrupper som är vanliga inom branschen. För finanssektorn finns det t.ex. fältgrupper för saldoöverföringar och låneansökningar. För rese- och turismbranschen finns det fältgrupper för bokningar av flyg och inkvartering.

Vi rekommenderar att du använder de inbyggda fältgrupperna där det är möjligt när du skapar ditt schema. Vi förstår också att du kan behöva fält som är specifika för ditt eget företag. Därför kan du skapa egna fältgrupper som du kan använda i de scheman du skapar.

Låt oss gå igenom hur vi skapar ett schema för en vanlig e-handelswebbplats.

1. Välj **[!UICONTROL Scheman]** under [!UICONTROL Datahantering] från den vänstra menyn i Adobe Experience Platform gränssnitt.
1. Välj **[!UICONTROL Skapa schema]** i det övre högra hörnet, och **[!UICONTROL XDM ExperienceEvent]** i listrutan.

Du är nu på arbetsytan i Schemaläggaren.
![Schemavy](../assets/schemas-view.png)

## Lägg till fältgrupper

1. I **[!UICONTROL Fältgrupper]** till vänster i **[!UICONTROL Struktur]** markerar du **[!UICONTROL + Lägg till]** länk. Nu visas en modal som väljer vilka fältgrupper som ska läggas till i schemat.
1. Markera först fältgruppen med namnet **[!UICONTROL AEP Web SDK ExperienceEvent]**. Den här fältgruppen lägger till en uppsättning fält som rymmer data som automatiskt samlas in av Adobe Experience Platform Web SDK.
   ![AEP Web SDK mixin](../assets/aep-web-sdk-mixin.png)
1. Eftersom webbplatsen för den här självstudiekursen är en e-handelswebbplats väljer du **[!UICONTROL Handelsinformation]** fältgrupp. Med den här fältgruppen kan du skicka vanliga affärsdata som vilka produkter som visas, läggs till i kundvagnen och köps.
1. Välj **[!UICONTROL Lägg till fältgrupper]** längst upp till höger i dialogrutan.
   ![Blanda handelsdetaljer](../assets/commerce-details-mixin.png)
1. Nu bör du se schemats struktur.
   ![Schema med blandningar](../assets/schema-with-mixins.png)

## Spara schemat

1. Ange ett namn och en beskrivning till höger på skärmen och välj **[!UICONTROL Spara]**.
   ![Schema med namn och beskrivning](../assets/schema-name-description.png)

Ditt schema har skapats. Nu ska vi lära oss hur du skapar en datauppsättning för att lagra dina data.

Mer information om att skapa scheman finns i [Skapa scheman](/help/platform/schemas/create-schemas.md).

[Nästa: ](create-a-dataset.md)

>[!NOTE]
>
>Tack för att du har lagt ned din tid på att lära dig om datainsamling. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela med dig av dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)
