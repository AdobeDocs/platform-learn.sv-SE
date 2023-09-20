---
title: Installera Adobe Experience Platform Mobile SDKs
description: Lär dig hur du implementerar Adobe Experience Platform Mobile SDK i en mobilapp.
hide: true
source-git-commit: a2788110b1c43d24022672bb5ba0f36af66d962b
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 0%

---

# Installera Adobe Experience Platform Mobile SDKs

Lär dig hur du implementerar Adobe Experience Platform Mobile SDK i en mobilapp.

## Förutsättningar

* Ett taggbibliotek med tilläggen som beskrivs i [föregående lektion](configure-tags.md).
* Fil-ID för utvecklingsmiljö från [Instruktioner för mobilinstallation](configure-tags.md#generate-sdk-install-instructions).
* Tomma filer har hämtats [exempelapp](https://git.corp.adobe.com/rmaur/Luma){target="_blank"}.
* Upplev [Xcode](https://developer.apple.com/xcode/){target="_blank"}.

## Utbildningsmål

I den här lektionen kommer du att:

* Lägg till önskade SDK:er i projektet med Swift Package Manager.
* Registrera tilläggen.

>[!NOTE]
>
>I en mobilappsimplementering är termerna &quot;extensions&quot; och &quot;SDKs&quot; nästan utbytbara.

## Swift Package Manager

Istället för att använda CocoaPods och använda en Pod-fil (se Mobile Install Instructions, se [Generera installationsanvisningar för SDK](./configure-tags.md#generate-sdk-install-instructions)) kan du lägga till enskilda paket med Xcodes inbyggda Swift Package Manager. Xcode-projektet har redan alla paketberoenden tillagda. Xcode **[!UICONTROL Paketberoenden]** ska se ut så här:

![Xcode-paketberoenden](assets/xcode-package-dependencies.png){zoomable=&quot;yes&quot;}


I Xcode kan du använda **[!UICONTROL Fil]** > **[!UICONTROL Lägg till paket...]** för att lägga till paket. Tabellen nedan innehåller länkar till de URL:er som du skulle använda för att lägga till paket. Länkarna visar även mer information om varje paket.

| Paket | Beskrivning |
|---|---|
| [AEP Core](https://github.com/adobe/aepsdk-core-ios.git) | The `AEPCore`, `AEPServices`och `AEPIdentity` tillägg utgör grunden för Adobe Experience Platform SDK - alla program som använder SDK måste innehålla dem. Dessa moduler innehåller en gemensam uppsättning funktioner och tjänster som krävs för alla SDK-tillägg.<br/><ul><li>`AEPCore` innehåller implementering av händelsehubben. Händelsehubben är den mekanism som används för att leverera händelser mellan appen och SDK:n. Händelsehubben används också för att dela data mellan tillägg.</li><li>`AEPServices` innehåller flera återanvändbara implementeringar som krävs för plattformsstöd, inklusive nätverk, diskåtkomst och databashantering.</li><li>`AEPIdentity` implementerar integreringen med Adobe Experience Platform Identity Services.</li><li>`AEPSignal` representerar Adobe Experience Platform SDK:s signaltillägg som gör att marknadsförarna kan skicka en signal till sina appar för att skicka data till externa destinationer eller till öppna URL:er.</li><li>`AEPLifecycle` representerar Adobe Experience Platform SDK:s Lifecycle-tillägg som hjälper till att samla in uppgifter om programmets livscykel, t.ex. information om installation eller uppgradering, programstart och session, enhetsinformation och eventuella ytterligare kontextdata från programutvecklaren.</li></ul> |
| [AEP Edge](https://github.com/adobe/aepsdk-edge-ios.git) | Mobiltillägget Adobe Experience Platform Edge Network (`AEPEdge`) kan du skicka data till Adobe Edge Network från ett mobilprogram. Med det här tillägget kan du implementera Adobe Experience Cloud-funktioner på ett mer robust sätt, leverera flera Adobe-lösningar via ett nätverksanrop och samtidigt vidarebefordra informationen till Adobe Experience Platform.<br/>Det mobila tillägget Edge Network är ett tillägg till Adobe Experience Platform SDK och kräver `AEPCore` och `AEPServices` tillägg för händelsehantering samt `AEPEdgeIdentity` tillägg för att hämta identiteter, som ECID. |
| [AEP Edge Identity](https://github.com/adobe/aepsdk-edgeidentity-ios.git) | Mobiltillägget AEP Edge Identity (`AEPEdgeIdentity`) används för att hantera användaridentitetsdata från ett mobilprogram när Adobe Experience Platform SDK och Edge Network-tillägget används. |
| [AEP Edge-samtycke](https://github.com/adobe/aepsdk-edgeconsent-ios.git) | Mobiltillägget AEP Consent Collection (`AEPConsent`) aktiverar insamling av medgivandeinställningar från mobilprogrammet när du använder Adobe Experience Platform SDK och Edge Network-tillägget. |
| [AEP-användarprofil](https://github.com/adobe/aepsdk-userprofile-ios.git) | Tillägget Adobe Experience Platform User Profile Mobile (`AEPUserProfile`) är ett tillägg för att hantera användarprofiler för Adobe Experience Platform SDK. |
| [AEP-platser](https://github.com/adobe/aepsdk-places-ios) | Tillägget AEP Places (`AEPPlaces`) kan du spåra geopositioneringshändelser enligt definitionen i Adobe Platser-gränssnittet och i Adobe Data Collection Tag-reglerna. |
| [AEP Messaging](https://github.com/adobe/aepsdk-messaging-ios.git) | Tillägget AEP Messaging (`AEPMessaging`) kan du skicka push-meddelandetokens och skicka vidare klickningsfeedback till Adobe Experience Platform. |
| [AEP-optimering](https://github.com/adobe/aepsdk-optimize-ios) | Tillägget AEP Optimize (`AEPOptimize`) innehåller API:er för att möjliggöra personalisering i realtid i Adobe Experience Platform Mobile SDK:er med Adobe Target eller Adobe Journey Optimizer Offer decisioning. Den kräver `AEPCore` och `AEPEdge` tillägg för att skicka personaliseringsfrågehändelser till Experience Edge-nätverket. |
| [AEP Assurance](https://github.com/adobe/aepsdk-assurance-ios.git) | Assurance (alias project Griffon) är en ny, innovativ förlängning (`AEPAssurance`) för att hjälpa er att inspektera, bevisa, simulera och validera hur ni samlar in data eller levererar upplevelser i er mobilapp. Det här tillägget aktiverar din app för Assurance. |


## Importera tillägg

I Xcode navigerar du till **[!DNL Luma]** > **[!DNL Luma]** > **[!UICONTROL AppDelegate]** och se till att följande importer ingår i den här källfilen.

```swift
// import AEP MobileSDK libraries
import AEPCore
import AEPServices
import AEPIdentity
import AEPSignal
import AEPLifecycle
import AEPEdge
import AEPEdgeIdentity
import AEPEdgeConsent
import AEPUserProfile
import AEPPlaces
import AEPMessaging
import AEPOptimize
import AEPAssurance
```

Gör på samma sätt för **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]**.

## Uppdatera AppDelegate

Navigera till **[!DNL Luma]** > **[!DNL Luma]** > **AppDelegate** i Xcode Project-navigatorn.

1. Ersätt `@AppStorage` value `YOUR_ENVIRONMENT_ID_GOES_HERE` for `environmentFileId` till det fil-ID för utvecklingsmiljön som du hämtade från taggar i steg 6 i [Generera installationsanvisningar för SDK](configure-tags.md#generate-sdk-install-instructions).

   ```swift
   @AppStorage("environmentFileId") private var environmentFileId = "YOUR_ENVIRONMENT_ID_GOES_HERE"
   ```

1. Lägg till följande kod i `application(_, didFinishLaunchingWithOptions)` funktion.

   ```swift
   // Define extensions
   let extensions = [
       AEPIdentity.Identity.self,
       Lifecycle.self,
       Signal.self,
       Edge.self,
       AEPEdgeIdentity.Identity.self,
       Consent.self,
       UserProfile.self,
       Places.self,
       Messaging.self,
       Optimize.self,
       Assurance.self
   ]
   
   // Register extensions
   MobileCore.registerExtensions(extensions, {
       // Use the environment file id assigned to this application via Adobe Experience Platform Data Collection
       Logger.aepMobileSDK.info("Luma - using mobile config: \(self.environmentFileId)")
       MobileCore.configureWith(appId: self.environmentFileId)
   
       // set this to false or comment it when deploying to TestFlight (default is false),
       // set this to true when testing on your device.
       MobileCore.updateConfigurationWith(configDict: ["messaging.useSandbox": true])
       if appState != .background {
           // only start lifecycle if the application is not in the background
           MobileCore.lifecycleStart(additionalContextData: nil)
       }
   
       // assume unknown, adapt to your needs.
       MobileCore.setPrivacyStatus(.unknown)
   })
   ```

Koden ovan gör följande:

1. Registrerar nödvändiga tillägg.
1. Konfigurerar MobileCore och andra tillägg så att taggegenskapskonfigurationen används.
1. Aktiverar felsökningsloggning. Mer information och alternativ finns i [Dokumentation för Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/).
1. Startar livscykelövervakning. Se [Livscykel](lifecycle-data.md) i självstudiekursen för mer information.
1. Anger okänt standardsamtycke. Se [Godkännande](consent.md) i självstudiekursen för mer information.

>[!IMPORTANT]
>
>Se till att du uppdaterar `MobileCore.configureWith(appId: self.environmentFileId)` med `appId` baserat på `environmentFileId` från den taggmiljö du bygger för (utveckling, staging eller produktion).
>

>[!SUCCESS]
>
>Du har nu installerat de nödvändiga paketen och uppdaterat projektet för att korrekt registrera de Adobe Experience Platform Mobile SDK-tillägg som du kommer att använda för resten av kursen.<br/>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Mobile SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Nästa: **[Ställ in försäkring](assurance.md)**
