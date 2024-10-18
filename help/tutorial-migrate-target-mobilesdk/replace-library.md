---
title: Ersätt SDK - Migrera från Adobe Target till Adobe Journey Optimizer - mobiltillägg för beslut
description: Lär dig hur du ersätter SDK när du migrerar från Adobe Target till tillägget Adobe Journey Optimizer - Decisioning Mobile.
source-git-commit: afbc8248ad81a5d9080a4fdba1167e09bbf3b33d
workflow-type: tm+mt
source-wordcount: '1531'
ht-degree: 0%

---

# Ersätt mål-SDK med Optimera SDK

Lär dig hur du ersätter din Adobe Target-implementering på sidan för att migrera från at.js till Platform Web SDK. En grundläggande ersättning består av följande steg:

* Granska inställningarna för måladministration och notera ditt IMS-organisations-ID
* Ersätt at.js-biblioteket med Platform Web SDK
* Uppdatera det föregående fragmentet för synkrona biblioteksimplementeringar
* Konfigurera Platform Web SDK

>[!NOTE]
>
>Exemplen är till för illustrativa ändamål och den faktiska Target-implementeringen kan variera. Om din befintliga målinsimplementering använder tagghanteraren för Adobe Data Collection kan du även läsa [implementeringsjälvstudiekursen för plattforms-SDK-mål](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html) för mer information.


## Granska Administrationsinställningar för mål

Det första steget för att migrera Target till Platform Web SDK är att granska dina inställningar i målgränssnittets **[!UICONTROL Administration]**-avsnitt.

### [!UICONTROL Implementation]

#### [!UICONTROL Account details]

* **[!UICONTROL IMS Organization Id]** - Observera det här värdet eftersom det krävs för att konfigurera Platform Web SDK.
* **[!UICONTROL On-Device Decisioning]** - Den här funktionen stöds inte av Platform Web SDK. Den här inställningen kan inaktiveras när du har migrerat och om du inte längre använder at.js på någon av dina webbplatser eller har några användningsfall på serversidan för On-Device Decision.

#### [!UICONTROL Implementation methods]

Alla redigerbara inställningar i avsnittet **[!UICONTROL Implementation methods]** gäller endast för at.js. De här inställningarna används för att generera ett anpassat at at.js-bibliotek för implementeringen. Granska de här inställningarna för att kontrollera om du har någon anpassad kod eller ställer in cookies från första och tredje part för användning över domäner.

Inställningen **[!UICONTROL Profile Lifetime]** kan bara ändras av Adobe kundtjänst. Livslängden för målbesökarprofilen påverkas inte av implementeringsmetoden. Både at.js och Platform Web SDK använder samma livstid för besökarprofiler.

#### [!UICONTROL Privacy]

* **[!UICONTROL Obfuscate Visitor IP addresses]** - Den här inställningen påverkar geolokalisering. Både at.js och Platform Web SDK använder samma inställningar för bakomliggande IP-fakturering vid geolokalisering.

### [!UICONTROL Environments]

Platform Web SDK använder en datastream-konfiguration som gör att du uttryckligen kan definiera en [!UICONTROL Environment ID] för separata dataströmmar för utveckling, staging och produktion. Det viktigaste användningsexemplet för den här konfigurationen är implementeringar av mobilappar där det inte finns några URL:er för att enkelt kunna skilja på olika miljöer. Inställningen är valfri men kan användas för att säkerställa att alla begäranden är korrekt kopplade till den angivna miljön. Detta skiljer sig från en at.js-implementering där du måste tilldela Target-miljöer baserat på domäner och värdgruppsregler.

>[!NOTE]
>
>Om inget miljö-ID anges i datastream-konfigurationen använder Target domänen-till-miljö-mappningen enligt avsnittet **Värdar**.

Mer information finns i [datastream-konfigurationsguiden](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html#target) och dokumentationen för [målvärdarna](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html).

## Distribuera Platform Web SDK

Målfunktionerna finns i både at.js och Platform Web SDK. Om båda biblioteken används samtidigt kan det uppstå problem med återgivning och spårning. Det första steget är att ta bort at.js och ersätta den med Platform Web SDK (alloy.js) för att kunna migrera till Platform Web SDK.

Anta en enkel målinsimplementering med at.js:

* Ett datalager nära sidans överkant ger information om Target och andra program
* Ett eller flera hjälpbibliotek från tredje part vars funktioner kan användas i Target-aktiviteter (till exempel jQuery)
* Ett fördolt kodfragment som minskar flimret
* Målet-biblioteket at.js läses in asynkront med standardinställningar för att automatiskt begära och återge aktiviteter:

+++at.js, exempelimplementering på en HTML-sida

```HTML
<!doctype html>
<html>
<head>
  <title>Example page</title>
  <!--Data Layer to enable rich data collection and targeting-->
  <script>
    var digitalData = { 
      // Data layer information goes here
    };
  </script>
  <!--Third party libraries that may be used by Target offers and modifications-->
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.1/jquery.min.js"></script>
  <!--prehiding snippet for Target with asynchronous deployment-->
  <script>
    ;(function(win, doc, style, timeout) {
      var STYLE_ID = 'at-body-style';

      function getParent() {
        return doc.getElementsByTagName('head')[0];
      }

      function addStyle(parent, id, def) {
        if (!parent) {
          return;
        }
        var style = doc.createElement('style');
        style.id = id;
        style.innerHTML = def;
        parent.appendChild(style);
      }

      function removeStyle(parent, id) {
        if (!parent) {
          return;
        }
        var style = doc.getElementById(id);
        if (!style) {
          return;
        }
        parent.removeChild(style);
      }
      addStyle(getParent(), STYLE_ID, style);
      setTimeout(function() {
        removeStyle(getParent(), STYLE_ID);
      }, timeout);
    }(window, document, "body {opacity: 0 !important}", 3000));
  </script>
  <!--Target at.js library loaded asynchonously-->
  <script src="/libraries/at.js" async></script>
</head>
<body>
  <h1 id="title">Home Page</h1><br><br>
  <p id="bodyText">Navigation</p><br><br>
  <a id="home" class="navigationLink" href="#">Home</a><br>
  <a id="pageA" class="navigationLink" href="#">Page A</a><br>
  <a id="pageB" class="navigationLink" href="#">Page B</a><br>
  <a id="pageC" class="navigationLink" href="#">Page C</a><br>
  <div>Homepage Hero Banner Content</div>
</body>
</html>
```

+++

Om du vill uppgradera Target till att använda Platform Web SDK måste du först ta bort at.js:

```HTML
<!--Target at.js library loaded asynchonously-->
<script src="/libraries/at.js" async></script>
```

Och ersätt med antingen ett JavaScript-bibliotek eller med taggarna inbäddad kod och Adobe Experience Platform Web SDK-tillägget:

>[!BEGINTABS]

>[!TAB JavaScript]

```HTML
<!--Platform Web SDK base code-->
<script>
  !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
  []).push(o),n[o]=function(){var u=arguments;return new Promise(
  function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
  (window,["alloy"]);
</script>
<!--Platform Web SDK loaded asynchonously. Change the src to use the latest supported version.-->
<script src="https://cdn1.adoberesources.net/alloy/2.13.1/alloy.min.js" async></script>
```

>[!TAB Taggar]

```HTML
<!--Tags Header Embed Code: REPLACE WITH THE INSTALL CODE FROM YOUR OWN ENVIRONMENT-->
<script src="//assets.adobedtm.com/launch-EN93497c30fdf0424eb678d5f4ffac66dc.min.js" async></script>
```

Lägg till Adobe Experience Platform Web SDK-tillägget i taggegenskapen:

<!--![Add the Adobe Experience Platform Web SDK extension](assets/library-tags-addExtension.png){zoomable="yes"}-->


>[!ENDTABS]

Den fördefinierade fristående versionen kräver en &quot;baskod&quot; som läggs till direkt på sidan och som skapar en global funktion med namnet alloy. Använd den här funktionen för att interagera med SDK:n. Om du vill ge den globala funktionen ett annat namn ändrar du namnet på `alloy`.

Mer information och distributionsalternativ finns i [Installing the Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html) -dokumentationen.


## Uppdatera metod för att dölja innehåll

Implementeringen av Platform Web SDK kan kräva ett predhide-fragment beroende på om biblioteket läses in asynkront eller synkront.

### Asynkron implementering

Precis som med at.js, kan det hända att sidan slutför återgivningen innan Target har utfört en innehållsväxling om Platform Web SDK-biblioteket läses in asynkront. Det här beteendet kan leda till det som kallas&quot;flimmer&quot;, där standardinnehållet visas kort innan det ersätts av det anpassade innehåll som anges av Target. Om du vill undvika denna flimmer rekommenderar Adobe att du lägger till ett särskilt preddolt kodfragment omedelbart före den asynkrona Platform Web SDK-skriptreferensen eller taggarna bäddar in kod.

Om implementeringen är asynkron, som exemplen ovan, ska du ersätta fragmentet at.js med versionen nedan som är kompatibel med plattformens Web SDK:

```HTML
<!--Prehiding snippet for Target with asynchronous Web SDK deployment-->
<script>
  !function(e,a,n,t){var i=e.head;if(i){
  if (a) return;
  var o=e.createElement("style");
  o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
  (document, document.location.href.indexOf("mboxEdit") !== -1, "body { opacity: 0 !important }", 3000);
</script>
```

Med det föregående dolda fragmentet skapas en formattagg i sidhuvudet med den CSS-definition du väljer. Den här stiltaggen tas bort när ett svar från Target tas emot eller när tidsgränsen nås.

Beteendet för att dölja är styrt av två konfigurationer i slutet av fragmentet.

* `body { opacity: 0 !important }` anger den CSS-definition som ska användas för döljningen tills Target läses in. Som standard är hela sidan dold. Du kan uppdatera den här definitionen till de väljare som du vill dölja tillsammans med hur du vill dölja dem. Du kan inkludera flera definitioner eftersom det här värdet är det som infogas i den föregående formattaggen. Om du har ett enkelt identifierbart behållarelement som omsluter innehållet under navigeringen kan du använda den här inställningen för att begränsa det dolda innehållet till behållarelementet.

* `3000` anger timeout i millisekunder för predhide. Om inget svar från Target tas emot före timeout, tas den föregående dolda formattaggen bort. Det bör vara sällsynt att denna tidsgräns uppnås.

>[!IMPORTANT]
>
>Använd rätt fragment för plattformens Web SDK eftersom den använder ett annat format-ID, `alloy-prehiding`. Om fragmentet för at.js före döljning används kanske det inte fungerar som det ska.

### Synkron implementering

Adobe rekommenderar att du implementerar Platform Web SDK asynkront för bästa totala sidprestanda. Om alloy.js-biblioteket eller taggarna bäddar in kod synkront behöver du inte skriva ut predhide. I stället anges det fördolda formatet i konfigurationen för Platform Web SDK.

Det tidigare dolda formatet för synkrona implementeringar kan konfigureras med alternativet [`prehidingStyle`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#prehidingStyle). Konfiguration av Platform Web SDK beskrivs i nästa avsnitt.

Om du vill veta mer om hur Platform Web SDK kan hantera flimmer kan du läsa hjälpavsnittet: [hantera flimmer för personaliserade upplevelser](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/manage-flicker.html)

## Konfigurera Platform Web SDK

Platform Web SDK måste konfigureras för varje sidinläsning. I följande exempel antas att hela webbplatsen uppgraderas till Platform Web SDK i en enda distribution:

>[!BEGINTABS]

>[!TAB JavaScript]

Kommandot `configure` måste alltid vara det första SDK-kommandot som anropas. `edgeConfigId` är [!UICONTROL Datastream ID]

```JavaScript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

>[!TAB Taggar]

I taggitimeringar fylls många fält i automatiskt eller kan väljas i listrutor. Observera att olika plattformar [!UICONTROL sandboxes] och [!UICONTROL datastreams] kan väljas för varje miljö. Datastream ändras baserat på statusen för taggbiblioteket i publiceringsprocessen.

<!--![configuring the Web SDK tag extension](assets/tags-config.png){zoomable="yes"}-->
>[!ENDTABS]

Om du planerar att migrera från at.js till Platform Web SDK sida för sida krävs följande konfigurationsalternativ:


>[!BEGINTABS]

>[!TAB JavaScript]

```JavaScript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg",
  "targetMigrationEnabled":true,
  "idMigrationEnabled":true
});
```

>[!TAB Taggar]

<!--![configuring the Web SDK tag extension migration options](assets/tags-config-migration.png){zoomable="yes"}-->

>[!ENDTABS]

De alternativ för konfiguration som är relaterade till Target beskrivs nedan:

| Alternativ | Beskrivning | Exempelvärde |
| --- | --- | --- |
| `edgeConfigId` | DataStream ID | `ebebf826-a01f-4458-8cec-ef61de241c93` |
| `orgId` | Adobe Experience Cloud organisations-ID | `ADB3LETTERSANDNUMBERS@AdobeOrg` |
| `targetMigrationEnabled` | Använd det här alternativet om du vill att Web SDK ska kunna läsa och skriva de äldre mbox- och mboxEdgeCluster-cookies som används av at.js. Detta hjälper dig att behålla besökarprofilen när du går från en sida där Web SDK används till en sida där at.js-biblioteket används och tvärtom. | `true` |
| `idMigrationEnabled` | Om true läser SDK in gamla AMCV-cookies. Med det här alternativet kan du gå över till att använda Platform Web SDK medan vissa delar av webbplatsen fortfarande använder Visitor.js. | `true` |
| `thirdPartyCookiesEnabled` | Aktiverar inställningen av cookies från tredje part från Adobe. SDK:n kan behålla besökar-ID:t i ett tredjepartssammanhang för att samma besökar-ID ska kunna användas på olika platser. Använd det här alternativet om du har flera webbplatser, men ibland är det här alternativet inte önskvärt av sekretesskäl. | `true` |
| `prehidingStyle` | Används för att skapa en CSS-formatdefinition som döljer innehållsområden på webbsidan när anpassat innehåll läses in från servern. Detta används endast med synkrona distributioner av SDK. | `body { opacity: 0 !important }` |

En fullständig lista med alternativ finns i guiden [Konfigurera Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html) .

## Implementeringsexempel

När Platform Web SDK är rätt på plats ser exempelsidan ut så här.

>[!BEGINTABS]

>[!TAB JavaScript]

```HTML
<!doctype html>
<html>
<head>
  <title>Example page</title>
  <!--Data Layer to enable rich data collection and targeting-->
  <script>
    var digitalData = { 
      // Data layer information goes here
    };
  </script>

  <!--Third party libraries that may be used by Target offers and modifications-->
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.1/jquery.min.js"></script>

  <!--Prehiding snippet for Target with asynchronous Web SDK deployment-->
  <script>
    !function(e,a,n,t){var i=e.head;if(i){
    if (a) return;
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("mboxEdit") !== -1, ".body { opacity: 0 !important }", 3000);
  </script>

  <!--Platform Web SDK base code-->
  <script>
    !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
    []).push(o),n[o]=function(){var u=arguments;return new Promise(
    function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
    (window,["alloy"]);
  </script>

  <!--Platform Web SDK loaded asynchonously. Change the src to use the latest supported version.-->
  <script src="https://cdn1.adoberesources.net/alloy/2.13.1/alloy.min.js" async></script>
  
  <!--Configure Platform Web SDK-->
  <script>
    alloy("configure", {
      "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
      "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
    });
  </script>
</head>
<body>
  <h1 id="title">Home Page</h1><br><br>
  <p id="bodyText">Navigation</p><br><br>
  <a id="home" class="navigationLink" href="#">Home</a><br>
  <a id="pageA" class="navigationLink" href="#">Page A</a><br>
  <a id="pageB" class="navigationLink" href="#">Page B</a><br>
  <a id="pageC" class="navigationLink" href="#">Page C</a><br>
  <div id="homepage-hero">Homepage Hero Banner Content</div>
</body>
</html>
```

>[!TAB Taggar]

Sidkod:

```HTML
<!doctype html>
<html>
<head>
  <title>Example page</title>
  <!--Data Layer to enable rich data collection and targeting-->
  <script>
    var digitalData = { 
      // Data layer information goes here
    };
  </script>

  <!--Third party libraries that may be used by Target offers and modifications-->
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.1/jquery.min.js"></script>

  <!--Prehiding snippet for Target with asynchronous Web SDK deployment-->
  <script>
    !function(e,a,n,t){var i=e.head;if(i){
    if (a) return;
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("mboxEdit") !== -1, ".body { opacity: 0 !important }", 3000);
  </script>

    <!--Tags Header Embed Code: REPLACE WITH THE INSTALL CODE FROM YOUR OWN ENVIRONMENT-->
    <script src="//assets.adobedtm.com/launch-EN93497c30fdf0424eb678d5f4ffac66dc.min.js" async></script>
</head>
<body>
  <h1 id="title">Home Page</h1><br><br>
  <p id="bodyText">Navigation</p><br><br>
  <a id="home" class="navigationLink" href="#">Home</a><br>
  <a id="pageA" class="navigationLink" href="#">Page A</a><br>
  <a id="pageB" class="navigationLink" href="#">Page B</a><br>
  <a id="pageC" class="navigationLink" href="#">Page C</a><br>
  <div id="homepage-hero">Homepage Hero Banner Content</div>
</body>
</html>
```

Lägg till Adobe Experience Platform Web SDK-tillägget i taggar:

<!--![Add the Adobe Experience Platform Web SDK extension](assets/library-tags-addExtension.png){zoomable="yes"}-->

Och lägg till de önskade konfigurationerna:
<!--![configuring the Web SDK tag extension migration options](assets/tags-config-migration.png){zoomable="yes"}-->


>[!ENDTABS]



Det är viktigt att komma ihåg att inget nätverksanrop utförs till Adobe Edge-nätverket om du bara inkluderar och konfigurerar Platform Web SDK-biblioteket så som visas ovan.

Lär dig sedan [begära och använda formulärbaserade aktiviteter](render-activities.md) på sidan.

>[!NOTE]
>
>Vi strävar efter att hjälpa dig att lyckas med din migrering av mobilmål från måltillägget till beslutstillägget. Om du stöter på problem med din migrering eller om du känner att det saknas viktig information i den här guiden kan du meddela oss genom att publicera [den här communitydiskussionen](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
