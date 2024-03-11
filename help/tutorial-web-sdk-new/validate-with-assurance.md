---
title: Validera Web SDK-implementeringar med Experience Platform Assurance
description: Lär dig hur du validerar implementeringen av din Platform Web SDK med Adobe Experience Platform Assurance. Den här lektionen ingår i självstudiekursen Implementera Adobe Experience Cloud med Web SDK.
feature: Web SDK,Tags,Assurance
source-git-commit: fd366a4848c2dd9e01b727782e2f26005a440725
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 0%

---

# Validera Web SDK-implementeringar med Experience Platform Assurance

Adobe Experience Platform Assurance är en produkt från Adobe Experience Cloud som hjälper er att inspektera, bevisa, simulera och validera hur ni samlar in data eller levererar upplevelser. Läs mer om [Adobe Assurance](https://experienceleague.adobe.com/docs/experience-platform/assurance/home.html?lang=en).


## Utbildningsmål

När lektionen är klar kan du:

* Starta en Assurance-session
* Visa begäranden som skickas till och från Platform Edge Network

## Förutsättningar

Du känner till datainsamlingstaggar och [Luma demo site](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} och har avslutat tidigare lektioner i självstudiekursen:

* [Konfigurera ett XDM-schema](configure-schemas.md)
* [Konfigurera ett identitetsnamnutrymme](configure-identities.md)
* [Konfigurera ett datastream](configure-datastream.md)
* [Web SDK-tillägget är installerat i taggegenskapen](install-web-sdk.md)
* [Skapa dataelement](create-data-elements.md)
* [Skapa identiteter](create-identities.md)
* [Skapa taggregler](create-tag-rule.md)
* [Validera med felsökning](validate-with-debugger.md)


## Starta och visa en Assurance-session

Det finns flera sätt att starta en Assurance-session.

### Starta en kontrollsession i felsökaren

Varje gång du aktiverar Edge Trace i Adobe Experience Platform Debugger startas en Assurance-session i bakgrunden.

Se hur vi gjorde det här i felsökningslektionen:

1. Gå till [Luma demo site](https://luma.enablementadobe.com/content/luma/us/en.html) och använder felsökaren för att [växla taggegenskapen på webbplatsen till din egen utvecklingsegenskap](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tags-property)
1. I vänster navigering i **[!UICONTROL Experience Platform Debugger]** välj **[!UICONTROL Logs]**
1. Välj **[!UICONTROL Edge]** och markera **[!UICONTROL Connect]**

   ![Koppla kantkalkering](assets/analytics-debugger-edgeTrace.png)
1. När Edge Trace är aktiverat visas en utgående länkikon högst upp. Välj ikonen för att öppna Assurance. En ny flik i webbläsaren öppnas.

   ![Starta Assurance-session](assets/validate-debugger-start-assurnance.png)


### Starta en Assurance-session från försäkringsgränssnittet

1. Öppna [Gränssnitt för datainsamling](https://experience.adobe.com/#/data-collection/home){target="_blank"}
1. Välj Assurance i den vänstra navigeringen
1. Välj Skapa session
1. Välj Start
1. Ge sessionen ett namn, till exempel `Luma Web SDK validation`
1. Som **[!UICONTROL Base URL]** enter `https://luma.enablementadobe.com/`
1. På nästa skärm väljer du **[!UICONTROL Copy Link]**
1. Markera ikonen om du vill kopiera länken till Urklipp
1. Klistra in URL:en i webbläsaren, som öppnar Luma-webbplatsen med en speciell URL-parameter `adb_validation_sessionid` och starta sessionen
1. I Assurance-gränssnittet bör du se ett meddelande som anger att du har anslutit till sessionen och du bör se händelser som har hämtats i Assurance-gränssnittet.

## Validera det aktuella läget för Web SDK-implementeringen

Det finns begränsad information att visa i det här skedet av implementeringen. Ett värde som vi kan se är ditt Experience Cloud-ID (ECID) som genereras i Platform Edge Network:

1. Markera raden med händelsen Adobe-svarshandtag.
1. En meny visas till höger. Välj `+` signera bredvid `[!UICONTROL ACPExtensionEvent]`
1. Granska nedåt genom att välja `[!UICONTROL payload > 0 > payload > 0 > namespace]`. Det ID som visas under den sista `0` motsvarar `ECID`. Det vet du genom det värde som visas under `namespace` matchning `ECID`

   ![Verifiera ECID för försäkring](assets/validate-assurance-ecid.png)

   >[!CAUTION]
   >
   >Du kan se ett trunkerat ECID-värde på grund av fönstrets bredd. Markera bara handtagsfältet i gränssnittet och dra åt vänster för att visa hela ECID:t.

I framtida lektioner använder du Assurance för att validera fullt bearbetade nyttolaster som når ett Adobe-program som är aktiverat i ditt datastream.

Med ett XDM-objekt som nu utlöses på en sida, och med kännedom om hur datainsamlingen ska valideras, är du redo att skapa de enskilda Adobe-programmen med Platform Web SDK.

[Nästa: ](setup-experience-platform.md)

>[!NOTE]
>
>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Web SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela med dig av dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)