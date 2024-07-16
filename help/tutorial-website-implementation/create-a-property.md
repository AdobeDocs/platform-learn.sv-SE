---
title: Skapa en taggegenskap
description: Lär dig hur du loggar in i gränssnittet för datainsamling och skapar en taggegenskap. Den här lektionen är en del av självstudiekursen Implementera Experience Cloud på webbplatser.
exl-id: f83d374a-a831-4598-b9d3-6f183224b589
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---

# Skapa en taggegenskap

I den här lektionen skapar du din första taggegenskap.

En egenskap är i princip en behållare som du fyller med tillägg, regler, dataelement och bibliotek när du distribuerar taggar till webbplatsen.

## Förhandskrav

För att kunna slutföra de kommande lektionerna måste du ha behörighet att skapa, godkänna, Publish, hantera tillägg och hantera miljöer i taggar. Om du inte kan slutföra något av dessa steg eftersom du inte har tillgång till gränssnittsalternativen ber du Experience Cloud-administratören att få åtkomst. Mer information om tagganvändarbehörigheter finns i [dokumentationen](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html).

>[!NOTE]
>
>Adobe Experience Platform Launch håller på att integreras i Adobe Experience Platform som en serie datainsamlingstekniker. Flera terminologiska förändringar har introducerats i gränssnittet som du bör vara medveten om när du använder det här innehållet:
>
> * Platforma launchen (klientsidan) är nu **[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=sv)**
> * Platforma launchens serversida är nu **[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html)**
> * Edge-konfigurationer är nu **[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html)**

## Utbildningsmål

När lektionen är klar kan du:

* Logga in i användargränssnittet för datainsamling
* Skapa en ny taggegenskap
* Konfigurera en taggegenskap

## Gå till gränssnittet Datainsamling

**För att komma till datainsamlingen**

1. Logga in på [Adobe Experience Cloud](https://experiencecloud.adobe.com)

1. Klicka på ikonen ![Solution Switcher ](images/launch-solutionSwitcher.png) för att öppna appväljaren

1. Välj **[!UICONTROL Launch/Data Collection]** på menyn ![Öppna lösningsväljaren med hjälp av ikonen och klicka på Starta/Datainsamling](images/launch-solutionSwitcherActivation.png)

Du bör nu se skärmen `Tags Properties` (om inga egenskaper har skapats i kontot kan den här skärmen vara tom):

![Skärmen Egenskaper](images/launch-propertiesScreen.png)

## Skapa en egenskap

En egenskap är i princip en behållare som du fyller med tillägg, regler, dataelement och bibliotek när du distribuerar taggar till webbplatsen. En egenskap kan vara en gruppering av en eller flera domäner och underdomäner. Du kan hantera och spåra dessa resurser på liknande sätt. Anta till exempel att du har flera webbplatser som är baserade på en mall och vill spåra samma resurser på alla. Du kan använda en egenskap på flera domäner. Mer information om hur du skapar egenskaper finns i [&quot;Företag och egenskaper&quot;](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/companies-and-properties.html) i produktdokumentationen.

**Så här skapar du en egenskap**

1. Klicka på knappen **[!UICONTROL New Property]**:

   ![Klicka på Ny egenskap](images/launch-addNewProperty.png)

1. Namnge din egenskap (t.ex. `Luma Tutorial` eller `Luma Tutorial - Daniel`)
1. Som domän anger du `enablementadobe.com` eftersom det här är den domän där Luma-demowebbplatsen finns. Trots att fältet &quot;Domän&quot; är obligatoriskt fungerar taggegenskapen på alla domäner där det implementeras. Huvudsyftet med det här fältet är att förifylla menyalternativ i regelbyggaren.
1. Expandera avsnittet **[!UICONTROL Advanced Options]** och markera kryssrutan till **[!UICONTROL Run rule components in sequence]**
1. Klicka på knappen **[!UICONTROL Save]**

   ![Skapa en ny egenskap](images/launch-newProperty.png)

Den nya egenskapen bör visas på sidan Egenskaper. Observera att om du markerar rutan bredvid egenskapsnamnet visas alternativen för **[!UICONTROL Configure]** eller **[!UICONTROL Delete]** egenskapen ovanför egenskapslistan. Klicka på namnet på din egenskap (t.ex. `Luma Tutorial`) för att öppna skärmen `Overview`.
![Klicka på egenskapens namn för att öppna den](images/launch-openProperty.png)

[Nästa&quot;Lägg till inbäddningskod&quot; >](add-embed-code.md)
