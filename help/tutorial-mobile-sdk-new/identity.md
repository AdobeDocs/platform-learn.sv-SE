---
title: Identitet
description: Lär dig hur du samlar in identitetsdata i en mobilapp.
feature: Mobile SDK,Identities
hide: true
hidefromtoc: true
source-git-commit: ca83bbb571dc10804adcac446e2dba4fda5a2f1d
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 1%

---

# Identitet

Lär dig hur du samlar in identitetsdata i en mobilapp.

Adobe Experience Platform identitetstjänst hjälper er att få en bättre bild av era kunder och deras beteenden genom att överbrygga identiteter mellan olika enheter och system, så att ni kan leverera slagkraftiga, personliga digitala upplevelser i realtid. Identitetsfält och namnutrymmen är den kombination som förenar olika datakällor för att skapa en 360-graders kundprofil i realtid.

Läs mer om [Identitetstillägg](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/) och [identitetstjänst](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=sv) i dokumentationen.

## Förutsättningar

* App med SDK:er har installerats och konfigurerats.

## Utbildningsmål

I den här lektionen kommer du att:

* Konfigurera ett anpassat ID-namnutrymme.
* Uppdatera identiteter.
* Validera identitetsdiagrammet.
* Hämta ECID och andra identiteter.


## Konfigurera ett anpassat ID-namnutrymme

Identitetsnamnutrymmen är komponenter i [Identitetstjänst](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=en) som fungerar som indikatorer för det sammanhang som en identitet hör till. De skiljer till exempel på värdet `name@email.com` som e-postadress eller `443522` som ett numeriskt CRM-ID.

1. I gränssnittet för datainsamling väljer du **[!UICONTROL Identiteter]** från vänster-rälsnavigering.
1. Välj **[!UICONTROL Skapa namnutrymme för identitet]**.
1. Ange en **[!UICONTROL Visningsnamn]** av `Luma CRM ID` och **[!UICONTROL Identitetssymbol]** värde för `lumaCRMId`.
1. Välj **[!UICONTROL Enhetsoberoende ID]**.
1. Välj **[!UICONTROL Skapa]**.

   ![skapa namnutrymme för identitet](assets/identity-create.png)




## Uppdatera identiteter

Du vill uppdatera både standardidentiteten (e-post) och den anpassade identiteten (Luma CRM ID) när användaren loggar in i programmet.

1. Navigera till **[!UICONTROL LoginSheet]** (in **[!UICONTROL Vyer]** > **[!UICONTROL Allmänt]**) i Xcode Luma-appprojektet och hitta `updateIdentities`:

   ```swift {highlight="3,4"}
   Button("Login") {
       // call updaeIdentities
       MobileSDK.shared.updateIdentities(emailAddress: currentEmailId, crmId: currentCRMId)
   
       // Send app interaction event
       MobileSDK.shared.sendAppInteractionEvent(actionName: "login")
       dismiss()
   }
   .disabled(currentEmailId.isValidEmail == false)
   .buttonStyle(.bordered)
   ```

1. Navigera till `updateIdentities` funktionsimplementering i **[!UICONTROL MobileSDK]** (in **[!UICONTROL Utils]**) i Xcode Luma-appprojektet. Lägg till följande markerade kod i funktionen.

   ```swift {highlight="2-12"}
   func updateIdentities(emailAddress: String, crmId: String) {
       let identityMap: IdentityMap = IdentityMap()
       // Add identity items
       let emailIdentity = IdentityItem(id: emailAddress, authenticatedState: AuthenticatedState.authenticated)
       let crmIdentity = IdentityItem(id: crmId, authenticatedState: AuthenticatedState.authenticated)
       identityMap.add(item:emailIdentity, withNamespace: "Email")
       identityMap.add(item: crmIdentity, withNamespace: "lumaCRMId")
   
       // Update identities
       Identity.updateIdentities(with: identityMap)
   }
   ```

   Den här koden:

   1. Skapar en tom `IdentityMap` -objekt.

      ```swift
      let identityMap: IdentityMap = IdentityMap()
      ```

   1. Inställningar `IdentityItem` objekt för e-post och CRM-ID.

      ```swift
      let emailIdentity = IdentityItem(id: emailAddress, authenticatedState: AuthenticatedState.authenticated)
      let crmIdentity = IdentityItem(id: crmId, authenticatedState: AuthenticatedState.authenticated)
      ```

   1. Lägger till dessa `IdentityItem` objekt till `IdentityMap` -objekt.

      ```swift
      identityMap.add(item:emailIdentity, withNamespace: "Email")
      identityMap.add(item: crmIdentity, withNamespace: "lumaCRMId")
      ```

   1. Skickar `IdentityItem` objektet som en del av `Identity.updateIdentities` API-anrop till Edge Network.

      ```swift
      Identity.updateIdentities(with: identityMap) 
      ```


>[!NOTE]
>
>Du kan skicka flera identiteter i en enda `updateIdentities` ring. Du kan också ändra identiteter som du tidigare skickat.


## Ta bort en identitet

Du kan använda `removeIdentity` för att ta bort identiteten från den lagrade identitetsmappningen på klientsidan. Identitetstillägget slutar skicka identifieraren till Edge Network. Om du använder detta API tas inte identifieraren bort från användarprofildiagrammet eller identitetsdiagrammet på serversidan.

1. Navigera till **[!UICONTROL LoginSheet]** (in **[!UICONTROL Vyer]** > **[!UICONTROL Allmänt]**) i Xcode Luma-appprojektet och hitta `removeIdentities`:

   ```swift {highlight="3"}
   Button("Logout", role: .destructive) {
       // call removeIdentities
       MobileSDK.shared.removeIdentities(emailAddress: currentEmailId, crmId: currentCRMId)
       dismiss()                   
   }
   .buttonStyle(.bordered)
   ```

1. Lägg till följande kod i `removeIdentities` function in `MobileSDK`:

   ```swift {highlight="2-8"}
   func removeIdentities(emailAddress: String, crmId: String) {
       Identity.removeIdentity(item: IdentityItem(id: emailAddress), withNamespace: "Email")
       Identity.removeIdentity(item: IdentityItem(id: crmId), withNamespace: "lumaCRMId")
       // reset email and CRM Id to their defaults
       currentEmailId = "testUser@gmail.com"
       currentCRMId = "112ca06ed53d3db37e4cea49cc45b71e"
   }
   ```


## Validera med Assurance

1. Granska [installationsanvisningar](assurance.md) och koppla simulatorn eller enheten till Assurance.
1. I Luma-appen
   1. Välj **[!UICONTROL Startsida]** -fliken.
   1. Välj **[!UICONTROL Inloggning]** ikonen längst upp till höger.
   1. Ange en e-postadress och ett CRM-ID, eller
   1. Välj A| om du vill generera ett slumpmässigt **[!UICONTROL E-post]** och **[!UICONTROL CRM-ID]**.
   1. Välj **[!UICONTROL Inloggning]**.

      <img src="./assets/identity1.png" width="300"> <img src="./assets/identity2.png" width="300">


1. Leta i webbgränssnittet för Assurance efter **[!UICONTROL Edge Identity Update Identities]**event från **[!UICONTROL com.adobe.griffon.mobile]** leverantör.
1. Markera händelsen och granska data i **[!UICONTROL ACPExtensionEventData]** -objekt. Du bör se de identiteter som du har uppdaterat.
   ![validera identitetsuppdatering](assets/identity-validate-assurance.png)

## Validera med identitetsdiagram

När du är klar med stegen i [Experience Platform lektion](platform.md)kan du bekräfta infångningen i visningsprogrammet för plattformsidentitetsdiagram:

1. Välj **[!UICONTROL Identiteter]** i användargränssnittet för datainsamling.
1. Välj **[!UICONTROL Identitetsdiagram]** i det övre fältet.
1. Retur `Luma CRM ID` som **[!UICONTROL Namnutrymme för identitet]** och ditt CRM-ID (till exempel `24e620e255734d8489820e74f357b5c8`) som **[!UICONTROL Identitetsvärde]**.
1. Du ser **[!UICONTROL Identiteter]** listas.

   ![validera identitetsdiagram](assets/identity-validate-graph.png)


>[!SUCCESS]
>
>Du har nu konfigurerat din app för att uppdatera identiteter i Edge Network och (när den har konfigurerats) med Adobe Experience Platform.<br/>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Mobile SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Nästa: **[Profil](profile.md)**
