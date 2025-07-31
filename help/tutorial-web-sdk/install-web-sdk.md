---
title: Installera och konfigurera taggtillägget Adobe Experience Platform Web SDK
description: Lär dig hur du installerar och konfigurerar tillägget Platform Web SDK i gränssnittet för datainsamling. Den här lektionen är en del av självstudiekursen Implementera Adobe Experience Cloud med Web SDK.
feature: Web SDK, Tags
jira: KT-15404
exl-id: f30a44bb-99d7-476e-873a-b7802a0fe6aa
source-git-commit: 7ccbaaf4db43921f07c971c485e1460a1a7f0334
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 0%

---

# Installera taggtillägget Adobe Experience Platform Web SDK

Lär dig hur du installerar och konfigurerar taggtillägget Adobe Experience Platform Web SDK. Det enklaste sättet att implementera Web SDK är att använda Adobe tagghanterare, taggar (tidigare Launch). Platsens SDK-taggtillägg är det _enda taggtillägg_ som krävs för att skicka data till _alla Adobe Experience Cloud-program_, inklusive [Analytics](setup-analytics.md), [Target](setup-target.md), [Audience Manager](setup-audience-manager.md), Real-Time Customer Data Platform och [Journey Optimizer](setup-web-channel.md)!

## Utbildningsmål

När lektionen är klar kan du:

* Skapa en taggegenskap i datainsamlingsgränssnittet
* Installera plattformens SDK-taggtillägg
* Mappa tidigare skapade data till tillägget

## Förhandskrav

Du måste ha slutfört föregående lektioner i den här självstudien:

* [Konfigurera ett datastream](configure-datastream.md)

### Lägga till en taggegenskap

Först måste du ha en taggegenskap. En egenskap är en behållare för alla JavaScript, regler och andra funktioner som krävs för att samla in information från en webbsida och skicka den till olika platser.

Skapa en ny taggegenskap för självstudiekursen:

1. Öppna [gränssnittet för datainsamling](https://experience.adobe.com/data-collection/){target="_blank"}
1. Välj **[!UICONTROL Tags]** i den vänstra navigeringen
1. Markera knappen **[!UICONTROL New Property]**
   ![Lägg till en ny egenskap](assets/websdk-property-addNewProperty.png)
1. Som **[!UICONTROL Name]** anger du `Web SDK Course` (lägg till ditt namn i slutet om flera personer från ditt företag använder den här självstudiekursen)
1. Ange **[!UICONTROL Domains]** som `enablementadobe.com` (förklaras senare)
1. Välj **[!UICONTROL Save]**
   ![Egenskapsinformation](assets/websdk-property-propertyDetails.png)

## Lägg till Web SDK-tillägget

Med ditt XDM-schema, datastream och taggegenskap som nu skapas är du redo att installera Platform Web SDK-tillägget:

1. Öppna den nya taggegenskapen
1. Gå till **[!UICONTROL Extensions]** > **[!UICONTROL Catalog]**
1. Sök efter `Adobe Experience Platform Web SDK`
1. Välj **[!UICONTROL Install]**

   ![Installera SDK-tillägget för webben](assets/extension-platform-web-sdk.png)


## Länka tillägget till din datastream

Lämna de flesta standardinställningarna och uppdatera dem senare efter behov. Det enda du måste göra nu är att länka tillägget till ditt datastream:

1. Under **[!UICONTROL Datastreams]** väljer du indatametoden **[!UICONTROL Choose from list]**
1. Välj den sandlåda som du skapade schemat i, identitetsnamnområdet och datastream
1. Välj den datastream som du skapade tidigare, `Luma Web SDK`
1. Välj **[!UICONTROL Save]**

   >[!NOTE]
   >
   > Om du inte hittar ditt datastream går du till [Konfigurera ett datastream](configure-datastream.md)-lektioner och följer stegen för att skapa ett

   ![Val av dataström](assets/extension-luma-web-sdk-datastream-extension.png)

Mer information om de olika avsnitten i tillägget finns i [Konfigurera Adobe Experience Platform Web SDK-tillägget](https://experienceleague.adobe.com/sv/docs/experience-platform/tags/extensions/client/web-sdk/web-sdk-extension-configuration).

>[!NOTE]
>
>Du konfigurerade inte en CNAME i inställningen [!UICONTROL Edge domain] i den här lektionen, men Adobe rekommenderar att du använder en CNAME när du implementerar Platform Web SDK på din egen webbplats. En CNAME-implementering ger inga fördelar vad gäller cookie-livstid, men det kan finnas andra fördelar. Fördelarna är annonsblockerare och mindre vanliga webbläsare som förhindrar att data skickas till domäner som de klassificerar som spårare. I dessa fall kan användning av CNAME förhindra att datainsamlingen avbryts för användare som använder dessa verktyg.

>[!NOTE]
>
>Under den här självstudiekursen konfigurerar du bara en datastream och associerar den med alla taggmiljöer (utveckling, scen och produktion). När du implementerar Platform Web SDK på din egen webbplats bör du konfigurera ett separat datastam för varje miljö och mappa dem därefter i tilläggskonfigurationen.

Nu när du har installerat Platform Web SDK och kopplat det till datastream är du redo att börja samla in data.

>[!NOTE]
>
>Tack för att du har lagt ned din tid på att lära dig om Adobe Experience Platform Web SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela dem i det här [Experience League diskussionsgruppsinlägget](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
