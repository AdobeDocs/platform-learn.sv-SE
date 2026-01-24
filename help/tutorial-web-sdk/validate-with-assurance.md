---
title: Validera Web SDK-implementeringar med Experience Platform Assurance
description: Lär dig hur du validerar din Platform Web SDK-implementering med Adobe Experience Platform Assurance. Den här lektionen är en del av självstudiekursen Implementera Adobe Experience Cloud med Web SDK.
feature: Web SDK,Tags,Assurance
jira: KT-15406
exl-id: 31e381ea-fbaf-495f-a6e9-2ff6c0d36939
source-git-commit: 7ccbaaf4db43921f07c971c485e1460a1a7f0334
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 0%

---

# Validera Web SDK-implementeringar med Experience Platform Assurance

Adobe Experience Platform Assurance är en funktion som hjälper er att inspektera, bevisa, simulera och validera hur ni samlar in data eller levererar upplevelser. Läs mer om [Adobe Assurance](https://experienceleague.adobe.com/sv/docs/experience-platform/assurance/home).


## Utbildningsmål

När lektionen är klar kan du:

* Starta en Assurance-session
* Visa förfrågningar som skickats till och från Platform Edge Network

## Förhandskrav

Du är bekant med datainsamlingstaggar och [Luma demo-webbplatsen](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} och har slutfört föregående lektioner i självstudiekursen:

* [Konfigurera ett XDM-schema](configure-schemas.md)
* [Konfigurera ett identitetsnamnutrymme](configure-identities.md)
* [Konfigurera ett datastream](configure-datastream.md)
* [Web SDK-tillägget är installerat i taggegenskapen](install-web-sdk.md)
* [Skapa dataelement](create-data-elements.md)
* [Skapa identiteter](create-identities.md)
* [Skapa en taggregel](create-tag-rule.md)
* [Validera med felsökning](validate-with-debugger.md)


## Starta och visa en Assurance-session

Det finns flera sätt att starta en Assurance-session.

### Starta en Assurance-session i Felsökning

Varje gång du aktiverar Edge Trace i Adobe Experience Platform Debugger startas en Assurance-session i bakgrunden.

Se hur vi gjorde det här i felsökningslektionen:

1. Gå till [demowebbplatsen för luma](https://luma.enablementadobe.com/content/luma/us/en.html) och använd felsökaren för att [växla taggegenskapen på webbplatsen till din egen utvecklingsegenskap](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tags-property)
1. I den vänstra navigeringen för **[!UICONTROL Experience Platform Debugger]** väljer du **[!UICONTROL Logs]**
1. Välj fliken **[!UICONTROL Edge]** och välj **[!UICONTROL Connect]**

   ![Anslut Edge Trace](assets/analytics-debugger-edgeTrace.png)
1. När Edge Trace är aktiverat visas en utgående länkikon högst upp. Klicka på ikonen för att öppna Assurance.

   ![Starta Assurance-session](assets/validate-debugger-start-assurnance.png)

1. En ny flik i webbläsaren öppnas med Assurance gränssnitt.

### Starta en Assurance-session från Assurance gränssnitt

1. Öppna [gränssnittet för datainsamling](https://experience.adobe.com/#/data-collection/home){target="_blank"}
1. Välj Assurance i den vänstra navigeringen
1. Välj Skapa session
   ![Skapa en Assurance-session](assets/assurance-create-session.png)
1. Välj Start
1. Ge sessionen ett namn, till exempel `Luma Web SDK validation`
1. Som **[!UICONTROL Base URL]** anger du `https://luma.enablementadobe.com/`
   ![Namnge Assurance-sessionen](assets/assurance-name-session.png)
1. På nästa skärm väljer du **[!UICONTROL Copy Link]**
1. Markera ikonen om du vill kopiera länken till Urklipp
1. Klistra in URL:en i webbläsaren, som öppnar Luma-webbplatsen med den särskilda URL-parametern `adb_validation_sessionid` och startar sessionen
1. I Assurance-gränssnittet bör du se ett meddelande som anger att du har anslutit till sessionen och du bör se händelser som har hämtats i Assurance-gränssnittet.
   ![Assurance-sessionen har anslutits](assets/assurance-success.png)

## Validera det aktuella läget för Web SDK-implementeringen

Det finns begränsad information att visa i det här skedet av implementeringen. Ett värde som vi kan se är ditt Experience Cloud ID (ECID) som genereras på Platform Edge Network:

1. Markera raden med händelsen `Alloy Response Handle`.
1. En meny visas till höger. Markera `+`-tecknet bredvid `[!UICONTROL ACPExtensionEventData]`
1. Gå ned genom att välja `[!UICONTROL payload > 0 > payload > 0 > namespace]`. Det ID som visas under den sista `0` motsvarar `ECID`. Det vet du med det värde som visas under `namespace` matchande `ECID`

   ![Assurance validate ECID](assets/validate-assurance-ecid.png)

   >[!CAUTION]
   >
   >Du kan se ett trunkerat ECID-värde på grund av fönstrets bredd. Markera bara handtagsfältet i gränssnittet och dra åt vänster för att visa hela ECID:t.

I framtida lektioner använder du Assurance för att validera fullt bearbetade nyttolaster och nå ett Adobe-program som är aktiverat i din datastam.

Med ett XDM-objekt som nu utlöses på en sida, och med kännedom om hur datainsamlingen ska valideras, är du redo att skapa Experience Platform och de enskilda Adobe-programmen med Platform Web SDK.

>[!NOTE]
>
>Tack för att du har lagt ned din tid på att lära dig om Adobe Experience Platform Web SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela dem i det här [Experience League diskussionsgruppsinlägget](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996?profile.language=sv)
