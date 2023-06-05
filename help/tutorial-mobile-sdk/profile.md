---
title: Profil
description: Lär dig hur du samlar in profildata i en mobilapp.
exl-id: 97717611-04d9-45e3-a443-ea220a13b57c
source-git-commit: b2e1bf08d9fb145ba63263dfa078c96258342708
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 1%

---

# Profil

Lär dig hur du samlar in profildata i en mobilapp.

Du kan använda profiltillägget för att lagra attribut om användaren på klienten. Den här informationen kan användas senare för att målinrikta och personalisera meddelanden i online- eller offlinescenarier, utan att du behöver ansluta till en server för optimala prestanda. Profiltillägget hanterar CSOP (Client-Side Operation Profile), ger ett sätt att reagera på API:er, uppdatera attribut för användarprofiler och delar attribut för användarprofiler med resten av systemet som en genererad händelse.

Profildata används av andra tillägg för att utföra profilrelaterade åtgärder. Ett exempel är tillägget Regelmotor som förbrukar profildata och kör regler baserat på profildata. Läs mer om [Profiltillägg](https://developer.adobe.com/client-sdks/documentation/profile/) i dokumentationen

>[!IMPORTANT]
>
>Profilfunktionerna som beskrivs i den här lektionen skiljer sig från kundprofilfunktionerna i realtid i Adobe Experience Platform och plattformsbaserade program.


## Förutsättningar

* Programmet har skapats och körts med SDK:er installerade och konfigurerade.
* Profil-SDK importerades.

   ```swift
   import AEPUserProfile
   ```

## Utbildningsmål

I den här lektionen kommer du att:

* Ange eller uppdatera användarattribut.
* Hämta användarattribut.


## Ange och uppdatera

Det skulle vara praktiskt för målgruppsanpassning och/eller personalisering att snabbt veta om en användare har köpt appen tidigare. Låt oss konfigurera det i Luma-appen.

1. Navigera till `Cart.swift`

1. Lägg till nedanstående kod i `processOrder() `funktion.

   ```swift
   var profileMap = [String: Any]()
   profileMap["isPaidUser"] = "yes"
   UserProfile.updateUserAttributes(attributeDict: profileMap)
   ```

Personaliseringsteamet kanske också vill rikta sig baserat på användarens lojalitetsnivå. Låt oss konfigurera det i Luma-appen.

1. Navigera till `Account.swift`

1. Lägg till nedanstående kod i `showUserInfo()` funktion.

   ```swift
   var profileMap = [String: Any]()
   profileMap["loyaltyLevel"] = loyaltyLevel
   UserProfile.updateUserAttributes(attributeDict: profileMap)
   ```

Ytterligare `updateUserAttributes` dokumentation finns [här](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#updateuserattribute).

## Hämta

När du har uppdaterat en användares attribut är det tillgängligt för andra Adobe SDK:er, men du kan även hämta attribut explicit.

```swift
UserProfile.getUserAttributes(attributeNames: ["isPaidUser","loyaltyLevel"]){
    attributes, error in
    print("Profile: getUserAttributes: ",attributes as Any)
}
```

Ytterligare `getUserAttributes` dokumentation finns [här](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#getuserattributes).

## Validera med Assurance

1. Granska [installationsanvisningar](assurance.md) -avsnitt.
1. Installera programmet.
1. Starta appen med den URL som skapas av försäkringen.
1. Markera kontoikonen och välj sedan Logga in. Obs! du inte har angett några autentiseringsuppgifter.
1. Stäng inloggningsmenyerna och välj sedan kontoikonen igen. Det här visar skärmen med kontoinformation där `loyaltyLevel` är inställt.
1. Du borde se en **[!UICONTROL UserProfileUpdate]** händelse i försäkringsgränssnittet med den uppdaterade `profileMap` värde.
   ![validera profil](assets/mobile-profile-validate.png)

Nästa: **[Mappa data till Adobe Analytics](analytics.md)**

>[!NOTE]
>
>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Mobile SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela med dig av dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)