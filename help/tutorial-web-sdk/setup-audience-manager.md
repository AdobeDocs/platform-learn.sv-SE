---
title: Konfigurera Audience Manager med Platform Web SDK
description: Lär dig hur du konfigurerar Adobe Audience Manager med Platform Web SDK och validerar implementeringen med hjälp av en cookie-destination. Den här lektionen ingår i självstudiekursen Implementera Adobe Experience Cloud med Web SDK.
solution: Data Collection, Audience Manager
exl-id: 45db48e9-73cf-4a9c-88f4-b5872a8224d3
source-git-commit: 9f75ef042342e1ff9db6039e722159ad96ce5e5b
workflow-type: tm+mt
source-wordcount: '1276'
ht-degree: 0%

---

# Konfigurera Audience Manager med Platform Web SDK


>[!CAUTION]
>
>Vi räknar med att publicera viktiga ändringar av den här självstudiekursen fredagen den 15 mars 2024. Därefter kommer många övningar att ändras och du kan behöva starta om självstudiekursen från början för att kunna slutföra alla lektioner.

Lär dig hur du konfigurerar Adobe Audience Manager med Platform Web SDK och validerar implementeringen med hjälp av en cookie-destination.

[Adobe Audience Manager](https://experienceleague.adobe.com/docs/audience-manager.html) är en Adobe Experience Cloud-lösning som innehåller allt som krävs för att samla in kommersiellt relevant information om webbplatsbesökare, skapa marknadsföringsbara segment och leverera riktad reklam och innehåll till rätt målgrupp.


## Utbildningsmål

När lektionen är klar kan du:

* Konfigurera ett datastream för att aktivera Audience Manager
* Aktivera en cookie-destination i Audience Manager
* Validera Audience Manager-implementeringen genom att bekräfta målgruppskvalifikation med Adobe Experience Platform Debugger

## Förutsättningar

För att slutföra lektionen måste du först:

* Slutför de tidigare lektionerna i avsnitten Inledande konfiguration och Tagginställningar i den här självstudien.
* ha tillgång till Adobe Audience Manager och de behörigheter som krävs för att skapa, läsa och skriva egenskaper, segment och mål. Mer information finns på [Audience Manager Role-baserad åtkomstkontroll](https://experienceleague.adobe.com/docs/audience-manager-learn/tutorials/setup-and-admin/user-management/setting-permissions-with-role-based-access-control.html?lang=en).

## Konfigurera datastream

Implementeringen av Audience Manager med Platform Web SDK skiljer sig från implementeringen med [vidarebefordran på serversidan (SSF)](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/server-side-forwarding/ssf.html). Vidarebefordran på serversidan skickar Adobe Analytics data för begäran till Audience Manager. En SDK-implementering för en plattform skickar XDM-data som skickas till Platform Edge Network till Audience Manager. Audience Manager är aktiverat i datastream:

1. Gå till [Datainsamling](https://experience.adobe.com/#/data-collection){target="blank"} gränssnitt
1. Välj **[!UICONTROL Datastreams]**
1. Markera tidigare skapade `Luma Web SDK` datastream

   ![Välj dataströmmen för Luma Web SDK](assets/datastream-luma-web-sdk.png)

1. Välj **[!UICONTROL Add Service]**
   ![Lägg till en tjänst i datastream](assets/aam-datastream-addService.png)
1. Välj **[!UICONTROL Adobe Audience Manager]** som **[!UICONTROL Service]**
1. Bekräfta att **[!UICONTROL Cookie Destinations Enabled]** och **[!UICONTROL URL Destinations Enabled]** är markerade
1. Välj **[!UICONTROL Save]**
   ![Bekräfta datastream-inställningarna för Audience Manager och spara](assets/aam-datastream-save.png)

## Skapa en datakälla

Skapa sedan en [Datakälla](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-sources/datasources-list-and-settings.html?lang=en), ett grundläggande verktyg för att ordna data i Audience Manager:

1. Gå till [Audience Manager](https://experience.adobe.com/#/audience-manager/) gränssnitt
1. Välj **[!UICONTROL Audience Data]** från den övre navigeringen
1. Välj **[!UICONTROL Data Sources]** i listrutan
1. Välj **[!UICONTROL Add New]** längst upp på sidan Datakällor

   ![Adobe Experience Platform Audience Manager datakällor](assets/data-sources-list.jpg)

1. Ge datakällan ett eget namn och en beskrivning. För den första konfigurationen kan du namnge detta`Platform Web SDK tutorial`.
1. Ange **[!UICONTROL ID Type]** till **[!UICONTROL Cookie]**
1. I **[!UICONTROL Data Export Controls]** avsnitt, markera **[!UICONTROL No Restriction]**

   ![Inställningar för Adobe Experience Platform Audience Manager-datakälla](assets/data-source-details.png)

1. **[!UICONTROL Save]** datakällan


## Skapa ett varumärke

När datakällan har sparats ställer du in en [trait](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/traits-overview.html?lang=en). Traits är en kombination av en eller flera signaler i Audience Manager. Skapa ett varumärke för besökare på hemsidan.

>[!NOTE]
>
>Alla XDM-data skickas till Audience Manager om de är aktiverade i datastream, men data kan ta 24 timmar tills de blir tillgängliga i rapporten Oanvända signaler. Skapa explicita egenskaper för XDM-data som du vill använda direkt i Audience Manager, enligt beskrivningen i den här övningen.

1. Välj **[!UICONTROL Audience Data]** >  **[!UICONTROL Traits]**
1. Välj **[!UICONTROL Add New]** >  **[!UICONTROL Rule-Based]** trait

   ![Adobe Experience Platform Audience Manager regelbaserat varumärke](assets/rule-based-trait.jpg)

1. Ge ditt varumärke ett eget namn och en beskrivning, `Luma homepage view`
1. Välj **[!UICONTROL Data Source]** som du skapade i föregående avsnitt.
1. **[!UICONTROL Select a Folder]** där du kan spara ditt spår i rutan till höger. Du kan skapa en mapp med **markera ikonen +** bredvid en befintlig överordnad mapp. Du kan namnge den nya mappen `Platform Web SDK tutorial`.
1. Expandera **[!UICONTROL Trait Expression]** cirkumflex och markera **[!UICONTROL Expression Builder]** Du måste ange ett nyckelvärdepar som betecknar ett hemsidesbesök.
1. Öppna [Lumas hemsida](https://luma.enablementadobe.com/content/luma/us/en.html) (mappas till taggegenskapen) och **SDK-felsökning för plattform** och uppdatera sidan.
1. Titta på nätverksförfrågningar och händelseinformationen för Platform Web SDK för att hitta nyckel- och namnvärdet för hemsidan.
   ![Adobe Experience Platform Audience Manager XDM-data](assets/xdm-keyvalue.jpg)
1. Gå tillbaka till Expression Builder i användargränssnittet för Audience Manager och ange tangenten som **`web.webPageDetails.name`** och värdet av **`content:luma:us:en`**. Det här steget gör att du får ett spår när du läser in hemsidan.
1. **[!UICONTROL Save]** egenskapen.


## Skapa ett segment

Nästa steg är att skapa en **segment** och tilldela det här segmentet din nydefinierade egenskap.

1. Välj **[!UICONTROL Audience Data]** i den övre navigeringen och välj **[!UICONTROL Segments]**
1. Välj **[!UICONTROL Add New]** i det övre vänstra hörnet på sidan för att öppna segmentverktyget
1. Ge segmentet ett eget namn och en beskrivning, till exempel `Platform Web SDK - Homepage visitors`
1. **[!UICONTROL Select a Folder]** där segmentet sparas i rutan till höger. Du kan skapa en mapp med **markera ikonen +** bredvid en befintlig överordnad mapp. Du kan namnge den nya mappen `Platform Web SDK tutorial`.
1. Lägg till en integrationskod, som i det här fallet är en slumpmässig uppsättning med siffror. 1. I **[!UICONTROL Data Source]** avsnitt, markera **[!UICONTROL Audience Manager]** och datakällan som du skapade tidigare
1. Expandera **[!UICONTROL Traits]** och sök efter den egenskap du har skapat
1. Välj **[!UICONTROL Add Trait]**.
1. Välj **[!UICONTROL Save]** längst ned på sidan

   ![Adobe Experience Platform Audience Manager Add Trait](assets/add-trait-segment.jpg)

   ![Adobe Experience Platform Audience Manager Add Trait](assets/saved-segment.jpg)

## Skapa ett mål

Skapa sedan en **Cookie-baserat mål** med **Destinationsverktyget**. Med Destination Builder kan du skapa och hantera mål för cookies, URL och server-till-server.

1. Öppna målverktyget genom att välja **[!UICONTROL Destinations]** inom **Målgruppsdata** menyn i den övre navigeringen
1. Välj **[!UICONTROL Create Destination]**
1. Ange ett namn och en beskrivning `Platform Web SDK tutorial`
1. Som **[!UICONTROL Category]**, markera **[!UICONTROL Custom]**
1. Som **[!UICONTROL Type]**, markera **[!UICONTROL Cookie]**

   ![Adobe Experience Platform Audience Manager Add Trait](assets/destination-settings.jpg)

1. Öppna **[!UICONTROL Configuration]** för att ange information om din cookie-destination
1. Ge din cookie ett eget namn, `platform_web_sdk_tutorial`
1. Som **[!UICONTROL Cookie Domain]**, lägg till domänen för den webbplats där du planerar att integrera, för självstudiekursen i Luma-domänen, `luma.enablementadobe.com`
1. Som **[!UICONTROL Publish data to]** alternativ, markera **[!UICONTROL Only the Selected domains]**
1. Välj din domän om den inte redan har lagts till
1. Som **[!UICONTROL Data Format]**, markera **[!UICONTROL Single Key]** och ge din kaka en nyckel. För den här självstudiekursen `segment` som nyckelvärde.
1. Äntligen väljer du **[!UICONTROL Save]** om du vill spara information om målkonfigurationen.

   ![Avsnittet Konfiguration av mål för Audience Manager](assets/aam-destination-config-dw.png)

<!--
   ![Adobe Experience Platform Audience Manager Add Trait](assets/aam-destination-config.jpg)


   ![Adobe Experience Platform Audience Manager Add Trait](assets/cookie-destination-config.jpg)
-->

1. I **[!UICONTROL Segment Mappings]** -avsnittet använder du **[!UICONTROL Search and Add Segments]** funktion för att söka efter tidigare skapade `Platform Web SDK - Homepage visitors` och markera **[!UICONTROL Add]**.


1. När du har lagt till ditt segment öppnas ett popup-fönster där du måste ange ett förväntat värde för din cookie. Ange värdet &quot;hpvisitor&quot; för den här övningen.

1. Välj **[!UICONTROL Save]**

1. Välj **[!UICONTROL Done]**
   ![Adobe Experience Platform Audience Manager Add Trait](assets/luma-cookie-segment-dw.png)

Segmentmappningsperioden tar några timmar att aktivera. När du är klar kan du uppdatera Audience Manager-gränssnittet och se att **Mappade segment** listan har uppdaterats.

## Validera segmentet

Några timmar efter det att segmentet ursprungligen skapades kan du verifiera att det fungerar som det ska.

Bekräfta först att du kan kvalificera dig för segmentet

1. Öppna [Startsida för Lumas demowebbplats](https://luma.enablementadobe.com/content/luma/us/en.html) med den mappad till taggegenskapen för att kvalificera dig för ditt nyligen skapade segment.
1. Öppna webbläsarens **utvecklingsverktyg**  > **Nätverk** tab
1. Filtrera till plattformens SDK-begäran med `interact` som textfilter
1. Välj ett samtal och öppna **Förhandsgranska** för att visa svarsinformation
1. Expandera **nyttolast** för att visa den förväntade cookie-informationen, som tidigare konfigurerats i Audience Manager. I det här exemplet visas det förväntade cookie-namnet `platform_web_sdk_tutorial`.

   ![Adobe Experience Platform Audience Manager Add Trait](assets/segment-validate-response.jpg)

1. Öppna **Program** och öppna **Cookies** från **Lagring** -menyn.
1. Välj **`https://luma.enablementadobe.com`** domänen och bekräfta att din cookie är korrekt skriven i listan

   ![Adobe Experience Platform Audience Manager Add Trait](assets/validate-cookie.jpg)


Slutligen bör du öppna segmentet i Audience Manager-gränssnittet och se till att **Segmentpopulationer** har ökat:

![Adobe Experience Platform Audience Manager Add Trait](assets/segment-population.jpg)


Nu när du är klar med den här lektionen bör du kunna se hur Platform Web SDK skickar data till Audience Manager och kan ange en segmentspecifik cookie med en cookie-destination.

[Nästa: ](setup-target.md)

>[!NOTE]
>
>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Web SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
