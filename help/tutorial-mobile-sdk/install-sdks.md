---
title: Installera Adobe Experience Platform Mobile SDKs
description: Lär dig hur du implementerar Adobe Experience Platform Mobile SDK i en mobilapp.
exl-id: 98d6f59e-b8a3-4c63-ae7c-8aa11e948f59
source-git-commit: b2e1bf08d9fb145ba63263dfa078c96258342708
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 0%

---

# Installera Adobe Experience Platform Mobile SDKs

Lär dig hur du implementerar Adobe Experience Platform Mobile SDK i en mobilapp.

## Förutsättningar

* Taggbiblioteket med tilläggen som beskrivs i [föregående lektion](configure-tags.md).
* Fil-ID för utvecklingsmiljö från [Instruktioner för mobilinstallation](configure-tags.md#generate-sdk-install-instructions).
* Nedladdad, tom [exempelapp](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"}.
* Upplevelse med [XCode](https://developer.apple.com/xcode/){target="_blank"}.
* Grundläggande [kommandorad](https://en.wikipedia.org/wiki/Command-line_interface){target="_blank"} kunskap.

## Utbildningsmål

I den här lektionen kommer du att:

* Uppdatera din CocoaPod-fil.
* Importera de SDK:er som behövs.
* Registrera tilläggen.

>[!NOTE]
>
>I en mobilappsimplementering är termerna &quot;extensions&quot; och &quot;SDKs&quot; nästan utbytbara.


## Uppdatera PodFile

>[!NOTE]
>
> Om du inte är bekant med CocoaPods, se den officiella [komma igång-guide](https://guides.cocoapods.org/using/getting-started.html).

Installera är vanligtvis ett enkelt sudo-kommando:

```console
sudo gem install cocoapods
```

Öppna Podfilen när du har installerat CocoaPods.

![initial podfile](assets/mobile-install-initial-podfile.png)

Uppdatera filen så att den innehåller följande punkter:

```swift
pod 'AEPCore', '~> 3'
pod 'AEPEdge', '~> 1'
pod 'AEPUserProfile', '~> 3'
pod 'AEPAssurance', '~> 3'
pod 'AEPServices', '~> 3'
pod 'AEPEdgeConsent', '~> 1'
pod 'AEPLifecycle', '~>3'
pod 'AEPMessaging', '~>1'
pod 'AEPEdgeIdentity', '~>1'
pod 'AEPSignal', '~>3'
```

>[!NOTE]
>
> `AEPMessaging` krävs bara om du tänker implementera push-meddelanden med Adobe Journey Optimizer. Läs självstudiekursen om [implementera push-meddelanden med Adobe Journey Optimizer](journey-optimizer-push.md) för mer information.

När du har sparat ändringarna i din Podfile navigerar du till mappen med ditt projekt och kör `pod install` för att installera ändringarna.

![pod-installation](assets/mobile-install-podfile-install.png)

>[!NOTE]
>
> Om du får &quot;No Podfile found in the project directory.&quot; fel, terminalen finns i fel mapp. Navigera till mappen med den PDF-fil du har uppdaterat och försök igen.

Om du vill uppgradera till den senaste versionen kör du `pod update` -kommando.

>[!INFO]
>
>Om du inte kan använda CocoaPods i dina egna program kan du lära dig mer om andra [implementeringar som stöds](https://github.com/adobe/aepsdk-core-ios#binaries) i GitHub-projektet.

## Bygg CocoaPods

Öppna om du vill bygga CocoaPods `Luma.xcworkspace`och markera **Produkt**, följt av **Rensa byggmapp**.

>[!NOTE]
>
> Du kan behöva ange **Skapa endast aktiv arkitektur** till **Nej**. Det gör du genom att välja Pods-projektet i projektnavigeraren och välja **Inställningar för bygge** och ange **Bygg aktiv arkitektur** till **Nej**.

Nu kan du skapa och köra projektet.

![bygginställningar](assets/mobile-install-build-settings.png)

>[!NOTE]
>
>Lumaprojektet byggdes med Xcode v12.5 på en M1-kretsuppsättning och körs i iOS-simulatorn. Om du använder en annan konfiguration kan du behöva ändra bygginställningarna så att de återspeglar din arkitektur.
>
>Om bygget inte lyckas kan du försöka återställa **Bygg aktiv arkitektur** > **Felsök** återställer till **Ja**.
>
>Simulatorkonfigurationen &quot;iPod touch (7:e generationen)&quot; användes när självstudiekursen skapades.

## Importera tillägg

I var och en av `.swift` lägger du till följande importer. Börja med att lägga till `AppDelegate.swift`.

```swift
import AEPUserProfile
import AEPAssurance
import AEPEdge
import AEPCore
import AEPEdgeIdentity
import AEPEdgeConsent
import AEPLifecycle
import AEPMessaging //Optional, used for AJO push messaging
import AEPSignal
import AEPServices
```

## Uppdatera AppDelegate

I `AppDelegate.swift` lägg till följande kod i `didFinishLaunchingWithOptions`. Ersätt currentAppId med det fil-ID för utvecklingsmiljöfil som du hämtade från taggar i [föregående lektion](configure-tags.md).

```swift
let currentAppId = "b5cbd1a1220e/bae66382cce8/launch-88492c6dcb6e-development"

let extensions = [Edge.self, Assurance.self, Lifecycle.self, UserProfile.self, Consent.self, AEPEdgeIdentity.Identity.self, Messaging.self]

MobileCore.setLogLevel(.trace)

MobileCore.registerExtensions(extensions, {
    MobileCore.configureWith(appId: currentAppId)
})
```

`Messaging.self` krävs bara om du tänker implementera push-meddelanden via Adobe Journey Optimizer enligt beskrivningen [här](journey-optimizer-push.md).

Koden ovan gör följande:

* Registrerar nödvändiga tillägg.
* Konfigurerar MobileCore och andra tillägg så att taggegenskapskonfigurationen används.
* Aktiverar felsökningsloggning. Mer information och alternativ finns i [Mobile SDK-dokumentation](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/).

>[!IMPORTANT]
>I en produktionsapp måste du växla AppId baserat på den aktuella miljön (dev/stag/prod).

Nästa: **[Ställ in försäkring](assurance.md)**

>[!NOTE]
>
>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Mobile SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela med dig av dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)