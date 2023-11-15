---
title: Lägg till inbäddningskoden
description: Lär dig hur du hämtar taggegenskapens inbäddningskoder och implementerar dem på din webbplats. Den här lektionen är en del av självstudiekursen Implementera Experience Cloud på webbplatser.
exl-id: a2959553-2d6a-4c94-a7df-f62b720fd230
source-git-commit: 277f5f2c07bb5818e8c5cc129bef1ec93411c90d
workflow-type: tm+mt
source-wordcount: '1056'
ht-degree: 0%

---

# Lägg till inbäddningskoden

I den här lektionen implementerar du den asynkrona inbäddningskoden för taggegenskapens utvecklingsmiljö. Under tiden kommer du att lära dig mer om två viktiga taggar: Miljöer och Bädda in koder.

>[!NOTE]
>
>Adobe Experience Platform Launch håller på att integreras i Adobe Experience Platform som en serie datainsamlingstekniker. Flera terminologiska förändringar har introducerats i gränssnittet som du bör vara medveten om när du använder det här innehållet:
>
> * Platforma launchen (klientsidan) är nu **[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=sv)**
> * Platform launch Server Side is now **[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html)**
> * Edge-konfigurationer är nu **[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html)**

## Utbildningsmål

När lektionen är klar kan du:

* Hämta inbäddningskoden för taggegenskapen
* Förstå skillnaden mellan en utvecklings-, mellanlagrings- och produktionsmiljö
* Lägga till en tagginbäddningskod i ett HTML-dokument
* Förklara den optimala platsen för taggens inbäddningskod i förhållande till annan kod i `<head>` av ett HTML-dokument

## Kopiera inbäddningskoden

Inbäddningskoden är en `<script>` tagg som du lägger in på dina webbsidor för att läsa in och köra logiken som du bygger in i taggar. Om du läser in biblioteket asynkront fortsätter webbläsaren att läsa in sidan, hämtar taggbiblioteket och kör det parallellt. I det här fallet finns det bara en inbäddningskod, som du placerar i `<head>`. (När taggar distribueras synkront finns det två inbäddningskoder, en som du placerar i `<head>` och en annan som du placerar före `</body>`).

På skärmen Egenskapsöversikt klickar du på **[!UICONTROL Miljö]** till vänster för att gå till miljösidan. Observera att utvecklings-, mellanlagrings- och produktionsmiljöer har skapats för dig.

![Klicka på Miljöer i den övre navigeringen](images/launch-environments.png)

Utvecklings-, mellanlagrings- och produktionsmiljöer motsvarar de typiska miljöerna i kodutvecklings- och versionsprocessen. Koden skrivs först av en utvecklare i en utvecklingsmiljö. När de har slutfört sitt arbete skickar de det till en mellanlagringsmiljö för kvalitetskontrollen och andra team för granskning. När kvalitetskontrollen och andra team är nöjda publiceras koden sedan i produktionsmiljön, som är den offentliga miljö som besökarna upplever när de kommer till er webbplats.

Taggar möjliggör ytterligare utvecklingsmiljöer, vilket är användbart i stora organisationer där flera utvecklare arbetar med olika projekt samtidigt.

Det här är de enda miljöer som vi behöver för att slutföra självstudiekursen. I miljöer kan du ha olika arbetsversioner av dina taggbibliotek på olika URL:er, så att du kan lägga till nya funktioner och göra dem tillgängliga för rätt användare (t.ex. utvecklare, QA-ingenjörer, allmänheten, osv.) vid rätt tidpunkt.

Nu kopierar vi inbäddningskoden:

1. I **[!UICONTROL Utveckling]** klickar du på ikonen Installera ![Ikonen Installera](images/launch-installIcon.png) för att öppna modal.

1. Observera att taggar som standard använder asynkrona inbäddningskoder

1. Klicka på ikonen Kopiera ![Kopiera, ikon](images/launch-copyIcon.png) om du vill kopiera inbäddningskoden till Urklipp.

1. Klicka **[!UICONTROL Stäng]** för att stänga modalen.

   ![Ikonen Installera](images/launch-copyInstallCode.png)

## Implementera inbäddningskoden i `<head>` på HTML-sidan

Inbäddningskoden ska implementeras i `<head>` element för alla HTML-sidor som ska dela egenskapen. Du kan ha en eller flera mallfiler som styr `<head>` globalt på hela webbplatsen, vilket gör det enkelt att lägga till taggar.

Om du inte redan har gjort det kopierar du HTML-sidkoden och klistrar in den i en kodredigerare. [Parenteser](https://brackets.io/) är en kostnadsfri redigerare med öppen källkod om du behöver en.

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

Ersätt den befintliga inbäddningskoden på eller runt rad 34 med den i Urklipp och spara sidan. Öppna sidan i en webbläsare. Om du läser in sidan med `file://` måste du lägga till&quot;https:&quot; i början av inbäddningskod-URL:en i kodredigeraren). Raderna 33-36 på exempelsidan kan se ut ungefär så här:

```html
    <!--Tags Header Embed Code: REPLACE LINE 39 WITH THE EMBED CODE FROM YOUR OWN DEVELOPMENT ENVIRONMENT-->
    <script src="https://assets.adobedtm.com/launch-ENa21cfed3f06f4ddf9690de8077b39e81-development.min.js" async></script>
    <!--/Tags Header Embed Code-->
```

Öppna webbläsarens utvecklarverktyg och gå till fliken Nätverk. Nu bör du se ett 404-fel för taggmiljöens URL:
![404-fel](images/samplepage-404.png)

Felet 404 förväntas eftersom du ännu inte har byggt ett bibliotek i den här tagg-miljön. Du kommer att göra det i nästa lektion. Om du ser ett meddelande om att det misslyckades i stället för ett 404-fel har du antagligen glömt att lägga till `https://` i inbäddningskoden. Du behöver bara ange `https://` -protokollet om du läser in exempelsidan med `file://` -protokoll. Gör den ändringen och läs in sidan igen tills felet 404 visas.

## Bästa praxis för taggimplementering

Låt oss titta lite närmare på några av de bästa metoderna för taggimplementering som visas på exempelsidan:

* **Datalager**:

   * Vi *starkt* rekommenderar att du skapar ett datalager på din webbplats som innehåller alla attribut som behövs för att fylla i variabler i lösningar för analys, målgruppsanpassning och annan marknadsföring. Den här exempelsidan innehåller bara ett mycket enkelt datalager, men ett riktigt datalager kan innehålla många fler detaljer om sidan, besökaren, kundvagnen osv. Mer information om datalager finns på [Customer Experience Digital Data Layer 1.0](https://www.w3.org/2013/12/ceddl-201312.pdf)

   * Definiera datalagret före taggens inbäddningskod för att maximera det du kan göra med Experience Cloud-lösningar.

* **Hjälpbibliotek för JavaScript**: Om du redan har ett bibliotek som JQuery implementerat i `<head>` av sidorna, läs in den före taggar för att använda syntaxen i taggar och Target

* **HTML5 doctype**: Dokumenttypen HTML5 krävs av Target

* **preconnect och dns-prefetch**: Använd preconnect och dns-prefetch för att förbättra sidinläsningstiden. Se även: [https://w3c.github.io/resource-hints/](https://w3c.github.io/resource-hints/)

* **fördölja fragment för asynkrona målinsimplementeringar**: Du kommer att lära dig mer om detta i Target-lektionen, men när Target distribueras via asynkrona inbäddningskoder för taggar bör du hårdkoda ett fragment som döljs på sidorna före taggens inbäddningskoder för att hantera innehållsflimret

Här är en sammanfattning av hur dessa bästa metoder ser ut i den föreslagna ordningen. Observera att det finns vissa platshållare för kontospecifik information:

```html
<!doctype html>
<html lang="en">
<head>
    <title>Basic Demo</title>
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
    <!--prehiding snippet for Adobe Target with asynchronous tags deployment-->
    <script>
        (function(g,b,d,f){(function(a,c,d){if(a){var e=b.createElement("style");e.id=c;e.innerHTML=d;a.appendChild(e)}})(b.getElementsByTagName("head")[0],"at-body-style",d);setTimeout(function(){var a=b.getElementsByTagName("head")[0];if(a){var c=b.getElementById("at-body-style");c&&a.removeChild(c)}},f)})(window,document,"body {opacity: 0 !important}",3E3);
    </script>
    <!--/prehiding snippet for Adobe Target with asynchronous tags deployment-->
    <!--Tags Header Embed Code: REPLACE LINE 39 WITH THE INSTALL CODE FROM YOUR OWN DEVELOPMENT ENVIRONMENT-->
    <script src="//assets.adobedtm.com/launch-EN93497c30fdf0424eb678d5f4ffac66dc.min.js" async></script>
    <!--/Tags Header Embed Code-->
</head>
<body>
    <h1>Tags Basic Demo</h1>
    <p>This is a very simple page to demonstrate basic concepts of tags</p>
</body>
</html>
```

Nu vet du hur du lägger till taggens inbäddningskod på din webbplats!

[Därefter&quot;Lägg till ett dataelement, en regel och ett bibliotek&quot; >](add-data-elements-rules.md)
