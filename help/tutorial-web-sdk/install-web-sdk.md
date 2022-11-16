---
title: Installera och konfigurera taggtillägget Adobe Experience Platform Web SDK
description: Lär dig hur du installerar och konfigurerar plattformens SDK-taggtillägg i gränssnittet för datainsamling. Den här lektionen är en del av självstudiekursen Implementera Adobe Experience Cloud med Web SDK.
feature: Web SDK
exl-id: f30a44bb-99d7-476e-873a-b7802a0fe6aa
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 0%

---

# Installera taggtillägget Adobe Experience Platform Web SDK

Lär dig hur du installerar och konfigurerar plattformens SDK-taggtillägg i gränssnittet för datainsamling. Det här taggtillägget är _endast taggtillägg_ som krävs för att skicka data till _alla Adobe Experience Cloud-program_, inklusive [Analyser](setup-analytics.md), [Mål](setup-target.md), [Audience Manager](setup-audience-manager.md), Real-time Customer Data Platform och Journey Optimizer!

## Utbildningsmål

När lektionen är klar kan du:

* Skapa en taggegenskap i datainsamlingsgränssnittet
* Installera plattformens SDK-taggtillägg
* Mappa tidigare skapade data till tillägget

## Förutsättningar

Du måste ha slutfört föregående lektioner i den här självstudien:

* [Konfigurera behörigheter](configure-permissions.md)
* [Konfigurera ett XDM-schema](configure-schemas.md)
* [Konfigurera ett identitetsnamnutrymme](configure-identities.md)
* [Konfigurera ett datastream](configure-datastream.md)

## Installera Experience Platform Web SDK-tillägg

### Lägg till en egenskap

Först måste du ha en taggegenskap. En egenskap är en behållare för alla JavaScript-skript, regler och andra funktioner som krävs för att samla in information från en webbsida och skicka den till olika platser.

Skapa en ny taggegenskap för självstudiekursen:

1. Öppna [Gränssnitt för datainsamling](https://launch.adobe.com/){target=&quot;_blank&quot;}
1. Välj **[!UICONTROL Taggar]** i den vänstra navigeringen
1. Välj **[!UICONTROL Ny egenskap]** knapp
   ![Lägg till en ny egenskap](assets/websdk-property-addNewProperty.png)
1. Som **[!UICONTROL Namn]**, ange `Web SDK Course` (lägg till ditt namn i slutet om flera personer från ditt företag använder den här självstudiekursen)
1. Som **[!UICONTROL Domäner]**, ange `enablementadobe.com` (förklaras senare)
1. Välj **[!UICONTROL Spara]**
   ![Egenskapsinformation](assets/websdk-property-propertyDetails.png)

## Lägg till Web SDK-tillägget

Med ditt XDM-schema, datastream och taggegenskap som nu skapas är du redo att installera Platform Web SDK-tillägget:

1. Öppna den nya taggegenskapen
1. Gå till **[!UICONTROL Tillägg]** > **[!UICONTROL Katalog]**
1. Sök efter `Adobe Experience Platform Web SDK`
1. Välj **[!UICONTROL Installera]**

   ![Installera SDK-tillägg för webben](assets/extension-platform-web-sdk.jpg)


## Länka Platform Web SDK till din datastream

Lämna de flesta standardinställningarna och uppdatera dem senare efter behov. Det enda du behöver göra nu är att länka tillägget till ditt datastream:

1. Under **[!UICONTROL Datastreams]** väljer du **[!UICONTROL Välj från lista]** indatametod
1. Välj den datastream du skapade tidigare, `Luma Web SDK`
1. Välj **[!UICONTROL Spara]**
   >[!NOTE]
   >
   > Om du inte hittar ditt datastream går du till [Konfigurera ett datastream](configure-datastream.md) lektion och följ stegen för att skapa en

   ![Val av datastam](assets/extension-luma-web-sdk-datastream-extension.png)

Nu när du har installerat Platform Web SDK och kopplat det till datastream är du redo att börja mappa dataelement till ett XDM-objekt med det schema du skapade.

>[!NOTE]
>
>Under den här självstudiekursen konfigurerar du bara en datastream och associerar den med alla taggmiljöer (utveckling, scen och produktion). När du implementerar Platform Web SDK på din egen webbplats bör du konfigurera ett separat datastam för varje miljö och mappa dem till dina taggmiljöer med **[!UICONTROL Indatametod]** > **[!UICONTROL Ange värden]**
>
>![Val av datastam](assets/extension-luma-web-sdk-datastream-extension-enterValues.png)

>[!NOTE]
>
>När du inte konfigurerade en CNAME i [!UICONTROL Edge domain] i den här lektionen rekommenderar Adobe att du använder en CNAME när du implementerar Platform Web SDK på din egen webbplats. En CNAME-implementering ger inga fördelar vad gäller cookie-livstid, men det kan finnas andra fördelar. Fördelarna är annonsblockerare och mindre vanliga webbläsare som förhindrar att data skickas till domäner som de klassificerar som spårare. I dessa fall kan användning av CNAME förhindra att datainsamlingen avbryts för användare som använder dessa verktyg.

Mer information om varje avsnitt av tillägget finns i [Konfigurera Adobe Experience Platform Web SDK-tillägget](https://experienceleague.adobe.com/docs/experience-platform/edge/extension/web-sdk-extension-configuration.html)



[Nästa: ](create-data-elements.md)

>[!NOTE]
>
>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Web SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela med dig av dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
