---
title: Implementera Experience Cloud på webbplatser med taggar
description: Implementera Experience Cloud på webbplatser med taggar är den perfekta startpunkten för gränssnittsutvecklare eller teknikmarknadsförare som vill lära sig hur man implementerar Adobe Experience Cloud lösningar på sin webbplats.
recommendations: catalog, noDisplay
exl-id: 1b95f0b2-3062-49d1-9b0b-e6824a54008f
source-git-commit: 2483409b52562e13a4f557fe5bdec75b5afb4716
workflow-type: tm+mt
source-wordcount: '851'
ht-degree: 0%

---

# Översikt

_Implementera Experience Cloud på webbplatser med taggar_ är den perfekta utgångspunkten för gränssnittsutvecklare eller teknikmarknadsförare som vill lära sig implementera Adobe Experience Cloud lösningar på sin webbplats.

Varje lektion innehåller övningar och grundläggande information som hjälper dig att implementera Experience Cloud och förstå dess värde.  Demonstrationssajter tillhandahålls så att du kan slutföra självstudiekursen och lära dig underliggande tekniker i en säker miljö. När du är klar med den här självstudiekursen bör du vara redo att börja implementera alla era marknadsföringslösningar med hjälp av taggar på din egen webbplats.

>[!INFO]
>
>I den här självstudien används programspecifika tillägg och bibliotek (AppMeasurement.js för Adobe Analytics, at.js för Adobe Target). Om du vill implementera Adobe Experience Platform Web SDK läser du självstudiekursen [Implementera Adobe Experience Cloud med Web SDK](/help/tutorial-web-sdk/overview.md).


När du är klar kan du:

* Skapa en taggegenskap

* Installera en taggegenskap på en webbplats

* Lägg till följande Adobe Experience Cloud-lösningar:
   * **[Adobe Experience Platform identitetstjänst](id-service.md)**
   * **[Adobe Target](target.md)**
   * **[Adobe Analytics](analytics.md)**
   * **[Adobe Audience Manager](audience-manager.md)**

* Skapa regler och dataelement för att skicka data till Adobe

* Validera implementeringen med Adobe Experience Cloud Debugger

* Publish förändras genom utvecklings-, staging- och produktionsmiljöer

>[!NOTE]
>
>Adobe Experience Platform Launch håller på att integreras i Adobe Experience Platform som en serie datainsamlingstekniker. Flera terminologiska förändringar har introducerats i gränssnittet som du bör vara medveten om när du använder det här innehållet:
>
> * Platforma launchen (klientsidan) är nu **[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=sv)**
> * Platforma launchens serversida är nu **[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=sv-SE)**
> * Edge-konfigurationer är nu **[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=sv-SE)**

>[!NOTE]
>
>Liknande självstudier med flera lösningar finns även för [Web SDK](../tutorial-web-sdk/overview.md) och [Mobile SDK](../tutorial-mobile-sdk/overview.md).

## Förhandskrav

I den här lektionen antas du ha ett Adobe-ID och de behörigheter som krävs för att slutföra övningarna. Om du inte gör det kan du behöva kontakta din Experience Cloud-administratör för att begära åtkomst.

* För taggar måste du ha behörighet att utveckla, godkänna, Publish, hantera tillägg och hantera miljöer. Mer information om tagganvändarbehörigheter finns i [dokumentationen](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html?lang=sv-SE).
* För Adobe Analytics måste du känna till din spårningsserver och vilka rapportsviter du kommer att använda för att slutföra kursen
* För Audience Manager måste du känna till din Audience Manager-underdomän (även känd som &quot;Partner Name&quot;, &quot;Partner ID&quot; eller &quot;Partner Subdomain&quot;)

Man utgår också från att man känner till utvecklingsspråk som HTML och JavaScript. Du behöver inte vara expert på de här språken för att slutföra lektionerna, men du får ut mer av dem om du kan läsa och förstå kod på ett bekvämt sätt.

## Om taggar

Taggfunktionen i Adobe Experience Platform är nästa generation av funktioner för hantering av webbplatstaggar och SDK för mobila enheter från Adobe. Taggar ger kunderna ett enkelt sätt att driftsätta och hantera alla analys-, marknadsförings- och annonslösningar som behövs för att skapa relevanta kundupplevelser. Taggar kostar inget extra. Den kan köpas av alla Adobe Experience Cloud-kunder.

Taggar för webbplatser gör det möjligt att centralt hantera alla JavaScript-lösningar för analys, marknadsföring och reklam som används på både dator- och mobilsajter. Om du till exempel distribuerar Adobe Analytics kommer taggar att hantera AppMeasurementet i JavaScript-biblioteket, fylla i variabler och utlösa brandförfrågningar.

Innehållet i behållaren är minifierat, inklusive din egen kod. Allt är modulärt. Om du inte behöver något objekt inkluderas det inte i ditt bibliotek. Resultatet är en snabb och kompakt implementering.

Taggar är också en plattform som gör det möjligt för tredjepartsleverantörer att skapa tillägg som gör det enkelt att driftsätta sina lösningar med hjälp av taggar. Ett tillägg är ett kodpaket (JavaScript, HTML och CSS) som utökar tagggränssnittet och klientfunktionerna. Du kan tänka dig taggar som ett operativsystem, och tillägg är de program du använder för att utföra dina uppgifter.

## Om lektionerna

I den här lektionen kommer du att implementera Adobe Experience Cloud i en falsk detaljhandelswebbplats som kallas Luma. [Luma-webbplatsen](https://luma.enablementadobe.com/content/luma/us/en.html) har ett omfattande datalager och funktioner som gör att du kan skapa en realistisk implementering. Du skapar en egen taggegenskap i din egen Experience Cloud-organisation och mappar den till vår värdbaserade Luma-webbplats med Experience Cloud Debugger.

[![Luma-webbplats](images/overview-luma.png)](https://luma.enablementadobe.com/content/luma/us/en.html)

## Skaffa verktygen

1. Eftersom du kommer att använda vissa webbläsarspecifika tillägg rekommenderar vi att du slutför kursen med [Chrome webbläsare](https://www.google.com/chrome/)
1. Lägg till tillägget [Adobe Experience Platform Debugger](https://chromewebstore.google.com/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) i din Chrome-webbläsare
1. Kopiera HTML-exempelsidkoden

   +++Exempel på HTML-sidkod

   ```html
   <!doctype html>
   <html lang="en">
   <head>
       <title>Tags: Sample HTML Page</title>
       <!--Preconnect and DNS-Prefetch to improve page load time. REPLACE "techmarketingdemos" WITH YOUR OWN AAM PARTNER ID, TARGET CLIENT CODE, AND ANALYTICS TRACKING SERVER-->
       <link rel="preconnect" href="//dpm.demdex.net">
       <link rel="preconnect" href="//fast.techmarketingdemos.demdex.net">
       <link rel="preconnect" href="//techmarketingdemos.demdex.net">
       <link rel="preconnect" href="//cm.everesttech.net">
       <link rel="preconnect" href="//techmarketingdemos.tt.omtrdc.net">
       <link rel="preconnect" href="//techmarketingdemos.sc.omtrdc.net">
       <link rel="dns-prefetch" href="//dpm.demdex.net">
       <link rel="dns-prefetch" href="//fast.techmarketingdemos.demdex.net">
       <link rel="dns-prefetch" href="//techmarketingdemos.demdex.net">
       <link rel="dns-prefetch" href="//cm.everesttech.net">
       <link rel="dns-prefetch" href="//techmarketingdemos.tt.omtrdc.net">
       <link rel="dns-prefetch" href="//techmarketingdemos.sc.omtrdc.net">
       <!--/Preconnect and DNS-Prefetch-->
       <!--Data Layer to enable rich data collection and targeting-->
       <script>
       var digitalData = {
           "page": {
               "pageInfo" : {
                   "pageName": "Home"
                   }
               }
       };
       </script>
       <!--/Data Layer-->
       <!--jQuery or other helper libraries-->
       <script src="https://code.jquery.com/jquery-3.3.1.min.js"></script>
       <!--/jQuery-->
       <!--Tags Header Embed Code: REPLACE THE NEXT LINE WITH THE EMBED CODE FROM YOUR OWN DEVELOPMENT ENVIRONMENT-->
       <script src="//assets.adobedtm.com/launch-EN93497c30fdf0424eb678d5f4ffac66dc.min.js" async></script>
       <!--/Tags Header Embed Code-->
   </head>
   <body>
       <h1>Tags: Sample HTML Page</h1>
       <p>This is a very simple page to demonstrate basic implementation concepts of Tags</p>
       <p>See <a href="https://docs.adobe.com/content/help/sv-SE/experience-cloud/implementing-in-websites-with-launch/index.html">Implementing the Experience Cloud in Websites with Tags</a> for the complete tutorial</p>
   </body>
   </html>
   ```

   +++

1. Skaffa en textredigerare där du kan ändra HTML-exempelsidan. (Om du inte har någon bör du prova [hakparenteser](https://brackets.io/))
1. Bokmärk [Luma-webbplatsen](https://luma.enablementadobe.com/content/luma/us/en.html)

>[!NOTE]
>
>Det kan vara enklare att slutföra den här självstudiekursen med Luma-webbplatsen öppen i Chrome, medan du läser den här självstudiekursen och slutför stegen i gränssnittet för datainsamling i en annan webbläsare.

Kom så börjar vi!

[Nästa&quot;Skapa en taggegenskap&quot; >](create-a-property.md)
