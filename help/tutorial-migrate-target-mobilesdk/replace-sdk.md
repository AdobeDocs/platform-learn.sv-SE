---
title: Byt ut SDK - Migrera Adobe Target-implementeringen i din mobilapp till Adobe Journey Optimizer - Beslutstillägg
description: Lär dig hur du ersätter SDK när du migrerar från Adobe Target till Adobe Journey Optimizer - Decisioning Mobile.
exl-id: f1b77cad-792b-4a80-acff-e1a2f29250e1
source-git-commit: b8baa6d48b9a99d2d32fad2221413b7c10937191
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 0%

---

# Byt ut SDK Target mot Optimera SDK

Lär dig hur du ersätter Adobe Target SDK:er med Optimera SDK:er i din mobilimplementering. En grundläggande ersättning består av följande steg:

* Uppdatera beroenden i din Podfile eller `build.gradle`-fil
* Uppdatera importer
* Uppdatera programkod

>[!INFO]
>
>I Adobe Experience Platform Mobile SDK-ekosystemet implementeras tillägg av SDK:er som importeras till dina program och som kan ha olika namn:
>
> * **Mål-SDK** implementerar **Adobe Target-tillägget**
> * **Optimera SDK** implementerar tillägget **Adobe Journey Optimizer - Bestämning**

## Uppdatera beroenden

+++Android-exempel

>[!BEGINTABS]

>[!TAB Optimera SDK]

`build.gradle` beroenden efter migrering

```Java
implementation platform('com.adobe.marketing.mobile:sdk-bom:3.+')
implementation 'com.adobe.marketing.mobile:core'
implementation 'com.adobe.marketing.mobile:edgeidentity'
implementation 'com.adobe.marketing.mobile:edge'
implementation 'com.adobe.marketing.mobile:optimize'
```


>[!TAB SDK som mål]

`build.gradle` beroenden före migrering

```Java
implementation platform('com.adobe.marketing.mobile:sdk-bom:3.+')
implementation 'com.adobe.marketing.mobile:analytics'
implementation 'com.adobe.marketing.mobile:target'
implementation 'com.adobe.marketing.mobile:core'
implementation 'com.adobe.marketing.mobile:identity'
implementation 'com.adobe.marketing.mobile:lifecycle'
implementation 'com.adobe.marketing.mobile:signal'
implementation 'com.adobe.marketing.mobile:userprofile'
```


>[!ENDTABS]

+++

+++ Exempel på iOS

>[!BEGINTABS]


>[!TAB Optimera SDK]

`Podfile` beroenden efter migrering

```Swift
use_frameworks!
target 'YourAppTarget' do
    pod 'AEPCore', '~> 5.0'
    pod 'AEPEdge', '~> 5.0'
    pod 'AEPEdgeIdentity', '~> 5.0'
    pod 'AEPOptimize', '~> 5.0'
end
```

>[!TAB SDK som mål]

`Podfile` beroenden före migrering

```Swift
use_frameworks!
pod 'AEPAnalytics', '~> 5.0'
pod 'AEPTarget', '~> 5.0'
pod 'AEPCore', '~> 5.0'
pod 'AEPIdentity', '~> 5.0'
pod 'AEPSignal', '~>5.0'
pod 'AEPLifecycle', '~>5.0'
pod 'AEPUserProfile', '~> 5.0'
```

>[!ENDTABS]

+++

## Uppdatera importer och kod

+++ Exempel på Android

>[!BEGINTABS]

>[!TAB Optimera SDK]

Java-initieringskod efter migrering

```Java
import com.adobe.marketing.mobile.MobileCore;
import com.adobe.marketing.mobile.Edge;
import com.adobe.marketing.mobile.edge.identity.Identity;
import com.adobe.marketing.mobile.optimize.Optimize;
import com.adobe.marketing.mobile.AdobeCallback;
 
public class MainApp extends Application {
 
  private final String ENVIRONMENT_FILE_ID = "YOUR_APP_ENVIRONMENT_ID";
 
    @Override
    public void onCreate() {
        super.onCreate();
 
        MobileCore.setApplication(this);
        MobileCore.configureWithAppID(ENVIRONMENT_FILE_ID);
 
        MobileCore.registerExtensions(
            Arrays.asList(Edge.EXTENSION, Identity.EXTENSION, Optimize.EXTENSION),
            o -> Log.d("MainApp", "Adobe Journey Optimizer - Decisioning Mobile SDK was initialized.")
        );
    }
}
```

>[!TAB SDK som mål]

Java-initieringskod före migrering

```Java
import com.adobe.marketing.mobile.AdobeCallback;
import com.adobe.marketing.mobile.Analytics;
import com.adobe.marketing.mobile.Extension;
import com.adobe.marketing.mobile.Identity;
import com.adobe.marketing.mobile.Lifecycle;
import com.adobe.marketing.mobile.LoggingMode;
import com.adobe.marketing.mobile.MobileCore;
import com.adobe.marketing.mobile.Signal;
import com.adobe.marketing.mobile.Target;
import com.adobe.marketing.mobile.UserProfile;
import java.util.Arrays;
import java.util.List;
...
import android.app.Application;
...
public class MainApp extends Application {
...
    @Override
    public void onCreate() {
        super.onCreate();
        MobileCore.setApplication(this);
        MobileCore.setLogLevel(LoggingMode.DEBUG);
        ...
        List<Class<? extends Extension>> extensions = Arrays.asList(
            Analytics.EXTENSION,
            Target.EXTENSION,
            Identity.EXTENSION,
            Lifecycle.EXTENSION,
            Signal.EXTENSION,
            UserProfile.EXTENSION
        );
 
 
        MobileCore.registerExtensions(extensions, new AdobeCallback () {
            @Override
            public void call(Object o) {
                MobileCore.configureWithAppID(<Environment File ID>);
            }
        });
    }
}
```

>[!ENDTABS]

+++

+++ iOS

>[!BEGINTABS]

>[!TAB Optimera SDK]

Swift-initieringskod efter migrering

```Swift
import AEPCore
import AEPEdge
import AEPEdgeIdentity
import AEPOptimize
 
@UIApplicationMain
final class AppDelegate: UIResponder, UIApplicationDelegate {
  var window: UIWindow?
 
  func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]? = nil) -> Bool {
 
      // register the extensions
      MobileCore.registerExtensions([Edge.self, AEPEdgeIdentity.Identity.self, Optimize.self]) {
        MobileCore.configureWith(appId: <YOUR_ENVIRONMENT_FILE_ID>) // Replace <YOUR_ENVIRONMENT_FILE_ID> with a String containing your own ID.
      }
 
      return true
  }
}
```

>[!TAB SDK som mål]

Swift-initieringskod före migrering

```Swift
import AEPCore
import AEPAnalytics
import AEPTarget
import AEPIdentity
import AEPLifecycle
import AEPSignal
import AEPServices
import AEPUserProfile
...
@UIApplicationMain
class AppDelegate: UIResponder, UIApplicationDelegate {
    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        MobileCore.setLogLevel(.debug)
        let appState = application.applicationState
        ...
        let extensions = [
            Analytics.self,
            Target.self,
            Identity.self,
            Lifecycle.self,
            Signal.self,
            UserProfile.self
        ]
        MobileCore.registerExtensions(extensions, {
        MobileCore.configureWith(<Environment File ID>)
        if appState != .background {
            MobileCore.lifecycleStart(additionalContextData: ["contextDataKey": "contextDataVal"])
            }
        })
        ...
        return true
    }
}
```

>[!ENDTABS]

+++

## Funktionsjämförelse

Många Target-tilläggsfunktioner har en likvärdig metod med hjälp av det beslutstillägg som beskrivs i tabellen nedan. Mer information om [funktionerna](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/atjs-functions/) finns i Adobe Target Developer Guide.

| Måltillägg | Beslutstillägg | Anteckningar |
| --- | --- | --- | 
| `prefetchContent` | `updatePropositions` |  |
| `retrieveLocationContent` | `getPropositions` | När du använder `getPropositions` API görs inget fjärranrop för att hämta icke-cachelagrade scope i SDK. |
| `displayedLocations` | Erbjudande -> `displayed()` | Dessutom kan erbjudandemetoden `generateDisplayInteractionXdm` användas för att generera XDM för objektvisning. Därefter kan Edge-nätverkets SDK-API för sendEvent användas för att bifoga ytterligare XDM-data, frihandsdata och skicka en Experience Event till fjärrservern. |
| `clickedLocation` | Erbjudande -> `tapped()` | Dessutom kan erbjudandemetoden `generateTapInteractionXdm` användas för att generera XDM för artikelknackning. Därefter kan Edge-nätverkets SDK-API för sendEvent användas för att bifoga ytterligare XDM-data, frihandsdata och skicka en Experience Event till fjärrservern. |
| `clearPrefetchCache` | `clearCachedPropositions` |  |
| `resetExperience` | n/a | Använd `removeIdentity` API från tillägget Identity för Edge Network för SDK för att sluta skicka besöksidentifieraren till Edge-nätverket. Mer information finns i [dokumentationen för API:t removeIdentity](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/api-reference/#removeidentity). <br><br>Obs! Mobile Core `resetIdentities` API tar bort alla lagrade identiteter i SDK, inklusive Experience Cloud ID (ECID), och det bör användas sparsamt! |
| `getSessionId` | n/a | `state:store`-svarsreferensen innehåller sessionsrelaterad information. Edge-nätverkstillägg hjälper till att hantera det genom att koppla tillståndslagringsobjekt som inte har förfallit till efterföljande begäranden. |
| `setSessionId` | n/a | `state:store`-svarsreferensen innehåller sessionsrelaterad information. Edge-nätverkstillägg hjälper till att hantera det genom att koppla tillståndslagringsobjekt som inte har förfallit till efterföljande begäranden. |
| `getThirdPartyId` | n/a | Använd API:t updateIdentities från tillägget Identity för Edge Network för att ange ID-värdet för tredje part. Konfigurera sedan namnutrymmet för det tredje parts-ID:t i datastream. Mer information finns i [Målets mobildokumentation för tredjeparts-ID](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#target-third-party-id). |
| `setThirdPartyId` | n/a | Använd API:t updateIdentities från tillägget Identity för Edge Network för att ange ID-värdet för tredje part. Konfigurera sedan namnutrymmet för det tredje parts-ID:t i datastream. Mer information finns i [Målets mobildokumentation för tredjeparts-ID](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#target-third-party-id). |
| `getTntId` | n/a | Svarshandtaget `locationHint:result` innehåller information om målplatstips. Det antas att Target-kanten kommer att samlokaliseras med Experience Edge. <br> <br>Edge-nätverkstillägget använder platsledtråden för EdgeNetwork för att avgöra vilket Edge-nätverkskluster som begäranden ska skickas till. Använd API:erna `getLocationHint` och `setLocationHint` från Edge Network-tillägget om du vill dela Edge-nätverksplatstips i olika SDK:er (hybridappar). Mer information finns i [API-dokumentationen för `getLocationHint`](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#getlocationhint). |
| `setTntId` | n/a | Svarshandtaget `locationHint:result` innehåller information om målplatstips. Det antas att Target-kanten kommer att samlokaliseras med Experience Edge. <br> <br>Edge-nätverkstillägget använder platsledtråden för EdgeNetwork för att avgöra vilket Edge-nätverkskluster som begäranden ska skickas till. Använd API:erna `getLocationHint` och `setLocationHint` från Edge Network-tillägget om du vill dela Edge-nätverksplatstips i olika SDK:er (hybridappar). Mer information finns i [API-dokumentationen för `getLocationHint`](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#getlocationhint). |


Läs sedan om hur du [begär och återger aktiviteter](retrieve-activities.md) på sidan.

>[!NOTE]
>
>Vi strävar efter att hjälpa dig att lyckas med din migrering av mobilmål från måltillägget till beslutstillägget. Om du stöter på problem med din migrering eller om du känner att det saknas viktig information i den här guiden kan du meddela oss genom att publicera [den här communitydiskussionen](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
