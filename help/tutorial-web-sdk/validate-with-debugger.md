---
title: Validera Web SDK-implementeringar med Experience Platform Debugger
description: Lär dig hur du validerar din Platform Web SDK-implementering med Adobe Experience Platform Debugger. Den här lektionen är en del av självstudiekursen Implementera Adobe Experience Cloud med Web SDK.
feature: Web SDK,Tags,Debugger
jira: KT-15405
exl-id: 150bb1b1-4523-4b44-bd4e-6cabc468fc04
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '1131'
ht-degree: 0%

---

# Validera Web SDK-implementeringar med Experience Platform Debugger

Lär dig validera Adobe Experience Platform Web SDK-implementeringen med Adobe Experience Platform Debugger.

Experience Platform Debugger är ett tillägg för Chrome- och Firefox-webbläsare som hjälper dig att se hur Adobe-tekniken som används på dina webbsidor fungerar. Ladda ned den version du föredrar:

* [Firefox-tillägg](https://addons.mozilla.org/sv-SE/firefox/addon/adobe-experience-platform-dbg/)
* [Chrome-tillägg](https://chromewebstore.google.com/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

Om du aldrig har använt felsökaren tidigare kanske du vill titta på den här översiktsvideon på fem minuter:

>[!VIDEO](https://video.tv.adobe.com/v/32156?learn=on&enablevpops)

I den här lektionen använder du [Adobe Experience Platform Debugger-tillägget](https://chromewebstore.google.com/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) för att ersätta taggegenskapen som är hårdkodad på [Luma-demowebbplatsen](https://luma.enablementadobe.com/content/luma/us/en.html) med din egen egenskap.

Den här tekniken kallas för miljöväxling och kan vara användbar senare när du arbetar med taggar på din egen webbplats. Du kan läsa in din produktionswebbplats i webbläsaren, men med ditt *development* -taggbibliotek. På så sätt kan du tryggt göra och validera taggändringar oberoende av dina vanliga kodreleaser. Den här åtskillnaden mellan marknadsföringstaggreleaser och vanliga kodreleaser är ju en av de främsta anledningarna till att kunderna använder taggar i första hand!

## Utbildningsmål

När lektionen är klar kan du använda felsökaren för att:

* Läsa in ett alternativt taggbibliotek
* Validera att XDM-händelsen på klientsidan hämtar in och skickar data som förväntas till Platform Edge Network
* Aktivera Edge Trace för att visa begäranden på serversidan som skickats av Platform Edge Network

## Förhandskrav

Du är bekant med datainsamlingstaggar och [Luma demo-webbplatsen](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} och har slutfört föregående lektioner i självstudiekursen:

* [Konfigurera ett XDM-schema](configure-schemas.md)
* [Konfigurera ett identitetsnamnutrymme](configure-identities.md)
* [Konfigurera ett datastream](configure-datastream.md)
* [Web SDK-tillägget är installerat i taggegenskapen](install-web-sdk.md)
* [Skapa dataelement](create-data-elements.md)
* [Skapa identiteter](create-identities.md)
* [Skapa taggregler](create-tag-rule.md)

## Läsa in alternativa taggbibliotek med Felsökning

Experience Platform Debugger har en cool funktion som gör att du kan ersätta ett befintligt taggbibliotek med ett annat. Den här tekniken är användbar vid validering och gör att vi kan hoppa över många implementeringssteg i den här självstudiekursen.

1. Kontrollera att du har webbplatsen [Luma demo](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} öppen och välj ikonen för Experience Platform Debugger-tillägget
1. Felsökaren öppnas och visar information om den hårdkodade implementeringen (du kan behöva läsa in Luma-webbplatsen igen när du har öppnat felsökaren)
1. Bekräfta att felsökaren är **[!UICONTROL Connected to Luma]** enligt bilden nedan och välj sedan ikonen **[!UICONTROL lock]** för att låsa felsökaren till Luma-webbplatsen.
1. Välj knappen **[!UICONTROL Sign In]** och logga in på Adobe Experience Cloud med ditt Adobe ID.
1. Gå nu till **[!UICONTROL Experience Platform Tags]** i den vänstra navigeringen

   ![Skärm för felsökningstagg](assets/validate-launch-screen.png)

1. Välj fliken **[!UICONTROL Configuration]**
1. Öppna listrutan **[!UICONTROL Actions]** till höger om den plats där **[!UICONTROL Page Embed Codes]** visas och välj **[!UICONTROL Replace]**

   ![Välj Åtgärder > Ersätt](assets/validate-switch-environment.png)

1. Eftersom du är autentiserad kommer felsökaren att hämta tillgängliga taggegenskaper och -miljöer. Välj din egenskap
1. Välj din `Development`-miljö
1. Markera knappen **[!UICONTROL Apply]**

   ![Välj den alternativa taggegenskapen](assets/validate-switch-selection.png)

1. Luma-webbplatsen kommer nu att läsa in _igen med din egen taggegenskap_.

   ![taggegenskap ersatt](assets/validate-switch-success.png)

När du fortsätter med självstudiekursen använder du den här tekniken för att mappa Luma-webbplatsen till din egen taggegenskap för att validera din Platform Web SDK-implementering. När du använder taggar på din egen webbplats kan du använda samma teknik för att validera utvecklingstaggbibliotek på din produktionswebbplats.

## Validera nätverksbegäranden på klientsidan med Experience Platform Debugger

Du kan använda felsökaren för att validera klientsidesbeacons som aktiveras från din Platform Web SDK-implementering för att visa data som skickas till Platform Edge Network:

1. Gå till **[!UICONTROL Summary]** i den vänstra navigeringen om du vill se information om taggegenskapen

   ![Fliken Sammanfattning](assets/validate-summary.png)

1. Gå nu till **[!UICONTROL Experience Platform Web SDK]** i den vänstra navigeringen för att se **[!UICONTROL Network Requests]**
1. Öppna raden **[!UICONTROL events]**

   ![Adobe Experience Platform Web SDK-begäran](assets/validate-aep-screen.png)

1. Observera hur du kan se händelsetypen `web.webpagedetails.pageView` som du angav i åtgärden [!UICONTROL Update variable] och andra variabler som inte finns i rutan enligt fältgruppen `AEP Web SDK ExperienceEvent`

   ![Händelseinformation](assets/validate-event-pageViews.png)

1. Bläddra ned till objektet `web`, välj att öppna det och inspektera `webPageDetails.name`, `webPageDetails.server` och `webPageDetails.siteSection`. De ska matcha motsvarande `digitalData` datalagervariabler på startsidan

>[!TIP]
>
> Så här visar och jämför du datalagret `digitalData` på hemsidan:
>
> 1. Öppna webbläsarutvecklarverktygen på Lumas hemsida. Om det är Chrome väljer du knappen `F12` på tangentbordet
> 1. Välj fliken **[!UICONTROL Console]**
> 1. Ange `digitalData` och välj `Enter` på tangentbordet för att visa datalagrets värden

![Fliken Nätverk](assets/validate-xdm-content.png)

Du kan även validera informationen i identitetskartan:

1. Logga in på Luma-webbplatsen med inloggningsuppgifterna `test@adobe.com`/`test`

1. Återgå till [Lumas hemsida](https://luma.enablementadobe.com/content/luma/us/en.html)

1. Öppna avsnittet **[!UICONTROL Experience Platform Web SDK]** i den vänstra navigeringen

   ![SDK för webben i felsökning](assets/identity-debugger-websdk-dark.png)

1. Markera raden **[!UICONTROL events]** om du vill öppna information i ett popup-fönster

   ![SDK för webben i felsökning](assets/identity-deugger-websdk-event-dark.png)

1. Sök efter **identityMap** i popup-fönstret. Här visas `lumaCrmId` med tre nycklar för authenticatedState, id och primär:
   ![SDK för webben i felsökning](assets/identity-deugger-websdk-event-lumaCrmId-dark.png)

### Validera klientförfrågningar med utvecklingsverktyg i webbläsaren

Den här typen av begärandeinformation visas också på fliken **Nätverk** i webbläsaren (förutsatt att webbplatsen läser in ditt taggbibliotek).

1. Öppna fliken **Nätverk** för webbläsarens webbutvecklingsverktyg och läs in sidan igen. Filtrera efter samtal med `/ee` för att hitta samtalet, markera det och titta sedan på fliken **Huvuden** och fliken **Nyttolast**

   ![Fliken Nätverk](assets/validate-dev-console.png)

1. Gå till fliken **Svar** och notera hur ECID-värdet inkluderas i svaret.

   ![Fliken Nätverk](assets/validate-dev-console-ecid.png)

   >[!NOTE]
   >
   > ECID-värdet visas i nätverkssvaret. Den ingår inte i `identityMap`-delen av nätverksbegäran och lagras inte i det här formatet i en cookie.

## Validera nätverksbegäranden på serversidan med Experience Platform Debugger

Som du lär dig i lektionen [Konfigurera en datastream](configure-datastream.md) skickar Platform Web SDK först data från din digitala egenskap till Platform Edge Network. Sedan gör Platform Edge Network ytterligare serverförfrågningar till motsvarande tjänster som är aktiverade i din datastream. Du kan validera de serverförfrågningar som gjorts av Platform Edge Network med Edge Trace i felsökningsprogrammet.

<!--Furthermore, you can also validate the fully processed payload after it reaches an Adobe application by using [Adobe Experience Platform Assurance](https://experienceleague.adobe.com/en/docs/experience-platform/assurance/home). -->


### Aktivera Edge Trace

Aktivera Edge Trace:

1. I den vänstra navigeringen för **[!UICONTROL Experience Platform Debugger]** väljer du **[!UICONTROL Logs]**
1. Välj fliken **[!UICONTROL Edge]** och välj **[!UICONTROL Connect]**

   ![Anslut Edge Trace](assets/analytics-debugger-edgeTrace.png)

1. Det är tomt för tillfället

   ![Ansluten Edge Trace](assets/analytics-debugger-edge-connected.png)

1. Uppdatera startsidan för [Luma](https://luma.enablementadobe.com/) och kontrollera **[!UICONTROL Experience Platform Debugger]** igen för att se data som kommer igenom.

   ![Analysfyr för Edge Trace](assets/validate-edge-trace.png)

För närvarande kan du inte visa några plattformsbegäranden från Edge Network som går till Adobe-program eftersom du inte har aktiverat några i datastream. I framtida lektioner använder du Edge Trace för att visa utgående begäranden på serversidan till Adobe-program och händelsevidarebefordran. Men först och främst vill vi veta mer om ett annat verktyg för att validera serverförfrågningar från Platform Edge Network - Adobe Experience Platform Assurance!

[Nästa: ](validate-with-assurance.md)

>[!NOTE]
>
>Tack för att du har lagt ned din tid på att lära dig om Adobe Experience Platform Web SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela dem i det här [Experience League diskussionsgruppsinlägget](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
