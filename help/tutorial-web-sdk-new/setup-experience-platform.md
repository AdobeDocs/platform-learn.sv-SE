---
title: Strömma data till Adobe Experience Platform med Web SDK
description: Lär dig hur du direktuppspelar webbdata till Adobe Experience Platform med Web SDK. Den här lektionen ingår i självstudiekursen Implementera Adobe Experience Cloud med Web SDK.
source-git-commit: 58034fc649a06b4e17ffddfd0640a81a4616f688
workflow-type: tm+mt
source-wordcount: '1608'
ht-degree: 0%

---

# Strömma data till Experience Platform med Web SDK

Lär dig hur du strömmar webbdata till Adobe Experience Platform med Platform Web SDK.

Experience Platform är ryggraden i alla nya Experience Cloud-program, som Adobe Real-time Customer Data Platform, Adobe Customer Journey Analytics och Adobe Journey Optimizer. Dessa program är utformade för att använda Platform Web SDK som den optimala metoden för webbdatainsamling.


![Web SDK och Adobe Experience Platform](assets/dc-websdk-aep.png)

Experience Platform använder samma XDM-schema som du skapade tidigare för att hämta händelsedata från Luma-webbplatsen. När dessa data skickas till Platform Edge Network kan datastream-konfigurationen vidarebefordra dem till Experience Platform.

## Utbildningsmål

När lektionen är klar kan du:

* Skapa en datauppsättning i Adobe Experience Platform
* Konfigurera dataströmmen för att skicka Web SDK-data till Adobe Experience Platform
* Aktivera direktuppspelande webbdata för kundprofil i realtid
* Validera att data har landats både i plattformsdatauppsättningen och i kundprofilen i realtid

## Förutsättningar

Du borde ha slutfört följande lektioner:

* The **Inledande konfiguration** lektioner:
   * [Konfigurera ett XDM-schema](configure-schemas.md)
   * [Konfigurera ett datastream](configure-datastream.md)
   * [Konfigurera ett identitetsnamnutrymme](configure-identities.md)

* The **Märkordskonfiguration** lektioner:
   * [Installera SDK-tillägg för webben](install-web-sdk.md)
   * [Skapa dataelement](create-data-elements.md)
   * [Skapa identiteter](create-identities.md)
   * [Skapa taggregler](create-tag-rule.md)


## Skapa en datauppsättning

Alla data som har inhämtats till Adobe Experience Platform lagras i datasjön som datauppsättningar. A [datauppsättning](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html?lang=en) är en lagrings- och hanteringskonstruktion för en samling data, vanligtvis en tabell, som innehåller ett schema (kolumner) och fält (rader). Datauppsättningar innehåller också metadata som beskriver olika aspekter av de data som lagras.

I den här övningen skapar du en datauppsättning för att spåra innehåll och e-handelsinformation för [Luma demo site](https://luma.enablementadobe.com/content/luma/us/en.html).

>[!WARNING]
>
>Du måste ha skapat `Luma Web Event Data` schemat, enligt instruktionerna i föregående lektion, [Konfigurera ett XDM-schema](configure-schemas.md).


1. Gå till [Experience Platform gränssnitt](https://experience.adobe.com/platform/)
1. Bekräfta att du befinner dig i den utvecklingssandlåda som du använder för den här självstudien
1. Öppna **[!UICONTROL Datahantering > Datauppsättningar]** från vänster navigering
1. Välj **[!UICONTROL Skapa datauppsättning]**

   ![Skapa schema](assets/experience-platform-create-dataset.png)

1. Välj **[!UICONTROL Skapa datauppsättning från schema]** option

   ![Skapa datauppsättning från schema](assets/experience-platform-create-dataset-schema.png)

1. Välj `Luma Web Event Data` schema som har skapats i [tidigare lektion](configure-schemas.md) och sedan **[!UICONTROL Nästa]**

   ![Datauppsättning, välj schema](assets/experience-platform-create-dataset-schema-selection.png)

1. Ange en **[!UICONTROL Namn]** och valfria **[!UICONTROL Beskrivning]** för datauppsättningen. För denna övning används `Luma Web Event Data`väljer **[!UICONTROL Slutför]**

   ![Namn på datauppsättning ](assets/experience-platform-create-dataset-schema-name.png)

En datauppsättning har nu konfigurerats för att börja samla in data från implementeringen av Platform Web SDK.

## Konfigurera datastream

Nu kan du konfigurera [!UICONTROL datastream] skicka data till [!UICONTROL Adobe Experience Platform]. Datastream är länken mellan taggegenskap, Platform Edge Network och datauppsättningen Experience Platform.

1. Öppna [Datainsamling](https://experience.adobe.com/#/data-collection){target="blank"} gränssnitt
1. Välj **[!UICONTROL Datastreams]** från vänster navigering
1. Öppna datastream som du skapade i [Konfigurera ett datastream](configure-datastream.md) lektion, `Luma Web SDK`

   ![Välj dataströmmen för Luma Web SDK](assets/datastream-luma-web-sdk.png)

1. Välj **[!UICONTROL Lägg till tjänst]**
   ![Lägg till en tjänst i datastream](assets/experience-platform-addService.png)
1. Välj **[!UICONTROL Adobe Experience Platform]** som **[!UICONTROL Tjänst]**
1. Välj `Luma Web Event Data` som **[!UICONTROL Händelsedatauppsättning]**

1. Välj **[!UICONTROL Spara]**.

   ![Datastream Config](assets/experience-platform-datastream-config.png)

När du genererar trafik på [Luma Demo Site](https://luma.enablementadobe.com/content/luma/us/en.html) mappas till taggegenskapen, data fyller i datauppsättningen i Experience Platform!

## Validera datauppsättningen

Det här steget är viktigt för att se till att data har landats i datauppsättningen. Det finns två aspekter av att validera data som skickas till datauppsättningen.

* Validera med [!UICONTROL Felsökning för Experience Platform]
* Validera med [!UICONTROL Förhandsgranska datauppsättning]
* Validera med [!UICONTROL Frågetjänst]

### Experience Platform Debugger

De här stegen är mer eller mindre desamma som i [Felsökningslektion](validate-with-debugger.md). Eftersom data bara skickas till plattformen när du har aktiverat den i datastream måste du generera fler exempeldata:

1. Öppna [Luma demo site](https://luma.enablementadobe.com/content/luma/us/en.html) och väljer [!UICONTROL Felsökning för Experience Platform] tilläggsikon

1. Konfigurera felsökaren för att mappa taggegenskapen till *din* Utvecklingsmiljö, enligt beskrivningen i [Validera med felsökning](validate-with-debugger.md) lektion

   ![Din startutvecklingsmiljö visas i Felsökning](assets/experience-platform-debugger-dev.png)

1. Logga in på Luma-webbplatsen med inloggningsuppgifterna `test@adobe.com`/`test`

1. Återgå till [Lumas hemsida](https://luma.enablementadobe.com/content/luma/us/en.html)

1. Markera på raden &quot;events&quot; i plattforms-Web SDK-nätverksbeacons som visas av felsökaren för att visa information i ett popup-fönster

   ![Web SDK in Debugger](assets/experience-platform-debugger-dev-eventType.png)

1. Sök efter &quot;identityMap&quot; i popup-fönstret. Här visas lumaCrmId med tre nycklar för authenticatedState, id och primär
   ![Web SDK in Debugger](assets/experience-platform-debugger-dev-idMap.png)

Nu ska data fyllas i i `Luma Web Event Data` datauppsättning och klar för validering av Preview Dataset.

### Förhandsgranska datauppsättningen

För att bekräfta att data har landat i plattformens datasjön är ett snabbt alternativ att använda **[!UICONTROL Förhandsgranska datauppsättning]** -funktion. SDK-data för webben mikrobatcheras till datasjön och uppdateras regelbundet i plattformsgränssnittet. Det kan ta 10-15 minuter att se data som du har skapat.

1. I [Experience Platform](https://experience.adobe.com/platform/) gränssnitt, välja **[!UICONTROL Datahantering > Datauppsättningar]** i den vänstra navigeringen för att öppna **[!UICONTROL Datauppsättningar]** kontrollpanel.

   Kontrollpanelen visar alla tillgängliga datauppsättningar för din organisation. Information visas för varje datamängd som anges, inklusive namn, schema som datauppsättningen följer och status för den senaste importen.

1. Välj `Luma Web Event Data` datauppsättning för att öppna **[!UICONTROL Datauppsättningsaktivitet]** skärm.

   ![Webbhändelse för Luma för datauppsättning](assets/experience-platform-dataset-validation-lumaSDK.png)

   Aktivitetsskärmen innehåller ett diagram som visar hur många meddelanden som har förbrukats samt en lista över lyckade och misslyckade batchar.

1. Från **[!UICONTROL Datauppsättningsaktivitet]** skärm, välja **[!UICONTROL Förhandsgranska datauppsättning]** i skärmens övre högra hörn om du vill förhandsgranska upp till 100 rader med data. Om datauppsättningen är tom inaktiveras förhandsgranskningslänken.

   ![Förhandsgranska datauppsättning](assets/experience-platform-dataset-preview.png)

   I förhandsgranskningsfönstret visas den hierarkiska vyn av datasetens schema till höger.

   ![Förhandsgranska datauppsättning 1](assets/experience-platform-dataset-preview-1.png)

>[!INFO]
>
>Adobe Experience Platform frågetjänst är en stabilare metod för att validera data i sjön, men den här självstudiekursen omfattar inte detta. Mer information finns i [Utforska data](https://experienceleague.adobe.com/docs/platform-learn/tutorials/queries/explore-data.html) i avsnittet Plattformssjälvstudiekurser.


## Aktivera datauppsättningen och schemat för kundprofil i realtid

Nästa steg är att aktivera datauppsättningen och schemat för kundprofilen i realtid. Dataströmning från Web SDK kommer att vara en av många datakällor som flödar på Platform och du vill koppla webbdata till andra datakällor för att skapa 360-graders kundprofiler. Titta på den här korta videon om du vill veta mer om kundprofilen i realtid:

>[!VIDEO](https://video.tv.adobe.com/v/27251?learn=on&captions=eng)

>[!CAUTION]
>
>När vi arbetar med din egen webbplats och data rekommenderar vi en mer robust validering av data innan vi aktiverar den för kundprofil i realtid.


**Så här aktiverar du datauppsättningen:**

1. Öppna datauppsättningen som du skapade, `Luma Web Event Data`

1. Välj **[!UICONTROL Växla profil]** för att aktivera

   ![Växla profil](assets/setup-experience-platform-profile.png)

1. Bekräfta att du vill **[!UICONTROL Aktivera]** datauppsättningen

   ![Aktivera profil/växla](assets/setup-experience-platform-profile-enable.png)

**Aktivera schemat:**

1. Öppna schemat som du skapade, `Luma Web Event Data`

1. Välj **[!UICONTROL Växla profil]** för att aktivera

   ![Växla profil](assets/setup-experience-platform-profile-schema.png)

1. Välj **[!UICONTROL Data för det här schemat kommer att innehålla en primär identitet i identityMap-fältet.]**

   >[!IMPORTANT]
   >
   >    Primära identiteter krävs i alla poster som skickas till kundprofilen i realtid. Vanligtvis är identitetsfält märkta i schemat. När du använder identitetskartor visas emellertid inte identitetsfälten i schemat. I den här dialogrutan bekräftar du att du har en primär identitet i åtanke och att du anger den i en identitetskarta när du skickar data. Som du vet använder Web SDK en identitetskarta och Experience Cloud-ID (ECID) är standardidentitet.


1. Välj **[!UICONTROL Aktivera]**

   ![Aktivera profil/växla](assets/setup-experience-platform-profile-schema-enable.png)

1. Välj **[!UICONTROL Spara]** för att spara det uppdaterade schemat

Nu är schemat även aktiverat för profilen.

>[!IMPORTANT]
>
>    När ett schema har aktiverats för profilen kan det inte inaktiveras eller tas bort. Det går inte heller att ta bort fält från schemat efter den här punkten. Dessa konsekvenser är viktiga att tänka på senare när du arbetar med egna data i produktionsmiljön. Du bör använda en utvecklingssandlåda i den här självstudiekursen, som du kan ta bort när som helst.
>
>   
> När du arbetar med egna data rekommenderar vi att du gör saker i följande ordning:
> 
> * För det första kan du importera vissa data i dina datauppsättningar.
> * Åtgärda eventuella problem som uppstår under dataöverföringsprocessen (till exempel datavalidering eller mappningsproblem).
> * Aktivera datauppsättningar och scheman för profil
> * Importera data igen


### Validera en profil

Du kan slå upp en kundprofil i plattformsgränssnittet (eller Journey Optimizer-gränssnittet) för att bekräfta att data har landats i kundprofilen i realtid. Som namnet antyder fyller profilerna i realtid, så det är ingen fördröjning som när data i datauppsättningen validerades.

Först måste du generera fler exempeldata. Upprepa stegen tidigare i den här lektionen för att logga in på Luma-webbplatsen när den mappas till taggegenskapen. Inspect-begäran om Platform Web SDK för att säkerställa att den skickar data med `lumaCRMId`.

1. I [Experience Platform](https://experience.adobe.com/platform/) gränssnitt, välja **[!UICONTROL Profiler]** i den vänstra navigeringen

1. Som **[!UICONTROL Namnutrymme för identitet]** use `lumaCRMId`
1. Kopiera och klistra in värdet för `lumaCRMId` godkändes i samtalet som du inspekterade i felsökaren i Experience Platform, i det här fallet `112ca06ed53d3db37e4cea49cc45b71e`.

   ![Profil](assets/experience-platform-validate-dataset-profile.png)

1. Om det finns ett giltigt värde i profilen för `lumaCRMId`fyller ett profil-ID i konsolen:

   ![Profil](assets/experience-platform-validate-dataset-profile-set.png)

1. Så här visar du de fullständiga **[!UICONTROL Kundprofil]** för varje ID väljer du **[!UICONTROL Profil-ID]** i huvudfönstret.

   >[!NOTE]
   >
   >Observera att du kan välja hyperlänken för profil-ID:t, eller om du markerar raden öppnas en högermeny där du kan välja hyperlänken för profil-ID
   > ![Kundprofil](assets/experience-platform-select-profileId.png)

   Här ser du alla identiteter som är länkade till `lumaCRMId`, till exempel `ECID`.

   ![Kundprofil](assets/experience-platform-validate-dataset-custProfile.png)

Du har nu aktiverat Platform Web SDK för Experience Platform (och Real-Time CDP! Och Journey Optimizer!)!


[Nästa: ](setup-analytics.md)

>[!NOTE]
>
>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Web SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela med dig av dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)