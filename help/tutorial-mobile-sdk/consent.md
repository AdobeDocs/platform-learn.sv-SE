---
title: Godkännande
description: Lär dig hur du implementerar samtycke i en mobilapp.
exl-id: 08042569-e16e-4ed9-9b5a-864d8b7f0216
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 1%

---

# Godkännande

Lär dig hur du implementerar samtycke i en mobilapp.

Med mobiltillägget Adobe Experience Platform Consent kan du samla in medgivandeinställningar från din mobilapp när du använder Adobe Experience Platform Mobile SDK och Edge Network-tillägget. Läs mer om [Godkänn tillägg](https://aep-sdks.gitbook.io/docs/foundation-extensions/consent-for-edge-network)i dokumentationen.

## Förutsättningar

* Programmet har skapats och körts med SDK:er installerade och konfigurerade.

## Utbildningsmål

I den här lektionen kommer du att:

* Fråga användaren om samtycke.
* Uppdatera tillägget baserat på användarens svar.
* Lär dig hur du får det aktuella tillståndet för samtycke.

## Be om samtycke

Om du följde självstudiekursen från början kommer du ihåg att ange **[!UICONTROL Standardnivå för samtycke]** till &quot;Väntar&quot;. För att kunna börja samla in data måste du få användarens samtycke. I den här självstudiekursen får du ditt medgivande genom att helt enkelt fråga med en varning i en app i verkligheten som du vill använda för att få ditt medgivande i din region.

1. Du vill bara fråga användaren en gång. Ett enkelt sätt att hantera det är att helt enkelt använda `UserDefaults`.
1. Navigera till `Home.swift`.
1. Lägg till följande kod i `viewDidLoad()`.

   ```swift
   let defaults = UserDefaults.standard
   let consentKey = "askForConsentYet"
   let hidePopUp = defaults.bool(forKey: consentKey)
   ```

1. Om användaren inte har sett varningen tidigare, visa den och uppdatera medgivandet baserat på deras svar. Lägg till följande kod i `viewDidLoad()`.

   ```swift
   if(hidePopUp == false){
       //Consent Alert
       let alert = UIAlertController(title: "Allow Data Collection?", message: "Selecting Yes will begin data collection", preferredStyle: .alert)
       alert.addAction(UIAlertAction(title: "Yes", style: .default, handler: { action in
           //Update Consent -> "yes"
           let collectConsent = ["collect": ["val": "y"]]
           let currentConsents = ["consents": collectConsent]
           Consent.update(with: currentConsents)
           defaults.set(true, forKey: consentKey)
       }))
       alert.addAction(UIAlertAction(title: "No", style: .cancel, handler: { action in
           //Update Consent -> "no"
           let collectConsent = ["collect": ["val": "n"]]
           let currentConsents = ["consents": collectConsent]
           Consent.update(with: currentConsents)
           defaults.set(true, forKey: consentKey)
       }))
       self.present(alert, animated: true)
   }
   ```


## Hämta aktuellt medgivandetillstånd

Tillägget för mobilen Consent inaktiverar/väntar automatiskt på/tillåter spårning baserat på det aktuella medgivandevärdet. Du kan även komma åt det aktuella medgivandetillståndet själv:

1. Navigera till `Home.swift`.
1. Lägg till följande kod i `viewDidLoad()`.

```swift
Consent.getConsents{ consents, error in
    guard error == nil, let consents = consents else { return }
    guard let jsonData = try? JSONSerialization.data(withJSONObject: consents, options: .prettyPrinted) else { return }
    guard let jsonStr = String(data: jsonData, encoding: .utf8) else { return }
    print("Consent getConsents: ",jsonStr)
}
```

I exemplet ovan skriver du bara ut medgivandestatus till konsolen. I ett verkligt scenario kan du använda det för att ändra vilka menyer eller alternativ som visas för användaren.

## Validera med Assurance

1. Granska [Säkerhet](assurance.md) lektion.
1. Installera programmet.
1. Starta programmet med den Assurance-genererade URL:en.
1. Om du har lagt till ovanstående kod korrekt uppmanas du att ge ditt medgivande. Välj **Ja**.
   ![medgivandepopup](assets/mobile-consent-validate.png)
1. Du borde se en **[!UICONTROL Inställningar för samtycke har uppdaterats]** -händelse i försäkringsgränssnittet.
   ![validera samtycke](assets/mobile-consent-update.png)

Nästa: **[Samla in livscykeldata](lifecycle-data.md)**

>[!NOTE]
>
>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Mobile SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela med dig av dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)