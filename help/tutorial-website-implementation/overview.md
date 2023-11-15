---
title: Implementera Experience Cloud på webbplatser med taggar
description: Implementera Experience Cloud på webbplatser med taggar är den perfekta startpunkten för gränssnittsutvecklare eller teknikmarknadsförare som vill lära sig hur man implementerar Adobe Experience Cloud lösningar på sin webbplats.
recommendations: catalog, noDisplay
exl-id: 1b95f0b2-3062-49d1-9b0b-e6824a54008f
source-git-commit: 277f5f2c07bb5818e8c5cc129bef1ec93411c90d
workflow-type: tm+mt
source-wordcount: '897'
ht-degree: 2%

---

# Översikt

_Implementera Experience Cloud på webbplatser med taggar_ är den perfekta utgångspunkten för utvecklare och teknikmarknadsförare som vill lära sig hur man implementerar Adobe Experience Cloud lösningar på sin webbplats.

Varje lektion innehåller övningar och grundläggande information som hjälper dig att implementera Experience Cloud och förstå dess värde.  Demonstrationssajter tillhandahålls så att du kan slutföra självstudiekursen och lära dig underliggande tekniker i en säker miljö. När du är klar med den här självstudiekursen bör du vara redo att börja implementera alla era marknadsföringslösningar med hjälp av taggar på din egen webbplats.

>[!INFO]
>
>I den här självstudien används programspecifika tillägg och bibliotek (AppMeasurement.js för Adobe Analytics, at.js för Adobe Target). Om du vill implementera Adobe Experience Platform Web SDK går du till [Implementera Adobe Experience Cloud med Web SDK](/help/tutorial-web-sdk/overview.md) självstudie.


När du är klar kan du:

* Skapa en taggegenskap

* Installera en taggegenskap på en webbplats

* Lägg till följande Adobe Experience Cloud-lösningar:
   * **[Adobe Experience Platform Identity Service](id-service.md)**
   * **[Adobe Target](target.md)**
   * **[Adobe Analytics](analytics.md)**
   * **[Adobe Audience Manager](audience-manager.md)**

* Skapa regler och dataelement för att skicka data till Adobe

* Validera implementeringen med Adobe Experience Cloud Debugger

* Publicera ändringar i utvecklings-, staging- och produktionsmiljöer

>[!NOTE]
>
>Adobe Experience Platform Launch håller på att integreras i Adobe Experience Platform som en serie datainsamlingstekniker. Flera terminologiska förändringar har introducerats i gränssnittet som du bör vara medveten om när du använder det här innehållet:
>
> * Platforma launchen (klientsidan) är nu **[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=sv)**
> * Platform launch Server Side is now **[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html)**
> * Edge-konfigurationer är nu **[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html)**

>[!NOTE]
>
>Liknande självstudiekurser om flera lösningar finns även för [Web SDK](../tutorial-web-sdk/overview.md) och [Mobile SDK](../tutorial-mobile-sdk/overview.md).

## Förutsättningar

I den här lektionen antas du ha ett Adobe-ID och de behörigheter som krävs för att slutföra övningarna. Om du inte gör det kan du behöva kontakta din Experience Cloud-administratör för att begära åtkomst.

* För taggar måste du ha behörighet att utveckla, godkänna, publicera, hantera tillägg och hantera miljöer. Mer information om att tagga användarbehörigheter finns i [dokumentationen](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html).
* För Adobe Analytics måste du känna till din spårningsserver och vilka rapportsviter du kommer att använda för att slutföra kursen
* För Audience Manager måste du känna till din Audience Manager-underdomän (även känd som &quot;Partner Name&quot;, &quot;Partner ID&quot; eller &quot;Partner Subdomain&quot;)

Du måste också känna till utvecklingsspråk som HTML och JavaScript. Du behöver inte vara expert på de här språken för att slutföra lektionerna, men du får ut mer av dem om du kan läsa och förstå kod på ett bekvämt sätt.

## Om taggar

Taggfunktionen i Adobe Experience Platform är nästa generation av funktioner för hantering av webbplatstaggar och SDK för mobila enheter från Adobe. Taggar ger kunderna ett enkelt sätt att driftsätta och hantera alla analys-, marknadsförings- och annonslösningar som behövs för att skapa relevanta kundupplevelser. Taggar kostar inget extra. Den kan köpas av alla Adobe Experience Cloud-kunder.

Taggar för webbplatser gör det möjligt att centralt hantera alla JavaScript-lösningar för analys, marknadsföring och annonsering som används på både dator- och mobilsajter. Om du till exempel distribuerar Adobe Analytics kommer taggar att hantera AppMeasurementets JavaScript-bibliotek, fylla i variabler och begära eld.

Innehållet i behållaren är minifierat, inklusive din egen kod. Allt är modulärt. Om du inte behöver något objekt inkluderas det inte i ditt bibliotek. Resultatet är en snabb och kompakt implementering.

Taggar är också en plattform som gör det möjligt för tredjepartsleverantörer att skapa tillägg som gör det enkelt att driftsätta sina lösningar med hjälp av taggar. Ett tillägg är ett kodpaket (JavaScript, HTML och CSS) som utökar tagggränssnittet och klientfunktionerna. Du kan tänka dig taggar som ett operativsystem, och tillägg är de program du använder för att utföra dina uppgifter.

## Om lektionerna

I den här lektionen kommer du att implementera Adobe Experience Cloud i en falsk detaljhandelswebbplats som kallas Luma. The [Luma-webbplats](https://luma.enablementadobe.com/content/luma/us/en.html) har ett omfattande datalager och funktionalitet som gör att du kan skapa en realistisk implementering. Du skapar en egen taggegenskap i din egen Experience Cloud-organisation och mappar den till vår värdbaserade Luma-webbplats med Experience Cloud Debugger.

[![Lumas webbplats](images/overview-luma.png)](https://luma.enablementadobe.com/content/luma/us/en.html)

## Skaffa verktygen

1. Eftersom du kommer att använda vissa webbläsarspecifika tillägg rekommenderar vi att du slutför självstudiekursen med [Chrome Web Browser](https://www.google.com/chrome/)
1. Lägg till [Adobe Experience Cloud Debugger](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj) tillägg till webbläsaren Chrome
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
    <p>See <a href="https://docs.adobe.com/content/help/en/experience-cloud/implementing-in-websites-with-launch/index.html">Implementing the Experience Cloud in Websites with Tags</a> for the complete tutorial</p>
</body>
</html>
```

+++

1. Skaffa en textredigerare där du kan ändra HTML-exempelsidan. (Om du inte har någon rekommenderar vi att du försöker [Parenteser](https://brackets.io/))
1. Bokmärk [Luma-webbplats](https://luma.enablementadobe.com/content/luma/us/en.html)

>[!NOTE]
>
>Det kan vara enklare att slutföra den här självstudiekursen när Luma-webbplatsen är öppen i Chrome, medan du läser den här självstudiekursen och slutför gränssnittsstegen för datainsamling i en annan webbläsare.

Kom så börjar vi!

[Nästa&quot;Skapa en taggegenskap&quot; >](create-a-property.md)
