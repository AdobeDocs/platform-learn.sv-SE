---
title: Installera Adobe Experience Platform Mobile SDKs
description: Lär dig hur du implementerar Adobe Experience Platform Mobile SDK i en mobilapp.
hide: true
hidefromtoc: true
source-git-commit: a7d20a6de8eb9bae62494ff5e71f47ed672e4681
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 0%

---

# Installera Adobe Experience Platform Mobile SDKs

Lär dig hur du implementerar Adobe Experience Platform Mobile SDK i en mobilapp.

## Förutsättningar

* Taggbiblioteket med tilläggen som beskrivs i [föregående lektion](configure-tags.md).
* Fil-ID för utvecklingsmiljö från [Instruktioner för mobilinstallation](configure-tags.md#generate-sdk-install-instructions).
* Nedladdad, tom [exempelapp](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App{target="_blank"}).
* Upplev [XCode](https://developer.apple.com/xcode/{target="_blank"}).

## Utbildningsmål

I den här lektionen kommer du att:

* Lägg till de SDK:er som behövs i projektet med hjälp av Swift Package Manager.
* Registrera tilläggen.

>[!NOTE]
>
>I en mobilappsimplementering är termerna &quot;extensions&quot; och &quot;SDKs&quot; nästan utbytbara.

## Swift Package Manager

Istället för att använda CocoaPods och använda en Pod-fil (se Mobile Install Instructions, se [Generera installationsanvisningar för SDK](./configure-tags.md#generate-sdk-install-instructions)) kan du lägga till enskilda paket med Xcodes inbyggda Swift Package Manager.

I Xcode använder du **[!UICONTROL Fil]** > **[!UICONTROL Lägg till paket...]** och installera alla paket som anges i tabellen nedan. Markera länken för paketet i tabellen för att hämta den fullständiga URL:en för det specifika paketet.

| Paket | Beskrivning |
|---|---|
| [AEP Core](https://github.com/adobe/aepsdk-core-ios.git) | The `AEPCore`, `AEPServices`och `AEPIdentity` tillägg utgör grunden för Adobe Experience Platform SDK - alla program som använder SDK måste innehålla dem. Dessa moduler innehåller en gemensam uppsättning funktioner och tjänster som krävs för alla SDK-tillägg.<br/>`AEPCore` innehåller implementering av händelsehubben. Händelsehubben är den mekanism som används för att leverera händelser mellan appen och SDK:n. Händelsehubben används också för att dela data mellan tillägg.<br/>`AEPServices` innehåller flera återanvändbara implementeringar som krävs för plattformsstöd, inklusive nätverk, diskåtkomst och databashantering.<br/>`AEPIdentity` implementerar integreringen med Adobe Experience Platform Identity Services.<br/>`AEPSignal` representerar Signal-tillägget för Adobe Experience Platform SDK som gör att marknadsförare kan skicka en signal till sina appar för att skicka data till externa destinationer eller till öppna URL:er.<br/>`AEPLifecycle` representerar Adobe Experience Platform SDK:s livscykeltillägg som hjälper till att samla in livscykelvärden för program, t.ex. information om programinstallation eller uppgradering, information om programstart och -session, enhetsinformation och eventuella ytterligare kontextdata från programutvecklaren. |
| [AEP Edge](https://github.com/adobe/aepsdk-edge-ios.git) | Med mobiltillägget Adobe Experience Platform Edge Network kan du skicka data till Adobe Edge Network från ett mobilprogram. Med det här tillägget kan du implementera Adobe Experience Cloud-funktioner på ett mer robust sätt, leverera flera Adobe-lösningar via ett nätverksanrop och samtidigt vidarebefordra informationen till Adobe Experience Platform.<br/>Det mobila tillägget Edge Network är ett tillägg till Adobe Experience Platform SDK och kräver `AEPCore` och `AEPServices` tillägg för händelsehantering samt `AEPEdgeIdentity` tillägg för att hämta identiteter, som ECID. |
| [AEP Edge Identity](https://github.com/adobe/aepsdk-edgeidentity-ios.git) | Med mobiltillägget AEP Edge Identity kan du hantera användaridentitetsdata från ett mobilprogram när du använder Adobe Experience Platform SDK och Edge Network-tillägget. |
| [AEP Edge-samtycke](https://github.com/adobe/aepsdk-edgeconsent-ios.git) | Med mobiltillägget AEP Consent Collection kan du samla in medgivandeinställningar från mobilprogrammet när du använder Adobe Experience Platform SDK och Edge Network-tillägget. |
| [AEP-användarprofil](https://github.com/adobe/aepsdk-userprofile-ios.git) | Adobe Experience Platform User Profile Mobile Extension är ett tillägg för hantering av användarprofiler för Adobe Experience Platform SDK. |
| [AEP-platser](https://github.com/adobe/aepsdk-places-ios) | Tillägget Adobe Experience Platform Places är ett tillägg till Adobe Experience Platform Swift SDK. Med tillägget AEPPlaces kan du spåra geopositioneringshändelser enligt definitionen i användargränssnittet för Adobe Platser och i startreglerna för Adobe. |
| [AEP Messaging](https://github.com/adobe/aepsdk-messaging-ios.git) | Tillägget AEP Messaging är ett tillägg till Adobe Experience Platform Swift SDK. Med AEP Messaging-tillägget kan du skicka push-meddelandetokens och skicka vidare klickningsfeedback till Adobe Experience Platform. |
| [AEP-optimering](https://github.com/adobe/aepsdk-optimize-ios) | Tillägget AEP Optimize innehåller API:er som möjliggör personalisering i realtid i Adobe Experience Platform Mobile SDK:er med Adobe Target eller Adobe Journey Optimizer Offer decisioning. Den kräver `AEPCore` och `AEPEdge` tillägg för att skicka personaliseringsfrågehändelser till Experience Edge-nätverket. |
| [AEP Assurance](https://github.com/adobe/aepsdk-assurance-ios.git) | Assurance (alias project Griffon) är en ny, innovativ produkt som hjälper er att inspektera, granska, simulera och validera hur ni samlar in data eller levererar upplevelser i er mobilapp. |


När du har installerat alla paket, din Xcode **[!UICONTROL Paketberoenden]** ska se ut så här:

![Xcode-paketberoenden](assets/xcode-package-dependencies.png)


## Importera tillägg

I Xcode, i källan för **[!UICONTROL AppDelegate]** och **[!UICONTROL MobileSDK]** lägger du till följande importer.

```swift
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

## Uppdatera AppDelegate

I **AppDelegate**,

1. Ange `@AppStorage` värde för `environmentFileId` till det fil-ID för utvecklingsmiljön som du hämtade från taggar i steg 6 i [Generera installationsanvisningar för SDK](configure-tags.md#generate-sdk-install-instructions).

   ```swift
   @AppStorage("environmentFileId") private var environmentFileId = "b5cbd1a1220e/1857ef6cacb5/launch-2594f26b23cd-development"
   ```

1. Lägg till följande kod i `application(_, didFinishLaunchingWithOptions)` funktion.

   ```swift
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
   
       // update version and build
       Logger.configuration.info("Luma - Updating version and build number...")
       SettingsBundleHelper.setVersionAndBuildNumber()
   })
   ```

Koden ovan gör följande:

1. Registrerar nödvändiga tillägg.
1. Konfigurerar MobileCore och andra tillägg så att taggegenskapskonfigurationen används.
1. Aktiverar felsökningsloggning. Mer information och alternativ finns i [Dokumentation för Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/).

>[!IMPORTANT]
>
>Se till att du uppdaterar `MobileCore.configureWith(appId: self.environmentFileId)` med `appId` baserat på `environmentFileId` från den taggmiljö du bygger för (utveckling, staging eller produktion).
>

>[!SUCCESS]
>
>Du har nu installerat de nödvändiga paketen och uppdaterat projektet för att korrekt registrera de Adobe Experience Platform Mobile SDK-tillägg som du kommer att använda för resten av kursen.<br/>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Mobile SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Nästa: **[Ställ in försäkring](assurance.md)**
