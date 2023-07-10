---
title: Skapa ett XDM-schema för webbdata
description: Lär dig hur du skapar ett XDM-schema för webbdata i gränssnittet för datainsamling. Den här lektionen är en del av självstudiekursen Implementera Adobe Experience Cloud med Web SDK.
feature: Web SDK,Tags,Schemas
exl-id: 2858ce03-4f95-43ac-966c-1b647b33ef16
source-git-commit: adbe8f4476340abddebbf9231e3dde44ba328063
workflow-type: tm+mt
source-wordcount: '1121'
ht-degree: 0%

---

# Skapa ett XDM-schema för webbdata

Lär dig hur du skapar ett XDM-schema för webbdata i gränssnittet för datainsamling.

XDM-scheman (Experience Data Model) är byggstenar, principer och bästa tillvägagångssätt för att komponera scheman i Adobe Experience Platform.

Platform Web SDK använder ditt schema för att standardisera dina webbhändelsedata, skicka dem till Platform Edge Network och slutligen vidarebefordra data till alla Experience Cloud-program som konfigurerats i datastream. Det här steget är viktigt eftersom det definierar en standarddatamodell som krävs för inmatning av kundupplevelsedata i Experience Platform och möjliggör tjänster och applikationer som bygger på dessa standarder.

>[!NOTE]
>
> I demonstrationssyfte bygger övningarna i den här lektionen upp ett exempelschema för att fånga innehåll som visas och produkter som köpts av kunder i [Luma Demo Site](https://luma.enablementadobe.com/content/luma/us/en.html). Du kan använda de här stegen för att skapa ett annat schema för dina egna syften, men vi rekommenderar att du först följer med när du skapar exempelschemat för att lära dig funktionerna i schemaredigeraren.

Ta en kurs om du vill veta mer om XDM-scheman[Modellera era kundupplevelsedata med XDM](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm)&quot; eller se [XDM - systemöversikt](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=sv).

## Utbildningsmål

När lektionen är klar kan du:

* Skapa ett XDM-schema inifrån datainsamlingsgränssnittet
* Lägg till fältgrupper i XDM-schemat
* Skapa XDM-scheman för webbhändelsedata enligt vedertagna standarder

## Förutsättningar

Alla nödvändiga etablerings- och användarbehörigheter för datainsamling och Adobe Experience Platform som beskrivs i [Konfigurera behörigheter](configure-permissions.md) lektion.

## Skapa ett XDM-schema

XDM-scheman är standardsättet att beskriva data i Experience Platform, vilket gör att alla data som överensstämmer med scheman kan återanvändas i en organisation utan konflikter, eller till och med delas mellan flera organisationer. Mer information finns i [Grunderna för schemakomposition](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=en).

I den här övningen skapar du ett XDM-schema med de rekommenderade baslinjefältgrupperna för att hämta webbhändelsedata på [Luma Demo Site](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"}:

1. Öppna [Gränssnitt för datainsamling](https://launch.adobe.com/){target="_blank"}
1. Kontrollera att du befinner dig i rätt sandlåda

   >[!NOTE]
   >
   >Om du använder ett plattformsbaserat program som Real-Time CDP rekommenderar vi att du använder en utvecklingssandlåda för den här självstudiekursen. Om du inte gör det använder du **[!UICONTROL Prod]** sandlåda.

1. Gå till **[!UICONTROL Scheman]** i den vänstra navigeringen
1. Välj **[!UICONTROL Skapa schema]** överst till höger
1. Välj **[!UICONTROL XDM ExperienceEvent]**

![Schemaupplevelsehändelse](assets/schema-XDM-experience-event.jpg)

## Lägg till fältgrupper

Som tidigare nämnts är XDM det centrala ramverket som standardiserar kundupplevelsedata genom att tillhandahålla gemensamma strukturer och definitioner för användning i Adobe Experience Platform-tjänster längre fram i kedjan. Genom att följa XDM-standarder _alla kundupplevelsedata_ kan införlivas i en gemensam representation. Med den här metoden kan ni få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och uttrycka kundattribut för personalisering med hjälp av data från flera olika källor. Se [Bästa tillvägagångssätt för datamodellering](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/best-practices.html?lang=en) för mer information.

När det är möjligt bör du använda befintliga fältgrupper och följa en produktmedveten modell och namnkonventioner. För alla data som är specifika för din organisation och som inte passar in i de fördefinierade fältgrupperna ovan kan du skapa en anpassad fältgrupp. Se [Skapa ett schema med Schemaredigeraren](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html?lang=en#create) för mer detaljerade steg om anpassade scheman.

>[!TIP]
> 
>I den här övningen lägger du till de rekommenderade fördefinierade fältgrupperna för insamling av webbdata: _**[!UICONTROL AEP Web SDK ExperienceEvent]**_ och _**[!UICONTROL Consumer Experience Event]**_.

1. I **[!UICONTROL Fältgrupper]** avsnitt, markera **[!UICONTROL Lägg till]**
1. Sök efter [!UICONTROL `AEP Web SDK ExperienceEvent`]
1. Markera rutan
1. Sök efter [!UICONTROL `Consumer Experience Event`]
1. Markera rutan
1. Välj **[!UICONTROL Lägg till fältgrupper]**

   ![Lägg till fältgrupp](assets/schema-add-field-group.jpg)

När fältgrupperna är markerade är du redo att namnge schemat. En vanlig namnkonvention för XDM-scheman är att namnge schemat efter datakällan:

1. I[!UICONTROL Disposition**] väljer du `Untitled schema name`
1. I **[!UICONTROL Schemaegenskaper]** panelen, ange **[!UICONTROL Visningsnamn]** `Luma Web Event Data`
1. Markera något utanför **[!UICONTROL Visningsnamn]** fält för att aktivera **[!UICONTROL Spara]** option
1. Välj **[!UICONTROL Spara]**

![Webbhändelsedata för Luma](assets/schema-luma-web-event-data.png)

Observera att du har tillgång till de mest använda nyckelvärdepar som krävs för datainsamling på webben i båda fältgrupperna. The [!UICONTROL visningsnamn] av varje fält visas för marknadsförarna i segmentbygggränssnittet i plattformsbaserade program och du kan ändra visningsnamnet för standardfält efter behov. Du kan också ta bort fält som du inte vill ha. När du klickar på något av fältgruppsnamnen markeras vilka nyckelvärdepar som tillhör det. I exemplet nedan ser du vilka grupper som tillhör **[!UICONTROL Consumer Experience Event]**.

![Fältgrupper för schema](assets/schema-consumer-experience-event.jpg)

Den här lektionen är bara en startpunkt. När du skapar ett eget webbeventschema måste du utforska och dokumentera dina affärskrav. Den här processen påminner om att skapa en [Dokument för verksamhetskrav](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/implementation-basics/creating-a-business-requirements-document.html) och [Referens för lösningsdesign](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/implementation-basics/creating-and-maintaining-an-sdr.html) för en Adobe Analytics-implementering, men bör innehålla krav för _alla nedströmsdatamottagare_ som till exempel mål för plattform, mål och händelsespelare.


### identityMap-objektet

Det finns en särskild uppsättning data som krävs för att identifiera webbanvändare som kallas `[!UICONTROL identityMap]`.

![Webbhändelsedata för Luma](assets/schema-identityMap.png)

Det är ett måste-ha-objekt för alla webbrelaterade datainsamlingar eftersom det innehåller det Experience Cloud-ID som krävs för att identifiera användare på webben. Det är också nyckeln till att ange interna kund-ID:n för autentiserade användare. `[!UICONTROL identityMap]` diskuteras mer i [Konfigurera identiteter](configure-identities.md) lektion. Den inkluderas automatiskt i alla scheman med **[!UICONTROL XDM ExperienceEvent]** klassen.


>[!IMPORTANT]
>
> Det går att aktivera **[!UICONTROL Profil]** för ett schema innan du sparar schemat. **Gör inte** aktivera det nu. När ett schema har aktiverats för profilen kan det inte inaktiveras eller tas bort. Det går inte heller att ta bort fält från schemat efter den här punkten. Dessa konsekvenser är viktiga att tänka på senare när du arbetar med egna data i produktionsmiljön.
>
>Den här inställningen diskuteras mer under [Konfigurera Experience Platform](setup-experience-platform.md) lektion.
>![Profilschema](assets/schema-profile.png)

Nu kan du referera till det här schemat när du lägger till Web SDK-tillägget för din taggegenskap.


[Nästa: ](configure-identities.md)

>[!NOTE]
>
>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Web SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela med dig av dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
