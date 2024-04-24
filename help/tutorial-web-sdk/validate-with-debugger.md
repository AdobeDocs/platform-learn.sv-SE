---
title: Validera Web SDK-implementeringar med Experience Platform Debugger
description: Lär dig hur du validerar implementeringen av din Platform Web SDK med Adobe Experience Platform Debugger. Den här lektionen ingår i självstudiekursen Implementera Adobe Experience Cloud med Web SDK.
feature: Web SDK,Tags,Debugger
exl-id: 150bb1b1-4523-4b44-bd4e-6cabc468fc04
source-git-commit: aeff30f808fd65370b58eba69d24e658474a92d7
workflow-type: tm+mt
source-wordcount: '1165'
ht-degree: 0%

---

# Validera Web SDK-implementeringar med Experience Platform Debugger

Lär dig hur du validerar implementeringen av din Platform Web SDK med Adobe Experience Platform Debugger.

Felsökaren Experience Platform är ett tillägg för webbläsarna Chrome och Firefox som gör att du kan se Adobe-tekniken som används på dina webbsidor. Ladda ned den version du föredrar:

* [Firefox-tillägg](https://addons.mozilla.org/sv-SE/firefox/addon/adobe-experience-platform-dbg/)
* [Kromtillägg](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

Om du aldrig har använt felsökningsfunktionen tidigare - och den här är en annan än den tidigare Adobe Experience Cloud Debugger - kan du titta på den här översiktsvideon med fem minuter:

>[!VIDEO](https://video.tv.adobe.com/v/32156?learn=on)

I den här lektionen använder du [Adobe Experience Cloud Debugger-tillägg](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj) som ersätter taggegenskapen hårdkodad på [Luma demo site](https://luma.enablementadobe.com/content/luma/us/en.html) med din egen egendom.

Den här tekniken kallas för miljöväxling och kan vara användbar senare när du arbetar med taggar på din egen webbplats. Du kan läsa in din produktionswebbplats i webbläsaren, men med *utveckling* -tagg. På så sätt kan du tryggt göra och validera taggändringar oberoende av dina vanliga kodreleaser. Den här åtskillnaden mellan marknadsföringstaggreleaser och vanliga kodreleaser är ju en av de främsta anledningarna till att kunderna använder taggar i första hand!

## Utbildningsmål

När lektionen är klar kan du använda felsökaren för att:

* Läsa in ett alternativt taggbibliotek
* Validera att XDM-händelsen på klientsidan hämtar in och skickar data som förväntas till Platform Edge Network
* Aktivera Edge Trace för att visa begäranden på serversidan som skickats av Platform Edge Network

## Förutsättningar

Du känner till datainsamlingstaggar och [Luma demo site](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} och har avslutat tidigare lektioner i självstudiekursen:

* [Konfigurera ett XDM-schema](configure-schemas.md)
* [Konfigurera ett identitetsnamnutrymme](configure-identities.md)
* [Konfigurera ett datastream](configure-datastream.md)
* [Web SDK-tillägget är installerat i taggegenskapen](install-web-sdk.md)
* [Skapa dataelement](create-data-elements.md)
* [Skapa identiteter](create-identities.md)
* [Skapa taggregler](create-tag-rule.md)

## Läsa in alternativa taggbibliotek med Felsökning

Felsökaren i Experience Platform har en cool funktion som gör att du kan ersätta ett befintligt taggbibliotek med ett annat. Den här tekniken är användbar vid validering och gör att vi kan hoppa över många implementeringssteg i den här självstudiekursen.

1. Se till att du har [Lumas demowebbplats](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} öppna och markera Experience Platform-ikonen för felsökningstillägget
1. Felsökaren öppnas och visar information om den hårdkodade implementeringen (du kan behöva läsa in Luma-webbplatsen igen när du har öppnat felsökaren)
1. Bekräfta att felsökaren är **[!UICONTROL Connected to Luma]**&quot; enligt bilden nedan och välj sedan &quot;**[!UICONTROL lock]**&quot; om du vill låsa felsökaren till Luma-webbplatsen.
1. Välj **[!UICONTROL Sign In]** och logga in på Adobe Experience Cloud med ditt Adobe ID.
1. Gå till **[!UICONTROL Experience Platform Tags]** till vänster navigering

   ![Skärm för felsökningstagg](assets/validate-launch-screen.png)

1. Välj **[!UICONTROL Configuration]** tab
1. Till höger om där den visar dig **[!UICONTROL Page Embed Codes]**&#x200B;öppnar du **[!UICONTROL Actions]** och markera **[!UICONTROL Replace]**

   ![Välj Åtgärder > Ersätt](assets/validate-switch-environment.png)

1. Eftersom du är autentiserad kommer felsökaren att hämta tillgängliga taggegenskaper och -miljöer. Välj din egenskap, i det här fallet `Web SDK Course 3`
1. Välj `Development` miljö
1. Välj **[!UICONTROL Apply]** knapp

   ![Välj den alternativa taggegenskapen](assets/validate-switch-selection.png)

1. Lumas webbplats kommer nu att läsas in igen _med din egen taggegenskap_.

   ![tagg, egenskap ersatt](assets/validate-switch-success.png)

När du fortsätter med självstudiekursen använder du den här tekniken för att mappa Luma-webbplatsen till din egen taggegenskap för att validera implementeringen av din Platform Web SDK. När du börjar använda taggar på produktionswebbplatsen kan du använda samma teknik för att validera ändringar som du gör i utvecklingsmiljön för taggar.

## Validera nätverksbegäranden på klientsidan med Experience Platform Debugger

Du kan använda felsökaren för att validera klientsidesbeacons som aktiveras från plattformens Web SDK-implementering för att visa data som skickas till Platform Edge Network:

1. Gå till **[!UICONTROL Summary]** i den vänstra navigeringen om du vill se information om taggegenskapen

   ![Fliken Sammanfattning](assets/validate-summary.png)

1. Gå till **[!UICONTROL Experience Platform Web SDK]** i den vänstra navigeringen för att se **[!UICONTROL Network Requests]**
1. Öppna **[!UICONTROL events]** rad

   ![Adobe Experience Platform Web SDK-begäran](assets/validate-aep-screen.png)

1. Se hur du kan se `web.webpagedetails.pageView` händelsetyp som du har angett i [!UICONTROL Update variable] och andra färdiga variabler som följer `AEP Web SDK ExperienceEvent` fältgrupp

   ![Händelseinformation](assets/validate-event-pageViews.png)

1. Bläddra nedåt till `web` -objekt, välj att öppna det och inspektera `webPageDetails.name`, `webPageDetails.server`och `webPageDetails.siteSection`. De ska matcha motsvarande `digitalData` datalagervariabler på hemsidan

>[!TIP]
>
> Visa och jämföra `digitalData` datalager på hemsidan:
>
> 1. Öppna webbläsarutvecklarverktygen på Lumas hemsida. I Chrome väljer du knapp `F12` på tangentbordet
> 1. Välj **[!UICONTROL Console]** tab
> 1. Retur `digitalData` och markera `Enter` på tangentbordet för att visa datalagrets värden

![Fliken Nätverk](assets/validate-xdm-content.png)

Du kan även validera informationen i identitetskartan:

1. Logga in på Luma-webbplatsen med inloggningsuppgifterna `test@adobe.com`/`test`

1. Återgå till [Lumas hemsida](https://luma.enablementadobe.com/content/luma/us/en.html)

1. Öppna **[!UICONTROL Experience Platform Web SDK]** till vänster

   ![Web SDK in Debugger](assets/identity-debugger-websdk-dark.png)

1. Välj **[!UICONTROL events]** rad för att öppna information i ett popup-fönster

   ![Web SDK in Debugger](assets/identity-deugger-websdk-event-dark.png)

1. Sök efter **identityMap** i popup-fönstret. Här ska du se `lumaCrmId` med tre nycklar för authenticatedState, id och primär:
   ![Web SDK in Debugger](assets/identity-deugger-websdk-event-lumaCrmId-dark.png)

### Validera klientförfrågningar med utvecklingsverktyg i webbläsaren

Den här typen av förfrågningsinformation visas också i webbläsarens webbutvecklingsverktyg **Nätverk** (förutsatt att webbplatsen läser in taggbiblioteket).

1. Öppna webbläsarens webbutvecklingsverktyg **Nätverk** och läsa in sidan igen. Filtrera samtal med `/ee` för att hitta samtalet markerar du det och tittar sedan på **Sidhuvuden** och **Nyttolast** tab

   ![Fliken Nätverk](assets/validate-dev-console.png)

1. Gå till **Svar** och notera hur ECID-värdet ingår i svaret. Kopiera det här värdet så som du kommer att använda det för att validera profilinformationen i nästa övning

   ![Fliken Nätverk](assets/validate-dev-console-ecid.png)

   >[!NOTE]
   >
   > ECID-värdet visas i nätverkssvaret. Den ingår inte i `identityMap` del av nätverksbegäran, och den lagras inte i det här formatet i en cookie.

## Validera nätverksbegäranden på serversidan med Experience Platform Debugger

Som du lärde dig i [Konfigurera ett datastream](configure-datastream.md) Platform Web SDK skickar först data från din digitala egendom till Platform Edge Network. Sedan gör Platform Edge Network ytterligare serverförfrågningar till motsvarande tjänster som är aktiverade i ditt datastream. Du kan validera de serverförfrågningar som gjorts av Platform Edge Network genom att använda Edge Trace i felsökaren.

<!--Furthermore, you can also validate the fully processed payload after it reaches an Adobe application by using [Adobe Experience Platform Assurance](https://experienceleague.adobe.com/en/docs/experience-platform/assurance/home). -->


### Aktivera Edge Trace

Så här aktiverar du Edge Trace:

1. I vänster navigering i **[!UICONTROL Experience Platform Debugger]** välj **[!UICONTROL Logs]**
1. Välj **[!UICONTROL Edge]** och markera **[!UICONTROL Connect]**

   ![Koppla kantkalkering](assets/analytics-debugger-edgeTrace.png)

1. Det är tomt för tillfället

   ![Ansluten kantkalkering](assets/analytics-debugger-edge-connected.png)

1. Uppdatera [Lumas startsida](https://luma.enablementadobe.com/) och kontrollera **[!UICONTROL Experience Platform Debugger]** än en gång för att se data komma igenom.

   ![Kantkalkering för analysfyr](assets/validate-edge-trace.png)

För närvarande kan du inte visa några Platform Edge Network-begäranden som går till ett Adobe-program eftersom du inte har aktiverat några i datastream. I framtida lektioner använder du Edge Trace för att visa utgående begäranden på serversidan till Adobe-program och händelsevidarebefordran. Men först får du lära dig mer om ett annat verktyg för att validera serverförfrågningar från Platform Edge Network - Adobe Experience Platform Assurance!

[Nästa: ](validate-with-assurance.md)

>[!NOTE]
>
>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Web SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela med dig av dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
