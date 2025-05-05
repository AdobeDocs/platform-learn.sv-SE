---
title: Felsöka och validera din SDK-migrering på webben
description: Lär dig hur du felsöker och validerar data när du migrerar till SDK på webben
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16763
exl-id: 68f87266-4b87-4953-8de4-6a9a62bac9e6
source-git-commit: 7c0a6c769d56b3e56a5667d5aeff47b55ab6dc33
workflow-type: tm+mt
source-wordcount: '1253'
ht-degree: 0%

---

# Felsöka och validera din SDK-migrering på webben

I den här övningen får du lära dig att felsöka och validera data när du migrerar till Web SDK. Vi vill uppmuntra till två olika valideringsaktiviteter som kan hjälpa dig att se till att allt fungerar som det ska:

1. **Verifieringsaktiviteten #1** kör Adobe Experience Platform Debugger, som är ett webbläsartillägg, och gör att du kan kontrollera hur data skickas till Analytics på rätt sätt. Vi rekommenderar att du gör den här aktiviteten ofta när du gör ändringar i taggegenskapen och publicerar ändringarna i ett utvecklingsbibliotek.
1. **Verifieringsaktivitet nr 2** går till Adobe Analytics, konfigurerar ett eller flera projekt för att ta emot data från Web SDK (via din nyligen skapade migreringsrapportsserie) och verifierar att dina data verkligen kommer in i rapporterna korrekt när du klickar på webbplatsen, osv.

## Adobe Experience Platform Debugger

Felsökaren är ett webbläsartillägg och finns på Chrome Store. Det finns en [videosjälvstudiekurs](https://experienceleague.adobe.com/sv/docs/platform-learn/data-collection/debugger/overview) som förklarar hur du hämtar och använder felsökaren, och vi rekommenderar att du först går igenom den för att ta reda på den grundläggande användningen.

När du har startat felsökningen kan du använda den för att se till att data flödar från din plats och från Edge Network korrekt. Den här självstudiekursen kommer att användas i ganska grundläggande utsträckning, men använd felsökaren till fullo för att kontrollera dina data.

**Förutsättning (alltid farligt, men förhoppningsvis finjusterat i det här fallet):** Eftersom vi migrerar taggegenskapen till Web SDK i det här exemplet behöver vi inte placera någon ny inbäddningskod på webbplatsen. Den kommer redan ha varit där. Om du däremot bestämmer dig för att du vill göra mer av en&quot;lyft och förskjutning&quot;-strategi i en helt ny taggegenskap, har du nya inbäddningskoder att placera i din utvecklings-, staging- och produktionsmiljö. Så i den här självstudiekursen visas data i felsökaren så länge som vi har Web SDK-tillägget installerat och konfigurerat med regler som skickar data in.

### Visa SDK-data för webben i felsökaren

Nu när du har migrerat din standardsidregel (eller om du har migrerat några regler) och publicerat den i ett bibliotek i utvecklingsmiljön bör du kunna köra din webbplats och se data som flödar in i felsökaren.

Steg för att visa dina data:

1. Öppna utvecklingsmiljön för webbplatsen i webbläsaren
1. Öppna felsökaren genom att klicka på webbläsartillägget i tilläggsfältet högst upp i webbläsarfönstret

   ![Felsökningstillägg](assets/debugger-extension.jpg)

   >[!TIP]
   >
   >I det nedre högra hörnet av felsökningen finns en&quot;låsikon&quot; och en etikett, och till vänster om den ser du vilken sida du felsöker. Klicka på låsikonen när du befinner dig på webbplatsen, vilket låser felsökaren till webbplatsens fönster. Annars skulle felsökaren svara på webbplatsen om du klickade in på en annan flik eller ett annat fönster i webbläsaren. Under felsökningen av webbplatsen är det bara enklare att se till att felsökaren alltid ger dig information om webbplatsen.

1. Kontrollera att du är på sidan **Sammanfattning** i felsökaren (&quot;Hem&quot;-ikonen längst upp till vänster). **Uppdatera platsen** i webbläsarfönstret. Om felsökaren hämtar inbäddningskoden på din webbplats, och om du inte tog bort Analytics-koden (enligt den här självstudien), visas indikationer på att det fanns kod för både Adobe Experience Platform Web SDK och Adobe Analytics samt för Adobe Experience Platform Tags. Andra blir gråtonade.

   ![Sammanfattning av felsökning](assets/debugger-summary.jpg)

1. Klicka på länken **Experience Platform Web SDK** i den vänstra listen om du vill se data som lagts till via SDK på webben
1. Klicka på **Rensa händelser** bara för att ta bort träffar som har inträffat
1. Uppdatera webbplatsen igen och gå tillbaka till felsökaren
1. Klicka sedan på datafältet bredvid **händelser** i tabellen

   ![Händelsefält i felsökaren](assets/events-field-in-debugger.jpg)

1. I fältet Värde expanderar du nedåt genom 0, data, __adobe och analyser
1. Du bör se variablerna som du anger i de regler som utlöses på den sidan, inklusive standardregeln för sidinläsning och eventuella specialregler.

   ![Dataobjekt i felsökning](assets/data-object-in-debugger.jpg)

1. Utför dessa steg när du har ändrat något i taggegenskapen och publicerat ändringarna i utvecklingen, så att du kan se effekten av de ändringar du har gjort i Analytics-implementeringen.

## Validera data i Analysis Workspace

Den främsta tonen i den här rekommendationen är att ta aktuella analysdata som kommer in från implementeringen av taggar med Adobe Analytics-tillägget och jämföra dem med samma rapporter som nu kommer att fyllas av Web SDK.
Det finns kanske flera sätt att göra jämförelserna, men jag ska ge er två exempel på hur man gör det här.

### Alternativ 1: Jämför data med två paneler i ett enda projekt

1. Skapa ett nytt projekt i Analysis Workspace och lägg till två paneler
1. Ställ in rapportsviten i panel 1 på din nuvarande Adobe Analytics-serie
1. Ange rapportsviten i panel 2 i din nya Web SDK-utvecklingsrapportsserie
1. Lägg in samma rapport i båda panelerna, med en tidsperiod som endast omfattar fullständiga dagar då data skickades till båda rapportsviterna
1. Jämför data

Det här kan se ut ungefär så här (eftersom det inte finns några data i dessa tomma demorapporteringsprogram):

![Jämför rapportsvitens nummer](assets/compare-report-suite-numbers-panels.jpg)

Som du ser är rapporten densamma på båda panelerna och kalendern är densamma. Skillnaden är rapportsviten, som framgår av stegen ovan.
**Fördelar med det här alternativet:** Du kan gå en i taget med rapporter/dimensioner och testa exakt det du vill testa när du gör ändringar i implementeringen.

### Alternativ 2: Jämför data med två projekt

1. Öppna ett befintligt projekt som använder dina aktuella Adobe Analytics-tilläggsdata
1. Gör en Spara som-kopia av projektet och ge det ett namn som &quot;Web SDK Migration validation project&quot;
1. Ändra rapportsviten för det kopierade projektet så att den pekar på webbutvecklingsrapportsviten för SDK
1. Öppna varje projekt i ett eget fönster och ändra storlek på dem så att du kan se dem bredvid varandra på skärmen
1. Jämför data

Det ser ut ungefär som bilden ovan, förutom att varje panel är i ett eget projekt och i ett annat fönster.
**Fördelar med det här alternativet:** I det här fallet behöver du inte lägga till och konfigurera alla dina rapporter igen, men du får se hur dina aktuella rapporter kommer att se ut med det nya Web SDK-tillägget med minimal konfiguration.

Det är möjligt att du vill göra båda, vilket också är ett bra alternativ.

>[!IMPORTANT]
>
>Nu när du har slutfört valideringen av standardregeln för sidinläsning kan du gå vidare i självstudiekursen. Vi implementerar emellertid att du testar/validerar ofta, förmodligen åtminstone varje gång du ändrar en regel eller gör andra betydande ändringar. Kom ihåg att om du upptäcker ett problem när du går vidare kommer du att bli nöjdare om du bara behöver kontrollera EN sak i stället för att testa flera ändringar som du har gjort sedan den senaste valideringen.

Grattis på valideringen!
