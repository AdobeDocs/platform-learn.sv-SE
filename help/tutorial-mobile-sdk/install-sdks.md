---
title: Installera Adobe Experience Platform Mobile SDKs
description: Lär dig implementera Adobe Experience Platform Mobile SDK i en mobilapp.
jira: KT-14627
exl-id: 98d6f59e-b8a3-4c63-ae7c-8aa11e948f59
source-git-commit: 463a5d54e99ddf6587fe19081c07025f7caf648e
workflow-type: tm+mt
source-wordcount: '909'
ht-degree: 0%

---

# Installera Adobe Experience Platform Mobile SDKs

>[!CONTEXTUALHELP]
>id="platform_mobile_sdk_tutorial_install"
>title="Installera Adobe Experience Platform Mobile SDKs"
>abstract="Lär dig implementera Adobe Experience Platform Mobile SDK i en mobilapp."

Lär dig implementera Adobe Experience Platform Mobile SDK i en mobilapp.

## Förhandskrav

* Ett taggbibliotek med tilläggen som beskrivs i [föregående lektion](configure-tags.md) har skapats.
* Fil-ID för utvecklingsmiljö från [Mobile Install Instructions](configure-tags.md#generate-sdk-install-instructions).
* Den tomma [exempelappen](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"} hämtades.
* Upplev [Xcode](https://developer.apple.com/xcode/){target="_blank"}.

## Utbildningsmål

I den här lektionen kommer du att:

* Lägg till önskade SDK:er i projektet med Swift Package Manager.
* Registrera tilläggen.

>[!NOTE]
>
>I en mobilappsimplementering är termerna &quot;extensions&quot; och &quot;SDKs&quot; nästan utbytbara.

## Swift Package Manager

I stället för att använda CocoaPods och en Pod-fil (enligt anvisningarna i [Generera installationsanvisningar för SDK](./configure-tags.md#generate-sdk-install-instructions)), lägger du till enskilda paket med Xcodes inbyggda Swift Package Manager. Xcode-projektet har redan alla paketberoenden tillagda. Xcode **[!UICONTROL Package Dependencies]**-skärmen ska se ut så här:

![Xcode-paketberoenden](assets/xcode-package-dependencies.png){zoomable="yes"}


I Xcode kan du använda **[!UICONTROL File]** > **[!UICONTROL Add Packages...]** för att lägga till paket. Tabellen nedan innehåller länkar till de URL:er som du skulle använda för att lägga till paket. Länkarna visar även mer information om varje paket.

| Paket | Beskrivning |
|---|---|
| [AEP Core](https://github.com/adobe/aepsdk-core-ios) | Tilläggen `AEPCore`, `AEPServices` och `AEPIdentity` utgör grunden för Adobe Experience Platform SDK - alla program som använder SDK måste innehålla dem. Dessa moduler innehåller en gemensam uppsättning funktioner och tjänster som krävs av alla SDK-tillägg.<br/><ul><li>`AEPCore` innehåller implementering av händelsehubben. Händelsehubben är den mekanism som används för att leverera händelser mellan appen och SDK. Händelsehubben används också för att dela data mellan tillägg.</li><li>`AEPServices` innehåller flera återanvändbara implementeringar som krävs för plattformsstöd, inklusive nätverk, diskåtkomst och databashantering.</li><li>`AEPIdentity` implementerar integreringen med Adobe Experience Platform Identity Services.</li><li>`AEPSignal` representerar signeringstillägget för Adobe Experience Platform SDK:er som gör att marknadsförarna kan skicka en signal till sina appar för att skicka data till externa mål eller öppna URL:er.</li><li>`AEPLifecycle` representerar Adobe Experience Platform SDKs Lifecycle-tillägget som hjälper till att samla in livscykelvärden för program, som installations- eller uppgraderingsinformation för program, information om programstart och session, enhetsinformation och eventuella ytterligare kontextdata från programutvecklaren.</li></ul> |
| [AEP Edge](https://github.com/adobe/aepsdk-edge-ios) | Med mobiltillägget Adobe Experience Platform Edge Network (`AEPEdge`) kan du skicka data till Adobe Edge Network från ett mobilprogram. Med det här tillägget kan du implementera Adobe Experience Cloud-funktioner på ett mer robust sätt, leverera flera Adobe-lösningar via ett nätverksanrop och samtidigt vidarebefordra informationen till Adobe Experience Platform.<br/>Mobiltillägget Edge Network är ett tillägg för Adobe Experience Platform SDK och kräver `AEPCore` och `AEPServices` för händelsehantering samt `AEPEdgeIdentity`-tillägget för hämtning av identiteter, som ECID. |
| [AEP Edge Identity](https://github.com/adobe/aepsdk-edgeidentity-ios) | Med mobiltillägget AEP Edge Identity (`AEPEdgeIdentity`) kan du hantera användaridentitetsdata från ett mobilprogram när du använder Adobe Experience Platform SDK och Edge Network. |
| [AEP Edge-samtycke](https://github.com/adobe/aepsdk-edgeconsent-ios) | Mobiltillägget AEP Consent Collection (`AEPConsent`) aktiverar insamling av medgivandeinställningar från mobilprogrammet när du använder Adobe Experience Platform SDK och tillägget Edge Network. |
| [AEP-användarprofil](https://github.com/adobe/aepsdk-userprofile-ios) | Tillägget Adobe Experience Platform User Profile Mobile (`AEPUserProfile`) är ett tillägg för att hantera användarprofiler för Adobe Experience Platform SDK. |
| [AEP-platser](https://github.com/adobe/aepsdk-places-ios) | Med tillägget AEP-platser (`AEPPlaces`) kan du spåra geopositioneringshändelser enligt definitionen i gränssnittet Adobe Platser och i taggreglerna för Adobe-datainsamling. |
| [AEP-meddelanden](https://github.com/adobe/aepsdk-messaging-ios) | Med AEP Messaging-tillägget (`AEPMessaging`) kan du skicka push-meddelandetokens och push-meddelanden via-feedback till Adobe Experience Platform. |
| [AEP-optimering](https://github.com/adobe/aepsdk-optimize-ios) | Tillägget AEP Optimize (`AEPOptimize`) innehåller API:er för att aktivera arbetsflöden för personalisering i realtid i Adobe Experience Platform Mobile SDK:er med Adobe Target eller Adobe Journey Optimizer Offer decisioning. Det krävs `AEPCore` och `AEPEdge` tillägg för att skicka personaliseringsfrågehändelser till Experience Edge-nätverket. |
| [AEP Assurance](https://github.com/adobe/aepsdk-assurance-ios) | Assurance (även kallat Griffon-projektet) är ett nytt, innovativt tillägg (`AEPAssurance`) som hjälper dig att inspektera, granska, simulera och validera hur du samlar in data eller levererar upplevelser i din mobilapp. Med det här tillägget kan du använda din app för Assurance. |


## Importera tillägg

I Xcode går du till **[!DNL Luma]** > **[!DNL Luma]** > **[!UICONTROL AppDelegate]** och ser till att följande importer ingår i den här källfilen.

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

Gör samma sak för **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]**.

## Uppdatera AppDelegate

Navigera till **[!DNL Luma]** > **[!DNL Luma]** > **AppDelegate** i Xcode Project-navigatorn.

1. Ersätt `@AppStorage`-värdet `YOUR_ENVIRONMENT_ID_GOES_HERE` för `environmentFileId` med det fil-ID för utvecklingsmiljö som du hämtade från taggar i [Generera installationsanvisningar för SDK](configure-tags.md#generate-sdk-install-instructions).

   ```swift
   @AppStorage("environmentFileId") private var environmentFileId = "YOUR_ENVIRONMENT_ID_GOES_HERE"
   ```

1. Lägg till följande kod i funktionen `application(_, didFinishLaunchingWithOptions)`.

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
1. Aktiverar felsökningsloggning. Mer information och alternativ finns i [Adobe Experience Platform Mobile SDK-dokumentationen](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/).
1. Startar livscykelövervakning. Mer information finns i [steget Livscykel](lifecycle-data.md) i självstudiekursen.
1. Anger okänt standardsamtycke. Mer information finns i steget [Medgivande](consent.md) i självstudiekursen.

>[!IMPORTANT]
>
>Se till att du uppdaterar `MobileCore.configureWith(appId: self.environmentFileId)` med `appId` baserat på `environmentFileId` från den taggmiljö som du skapar för (utveckling, mellanlagring eller produktion).
>

>[!SUCCESS]
>
>Du har nu installerat de nödvändiga paketen och uppdaterat projektet för att registrera de Adobe Experience Platform Mobile SDK-tillägg som du kommer att använda för resten av kursen.
>
>Tack för att du har lagt ned din tid på att lära dig om Adobe Experience Platform Mobile SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela dem i det här [Experience League-diskussionsinlägget](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Nästa: **[Konfigurera Assurance](assurance.md)**
