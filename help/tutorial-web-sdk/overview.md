---
title: Implementera Adobe Experience Cloud med Web SDK, genomgång
description: Lär dig hur du implementerar Experience Cloud-program med Adobe Experience Platform Web SDK.
recommendations: catalog, noDisplay
exl-id: cf0ff74b-e81e-4f6d-ab7d-6c70e9b52d78
source-git-commit: cf0193e3aae4d6536c868f078f4773ee14e90408
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 1%

---

# Implementera Adobe Experience Cloud med Web SDK, genomgång

Lär dig hur du implementerar Experience Cloud-program med Adobe Experience Platform Web SDK.

Experience Platform Web SDK är ett JavaScript-bibliotek på klientsidan som gör det möjligt för Adobe Experience Cloud kunder att interagera med både Adobe-program och tredjepartstjänster via Adobe Experience Platform Edge Network. Se [Adobe Experience Platform Web SDK - översikt](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html) för mer detaljerad information.

I den här självstudiekursen får du hjälp med att implementera Platform Web SDK på en exempelwebbplats som heter Luma. The [Luma site](https://luma.enablementadobe.com/content/luma/us/en.html) har ett omfattande datalager och funktioner som gör att du kan skapa en realistisk implementering. När du är klar med den här självstudiekursen kan du börja implementera alla dina marknadsföringslösningar via Platform Web SDK på din egen webbplats.

[![Lumas webbplats](assets/old-overview-luma.png)](https://luma.enablementadobe.com/content/luma/us/en.html)


## Utbildningsmål

När du är klar med självstudiekursen kan du:

* Konfigurera datastreams

* Skapa XDM-scheman

* Lägg till följande Adobe Experience Cloud-program:
   * **[Adobe Experience Platform](setup-experience-platform.md)** (och program som bygger på Platform som Adobe Real-time Customer Data Platform, Adobe Journey Optimizer och Adobe Customer Journey Analytics)
   * **[Adobe Analytics](setup-analytics.md)**
   * **[Adobe Audience Manager](setup-audience-manager.md)**
   * **[Adobe Target](setup-target.md)**

* Skapa taggregler och XDM-objektdataelement för att skicka data till Adobe-program

* Validera implementeringen med Adobe Experience Platform Debugger

* Inhämta användarens samtycke

* Vidarebefordra data till tredje part med händelsevidarebefordran

>[!NOTE]
>
>En liknande självstudiekurs om flera lösningar finns tillgänglig för [Mobile SDK](../tutorial-mobile-sdk/overview.md).

## Förutsättningar

Alla Experience Cloud-kunder kan använda Platform Web SDK. Det är inte ett krav att licensiera ett plattformsbaserat program som Real-time Customer Data Platform eller Journey Optimizer att använda Web SDK.

I den här lektionen antas att du har ett Adobe-konto och [nödvändiga behörigheter](configure-permissions.md) för att slutföra lektionerna. Om inte, måste du kontakta din Experience Cloud-administratör för att begära åtkomst.

Du måste också känna till utvecklingsspråk som HTML och JavaScript. Du behöver inte vara expert på de här språken, men du får ut mer av den här självstudiekursen om du kan läsa och förstå kod.

Kom så börjar vi!

[Nästa: ](configure-permissions.md)

>[!NOTE]
>
>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Web SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela med dig av dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
