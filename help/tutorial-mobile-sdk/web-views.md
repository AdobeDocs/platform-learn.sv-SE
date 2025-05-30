---
title: Hantera WebViews med Platform Mobile SDK
description: Lär dig hur du hanterar datainsamling med WebViews i en mobilapp.
jira: KT-14632
exl-id: 9b3c96fa-a1b8-49d2-83fc-ece390b9231c
source-git-commit: 25f0df2ea09bb7383f45a698e75bd31be7541754
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---

# Hantera WebViews

Lär dig hur du hanterar datainsamling med WebViews i en mobilapp.

## Förhandskrav

* App med SDK:er har installerats och konfigurerats.

## Utbildningsmål

I den här lektionen kommer du att:

* Förstå varför du måste ta särskild hänsyn till WebViews i din app.
* Förstå koden som krävs för att förhindra spårningsproblem.

## Potentiella spårningsproblem

Om du skickar data från appens inbyggda del och från en WebView i appen, genererar varje sitt eget Experience Cloud-ID (ECID), vilket resulterar i frånkopplade träffar och uppblåsta besöksdata. Mer information om ECID finns i [ECID-översikten](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=sv-SE).

För att lösa den oönskade situationen är det viktigt att skicka användarens ECID från den inbyggda delen av appen till en WebView som du kanske vill använda i appen.

Det AEP Edge Identity-tillägg som används i WebView samlar in det aktuella ECID:t och lägger till det i URL:en i stället för att skicka en begäran till Adobe om ett nytt ID. Implementeringen använder sedan detta ECID för att begära URL:en.

## Implementering

Navigera till **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL Info]** > **[!DNL TermsOfServiceSheet]** och leta upp funktionen `func loadUrl()` i klassen `final class SwiftUIWebViewModel: ObservableObject`. Lägg till följande anrop för att hantera webbvyn:

```swift
// Handle web view
AEPEdgeIdentity.Identity.getUrlVariables {(urlVariables, error) in
    if let error = error {
        print("Error with Webview", error)
        return;
    }
    
    if let urlVariables: String = urlVariables {
        urlString.append("?" + urlVariables)
        guard let url = URL(string: urlString) else {
            return
        }
        DispatchQueue.main.async {
            self.webView.load(URLRequest(url: url))
        }
    }
    Logger.aepMobileSDK.info("Successfully retrieved urlVariables for WebView, final URL: \(urlString)")
}
```

API:t [`AEPEdgeIdentity.Identity.getUrlVariables`](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables) ställer in variablerna för URL:en så att de innehåller all relevant information, som ECID, med mera. I exemplet använder du en lokal fil, men samma koncept gäller för fjärrsidor.

Du kan läsa mer om `Identity.getUrlVariables`-API:t i [API-referenshandboken för Edge Network-tillägg](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables).

## Validera

Så här kör du koden:

1. Granska avsnittet [Installationsanvisningar](assurance.md#connecting-to-a-session) för att ansluta simulatorn eller enheten till Assurance.
1. Gå till **[!UICONTROL Settings]** i appen
1. Tryck på knappen **[!DNL View...]** för att visa **[!DNL Terms of Use]**.

   <img src="./assets/tou1.png" width="300" /> <img src="./assets/tou2.png" width="300" />

1. I kontrollgränssnittet letar du efter händelsen **[!UICONTROL Edge Identity Response URL Variables]** från leverantören **[!UICONTROL com.adobe.griffon.mobile]**.
1. Markera händelsen och granska fältet **[!UICONTROL urlvariable]** i objektet **[!UICONTROL ACPExtensionEventData]**, vilket bekräftar att följande parametrar finns i URL:en: `adobe_mc`, `mcmid` och `mcorgid`.

   ![webbvyvalidering](assets/webview-validation.png)

   Ett exempel på `urvariables`-fält visas nedan:

   * Original (med escape-tecken)

     ```html
     adobe_mc=TS%3D1636526122%7CMCMID%3D79076670946787530005526183384271520749%7CMCORGID%3D7ABB3E6A5A7491460A495D61%40AdobeOrg
     ```

   * Fantastisk

     ```html
     adobe_mc=TS=1636526122|MCMID=79076670946787530005526183384271520749|MCORGID=7ABB3E6A5A7491460A495D61@AdobeOrg
     ```

Tyvärr är felsökningen av webbsessionen begränsad. Du kan till exempel inte använda Adobe Experience Platform Debugger i webbläsaren för att fortsätta felsöka webbvisningssessionen.

>[!NOTE]
>
>Sutning av besökare via dessa URL-parametrar stöds i Platform Web SDK (version 2.11.0 eller senare) och när `VisitorAPI.js` används.


>[!SUCCESS]
>
>Du har nu konfigurerat din app så att den visar innehåll baserat på en URL i en webbvy med samma ECID som det ECID som redan utfärdats av Adobe Experience Platform Mobile SDK.
>
>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Mobile SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela dem i det här [Experience League-diskussionsinlägget](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Nästa: **[Identitet](identity.md)**
