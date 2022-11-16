---
title: Skapa en taggegenskap
description: Lär dig hur du loggar in i gränssnittet för datainsamling och skapar en taggegenskap. Den här lektionen är en del av självstudiekursen Implementera Experience Cloud på webbplatser.
exl-id: f83d374a-a831-4598-b9d3-6f183224b589
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 1%

---

# Skapa en taggegenskap

I den här lektionen skapar du din första taggegenskap.

En egenskap är i princip en behållare som du fyller med tillägg, regler, dataelement och bibliotek när du distribuerar taggar till webbplatsen.

## Förutsättningar

För att kunna slutföra de kommande lektionerna måste du ha behörighet att utveckla, godkänna, publicera, hantera tillägg och hantera miljöer i taggar. Om du inte kan slutföra något av dessa steg eftersom du inte har tillgång till gränssnittsalternativen ber du Experience Cloud-administratören att få åtkomst. Mer information om att tagga användarbehörigheter finns i [dokumentationen](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html).

>[!NOTE]
>
>Adobe Experience Platform Launch håller på att integreras i Adobe Experience Platform som en serie datainsamlingstekniker. Flera terminologiska förändringar har introducerats i gränssnittet som du bör vara medveten om när du använder det här innehållet:
>
> * platforma launchen (klientsidan) är nu **[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=sv)**
> * platform launch Server Side is now **[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html)**
> * Edge-konfigurationer är nu **[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html)**


## Utbildningsmål

När lektionen är klar kan du:

* Logga in i användargränssnittet för datainsamling
* Skapa en ny taggegenskap
* Konfigurera en taggegenskap

## Gå till gränssnittet Datainsamling

**För att komma till datainsamling**

1. Logga in på [Adobe Experience Cloud](https://experiencecloud.adobe.com)

1. Klicka på ![Ikon för lösningsväljare](images/launch-solutionSwitcher.png) -ikon för att öppna appväljaren

1. Välj **[!UICONTROL Starta/samla in data]** från menyn ![Öppna lösningsväljaren med hjälp av ikonen och klicka på Starta/Samla in data](images/launch-solutionSwitcherActivation.png)

Nu bör du se `Tags Properties` skärm (den här skärmen kan vara tom om inga egenskaper har skapats i kontot):

![Egenskapsskärmen](images/launch-propertiesScreen.png)

## Skapa en egenskap

En egenskap är i princip en behållare som du fyller med tillägg, regler, dataelement och bibliotek när du distribuerar taggar till webbplatsen. En egenskap kan vara en gruppering av en eller flera domäner och underdomäner. Du kan hantera och spåra dessa resurser på liknande sätt. Anta till exempel att du har flera webbplatser som är baserade på en mall och vill spåra samma resurser på alla. Du kan använda en egenskap på flera domäner. Mer information om hur du skapar egenskaper finns i [&quot;Företag och egendomar&quot;](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/companies-and-properties.html) i produktdokumentationen.

**Skapa en egenskap**

1. Klicka på **[!UICONTROL Ny egenskap]** knapp:

   ![Klicka på Ny egenskap](images/launch-addNewProperty.png)

1. Namnge din egendom (t.ex. `Luma Tutorial` eller `Luma Tutorial - Daniel`)
1. Som domän anger du `enablementadobe.com` eftersom det är den domän där Lumas demowebbplats finns. Trots att fältet &quot;Domän&quot; är obligatoriskt fungerar taggegenskapen på alla domäner där det implementeras. Huvudsyftet med det här fältet är att förifylla menyalternativ i regelbyggaren.
1. Expandera **[!UICONTROL Avancerade alternativ]** och markera kryssrutan till **[!UICONTROL Kör regelkomponenter i sekvens]**
1. Klicka på **[!UICONTROL Spara]** knapp

   ![Skapa en ny egenskap](images/launch-newProperty.png)

Den nya egenskapen bör visas på sidan Egenskaper. Observera att om du markerar rutan bredvid egenskapsnamnet kan du välja **[!UICONTROL Konfigurera]** eller **[!UICONTROL Ta bort]** egenskapen visas ovanför egenskapslistan. Klicka på egenskapens namn (t.ex. `Luma Tutorial`) för att öppna `Overview` skärm.
![Klicka på namnet på egenskapen för att öppna den](images/launch-openProperty.png)

[Nästa&quot;Lägg till inbäddningskod&quot; >](add-embed-code.md)
