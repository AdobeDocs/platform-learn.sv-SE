---
title: Validera Web SDK-implementeringar med Experience Platform Assurance
description: Lär dig hur du validerar implementeringen av din Platform Web SDK med Adobe Experience Platform Assurance. Den här lektionen ingår i självstudiekursen Implementera Adobe Experience Cloud med Web SDK.
feature: Web SDK,Tags,Assurance
source-git-commit: 4361d8e688ff2c2f3b5472f2cfff246efa627c7f
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---

# Validera Web SDK-implementeringar med Experience Platform Assurance


## Starta en Assurance-session

Adobe Experience Platform Assurance är en produkt från Adobe Experience Cloud som hjälper er att inspektera, bevisa, simulera och validera hur ni samlar in data eller levererar upplevelser.

Läs mer om [Adobe Assurance](https://experienceleague.adobe.com/docs/experience-platform/assurance/home.html?lang=en).

Varje gång du aktiverar Edge Trace startas en Assurance-session i bakgrunden.

Så här visar du Assurance-sessionen:

1. När Edge Trace är aktiverat visas en utgående länkikon högst upp. Välj ikonen för att öppna Assurance. En ny flik i webbläsaren öppnas.

   ![Starta Assurance-session](assets/validate-debugger-start-assurnance.png)

1. Markera raden med händelsen Adobe-svarshandtag.
1. En meny visas till höger. Välj `+` signera bredvid `[!UICONTROL ACPExtensionEvent]`
1. Granska nedåt genom att välja `[!UICONTROL payload > 0 > payload > 0 > namespace]`. Det ID som visas under den sista `0` motsvarar `ECID`. Det vet du genom det värde som visas under `namespace` matchning `ECID`

   ![Verifiera ECID för försäkring](assets/validate-assurance-ecid.png)

   >[!CAUTION]
   >
   >Du kan se ett trunkerat ECID-värde på grund av fönstrets bredd. Markera bara handtagsfältet i gränssnittet och dra åt vänster för att visa hela ECID:t.

I framtida lektioner använder du Assurance för att validera fullt bearbetade nyttolaster som når ett Adobe-program som är aktiverat i ditt datastream.

Med ett XDM-objekt som nu utlöses på en sida, och med kännedom om hur datainsamlingen ska valideras, är du redo att skapa de enskilda Adobe-programmen med Platform Web SDK.