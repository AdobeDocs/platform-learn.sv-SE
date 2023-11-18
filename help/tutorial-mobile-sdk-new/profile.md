---
title: Samla in profildata
description: Lär dig hur du samlar in profildata i en mobilapp.
hide: true
exl-id: 6ce02ccc-6280-4a1f-a96e-1975f8a0220a
source-git-commit: 8f77843aec76e49c5e774016ed6cca5df510d3a4
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---

# Samla in profildata

Lär dig hur du samlar in profildata i en mobilapp.

Du kan använda profiltillägget för att lagra attribut om användaren på klienten. Den här informationen kan användas senare för att målinrikta och personalisera meddelanden i online- eller offlinescenarier, utan att du behöver ansluta till en server för optimala prestanda. Profiltillägget hanterar CSOP (Client-Side Operation Profile), ger ett sätt att reagera på API:er, uppdatera attribut för användarprofiler och delar attribut för användarprofiler med resten av systemet som en genererad händelse.

Profildata används av andra tillägg för att utföra profilrelaterade åtgärder. Ett exempel är tillägget Regelmotor som förbrukar profildata och kör regler baserat på profildata. Läs mer om [Profiltillägg](https://developer.adobe.com/client-sdks/documentation/profile/) i dokumentationen

>[!IMPORTANT]
>
>Profilfunktionerna som beskrivs i den här lektionen skiljer sig från kundprofilfunktionerna i realtid i Adobe Experience Platform och plattformsbaserade program.


## Förutsättningar

* App med SDK:er har installerats och konfigurerats.

## Utbildningsmål

I den här lektionen kommer du att:

* Ange eller uppdatera användarattribut.
* Hämta användarattribut.


## Ange och uppdatera användarattribut

Det kan vara bra att ha som mål och/eller personalisering i appen för att snabbt veta om en användare har köpt något tidigare eller nyligen. Låt oss konfigurera det i Luma-appen.

1. Navigera till **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** >  **[!DNL MobileSDK]** i Xcode Project navigator och hitta `func updateUserAttribute(attributeName: String, attributeValue: String)` funktion. Lägg till följande kod:

   ```swift
   // Create a profile map, add attributes to the map and update profile using the map
   var profileMap = [String: Any]()
   profileMap[attributeName] = attributeValue
   UserProfile.updateUserAttributes(attributeDict: profileMap)
   ```

   Den här koden:

   1. Ställer in en tom ordlista med namnet `profileMap`.

   1. Lägger till ett element i ordlistan med `attributeName` (till exempel `isPaidUser`), och `attributeValue` (till exempel `yes`).

   1. Använder `profileMap` ordlista som ett värde för `attributeDict` parametern för [`UserProfile.updateUserAttributes`](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#updateuserattributes) API-anrop.

1. Navigera till **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL Products]** > **[!DNL ProductView]** i Xcode Project navigator och hitta anropet till `updateUserAttributes` (inom koden för köpet) <img src="assets/purchase.png" width="15" /> -knapp). Lägg till följande kod:

   ```swift
   // Update attributes
   MobileSDK.shared.updateUserAttribute(attributeName: "isPaidUser", attributeValue: "yes")
   ```


## Hämta användarattribut

När du har uppdaterat en användares attribut är det tillgängligt för andra Adobe SDK:er, men du kan även hämta attribut explicit, så att appen fungerar som du vill.

1. Navigera till **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!DNL HomeView]** i Xcode Project navigator och hitta `.onAppear` modifierare. Lägg till följande kod:

   ```swift
   // Get attributes
   UserProfile.getUserAttributes(attributeNames: ["isPaidUser"]) { attributes, error in
       if attributes?.count ?? 0 > 0 {
           if attributes?["isPaidUser"] as? String == "yes" {
               showBadgeForUser = true
           }
           else {
               showBadgeForUser = false
           }
       }
   }
   ```

   Den här koden:

   1. Anropar [`UserProfile.getUserAttributes`](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#getuserattributes) API med `isPaidUser` attributnamn som enskilt element i `attributeNames` array.
   1. Kontrollerar sedan värdet för `isPaidUser` och när `yes`, placerar ett märke på <img src="assets/paiduser.png" width="20" /> i verktygsfältet längst upp till höger.

Ytterligare dokumentation finns [här](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#getuserattributes).

## Validera med Assurance

1. Granska [installationsanvisningar](assurance.md#connecting-to-a-session) för att ansluta simulatorn eller enheten till Assurance.
1. Kör appen för att logga in och interagera med en produkt.

   1. Flytta Assurance-ikonen åt vänster.
   1. Välj **[!UICONTROL Startsida]** i tabbfältet.
   1. Om du vill öppna inloggningsbladet väljer du <img src="assets/login.png" width="15" /> -knappen.

      <img src="./assets/mobile-app-events-1.png" width="300">

   1. Välj <img src="assets/insert.png" width="15" /> knapp .
   1. Välj **[!UICONTROL Inloggning]**.

      <img src="./assets/mobile-app-events-2.png" width="300">

   1. Välj **[!DNL Products]** i tabbfältet.
   1. Välj en produkt.
   1. Välj <img src="assets/saveforlater.png" width="15" />.
   1. Välj <img src="assets/addtocart.png" width="20" />.
   1. Välj <img src="assets/purchase.png" width="15" />.

      <img src="./assets/mobile-app-events-3.png" width="300">

   1. Återgå till **[!UICONTROL Startsida]** skärm. Du bör se att ett märke har lagts till <img src="assets/person-badge-icon.png" width="15" />.

      <img src="./assets/personbadges.png" width="300">



1. I försäkringsgränssnittet bör du se en **[!UICONTROL UserProfileUpdate]** och **[!UICONTROL getUserAttributes]** händelser med uppdaterade `profileMap` värde.
   ![validera profil](assets/profile-validate.png)

>[!SUCCESS]
>
>Du har nu konfigurerat din app för att uppdatera profilattribut i Edge Network och (när den har konfigurerats) med Adobe Experience Platform.
>
>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Mobile SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Nästa: **[Använd platser](places.md)**
