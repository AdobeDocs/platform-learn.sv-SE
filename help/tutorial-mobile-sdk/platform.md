---
title: Skicka data till Experience Platform med Platform Mobile SDK
description: Lär dig hur du skickar data till Experience Platform.
solution: Data Collection,Experience Platform
feature: Mobile SDK,Data Ingestion
exl-id: fdd2c90e-8246-4d75-a6db-df3ef31946c4
source-git-commit: d353de71d8ad26d2f4d9bdb4582a62d0047fd6b1
workflow-type: tm+mt
source-wordcount: '1072'
ht-degree: 0%

---

# Skicka data till Experience Platform

Lär dig hur du skickar mobilappsdata till Adobe Experience Platform.

Den här valfria lektionen gäller alla kunder som har Real-time Customer Data Platform (Real-Time CDP), Journey Optimizer och Customer Journey Analytics. Experience Platform, grundvalen för Experience Cloud-produkter, är ett öppet system som omvandlar alla era data (Adobe och inte Adobe) till robusta kundprofiler. Dessa kundprofiler uppdateras i realtid och använder AI-baserade insikter för att hjälpa er att leverera rätt upplevelser i alla kanaler.

The [event](events.md), [livscykel](lifecycle-data.md)och [identity](identity.md) data som du har samlat in och skickat till Platform Edge Network i tidigare lektioner vidarebefordras till de tjänster som konfigurerats i ditt datastam, inklusive Adobe Experience Platform.

![Arkitektur](assets/architecture-aep.png)


## Förutsättningar

Din organisation måste etableras och behörigheter beviljas för Adobe Experience Platform.

Om du inte har tillgång till [hoppa över den här lektionen](install-sdks.md).

## Utbildningsmål

I den här lektionen kommer du att:

* Skapa en Experience Platform-datauppsättning.
* Konfigurera dataströmmen för att vidarebefordra data till Experience Platform.
* Validera data i datauppsättningen.
* Aktivera ditt schema och din datauppsättning för kundprofil i realtid.
* Validera data i kundprofilen i realtid.
* Validera data i identitetsdiagrammet.


## Skapa en datauppsättning

Alla data som har inhämtats till Adobe Experience Platform lagras i datasjön som datauppsättningar. En datauppsättning är en lagrings- och hanteringskonstruktion för en datamängd (vanligtvis en tabell) som innehåller ett schema (kolumner) och fält (rader). Datauppsättningar innehåller också metadata som beskriver olika aspekter av de data som lagras. Se [dokumentation](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html) för information.

1. Navigera till gränssnittet Experience Platform genom att välja det i Appar ![Appar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Apps_18_N.svg) i det övre högra hörnet.


1. Välj **[!UICONTROL Datauppsättningar]** från den vänstra navigeringsmenyn.

1. Välj ![Lägg till](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Skapa datauppsättning]**.

1. Välj **[!UICONTROL Skapa datauppsättning från schema]**.
   ![startsida för datauppsättning](assets/dataset-create.png)

1. Sök efter ditt schema. till exempel använda `Luma Mobile` i sökfältet.
1. Välj ditt schema, till exempel **[!DNL Luma Mobile App Event Schema]**.

1. Välj **[!UICONTROL Nästa]**.
   ![konfigurera datauppsättning](assets/dataset-configure.png)

1. Ange en **[!UICONTROL Namn]**, till exempel `Luma Mobile App Events Dataset` och **[!UICONTROL Beskrivning]**.

1. Välj **[!UICONTROL Slutför]**.
   ![datauppsättningens slut](assets/dataset-finish.png)


## Lägg till Adobe Experience Platform datastream-tjänst

Om du vill skicka XDM-data från Edge Network till Adobe Experience Platform lägger du till Adobe Experience Platform-tjänsten i det datastream som du konfigurerat som en del av [Skapa ett datastream](create-datastream.md).

>[!IMPORTANT]
>
>Du kan bara aktivera Adobe Experience Platform-tjänsten när du har skapat en händelsedatamängd.

1. I gränssnittet för datainsamling väljer du **[!UICONTROL Datastreams]** och din datastream.

1. Välj sedan ![Lägg till](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Lägg till tjänst]**.

1. Välj **[!UICONTROL Adobe Experience Platform]** från [!UICONTROL Tjänst] lista.

1. Aktivera tjänsten genom att växla **[!UICONTROL Aktiverad]** på.

1. Välj **[!UICONTROL Händelsedatauppsättning]** som du skapade tidigare, till exempel **[!DNL Luma Mobile App Event Dataset]**.

1. Välj **[!UICONTROL Spara]**.

   ![Lägg till Adobe Experience Platform som datastream-tjänst](assets/datastream-service-aep.png)
1. Den slutliga konfigurationen bör se ut ungefär så här.

   ![datastream-inställningar](assets/datastream-settings.png)


## Validera data i datauppsättningen

Nu när du har skapat en datauppsättning och uppdaterat dataströmmen för att skicka data till Experience Platform vidarebefordras alla XDM-data som skickas till Platform Edge Network till Platform och körningar i datauppsättningen.

Öppna appen och navigera till skärmar där du spårar händelser. Du kan också utlösa livscykelvärden.

Öppna datauppsättningen i plattformsgränssnittet. Du bör se data som anländer i grupper till datauppsättningen. Data hämtas vanligtvis i mikrobatchar var 15:e minut, så du kanske inte ser dina data direkt.

![validera datauppsättningsbatchar för datalandningsplattform](assets/platform-dataset-batches.png)

Du bör också kunna se exempelposter och -fält med **[!UICONTROL Förhandsgranska datauppsättning]** funktion:
![validera livscykeln som skickas till plattformsdatauppsättningen](assets/lifecycle-platform-dataset.png)

Ett robustare verktyg för datavalidering är plattformens [frågetjänst](https://experienceleague.adobe.com/docs/platform-learn/tutorials/queries/explore-data.html).

## Aktivera kundprofil i realtid

Med Experience Platform Real-Time Customer Profile kan ni skapa en helhetsbild av varje enskild kund som kombinerar data från flera kanaler, inklusive online-, offline-, CRM- och tredjepartsdata. Med hjälp av en profil kan ni sammanställa olika kunddata i en enhetlig vy som ger ett användbart, tidsstämplat konto för varje kundinteraktion.

### Aktivera schemat

1. Öppna schemat, till exempel **[!DNL Luma Mobile App Event Schema]**.
1. Aktivera **[!UICONTROL Profil]**.
1. Välj **[!UICONTROL Data för det här schemat kommer att innehålla en primär identitet i identityMap-fältet.]** i dialogrutan.
1. **[!UICONTROL Spara]** schemat.

   ![aktivera schemat för profilen](assets/platform-profile-schema.png)

### Aktivera datauppsättningen

1. Öppna datauppsättningen, till exempel **[!DNL Luma Mobile App Event Dataset]**.
1. Aktivera **[!UICONTROL Profil]**.

   ![aktivera datauppsättningen för profilen](assets/platform-profile-dataset.png)

### Validera data i profilen

Öppna appen och navigera till skärmar där du spårar händelser, till exempel: logga in på Luma-appen och gör ett köp.

Använd Assurance för att hitta en av identiteterna som skickas i identityMap (Email, lumaCrmId eller ECID), till exempel CRM-ID:t.

![hämta ett identitetsvärde](assets/platform-identity.png)

I plattformsgränssnittet

1. Navigera till **[!UICONTROL Profiler]** och markera **[!UICONTROL Bläddra]** i det övre fältet.
1. Ange identitetsinformation som du just har gripit, till exempel `Luma CRM ID` for **[!UICONTROL Namnutrymme för identitet]** och det värde du kopierade för **[!UICONTROL Identitetsvärde]**. Välj sedan **[!UICONTROL Visa]**.
1. Om du vill visa information väljer du profilen.

![söka efter ett identitetsvärde](assets/platform-profile-lookup.png)

På **[!UICONTROL Detalj]** på skärmen kan du se grundläggande information om användaren, inklusive **[!UICONTROL ** länkade identiteter **]**:
![profilinformation](assets/platform-profile-details.png)

På **[!UICONTROL Händelser]** kan du se de händelser som samlats in från din mobilappsimplementering för den här användaren:

![profilhändelser](assets/platform-profile-events.png)


Från profilinformationsskärmen:

1. Om du vill visa identitetsdiagrammet klickar du på länken eller navigerar till **[!UICONTROL Identiteter]** väljer **[!UICONTROL Identitetsdiagram]** i det övre fältet.
1. Om du vill söka efter identitetsvärdet anger du `Luma CRM ID` som **[!UICONTROL Namnutrymme för identitet]** och det kopierade värdet som **[!UICONTROL Identitetsvärde]**. Välj sedan **[!UICONTROL Visa]**.

   Den här visualiseringen visar alla identiteter som är sammankopplade i en profil och deras ursprung. Här är ett exempel på ett identitetsdiagram som består av data som samlats in från den här självstudiekursen för Mobile SDK (datakälla 2) och [Web SDK, genomgång](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html) (datakälla 1):

   ![hämta ett identitetsvärde](assets/platform-profile-identitygraph.png)


## Nästa steg

Det finns mycket mer som marknadsförare och analytiker kan göra med data som samlats in i Experience Platform, inklusive att analysera dem i Customer Journey Analytics och bygga segment i Real-time Customer Data Platform. Du ska börja bra!


>[!SUCCESS]
>
>Du har nu konfigurerat din app så att den inte bara skickar data till Edge Network utan även till Adobe Experience Platform.<br>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Mobile SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Nästa: **[Skapa och skicka push-meddelanden](journey-optimizer-push.md)**
