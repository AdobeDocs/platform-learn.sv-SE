---
title: Använd ramverket för datastyrning
seo-title: Apply the data governance framework | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Använd ramverket för datastyrning
description: I den här lektionen kommer du att använda ramverket för datastyrning på data som du har inhämtat till din sandlåda.
role: Data Architect
feature: Data Governance
jira: KT-4348
thumbnail: 4348-apply-data-governance-framework.jpg
exl-id: 3cc3c794-5ffd-41bf-95d8-be5bca2e3a0f
source-git-commit: 00ef0f40fb3d82f0c06428a35c0e402f46ab6774
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 0%

---

# Använd ramverket för datastyrning

<!--15min-->

I den här lektionen kommer du att använda ramverket för datastyrning på data som du har inhämtat till din sandlåda.

Med Adobe Experience Platform Data Governance kan ni hantera kunddata och säkerställa att ni följer regler, begränsningar och policyer som gäller för dataanvändning. Det spelar en viktig roll inom Experience Platform på olika nivåer, bland annat när det gäller att kontrollera användningen av data.

Titta på följande korta videor om datastyrning innan du börjar övningarna:
>[!VIDEO](https://video.tv.adobe.com/v/36653?learn=on)

>[!VIDEO](https://video.tv.adobe.com/v/29708?learn=on)

<!--
## Permissions required

In the [Configure Permissions](configure-permissions.md) lesson, you set up all the access controls required to complete this lesson, specifically:

* Permission items **[!UICONTROL Data Governance]** > **[!UICONTROL Manage Usage Labels]**, **[!UICONTROL Manage Data Usage Policies]** and **[!UICONTROL View Data Usage Policies]**
* Permission items **[!UICONTROL Data Management]** > **[!UICONTROL View Datasets]** and **[!UICONTROL Manage Datasets]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` Product Profile
-->

## Affärsscenario

Luma lovar medlemmarna i deras lojalitetsprogram att lojalitetsdata inte delas med tredje part. Vi kommer att implementera det här scenariot i resten av lektionen.

## Använd etiketter för datastyrning

Det första steget i datastyrningsprocessen är att använda styrningsetiketter på dina data. Innan vi gör det ska vi ta en snabb titt på vilka etiketter som finns:

1. Välj **[!UICONTROL Policies]** i den vänstra navigeringen i plattformens användargränssnitt
1. Gå till fliken **[!UICONTROL Labels]** om du vill se alla etiketter i kontot.

Det finns många färdiga etiketter, och du kan skapa egna med knappen [!UICONTROL Create label]. Det finns tre huvudtyper: [!UICONTROL Contract labels], [!UICONTROL Identity labels] och [!UICONTROL Sensitive labels] som motsvarar vanliga orsaker. Data kan vara begränsade. Var och en av etiketterna har en [!UICONTROL Friendly Name] och en kort [!UICONTROL Name] som bara är en förkortning av typen och ett tal. Etiketten [!DNL C1] är till exempel för Ingen tredjepartsexport, vilket är vad vi behöver för vår lojalitetspolicy.

![Etikett för datastyrning](assets/governance-policies.png)

Nu är det dags att märka de data vars användning vi vill begränsa:

1. Välj **[!UICONTROL Datasets]** i den vänstra navigeringen i plattformens användargränssnitt
1. Öppna `Luma Loyalty Dataset`
1. Gå till fliken **[!UICONTROL Data Governance]**
1. Du kan antingen använda etiketter på enskilda fält eller använda dem på hela datauppsättningen. Vi kommer att tillämpa etiketten på hela datauppsättningen. Klicka på pennikonen. Om du inte ser ikonen kan du göra webbläsaren bredare eller rulla den mellersta panelen åt höger.
   ![Datastyrning](assets/governance-dataset.png)
1. Utöka avsnittet **[!UICONTROL Contract Labels]** i modal och kontrollera etiketten **[!UICONTROL C2]**
1. Markera knappen **[!UICONTROL Save changes]**
   ![Datastyrning](assets/governance-applyLabel.png)
1. Om du återgår till huvudskärmen [!UICONTROL Data Governance], med **[!UICONTROL Show inherited labels]** aktiverat, kan du se hur etiketten har tillämpats på alla fält i datauppsättningen.
   ![Datastyrning](assets/governance-labelsAdded.png)


<!--adding extra, unnecessary fields from field groups makes it harder to see which fields really need labels-->
<!--Are there any best practices for applying governance labels-->

## Skapa datastyrningspolicyer

Nu när våra data är märkta kan vi skapa en politik.

1. Välj **[!UICONTROL Policies]** i den vänstra navigeringen i plattformens användargränssnitt
1. På fliken Bläddra finns det redan en användningsprincip som heter &quot;Export restriction&quot; från tredje part som kopplar C2-etiketten till marknadsföringsåtgärden [!UICONTROL Export to Third Party] - exakt det vi behöver!
1. Välj profilen och aktivera den sedan via växlingsknappen **[!UICONTROL Policy status]**
   ![Datastyrning](assets/governance-enablePolicy.png)

Du kan skapa egna profiler genom att välja knappen **[!UICONTROL Create policy]**. Då öppnas en guide där du kan kombinera flera etiketter och begränsningar för marknadsföringsåtgärder.

## Stärk styrningspolicyer

Verkställandet av styrningspolitik är uppenbarligen en viktig del av ramverket. Tvingande åtgärder utförs längre fram i kedjan när data aktiveras och skickas från Platform, särskilt med Real-time Customer Data Platform, som du kanske inte har någon licens för. Vilket som. Det ligger utanför kursens räckvidd. Men så att du inte blir kvar kan du lära dig mer om hur policyer tillämpas i den här videon, som jag har ställt i kö upp till den relevanta delen. Den visar också vad som händer när en policy överträds.

>[!VIDEO](https://video.tv.adobe.com/v/33631/?t=151&quality=12&learn=on)


## Ytterligare resurser

* [Dokumentation för datastyrning](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html)
* [API-referens för datauppsättningstjänst](https://www.adobe.io/experience-platform-apis/references/dataset-service/)
* [API-referens för principtjänst](https://www.adobe.io/experience-platform-apis/references/policy-service/)

Nu går vi vidare till [frågetjänsten](run-queries.md).
