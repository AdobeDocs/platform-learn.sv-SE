---
title: Ersätta biblioteket | Migrera mål från at.js 2.x till Web SDK
description: Lär dig hur du migrerar en Adobe Target-implementering från at.js 2.x till Adobe Experience Platform Web SDK. Ämnen som omfattar biblioteksöversikt, implementeringsskillnader och andra viktiga hänvisningar.
source-git-commit: dad7a1b01c4313d6409ce07d01a6520ed83f5e89
workflow-type: tm+mt
source-wordcount: '1642'
ht-degree: 0%

---

# Ersätt at.js-biblioteket med Platform Web SDK

Lär dig hur du ersätter din Adobe Target-implementering på sidan för att migrera från at.js till Platform Web SDK. En grundläggande ersättning består av följande steg:

* Granska inställningarna för måladministration och notera ditt IMS-organisations-ID
* Ersätt at.js-biblioteket med Platform Web SDK
* Uppdatera det föregående fragmentet för synkrona biblioteksimplementeringar
* Konfigurera Platform Web SDK på sidan

>[!NOTE]
>
>Exemplen är till för illustrativa ändamål och den faktiska Target-implementeringen kan variera. Om den befintliga målimplementeringen använder tagghanteraren för Adobe Data Collection kan du även referera till [Implementering av SDK-mål för plattform](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html) för ytterligare information.


## Granska Administrationsinställningar för mål

Det första steget för att migrera Target till Platform Web SDK är att granska dina inställningar i Target-gränssnittets **[!UICONTROL Administration]** -avsnitt.

### [!UICONTROL Implementering]

#### [!UICONTROL Kontoinformation]

* **[!UICONTROL IMS-organisations-ID]** - Observera det här värdet eftersom det krävs för att konfigurera Platform Web SDK.
* **[!UICONTROL Beslut på enheten]** - Den här funktionen stöds inte av Platform Web SDK. Den här inställningen kan inaktiveras när du har migrerat och om du inte längre använder at.js på någon av dina webbplatser eller har några användningsfall på serversidan för On-Device Decision.

#### [!UICONTROL Implementeringsmetoder]

Alla redigerbara inställningar i **[!UICONTROL Implementeringsmetoder]** gäller endast för at.js. De här inställningarna används för att generera ett anpassat at at.js-bibliotek för implementeringen. Granska de här inställningarna för att kontrollera om du har någon anpassad kod eller ställer in cookies från första och tredje part för användning över domäner.

The **[!UICONTROL Profilens livstid]** inställningen kan endast ändras av Adobe kundtjänst. Livslängden för målbesökarprofilen påverkas inte av implementeringsmetoden. Både at.js och Platform Web SDK använder samma livstid för besökarprofiler.

#### [!UICONTROL Integritet]

* **[!UICONTROL Förhindra IP-adresser för besökare]** - Den här inställningen påverkar geolokalisering. Både at.js och Platform Web SDK använder samma inställningar för bakomliggande IP-fakturering vid geolokalisering.

### [!UICONTROL Miljöer]

Platform Web SDK använder en datastream-konfiguration som gör att du uttryckligen kan definiera en [!UICONTROL Miljö-ID] för separata datastreams för utveckling, staging och produktion. Det viktigaste användningsexemplet för den här konfigurationen är implementeringar av mobilappar där det inte finns några URL:er för att enkelt kunna skilja på olika miljöer. Inställningen är valfri men kan användas för att säkerställa att alla begäranden är korrekt kopplade till den angivna miljön. Detta skiljer sig från en at.js-implementering där du måste tilldela Target-miljöer baserat på domäner och värdgruppsregler.

>[!NOTE]
>
>Om inget miljö-ID anges i datastream-konfigurationen använder Target domänen-till-miljö-mappningen enligt specifikationen i **Värdar** -avsnitt.

Mer information finns i [datastream-konfiguration](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html#target) guide och mål [Värdar](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) dokumentation.

## Distribuera Platform Web SDK

Målfunktionerna finns i både at.js och Platform Web SDK. Om båda biblioteken används samtidigt kan det uppstå problem med återgivning och spårning. Det första steget är att ta bort at.js och ersätta den med Platform Web SDK (alloy.js) för att kunna migrera till Platform Web SDK.

Anta en enkel målinsimplementering med at.js:

* Ett datalager nära sidans överkant ger information om Target och andra program
* Ett eller flera hjälpbibliotek från tredje part vars funktioner kan användas i Target-aktiviteter (till exempel jQuery)
* Ett fördolt kodfragment som minskar flimret
* Målet-biblioteket at.js läses in asynkront med standardinställningar för att automatiskt begära och återge aktiviteter:

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

Om du vill uppgradera Target till att använda Platform Web SDK måste du först ta bort at.js:

```HTML
<!--Target at.js library loaded asynchonously-->
<script src="/libraries/at.js" async></script>
```

Ersätt med den version av Platform Web SDK (alloy.js) som stöds för närvarande:

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

Den fördefinierade fristående versionen kräver en &quot;baskod&quot; som läggs till direkt på sidan och som skapar en global funktion med namnet alloy. Använd den här funktionen för att interagera med SDK:n. Om du vill ge den globala funktionen ett annat namn ändrar du `alloy` namn.

>[!TIP]
>
> När du använder taggfunktionen (tidigare Launch) för att implementera Web SDK läggs biblioteket alloy.js till i taggbiblioteket genom att lägga till tillägget Adobe Experience Platform Web SDK.


Se [Installera Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html) dokumentation för mer information och distributionsalternativ.


## Uppdatera metod för att dölja innehåll

Implementeringen av Platform Web SDK kan kräva ett predhide-fragment beroende på om biblioteket läses in asynkront eller synkront.

### Asynkron implementering

Precis som med at.js, kan det hända att sidan slutför återgivningen innan Target har utfört en innehållsväxling om Platform Web SDK-biblioteket läses in asynkront. Det här beteendet kan leda till det som kallas&quot;flimmer&quot;, där standardinnehållet visas kort innan det ersätts av det anpassade innehåll som anges av Target. Om du vill undvika den här flimret rekommenderar Adobe att du lägger till ett särskilt preddolt fragment omedelbart före den asynkrona plattformsskriptreferensen för Web SDK.

Om implementeringen är asynkron, som i exemplet ovan, ska du ersätta fragmentet at.js med versionen nedan som är kompatibel med SDK för plattformen:

```HTML
<!--Prehiding snippet for Target with asynchronous Web SDK deployment-->
<script>
  !function(e,a,n,t){var i=e.head;if(i){
  if (a) return;
  var o=e.createElement("style");
  o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
  (document, document.location.href.indexOf("mboxEdit") !== -1, ".body { opacity: 0 !important }", 3000);
</script>
```

Med det föregående dolda fragmentet skapas en formattagg i sidhuvudet med den CSS-definition du väljer. Den här stiltaggen tas bort när ett svar från Target tas emot eller när tidsgränsen nås.

Beteendet för att dölja är styrt av två konfigurationer i slutet av fragmentet.

* `body { opacity: 0 !important }` Anger den CSS-definition som ska användas för döljningen tills Target läses in. Som standard är hela sidan dold. Du kan uppdatera den här definitionen till de väljare som du vill dölja tillsammans med hur du vill dölja dem. Du kan inkludera flera definitioner eftersom det här värdet är det som infogas i den föregående formattaggen. Om du har ett enkelt identifierbart behållarelement som omsluter innehållet under navigeringen kan du använda den här inställningen för att begränsa det dolda innehållet till behållarelementet.

* `3000` anger timeout i millisekunder för predhide. Om inget svar från Target tas emot före timeout, tas den föregående dolda formattaggen bort. Det bör vara sällsynt att denna tidsgräns uppnås.

>[!NOTE]
>
>Var noga med att använda rätt fragment för Platform Web SDK eftersom den använder ett annat format-ID för `alloy-prehiding`. Om fragmentet för at.js före döljning används kanske det inte fungerar som det ska.

### Synkron implementering

Adobe rekommenderar att du implementerar Platform Web SDK asynkront för bästa totala sidprestanda. Om biblioteket däremot läses in synkront behövs inte det föregående dolda fragmentet. I stället anges det fördolda formatet i konfigurationen för Platform Web SDK.

Föregående stil för synkrona implementeringar kan konfigureras med [`prehidingStyle`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#prehidingStyle) alternativ. Konfiguration av Platform Web SDK beskrivs i nästa avsnitt.

>[!TIP]
>
> När du använder taggfunktionen (tidigare Launch) för att implementera Web SDK kan du redigera det dolda formatet i tilläggskonfigurationen för Adobe Experience Platform Web SDK.

Om du vill veta mer om hur Platform Web SDK kan hantera flimmer kan du läsa hjälpavsnittet:  [hantera flimmer för personaliserade upplevelser](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/manage-flicker.html)

## Konfigurera Platform Web SDK

Platform Web SDK måste konfigureras för varje sidinläsning. The `configure` -kommandot måste alltid vara det första SDK-kommandot som anropas. I följande exempel antas att hela webbplatsen uppgraderas till Platform Web SDK i en enda distribution:

```JavaScript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

Om du planerar att migrera från at.js till Platform Web SDK sida för sida krävs följande konfigurationsalternativ:

```JavaScript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg",
  "targetMigrationEnabled":true,
  "idMigrationEnabled":true
});
```

De alternativ för konfiguration som är relaterade till Target beskrivs nedan:

| Alternativ | Beskrivning | Exempelvärde |
| --- | --- | --- |
| `edgeConfigId` | DataStream ID | `ebebf826-a01f-4458-8cec-ef61de241c93` |
| `orgId` | Adobe Experience Cloud organisations-ID | `ADB3LETTERSANDNUMBERS@AdobeOrg` |
| `targetMigrationEnabled` | Använd det här alternativet om du vill att Web SDK ska kunna läsa och skriva de äldre mbox- och mboxEdgeCluster-cookies som används av at.js. Detta hjälper dig att behålla besökarprofilen när du går från en sida där Web SDK används till en sida där at.js-biblioteket används och tvärtom. | `true` |
| `idMigrationEnabled` | Om true läser SDK in gamla AMCV-cookies. Med det här alternativet kan du gå över till att använda Platform Web SDK medan vissa delar av webbplatsen fortfarande använder Visitor.js. | `true` |
| `thirdPartyCookiesEnabled` | Aktiverar inställningen av cookies från tredje part från Adobe. SDK:n kan behålla besökar-ID:t i ett tredjepartssammanhang för att samma besökar-ID ska kunna användas på olika platser. Använd det här alternativet om du har flera platser, Men ibland är det här alternativet inte önskvärt av sekretesskäl. | `true` |
| `prehidingStyle` | Används för att skapa en CSS-formatdefinition som döljer innehållsområden på webbsidan när anpassat innehåll läses in från servern. Detta används endast med synkrona distributioner av SDK. | `body { opacity: 0 !important }` |

>[!NOTE]
>
>`thirdPartyCookiesEnabled` kan anges till `true` för att upprätthålla en konsekvent målbesökarprofil över flera domäner. Det här alternativet bör anges till `false` eller utelämnas såvida inte beständighet krävs för besökarprofilen i flera domäner.

>[!TIP]
>
> När du använder taggfunktionen (tidigare Launch) för att implementera Web SDK kan dessa konfigurationer hanteras i tilläggskonfigurationen för Adobe Experience Platform Web SDK.

En fullständig lista med alternativ finns i [konfigurera Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html) guide.

## Implementeringsexempel

När Platform Web SDK är rätt på plats ser exempelsidan ut så här.

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

>[!TIP]
>
> När du använder taggfunktionen (tidigare Launch) för att implementera Web SDK ersätter taggarna embed-koden grundkoden för Platform Web SDK, Platform Web SDK inläst asynkront och Configure Platform Web SDK ovan.

Det är viktigt att komma ihåg att inget nätverksanrop utförs till Adobe Edge-nätverket om du bara inkluderar och konfigurerar Platform Web SDK-biblioteket så som visas ovan.

Lär dig sedan hur du [begära och tillämpa VEC-baserad verksamhet](render-vec-activities.md) till sidan.

>[!NOTE]
>
>Vi vill hjälpa dig att lyckas med målmigreringen från at.js till Web SDK. Om du stöter på problem med din migrering eller känner att det saknas viktig information i den här guiden ber vi dig att meddela oss genom att publicera i [den här communitydiskussionen](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).