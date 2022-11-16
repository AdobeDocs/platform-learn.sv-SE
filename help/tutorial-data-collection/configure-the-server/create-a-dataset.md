---
title: Skapa en datauppsättning
description: Skapa en datauppsättning
exl-id: 19a60087-2f78-4510-b127-b1007a6b7a56
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# Skapa en datauppsättning

Förutom att beskriva data som du skickar till Adobe Experience Platform måste du ha en plats där du kan lagra data. I Adobe Experience Platform kallas de här bucklarna där du kan skicka data för datauppsättningar.

>[!NOTE]
>
>Datauppsättningar krävs inte om du bara använder Platform Web SDK för att skicka data till Adobe Analytics, Adobe Target och Adobe Audience Manager eller om du använder händelsevidarebefordran. Om du bara använder Web SDK för dessa ändamål kan du hoppa över den här sidan av självstudiekursen.

1. Välj **[!UICONTROL Datauppsättningar]** under [!UICONTROL Datahantering] från den vänstra menyn i Adobe Experience Platform.
1. Välj sedan **[!UICONTROL Skapa datauppsättning]** i det övre högra hörnet.
   ![Vyn Datauppsättningar](../assets/datasets-view.png)

## Skapa en datauppsättning från schema

1. Från [!UICONTROL Arbetsflöde] gränssnitt, välj den första plattan, **[!UICONTROL Skapa datauppsättning från schema]**.
1. Sök efter [schemat som du skapade tidigare](create-a-schema.md) och markera den.
   ![Val av schema](../assets/schema-selection.png)
1. Välj **[!UICONTROL Nästa]** och ange ett namn och en beskrivning.
   ![Datauppsättningens namn och beskrivning](../assets/dataset-name-description.png)
1. Välj **[!UICONTROL Slutför]**. Din datauppsättning har skapats och är klar att ta emot data.

När du börjar skicka data till en datauppsättning validerar Adobe Experience Platform att de data du försöker placera i datauppsättningen överensstämmer med det tillämpade schemat. Om data inte överensstämmer med schemat avvisas data och placeras inte i datauppsättningen. Som ett resultat av detta valideringssteg kan användare av datauppsättningen (Adobe-produkter, tredje parter eller ditt eget företag) ha viss säkerhet när det gäller datauppsättningens struktur och renhet.

Mer information om hur du skapar datauppsättningar finns i [Skapa datauppsättningar och importera data](/help/platform/data-ingestion/create-datasets-and-ingest-data.md).

[Nästa: ](create-a-datastream.md)

>[!NOTE]
>
>Tack för att du har lagt ned din tid på att lära dig om datainsamling. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela med dig av dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)

