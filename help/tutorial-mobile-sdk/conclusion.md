---
title: Slutsats och nästa steg
description: Så här gör du när du är klar med självstudien
recommendations: display,noCatalog
exl-id: 69db6cf3-0d5d-4864-aac2-e5e1aea4c02e
source-git-commit: 4a12f8261cf1fb071bc70b6a04c34f6c16bcce64
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 1%

---

# Slutsats och nästa steg

Grattis! Du har slutfört självstudiekursen&quot;Implementera Adobe Experience Cloud i mobilappar&quot;!

Låt oss snabbt granska allt du har gjort. Du har:

* Skapade ett schema med standardfältgrupper och anpassade fältgrupper.
* Konfigurera en datastream.
* En mobil taggegenskap har konfigurerats.
* Installerade och implementerade taggtillägg i en app.
* Följande funktioner har implementerats i ett program:
   * Godkännande
   * Livscykeldata
   * Händelsespårning
   * Identitet
   * Profil
* Experience Cloud-parametrar skickades korrekt till en webbvy.
* Implementeringen har validerats med Adobe Experience Platform Assurance.
* Ansluten implementeringen till följande Experience Cloud-program:
   * Adobe Analytics
   * Experience Platform
   * Journey Optimizer

Du är redo att påbörja nästa fas av din resa - implementera Adobe Experience Cloud i din egen mobilapp!

Och det finns alltid mer att lära sig! Här följer några förslag på annat innehåll som ska byggas på implementeringen:

* **Aktivera vidarebefordran av händelser**. Vidarebefordran av händelser kan enkelt aktiveras i din datastream. Här är [en praktisk lektion för att konfigurera vidarebefordran av händelser](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/event-forwarding/setup-event-forwarding.html) från självstudiekursen om Web SDK. Använd bara de resurser du skapat för din mobilimplementering och välj XDM-fält som du implementerat i appen.
* **Utlösa en resa i Journey Optimizer**. De händelser du implementerade i Luma-appen kan användas för att utlösa resor. Läs mer om detta [videosjälvstudie](https://experienceleague.adobe.com/docs/journey-optimizer-learn/tutorials/create-journeys/use-case-transactional-journey.html).
* **Connect Customer Journey Analytics**. Om du skapade [Plattformsdatauppsättning](platform.md)kan du ansluta datauppsättningen till Customer Journey Analytics. Läs mer om detta [videosjälvstudie](https://experienceleague.adobe.com/docs/customer-journey-analytics-learn/tutorials/connecting-customer-journey-analytics-to-data-sources-in-platform.html)
* **Aktivera Audience Manager** Gör det möjligt för Audience Manager i era datastream att skicka era XDM Experience Events och börja bygga segment baserat på mobilappsengagemang.
* **Implementera Adobe Target**. Target stöds nu med datastream-konfigurationer som är länkade till en mobil egenskap och kan implementeras med [Adobe Journey Optimizer - Beslutstillägg](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/).
* **Skapa ett segment i plattformen**. Om du har aktiverat [schema och datauppsättning för kundprofil i realtid](platform.md)kan ni skapa segment baserat på era mobilappshändelser, kombinera dem med data från andra källor och sedan skicka dessa segment till destinationer i Real-time Customer Data Platform. Läs mer om segmentbyggaren i det här [videosjälvstudie](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html).
* **Implementera Platform Web SDK**. Nu när du har bemästrat en SDK, lär du dig en annan! Adobe Experience Platform Web SDK är den JavaScript SDK som används för att driva Experience Cloud och tredjepartstjänster på webbplatser. Det finns en liknande [praktisk självstudiekurs för Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html). Fyll i båda och se profilerna sammanfogas mellan olika enheter!
* **Läs mer om Experience Platform**. Läs mer om hur du importerar data från andra källor och kombinerar det med dina SDK-data för mobilen i [Getting Started with Adobe Experience Platform for Data Architects and Data Engineers](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/overview.html)


>[!NOTE]
>
>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Mobile SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)