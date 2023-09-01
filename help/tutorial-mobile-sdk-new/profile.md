---
title: Profil
description: Lär dig hur du samlar in profildata i en mobilapp.
hide: true
source-git-commit: c31dd74cf8ff9c0856b29e82d9c8be2ad027df4a
workflow-type: tm+mt
source-wordcount: '592'
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

* App med SDK:er har installerats och konfigurerats.
* Profil-SDK importerades.

  ```swift
  import AEPUserProfile
  ```

## Utbildningsmål

I den här lektionen kommer du att:

* Ange eller uppdatera användarattribut.
* Hämta användarattribut.


## Ange och uppdatera användarattribut

Det skulle vara praktiskt för målgruppsanpassning och/eller personalisering att snabbt veta om en användare har köpt appen tidigare. Låt oss konfigurera det i Luma-appen.

1. Navigera till **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Utils]** >  **[!UICONTROL MobileSDK]** i Xcode Project navigator och hitta `func updateUserAttribute(attributeName: String, attributeValue: String)` funktion. Lägg till följande kod:

   ```swift
   // Create a profile map
   var profileMap = [String: Any]()
   // Add attributes to profile map
   profileMap[attributeName] = attributeValue
   // Use profile map to update user attributes
   UserProfile.updateUserAttributes(attributeDict: profileMap)
   ```

   Den här koden:

   1. Ställer in en tom ordlista med namnet `profileMap`.

   1. Lägger till ett element i ordlistan med `attributeName` (till exempel `isPaidUser`), och `attributeValue` (till exempel `yes`).

   1. Använder `profileMap` ordlista som ett värde för `attributeDict` parametern för `UserProfile.updateUserAttributes` API-anrop.

1. Navigera till **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Vyer]** > **[!UICONTROL Produkter]** > **[!UICONTROL ProductView]** i Xcode Project navigator och hitta anropet till `updateUserAttributes` (inom koden för köpet) <img src="assets/purchase.png" width="15" /> knapp):

   ```swift
   // Update attributes
   MobileSDK.shared.updateUserAttributes(attributeName: "isPaidUser", attributeValue: "yes")
   ```

Ytterligare dokumentation finns [här](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#updateuserattribute).

## Hämta användarattribut

När du har uppdaterat en användares attribut är det tillgängligt för andra Adobe SDK:er, men du kan även hämta attribut explicit.

1. Navigera till **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Vyer]** > Allmänt > **[!UICONTROL HomeView]** i Xcode Project navigator och hitta `.onAppear` modifierare. Lägg till följande kod:

   ```swift
   // Get attributes
   UserProfile.getUserAttributes(attributeNames: ["isPaidUser"]) { attributes, error in
       if attributes?["isPaidUser"] as! String == "yes" {
           showBadgeForUser = true
       }
       else {
           showBadgeForUser = false
       }
   }
   ```

   Den här koden:

   1. Anropar `UserProfile.getUserAttributes` stängning med `iPaidUser` attributnamn som enskilt element i `attributeNames` array.
   1. Kontrollerar sedan värdet för `isPaidUser` och när `yes`, placerar ett märke på <img src="assets/paiduser.png" width="20" /> i verktygsfältet längst upp till höger.

Ytterligare dokumentation finns [här](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#getuserattributes).

## Validera med Assurance

1. Granska [installationsanvisningar](assurance.md) -avsnitt.
1. Installera programmet.
1. Starta appen med den URL som skapas av försäkringen.
1. Kör appen för att logga in och interagera med en produkt.

   1. Flytta Assurance-ikonen åt vänster.
   1. Välj **[!UICONTROL Startsida]** i tabbfältet.
   1. Om du vill öppna inloggningsbladet väljer du <img src="assets/login.png" width="15" /> -knappen.
   1. Välj <img src="assets/insert.png" width="15" /> knapp .
   1. Välj **[!UICONTROL Inloggning]**.
   1. Välj **[!UICONTROL Produkter]** i tabbfältet.
   1. Välj en produkt.
   1. Välj <img src="assets/saveforlater.png" width="15" />.
   1. Välj <img src="assets/addtocart.png" width="20" />.
   1. Välj <img src="assets/purchase.png" width="15" />.

      <img src="./assets/mobile-app-events-1.png" width="200"> <img src="./assets/mobile-app-events-2.png" width="200"> <img src="./assets/mobile-app-events-3.png" width="200">
   1. Återgå till **[!UICONTROL Startsida]** skärm. Du bör se ett märke tillagt <img src="assets/person-badge-icon.png" width="15" />.

      <img src="./assets/personbadges.png" width="200">



1. I försäkringsgränssnittet bör du se en **[!UICONTROL UserProfileUpdate]** och **[!UICONTROL getUserAttributes]** händelser med uppdaterade `profileMap` värde.
   ![validera profil](assets/profile-validate.png)

>[!SUCCESS]
>
>Du har nu konfigurerat din app för att uppdatera profilattribut i Edge Network och (när den har konfigurerats) med Adobe Experience Platform.<br/>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Mobile SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Nästa: **[Använd geopositioneringstjänster](places.md)**
