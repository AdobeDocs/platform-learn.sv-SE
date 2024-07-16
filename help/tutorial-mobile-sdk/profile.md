---
title: Samla in profildata med Platform Mobile SDK
description: Lär dig hur du samlar in profildata i en mobilapp.
jira: KT-14634
exl-id: 97717611-04d9-45e3-a443-ea220a13b57c
source-git-commit: 25f0df2ea09bb7383f45a698e75bd31be7541754
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 0%

---

# Samla in profildata

Lär dig hur du samlar in profildata i en mobilapp.

Du kan använda profiltillägget för att lagra attribut om användaren på klienten. Den här informationen kan användas senare för att målinrikta och personalisera meddelanden i online- eller offlinescenarier, utan att du behöver ansluta till en server för optimala prestanda. Profiltillägget hanterar CSOP (Client-Side Operation Profile), ger ett sätt att reagera på API:er, uppdatera attribut för användarprofiler och delar attribut för användarprofiler med resten av systemet som en genererad händelse.

Profildata används av andra tillägg för att utföra profilrelaterade åtgärder. Ett exempel är tillägget Regelmotor som förbrukar profildata och kör regler baserat på profildata. Läs mer om [profiltillägget](https://developer.adobe.com/client-sdks/documentation/profile/) i dokumentationen

>[!IMPORTANT]
>
>Profilfunktionerna som beskrivs i den här lektionen skiljer sig från kundprofilfunktionerna i realtid i Adobe Experience Platform och plattformsbaserade program.


## Förhandskrav

* App med SDK:er har installerats och konfigurerats.

## Utbildningsmål

I den här lektionen kommer du att:

* Ange eller uppdatera användarattribut.
* Hämta användarattribut.


## Ange och uppdatera användarattribut

Det kan vara bra att ha som mål och/eller personalisering i appen för att snabbt veta om en användare har köpt något tidigare eller nyligen. Låt oss konfigurera det i Luma-appen.

1. Navigera till **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!DNL MobileSDK]** i Xcode Project-navigatorn och hitta funktionen `func updateUserAttribute(attributeName: String, attributeValue: String)`. Lägg till följande kod:

   ```swift
   // Create a profile map, add attributes to the map and update profile using the map
   var profileMap = [String: Any]()
   profileMap[attributeName] = attributeValue
   UserProfile.updateUserAttributes(attributeDict: profileMap)
   ```

   Den här koden:

   1. Ställer in en tom ordlista med namnet `profileMap`.

   1. Lägger till ett element i ordlistan med `attributeName` (till exempel `isPaidUser`) och `attributeValue` (till exempel `yes`).

   1. Använder `profileMap`-ordlistan som ett värde för parametern `attributeDict` i API-anropet [`UserProfile.updateUserAttributes`](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#updateuserattributes).

1. Navigera till **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL Products]** > **[!DNL ProductView]** i Xcode Project navigator och hitta anropet till `updateUserAttributes` (i koden för inköp) <img src="assets/purchase.png" width="15" />). Lägg till följande kod:

   ```swift
   // Update attributes
   MobileSDK.shared.updateUserAttribute(attributeName: "isPaidUser", attributeValue: "yes")
   ```


## Hämta användarattribut

När du har uppdaterat en användares attribut är det tillgängligt för andra Adobe SDK:er, men du kan även hämta attribut explicit, så att appen fungerar som du vill.

1. Navigera till **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!DNL HomeView]** i Xcode Project-navigatorn och hitta modifieraren `.onAppear`. Lägg till följande kod:

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

   1. Anropar [`UserProfile.getUserAttributes`](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#getuserattributes)-API:t med attributnamnet `isPaidUser` som ett element i arrayen `attributeNames`.
   1. Kontrollerar sedan värdet för attributet `isPaidUser` och placerar ett märke på`yes` ikonen <img src="assets/paiduser.png" width="20" /> i verktygsfältet längst upp till höger.

Ytterligare dokumentation finns [här](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#getuserattributes).

## Validera med Assurance

1. Granska avsnittet [Installationsanvisningar](assurance.md#connecting-to-a-session) för att ansluta simulatorn eller enheten till Assurance.
1. Kör appen för att logga in och interagera med en produkt.

   1. Flytta Assurance-ikonen åt vänster.
   1. Välj **[!UICONTROL Home]** i flikfältet.
   1. Om du vill öppna inloggningsbladet väljer du knappen <img src="assets/login.png" width="15" />.

      <img src="./assets/mobile-app-events-1.png" width="300">

   1. Välj <img src="assets/insert.png" width="15" />-knapp .
   1. Välj **[!UICONTROL Login]**.

      <img src="./assets/mobile-app-events-2.png" width="300">

   1. Välj **[!DNL Products]** i flikfältet.
   1. Välj en produkt.
   1. Välj <img src="assets/saveforlater.png" width="15" />.
   1. Välj <img src="assets/addtocart.png" width="20" />.
   1. Välj <img src="assets/purchase.png" width="15" />.

      <img src="./assets/mobile-app-events-3.png" width="300">

   1. Återgå till skärmen **[!UICONTROL Home]**. Du bör se att ett märke har lagts till <img src="assets/person-badge-icon.png" width="15" />.

      <img src="./assets/personbadges.png" width="300">



1. I Assurance-gränssnittet bör du se en **[!UICONTROL UserProfileUpdate]**- och **[!UICONTROL getUserAttributes]**-händelse med det uppdaterade `profileMap`-värdet.
   ![validera profil](assets/profile-validate.png)

>[!SUCCESS]
>
>Du har nu konfigurerat din app för att uppdatera profilattribut i Edge Network och (när den har konfigurerats) med Adobe Experience Platform.
>
>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Mobile SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela dem i det här [Experience League-diskussionsinlägget](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Nästa: **[Använd platser](places.md)**
