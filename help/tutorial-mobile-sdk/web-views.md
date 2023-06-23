---
title: Hantera WebViews
description: Lär dig hur du hanterar datainsamling med WebViews i en mobilapp.
jira: KT-6987
exl-id: 9b3c96fa-a1b8-49d2-83fc-ece390b9231c
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---

# Hantera WebViews

Lär dig hur du hanterar datainsamling med WebViews i en mobilapp.

## Förutsättningar

* Programmet har skapats och körts med SDK:er installerade och konfigurerade.

## Utbildningsmål

I den här lektionen kommer du att:

* Förstå varför du måste ta särskild hänsyn till WebViews.
* Förstå koden som krävs för att förhindra spårningsproblem.

## Potentiella spårningsproblem

Om du skickar data från den inbyggda delen av programmet och en WebView genererar varje sitt eget Experience Cloud-ID (ECID). Detta resulterar i osammanhängande träffar och uppblåsta besöksdata. Mer information om ECID finns i [ECID - översikt](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=en).

För att lösa den oönskade situationen är det viktigt att skicka användarens ECID från den ursprungliga delen till WebView.

JavaScript-tillägget för tjänsten Experience Cloud ID i WebView extraherar ECID från URL:en i stället för att skicka en begäran till Adobe om ett nytt ID. ID-tjänsten använder detta ECID för att spåra besökaren.

## Implementering

I Luma-exempelappen hittar du `TermsOfService.swift` -filen (i `Intro-Login_SignUp` och leta upp följande kod:

```swift
// Show tou.html
let url = Bundle.main.url(forResource: "tou", withExtension: "html")
let myRequest = URLRequest(url: url!)
self.webView.load(myRequest)
```

Det här är ett enkelt sätt att läsa in en WebView. I det här fallet är det en lokal fil, men samma koncept gäller för fjärrsidor.

Reaktera webbvykoden så som visas nedan:

```swift
let url = Bundle.main.url(forResource: "tou", withExtension: "html")
if var urlString = url?.absoluteString {
    // Adobe Experience Platform - Handle Web View
    AEPEdgeIdentity.Identity.getUrlVariables {(urlVariables, error) in
        if let error = error {
            self.simpleAlert("\(error.localizedDescription)")
            return;
        }

        if let urlVariables: String = urlVariables {
            urlString.append("?" + urlVariables)
        }

        DispatchQueue.main.async {
            self.webView.load(URLRequest(url: URL(string: urlString)!))
        }
        print("Successfully retrieved urlVariables for WebView, final URL: \(urlString)")
    }
} else {
    self.simpleAlert("Failed to create URL for webView")
}
```

Du kan läsa mer om `Identity.getUrlVariables` API i [Referenshandbok för API:t för Edge Network Extension](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables).

## Validering

När du har granskat [installationsanvisningar](assurance.md) och koppla simulatorn eller enheten till Assurance, läsa in WebView och leta efter `Edge Identity Response URL Variables` från `com.adobe.griffon.mobile` leverantör.

Om du vill läsa in WebView går du till startskärmen för Luma-appen och väljer kontoikonen följt av användningsvillkoren i sidfoten.

När du har läst in WebView markerar du händelsen och granskar `urlvariables` i `ACPExtensionEventData` objekt, som bekräftar att följande parametrar finns i URL:en: `adobe_mc`, `mcmid`och `mcorgid`.

![webbvyvalidering](assets/mobile-webview-validation.png)

Ett exempel `urvariables` visas nedan:

```html
// Original (with escaped characters)
adobe_mc=TS%3D1636526122%7CMCMID%3D79076670946787530005526183384271520749%7CMCORGID%3D7ABB3E6A5A7491460A495D61%40AdobeOrg

// Beautified
adobe_mc=TS=1636526122|MCMID=79076670946787530005526183384271520749|MCORGID=7ABB3E6A5A7491460A495D61@AdobeOrg
```

>[!NOTE]
>
>Besökarsytning via dessa URL-parametrar stöds för närvarande i Platform Web SDK (version 2.11.0 eller senare) och `VisitorAPI.js`.


Nästa: **[Identitet](identity.md)**

>[!NOTE]
>
>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Mobile SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela med dig av dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)