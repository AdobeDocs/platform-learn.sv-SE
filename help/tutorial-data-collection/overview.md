---
title: Översikt
description: Översikt
exl-id: 527d8f73-33d0-45a6-b7a4-5e46cdb7c138
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---

# Använd Adobe Experience Platform datainsamling

Att samla in data om händelser i en användares webbläsare är en grundläggande del av en marknadsföringsstrategi. Adobe har tillhandahållit flera verktyg som hjälper dig att hantera dessa data. Även om du kan bekanta dig med vart och ett av dessa verktyg var för sig, försöker den här självstudiekursen ge en mer heltäckande bild av vad varje verktyg gör och hur de fungerar tillsammans för att uppnå ett gemensamt mål.

I den här självstudiekursen diskuterar vi en strategi för:

1. Strukturera och lagra data inom Adobe Experience Platform,
1. Hantera data i webbläsaren och kommunicera om att vissa händelser har inträffat, och
1. Reagera på sådana händelser genom att skicka relevanta data till Adobe Experience Platform.

I den här självstudiekursen används Adobe Client Data Layer, Adobe Experience Platform Web SDK och [!DNL Tags] för en mer preskriptiv, smidig implementering kan du också blanda och matcha dessa verktyg med verktyg från tredje part eller internt för optimal flexibilitet.

## Exempelscenario

I den här självstudiekursen implementerar du datainsamling för en enkel produktsida på en e-handelsplats:

1. Produktsidan läses in i webbläsaren. Här ser du att användaren har tittat på produkten.
1. Användaren bestämmer sig för att köpa produkten, så att han/hon klickar på en knapp för att lägga produkten i kundvagnen. Här ser du att användaren har öppnat en ny kundvagn och lagt till produkten i kundvagnen genom att skicka upplevelsehändelser till Adobe Experience Platform.
1. Slutligen klickar användaren på en _Ladda ned appen_ eftersom de är intresserade av din mobilapp. Du kan spåra att användaren har klickat på länken.

Kom så börjar vi!

[Nästa: ](structuring-your-data.md)

>[!NOTE]
>
>Tack för att du har lagt ned din tid på att lära dig om datainsamling. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela med dig av dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)
