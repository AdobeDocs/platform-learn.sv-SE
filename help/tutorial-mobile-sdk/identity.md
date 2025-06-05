---
title: Samla in identitetsdata i en mobilapp med Mobile SDK
description: Lär dig hur du samlar in identitetsdata i en mobilapp.
feature: Mobile SDK,Identities
jira: KT-14633
exl-id: cbcd1708-29e6-4d74-be7a-f75c917ba2fa
source-git-commit: d73f9b3eafb327783d6bfacaf4d57cf8881479f7
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 0%

---

# Samla in identitetsdata

Lär dig hur du samlar in identitetsdata i en mobilapp.

Adobe Experience Platform identitetstjänst hjälper er att få en bättre bild av era kunder och deras beteenden genom att överbrygga identiteter mellan olika enheter och system, så att ni kan leverera slagkraftiga, personliga digitala upplevelser i realtid. Identitetsfält och namnutrymmen är den kombination som förenar olika datakällor för att skapa en 360-graders kundprofil i realtid.

Läs mer om [identitetstillägget](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/) och [identitetstjänsten](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=sv) i dokumentationen.

## Förhandskrav

* App med SDK:er har installerats och konfigurerats.

## Utbildningsmål

I den här lektionen kommer du att:

* Konfigurera ett anpassat ID-namnutrymme.
* Uppdatera identiteter.
* Validera identitetsdiagrammet.
* Hämta ECID och andra identiteter.


## Konfigurera ett anpassat ID-namnutrymme

Identitetsnamnutrymmen är komponenter i [identitetstjänsten](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=sv-SE) som fungerar som indikatorer för det sammanhang som en identitet relateras till. De särskiljer till exempel värdet `name@email.com` som en e-postadress eller `443522` som ett numeriskt CRM-ID.

>[!NOTE]
>
>Mobile SDK genererar en unik identitet i sitt eget namnutrymme med namnet Experience Cloud ID (ECID) när appen installeras. Detta ECID lagras i beständigt minne på den mobila enheten och skickas med varje träff. ECID tas bort när användaren avinstallerar programmet eller när användaren anger Mobile SDK globala sekretessstatus som avanmälan. I exempelappen Luma bör du ta bort och installera om appen för att skapa en ny profil med ett eget unikt ECID.


Så här skapar du ett nytt identitetsnamnutrymme:

1. I gränssnittet för datainsamling väljer du **[!UICONTROL Identities]** i navigeringen till vänster.
1. Välj **[!UICONTROL Create identity namespace]**.
1. Ange **[!UICONTROL Display name]** av `Luma CRM ID` och **[!UICONTROL Identity symbol]** värdet `lumaCRMId`.
1. Välj **[!UICONTROL Cross-device ID]**.
1. Välj **[!UICONTROL Create]**.

   ![skapa ID-namnområde](assets/identity-create.png)




## Uppdatera identiteter

Du vill uppdatera både standardidentiteten (e-post) och den anpassade identiteten (Luma CRM ID) när användaren loggar in i programmet.

1. Navigera till **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** i Xcode-projektnavigeraren och hitta `func updateIdentities(emailAddress: String, crmId: String)`-funktionsimplementeringen. Lägg till följande kod i funktionen.

   ```swift
   // Set up identity map, add identities to map and update identities
   let identityMap: IdentityMap = IdentityMap()
   
   let emailIdentity = IdentityItem(id: emailAddress, authenticatedState: AuthenticatedState.authenticated)
   let crmIdentity = IdentityItem(id: crmId, authenticatedState: AuthenticatedState.authenticated)
   identityMap.add(item:emailIdentity, withNamespace: "Email")
   identityMap.add(item: crmIdentity, withNamespace: "lumaCRMId")
   
   Identity.updateIdentities(with: identityMap)
   ```

   Den här koden:

   1. Skapar ett tomt `IdentityMap`-objekt.

      ```swift
      let identityMap: IdentityMap = IdentityMap()
      ```

   1. Ställer in `IdentityItem` objekt för e-post och CRM-ID.

      ```swift
      let emailIdentity = IdentityItem(id: emailAddress, authenticatedState: AuthenticatedState.authenticated)
      let crmIdentity = IdentityItem(id: crmId, authenticatedState: AuthenticatedState.authenticated)
      ```

   1. Lägger till dessa `IdentityItem`-objekt i `IdentityMap`-objektet.

      ```swift
      identityMap.add(item:emailIdentity, withNamespace: "Email")
      identityMap.add(item: crmIdentity, withNamespace: "lumaCRMId")
      ```

   1. Skickar `IdentityItem`-objektet som en del av `Identity.updateIdentities` API-anropet till Edge Network.

      ```swift
      Identity.updateIdentities(with: identityMap) 
      ```

1. Navigera till **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL LoginSheet]** i Xcode-projektnavigeraren och sök efter koden som ska köras när du väljer knappen **[!UICONTROL Login]**. Lägg till följande kod:

   ```swift
   // Update identities
   MobileSDK.shared.updateIdentities(emailAddress: currentEmailId, crmId: currentCRMId)                             
   ```


>[!NOTE]
>
>Du kan skicka flera identiteter i ett enda `updateIdentities`-samtal. Du kan också ändra identiteter som du tidigare skickat.


## Ta bort en identitet

Du kan använda API:t [`Identity.removeIdentity`](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#removeidentity) för att ta bort identiteten från den lagrade identitetskartan på klientsidan. Identitetstillägget slutar skicka identifieraren till Edge Network. Om du använder detta API tas inte identifieraren bort från serversidans identitetsdiagram. Mer information om identitetsdiagram finns i [Visa identitetsdiagram](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/view-identity-graphs.html?lang=sv-SE).

1. Navigera till **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** i Xcode Project-navigatorn och lägg till följande kod i funktionen `func removeIdentities(emailAddress: String, crmId: String)`:

   ```swift
   // Remove identities and reset email and CRM Id to their defaults
   Identity.removeIdentity(item: IdentityItem(id: emailAddress), withNamespace: "Email")
   Identity.removeIdentity(item: IdentityItem(id: crmId), withNamespace: "lumaCRMId")
   currentEmailId = "testUser@gmail.com"
   currentCRMId = "b642b4217b34b1e8d3bd915fc65c4452"
   ```

1. Navigera till **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL LoginSheet]** i Xcode-projektnavigeraren och sök efter koden som ska köras när du väljer knappen **[!UICONTROL Logout]**. Lägg till följande kod:

   ```swift
   // Remove identities
   MobileSDK.shared.removeIdentities(emailAddress: currentEmailId, crmId: currentCRMId)                  
   ```


## Validera med Assurance

1. Granska avsnittet [installationsanvisningar](assurance.md#connecting-to-a-session) för att ansluta simulatorn eller enheten till Assurance.
1. I Luma-appen
   1. Markera fliken **[!UICONTROL Home]** och flytta Assurance-ikonen åt vänster.
   1. Välj Ikonen <img src="assets/login.png" width="15" /> uppifrån till höger.

      <img src="./assets/identity1.png" width="300">

   1. Ange en e-postadress och ett CRM-ID, eller
   1. Välj <img src="assets/insert.png" width="15" /> om du vill generera en **[!UICONTROL Email]** och **[!UICONTROL CRM ID]** slumpmässigt.
   1. Välj **[!UICONTROL Login]**.

      <img src="./assets/identity2.png" width="300">


1. Leta i Assurance webbgränssnitt efter händelsen **[!UICONTROL Edge Identity Update Identities]** från leverantören **[!UICONTROL com.adobe.griffon.mobile]**.
1. Markera händelsen och granska data i objektet **[!UICONTROL ACPExtensionEventData]**. Du bör se de identiteter som du har uppdaterat.
   ![validera identitetsuppdatering](assets/identity-validate-assurance.png)

## Validera med identitetsdiagram

När du har slutfört stegen i [Experience Platform-lektionen](platform.md) kan du bekräfta identitetsfångsten i visningsprogrammet för plattformsidentitetsdiagram:

1. Välj **[!UICONTROL Identities]** i användargränssnittet för datainsamling.
1. Välj **[!UICONTROL Identity Graph]** i det övre fältet.
1. Ange `Luma CRM ID` som **[!UICONTROL Identity namespace]** och ditt CRM-ID (till exempel `24e620e255734d8489820e74f357b5c8`) som **[!UICONTROL Identity value]**.
1. **[!UICONTROL Identities]** visas.

   ![validera identitetsdiagram](assets/identity-validate-graph.png)

>[!INFO]
>
>Det finns ingen kod i programmet för att återställa ECID, vilket betyder att du bara kan återställa ECID (och effektivt skapa en ny profil med ett nytt ECID) genom en avinstallation och ominstallation av programmet. Information om hur du implementerar återställningen av identifierare finns i API-anropen för [`Identity.resetIdentities`](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/api-reference/#resetidentities) och [`MobileCore.resetIdentities`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#resetidentities). Tänk dock på att när du använder en identifierare för push-meddelanden (se [Skicka push-meddelanden](journey-optimizer-push.md)) blir den identifieraren en annan profilidentifierare för push-meddelanden på enheten.


>[!SUCCESS]
>
>Du har nu konfigurerat din app för att uppdatera identiteter i Edge Network och (när du konfigurerar den) med Adobe Experience Platform.
>
>Tack för att du har lagt ned din tid på att lära dig om Adobe Experience Platform Mobile SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela dem i det här [Experience League Community-diskussionsinlägget](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Nästa: **[Samla in profildata](profile.md)**
