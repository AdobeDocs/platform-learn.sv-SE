---
title: Installera Adobe Experience Platform Mobile SDKs
description: Lär dig implementera Adobe Experience Platform Mobile SDK i en mobilapp.
jira: KT-14627
exl-id: 98d6f59e-b8a3-4c63-ae7c-8aa11e948f59
source-git-commit: 008d3ee066861ea9101fe9fe99ccd0a088b63f23
workflow-type: tm+mt
source-wordcount: '1733'
ht-degree: 0%

---

# Installera Adobe Experience Platform Mobile SDKs {#tutorial_install_mobile_sdks}

>[!CONTEXTUALHELP]
>
>id="platform_mobile_sdk_tutorial_install"
>title="Installera Adobe Experience Platform Mobile SDKs"
>abstract="Lär dig implementera Adobe Experience Platform Mobile SDK i en mobilapp."

Lär dig implementera Adobe Experience Platform Mobile SDK i en mobilapp.

## Förhandskrav

* Ett taggbibliotek med tilläggen som beskrivs i [föregående lektion](configure-tags.md) har skapats.
* Fil-ID för utvecklingsmiljö från [Mobile Install Instructions](configure-tags.md#generate-sdk-install-instructions).
* [exempelappen för iOS](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) eller [exempelappen för Android](https://github.com/adobe/Luma-Android) hämtades.
* Upplev [Xcode](https://developer.apple.com/xcode/) (iOS) eller [Android Studio](https://developer.android.com/studio/intro?utm_source=android-studio) (Android)

## Utbildningsmål

I den här lektionen kommer du att:

* Lägg till de SDK:er som behövs i ditt projekt.
* Registrera tilläggen.

>[!NOTE]
>
>I en mobilappsimplementering är villkoren *extensions* och *SDK* nästan utbytbara.

>[!BEGINTABS]

>[!TAB iOS]

## Swift Package Manager

I stället för att använda CocoaPods och en Pod-fil (enligt anvisningarna i [Generera installationsanvisningar för SDK](./configure-tags.md#generate-sdk-install-instructions)), lägger du till enskilda paket med Xcodes inbyggda Swift Package Manager. Xcode-projektet har redan alla paketberoenden tillagda. Xcode **[!UICONTROL Package Dependencies]**-skärmen ska se ut så här:

![Xcode-paketberoenden](assets/xcode-package-dependencies.png){zoomable="yes"}


I Xcode kan du använda **[!UICONTROL File]** > **[!UICONTROL Add Packages...]** för att lägga till paket. Tabellen nedan innehåller länkar till de URL:er som du skulle använda för att lägga till paket. Länkarna visar även mer information om varje paket.

| Paket | Beskrivning |
|---|---|
| [AEP Core](https://github.com/adobe/aepsdk-core-ios) | Tilläggen `AEPCore`, `AEPServices` och `AEPIdentity` utgör grunden för Adobe Experience Platform SDK - alla program som använder SDK måste innehålla dem. Dessa moduler innehåller en gemensam uppsättning funktioner och tjänster som alla SDK-tillägg kräver.<br/><ul><li>`AEPCore` innehåller implementering av händelsehubben. Händelsehubben är den mekanism som används för att leverera händelser mellan appen och SDK. Händelsehubben används också för att dela data mellan tillägg.</li><li>`AEPServices` innehåller flera återanvändbara implementeringar som krävs för plattformsstöd, inklusive nätverk, diskåtkomst och databashantering.</li><li>`AEPIdentity` implementerar integreringen med Adobe Experience Platform Identity Services.</li><li>`AEPSignal` representerar signeringstillägget för Adobe Experience Platform SDK:er som gör att marknadsförarna kan skicka en signal till sina appar för att skicka data till externa mål eller öppna URL:er.</li><li>`AEPLifecycle` representerar Adobe Experience Platform SDKs Lifecycle-tillägget som hjälper till att samla in livscykelvärden för program, som installations- eller uppgraderingsinformation för program, information om programstart och session, enhetsinformation och eventuella ytterligare kontextdata från programutvecklaren.</li></ul> |
| [AEP Edge](https://github.com/adobe/aepsdk-edge-ios) | Med mobiltillägget Adobe Experience Platform Edge Network (`AEPEdge`) kan du skicka data till Adobe Edge Network från ett mobilprogram. Med det här tillägget kan du implementera Adobe Experience Cloud-funktioner på ett mer robust sätt, leverera flera Adobe-lösningar via ett enda nätverksanrop och samtidigt vidarebefordra informationen till Adobe Experience Platform.<br/>Mobiltillägget för Edge Network är ett tillägg för Adobe Experience Platform SDK. Tillägget kräver tilläggen `AEPCore` och `AEPServices` för händelsehantering samt tillägget `AEPEdgeIdentity` för att hämta identiteter, som ECID. |
| [AEP Edge Identity](https://github.com/adobe/aepsdk-edgeidentity-ios) | Med mobiltillägget Adobe Experience Platform Edge Identity (`AEPEdgeIdentity`) kan du hantera användaridentitetsdata från ett mobilprogram när du använder Adobe Experience Platform SDK och Edge Network. |
| [AEP Edge Consent](https://github.com/adobe/aepsdk-edgeconsent-ios) | Med mobiltillägget Adobe Experience Platform Consent Collection (`AEPConsent`) aktiveras insamling av medgivandeinställningar från mobilprogrammet när Adobe Experience Platform SDK och Edge Network-tillägget används. |
| [AEP-användarprofil](https://github.com/adobe/aepsdk-userprofile-ios) | Tillägget Adobe Experience Platform User Profile Mobile (`AEPUserProfile`) är ett tillägg för att hantera användarprofiler för Adobe Experience Platform SDK. |
| [AEP Platser](https://github.com/adobe/aepsdk-places-ios) | Med tillägget Adobe Experience Platform Places (`AEPPlaces`) kan du spåra geopositioneringshändelser enligt definitionen i gränssnittet för Adobe Platser och i taggreglerna för Adobe Data Collection. |
| [AEP Messaging](https://github.com/adobe/aepsdk-messaging-ios) | Med Adobe Experience Platform Messaging-tillägget (`AEPMessaging`) kan du skicka push-meddelandetokens och push-meddelanden via klickning till Adobe Experience Platform. |
| [AEP Optimize](https://github.com/adobe/aepsdk-optimize-ios) | Tillägget Adobe Experience Platform Optimize (`AEPOptimize`) innehåller API:er för att aktivera arbetsflöden för personalisering i realtid i Adobe Experience Platform Mobile SDK:er med Adobe Target eller Adobe Journey Optimizer Offer Decisioning. Det krävs `AEPCore` och `AEPEdge` tillägg för att skicka personaliseringsfrågehändelser till Experience Edge Network. |
| [AEP Assurance](https://github.com/adobe/aepsdk-assurance-ios) | Adobe Experience Platform Assurance är en produkt från Adobe Experience Cloud som hjälper er att inspektera, bevisa, simulera och validera hur ni samlar in data eller levererar upplevelser i er mobilapp. |


## Importera tillägg

Öppna projektet i Xcode i mappen **[!UICONTROL Start]** i exempelprogrammet.

I Xcode går du till **[!DNL Luma]** > **[!DNL Luma]** > **[!UICONTROL AppDelegate]** och ser till att följande importer är en del av den här källfilen.

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

1. Ersätt `@AppStorage`-värdet `YOUR_ENVIRONMENT_ID_GOES_HERE` för `environmentFileId` med det miljöfil-ID som du hämtade från taggar i [Generera installationsanvisningar för SDK](configure-tags.md#generate-sdk-install-instructions).

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

Se till att du uppdaterar `MobileCore.configureWith(appId: self.environmentFileId)` med `appId` baserat på `environmentFileId` från den taggmiljö som du skapar för (utveckling, mellanlagring eller produktion).

>[!TAB Android]

## Gråta

Du använder beroendena från [Generera installationsanvisningar för SDK](./configure-tags.md#generate-sdk-install-instructions) för att lägga till enskilda paket med hjälp av Gradle-integreringen med Android Studio. Android Studio-projektet har redan alla paketberoenden tillagda.

1. Välj ![FolderOutline](/help/assets/icons/FolderOutline.svg) som verktyg.
1. Välj vyn **[!UICONTROL Android]**.
1. Välj **[!UICONTROL Gradle scripts]** > **[!UICONTROL build.gradle.kts (Module :app)]** i den vänstra rutan. I den högra rutan rullar du sedan tills du ser `dependencies`.

   ![Android Gradle Dependencies](assets/androidstudio-package-dependencies.png){zoomable="yes"}

I Android Studio kan du använda **[!UICONTROL File]** > **[!UICONTROL Project Structure...]** för att lägga till modulberoenden. Välj **[!UICONTROL Dependencies]** och använd sedan **[!UICONTROL Modules]** ![Lägg till](/help/assets/icons/Add.svg) för att lägga till moduler. Tabellen nedan innehåller länkar till de URL:er som du skulle använda för att lägga till beroendemoduler. Länkarna visar även mer information om varje modul.

| Package<br/>com.adobe.<br/>marketing.mobile: | Beskrivning |
|---|---|
| [core](https://github.com/adobe/aepsdk-core-android) | Tilläggen `MobileCore` och `Identity` utgör grunden för Adobe Experience Platform SDK. Alla program som använder SDK måste inkludera dem. Dessa moduler innehåller en gemensam uppsättning funktioner och tjänster som alla SDK-tillägg kräver.<ul><li>`MobileCore` innehåller implementeringen av händelsehubben. Händelsehubben är den mekanism som används för att leverera händelser mellan appen och SDK. Händelsehubben används också för att dela data mellan tillägg och tillhandahåller flera återanvändbara implementeringar som behövs för plattformsstöd, inklusive nätverk, diskåtkomst och databashantering.</li><li>`Identity` implementerar integreringen med Adobe Experience Platform Identity Services.</li><li>`Signal` representerar Adobe Experience Platform SDK Signal-tillägget som gör att marknadsförare kan skicka en signal till sina appar för att skicka data till externa destinationer eller till öppna URL:er.</li><li>`Lifecycle` representerar Adobe Experience Platform SDK Lifecycle-tillägget som hjälper till att samla in livscykelvärden för program, som installations- eller uppgraderingsinformation för program, information om programstart och session, enhetsinformation och eventuella ytterligare kontextdata från programutvecklaren.</li></ul> |
| [kant](https://github.com/adobe/aepsdk-edge-android) | Med mobiltillägget Adobe Experience Platform Edge Network (`AEPEdge`) kan du skicka data till Adobe Edge Network från ett mobilprogram. Med det här tillägget kan du implementera Adobe Experience Cloud-funktioner på ett mer robust sätt, leverera flera Adobe-lösningar via ett enda nätverksanrop och samtidigt vidarebefordra informationen till Adobe Experience Platform.<br/>Mobiltillägget för Edge Network är ett tillägg för Adobe Experience Platform SDK. Tillägget kräver tilläggen `Mobile Core` och `Services` för händelsehantering. Tillägget `Identity for Edge Network` för att hämta identiteter, t.ex. ECID. |
| [edgeidentity](https://github.com/adobe/aepsdk-edgeidentity-android) | Med mobiltillägget Adobe Experience Platform Edge Identity kan man hantera användaridentitetsdata från mobilappar med Adobe Experience Platform SDK och Edge Network. |
| [edgeconsent](https://github.com/adobe/aepsdk-edgeconsent-android) | Med mobiltillägget Adobe Experience Platform Consent Collection kan du samla in medgivandeinställningar från mobilprogrammet när du använder Adobe Experience Platform SDK och Edge Network-tillägget. |
| [userprofile](https://github.com/adobe/aepsdk-userprofile-android) | Tillägget Adobe Experience Platform User Profile Mobile är ett tillägg för hantering av användarprofiler för Adobe Experience Platform SDK. |
| [platser](https://github.com/adobe/aepsdk-places-android) | Adobe Platser Service är en geolokaliseringstjänst som gör att mobilappar med platsmedvetenhet kan användas. Och för att förstå lokaliseringskontexten genom att använda avancerade och lättanvända SDK-gränssnitt som åtföljs av en flexibel databas med intressepunkter (POI). Mer information finns i dokumentationen för platstjänster.<br/>Den här tjänsten är Platser-mobiltillägget för Android 2.x Adobe Experience Platform SDK och kräver Core-tillägget för händelsehantering. |
| [meddelanden](https://github.com/adobe/aepsdk-messaging-android) | Tillägget Adobe Experience Platform Messaging hanterar push-meddelanden, meddelanden i appen och kodbaserade upplevelser för era mobilappar. Det här tillägget hjälper dig även att samla in push-tokens för användare och hantera interaktionsmätningar med Adobe Experience Platform tjänster. |
| [optimera](https://github.com/adobe/aepsdk-optimize-android) | Tillägget Adobe Experience Platform Optimize innehåller API:er som möjliggör personalisering i realtid i Adobe Experience Platform SDK:er med Adobe Target eller Adobe Journey Optimizer Offer Decisioning. Det är beroende av Mobile Core och kräver att Edge Extension skickar personaliseringshändelser till Experience Edge Network. |
| [säkring](https://github.com/adobe/aepsdk-assurance-android) | Assurance (även kallat Griffon-projektet) är ett mobiltillägg för Adobe Experience Platform som gör det möjligt att integrera med Adobe Experience Platform Assurance. Tillägget hjälper er att inspektera, bevisa, simulera och validera hur ni samlar in data eller levererar upplevelser i er mobilapp. Det här tillägget kräver MobileCore. |

## Importera tillägg

I Android Studio går du till **[!UICONTROL app]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL LumaApplication]** och ser till att följande importer är en del av källfilen.

```kotlin
import com.adobe.marketing.mobile.Assurance
import com.adobe.marketing.mobile.Edge
import com.adobe.marketing.mobile.Lifecycle
import com.adobe.marketing.mobile.LoggingMode
import com.adobe.marketing.mobile.Messaging
import com.adobe.marketing.mobile.MobileCore
import com.adobe.marketing.mobile.MobilePrivacyStatus
import com.adobe.marketing.mobile.Places
import com.adobe.marketing.mobile.Signal
import com.adobe.marketing.mobile.UserProfile
import com.adobe.marketing.mobile.edge.consent.Consent
import com.adobe.marketing.mobile.edge.identity.Identity
import com.adobe.marketing.mobile.optimize.Optimize
```

Gör samma sak för **[!UICONTROL app]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL models]** > **[!UICONTROL MobileSDK]**.


## Uppdatera LumaApplication

I vyn **[!UICONTROL Android]** går du till **[!UICONTROL app]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL LumaApplication]** i Android Studio.

1. Ersätt `"YOUR_ENVIRONMENT_FILE_ID"` i `private var environmentFileId = "YOUR_ENVIRONMENT_ID_GOES_HERE"` med det ID-värde för miljöfil som du hämtade från taggar i [Generera installationsanvisningar för SDK](configure-tags.md#generate-sdk-install-instructions).

   ```kotlin
   private var environmentFileId = "YOUR_ENVIRONMENT_ID_GOES_HERE"
   ```

1. Lägg till följande kod i funktionen `override fun onCreate()` i `class LumaApplication : Application()`.

   ```kotlin
   // Define extensions
   val extensions = listOf(
      Identity.EXTENSION,
      Lifecycle.EXTENSION,
      Signal.EXTENSION,
      Edge.EXTENSION,
      Consent.EXTENSION,
      UserProfile.EXTENSION,
      Places.EXTENSION,
      Messaging.EXTENSION,
      Optimize.EXTENSION,
      Assurance.EXTENSION
   )
   
   // Register extensions
   MobileCore.registerExtensions(extensions) {
   // Use the environment file id assigned to this application via Adobe Experience Platform Data Collection
     Log.i("Luma", "Using mobile config: $environmentFileId")
     MobileCore.configureWithAppID(environmentFileId)
   
     // set this to true when testing on your device, default is false.
     //MobileCore.updateConfiguration(mapOf("messaging.useSandbox" to true))
   
     // assume unknown, adapt to your needs.
     MobileCore.setPrivacyStatus(MobilePrivacyStatus.UNKNOWN)
   }
   ```

   Koden ovan gör följande:

   1. Registrerar nödvändiga tillägg.
   1. Konfigurerar MobileCore och andra tillägg så att taggegenskapskonfigurationen används.
   1. Aktiverar felsökningsloggning. Mer information och alternativ finns i [Adobe Experience Platform Mobile SDK-dokumentationen](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/).
   1. Startar livscykelövervakning. Mer information finns i [steget Livscykel](lifecycle-data.md) i självstudiekursen.
   1. Anger okänt standardsamtycke. Mer information finns i steget [Medgivande](consent.md) i självstudiekursen.

Se till att du uppdaterar `MobileCore.configureWith(environmentFileId)` med `environmentFileId` baserat på miljöfil-ID:t från den taggmiljö som du skapar för (utveckling, mellanlagring eller produktion).


>[!ENDTABS]

>[!SUCCESS]
>
>Du har nu installerat de nödvändiga paketen och uppdaterat projektet för att registrera de Adobe Experience Platform Mobile SDK-tillägg som du ska använda för resten av kursen.
>
>Tack för att du har lagt ned din tid på att lära dig om Adobe Experience Platform Mobile SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela dem i det här [Experience League Community-diskussionsinlägget](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796?profile.language=sv)

Nästa: **[Konfigurera Assurance](assurance.md)**
