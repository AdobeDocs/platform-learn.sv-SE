---
title: Migrera Adobe Analytics till Web SDK med taggar
description: Lär dig de steg du kommer att ta när du går över till Web SDK, liksom vilka beslut som måste fattas på vägen.
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16755
exl-id: e578b669-42b4-46ae-b6e6-6688e5c5c772
source-git-commit: 10982e1d5fa61d2f13ec7686f251a4c7cf6a3565
workflow-type: tm+mt
source-wordcount: '1079'
ht-degree: 0%

---

# Migrera Adobe Analytics till Web SDK med taggar

Lär dig hur du migrerar en Adobe Analytics-implementering med Analytics-tillägget i Experience Platform Tags (tidigare kallad Launch) till Web SDK med hjälp av Web SDK-tillägget även i Tags. När Adobe Analytics-tillägget i Tags används, används koden&quot;AppMeasurement.js&quot; bakom scenen. Därför kan du se det som en självstudiekurs som handlar om att migrera AppMeasurement till Web SDK, men den här självstudiekursen finns helt i Taggar och omfattar INTE att gå till eller från en JavaScript-implementering (med undantag för JavaScript-kod som används i tagggränssnittet). Information om migrering av JavaScript-implementeringar finns i [dokumentationen](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/web-sdk/appmeasurement-to-web-sdk).

## Vad du får ut av den här självstudiekursen

Innan vi börjar med stegen för att migrera din Analytics-implementering är det viktigt att du förstår exakt vad du kommer att göra, vilket ändrar/uppdaterar _implementeringen_ för Analytics. I slutet av den här självstudiekursen, när du går in på dina rapporter och när allt är detsamma, kan du fråga dig själv: &quot;Varför gjorde jag allt det där?&quot; Det finns andra dokument som beskriver fördelarna med att använda Web SDK för er Analytics-implementering, men några av dessa är:

1. Stöd för enhets-ID för första part
1. Bättre prestanda
1. Framtida korrektur av implementeringen när du börjar använda Adobe Experience Platform-programmen (aktivera nya användningsfall)

Tala med din Adobe Analytics-representant om du vill veta mer om hur Web SDK kan hjälpa dig. När vi går vidare med den här självstudiekursen fokuserar vi på _hur_ ska utföra migreringen.

>[!IMPORTANT]
>
>Det är viktigt att komma ihåg att ett av de viktigaste skälen till att du migrerar din implementering är att förbereda dig för att använda Adobe Experience Platform-program som Customer Journey Analytics, Real-Time CDP eller Journey Optimizer (se #3 ovan). Om du använder webbplatsdata för det här ändamålet kommer du att behöva utföra ytterligare steg som inte ingår i den här självstudiekursen, men den här självstudiekursen kommer säkert att vara en förutsättning för den fortsatta implementeringen. Slutför därför den här självstudiekursen och fortsätt sedan med att utföra de steg som krävs för att skicka samma webbplatsdata till Experience Platform.

## Migreringsmetod

Det finns förmodligen många sätt att göra migreringsprocessen, men vi måste prata om två saker här:

**Metod 1:** Uppdatera den befintliga taggegenskapen till Web SDK, skapa nya dataelement och ändra reglerna som redan finns i din egenskap.

**Metod 2:** Du kan också skapa en ny egenskap (genom att kopiera din befintliga egenskap eller skapa en helt ny) och sedan konfigurera den nya egenskapen med Web SDK i stället för Adobe Analytics-tillägget.

**För den här självstudiekursen om migrering kommer vi att använda metod 1.** På så sätt är inbäddningskoderna som är kopplade till egenskapen redan inbäddade på din utvecklar-, mellanlagrings- och produktionsplats, så du behöver inte ändra några inbäddningskoder. Om du väljer metod 2 ska du inte glömma att hämta de nya inbäddningskoderna för varje miljö från avsnittet **Miljö** i den nya egenskapen och placera dem i huvudsektionen på din plats.

>[!NOTE]
>
>Även om vi bara ska redigera vår befintliga egenskap i Taggar under den här migreringen är det fortfarande en bra idé att vara försiktig. Därför rekommenderar vi att du gör en kopia av den aktuella egenskapen innan du påbörjar migreringen. På så sätt kan du alltid gå in i texten och se hur det var innan du ändrade dem, hämta kod från den osv.
>Det är bara bra att vara försiktig, för säkerhets skull. Gör en kopia av din egendom. Jag väntar här tills du kommer tillbaka.

## Steg för att migrera din Analytics-implementering till Web SDK

När du går igenom stegen finns det några viktiga saker att tänka på:

1. Först kanske du behöver alla dessa steg. Det finns till exempel en lektion om hur du migrerar anpassad kod. Om du har en taggimplementering som inte använder anpassad kod (inklusive plugin-program) behöver du inte den här lektionen. Vi försökte inkludera de lektioner som skulle behövas av de flesta, så läs åtminstone igenom lektionerna för att se om du behöver göra några justeringar av din webbplats under migreringen.
1. Dessutom finns det inget sätt för oss att skapa en migreringstips som täcker 100 % av de användningsfall som alla använder. Som tidigare nämnts försökte vi inkludera de lektioner som de flesta människor kommer att behöva, och som kommer att omfatta de flesta av de viktigaste användningsområdena. Det kommer dock utan tvekan att finnas användningsfall som inte omfattas av den här självstudiekursen. I det här fallet bör du kontrollera om de inkluderade lektionerna ger dig en bra uppfattning om hur du bör migrera för ditt användningsfall. Du kan även fråga dina peer-datorer i [Experience League-communityn om datainsamling](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/ct-p/adobe-launch-community).

Migreringsprocessen omfattar följande viktiga steg:

1. Skapa en rapportsvit för migreringsvalidering.
1. Skapa och konfigurera ett datastream.
1. Lägg till och konfigurera Web SDK-tillägget i taggar (tidigare Adobe Launch).
1. Skapa ett nytt dataelement för att skicka data via Web SDK.
1. Migrera standardregeln för sidinläsning så att den använder dataelementet och åtgärderna i Web SDK.
1. Migrera egen kod i regler eller för plugin-program.
1. Publish implementeringsändringar.
1. Lär dig hur du felsöker och validerar dina ändringar och validerar standardregeln för sidinläsning och de variabler som är associerade med den. Valideringen bör sedan fortsätta under migreringen när du gör ändringar.
1. Migrera ytterligare sidinläsningsregler.
1. Migrera anpassade länkregler.
1. Efter fullständig validering tar du bort referenser till Analytics-tillägget och tar bort själva tillägget.
1. När du har gjort alla ändringar kan du överföra biblioteket till staging och sedan till produktion.
1. När allt är klart testar du igen. Detta är nödvändigt eftersom du har gjort ändringar genom att ta bort referenserna till den gamla Analytics-koden och du vill se till att allt fortfarande fungerar som det ska.

>[!NOTE]
>
>Vi vill hjälpa dig att lyckas med din Analytics-migrering till Web SDK. Om du stöter på problem med din migrering eller om du känner att det saknas viktig information i den här guiden kan du meddela oss genom att publicera [den här communitydiskussionen](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-adobe-analytics-to-web-sdk-using/m-p/732308#M604){target="_blank"}.
