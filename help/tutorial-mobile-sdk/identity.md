---
title: Identitet
description: Lär dig hur du samlar in identitetsdata i en mobilapp.
exl-id: cbcd1708-29e6-4d74-be7a-f75c917ba2fa
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 0%

---

# Identitet

Lär dig hur du samlar in identitetsdata i en mobilapp.

Adobe Experience Platform identitetstjänst hjälper er att få en bättre bild av era kunder och deras beteenden genom att överbrygga identiteter mellan olika enheter och system, så att ni kan leverera slagkraftiga, personliga digitala upplevelser i realtid. Identitetsfält och namnutrymmen är den kombination som förenar olika datakällor för att skapa en 360-graders kundprofil i realtid.

Läs mer om [Identitetstillägg](https://aep-sdks.gitbook.io/docs/foundation-extensions/identity-for-edge-network) och [identitetstjänst](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=en) i dokumentationen.

## Förutsättningar

* Programmet har skapats och körts med SDK:er installerade och konfigurerade.

## Utbildningsmål

I den här lektionen kommer du att:

* Uppdatera en standardidentitet.
* Konfigurera en anpassad identitet.
* Uppdatera en anpassad identitet.
* Validera identitetsdiagrammet.
* Hämta ECID och andra identiteter.

## Uppdatera en standardidentitet

Börja med att uppdatera användarens identitetskarta när användaren loggar in.

1. Navigera till `Login.swift` om Luma-appen och söker efter funktionen som anropas `loginButt`.

   I Luma-exempelappen finns ingen validering av användarnamn eller lösenord. Tryck bara på knapparna för att logga in.

1. Skapa `IdentityMap` och `IdentityItem`.

   ```swift
   let identityMap: IdentityMap = IdentityMap()
   let emailIdentity = IdentityItem(id: emailAddress, authenticatedState: AuthenticatedState.authenticated)
   ```

1. Lägg till `IdentityItem` till `IdentityMap`

   ```swift
   identityMap.add(item:emailIdentity, withNamespace: "Email")
   ```

1. Utlysning `updateIdentities` för att skicka data till Platform Edge Network.

   ```swift
   Identity.updateIdentities(with: identityMap)
   ```

>[!NOTE]
>
>Du kan skicka flera identiteter i ett enda updateIdentities-anrop. Du kan också ändra identiteter som du tidigare skickat.


## Konfigurera ett anpassat ID-namnutrymme

Identitetsnamnutrymmen är komponenter i [Identitetstjänst](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=en) som fungerar som indikatorer för det sammanhang som en identitet hör till. De skiljer till exempel på värdet&quot;name@email.com&quot; som e-postadress eller&quot;443522&quot; som ett numeriskt CRM-ID.

1. I gränssnittet för datainsamling väljer du **[!UICONTROL Identiteter]** från vänster-rälsnavigering.
1. Välj **[!UICONTROL Skapa namnutrymme för identitet]**.
1. Ange en **[!UICONTROL Visningsnamn]** av `Luma CRM ID` och **[!UICONTROL Identitetssymbol]** värde för `lumaCrmId`.
1. Välj **[!UICONTROL Enhetsoberoende ID]**.
1. Välj **[!UICONTROL Skapa]**.

![skapa namnutrymme för identitet](assets/mobile-identity-create.png)

## Uppdatera en anpassad identitet

Nu när du har skapat en anpassad identitet börjar du samla in den genom att ändra `updateIdentities` kod som du lade till i föregående steg. Skapa bara ett IdentityItem och lägg till det i IdentityMap. Så här ska hela kodblocket se ut:

```swift
//Hardcoded identity values
let emailAddress = "testuser@gmail.com"
let crmId = "112ca06ed53d3db37e4cea49cc45b71e"

// Create identity map
let identityMap: IdentityMap = IdentityMap()
// Add email (standard)
let emailIdentity = IdentityItem(id: emailAddress, authenticatedState: AuthenticatedState.authenticated)
identityMap.add(item:emailIdentity, withNamespace: "Email")
// Add lumaCrmId (custom)
let crmIdentity = IdentityItem(id: crmId, authenticatedState: AuthenticatedState.authenticated)
identityMap.add(item: crmIdentity, withNamespace: "lumaCrmId")
// Update
Identity.updateIdentities(with: identityMap)
```

## Ta bort en identitet

Du kan använda `removeIdentity` för att ta bort identiteten från den lagrade identitetsmappningen på klientsidan. Identitetstillägget slutar skicka identifieraren till Edge Network. Om du använder detta API tas inte identifieraren bort från användarprofildiagrammet eller identitetsdiagrammet på serversidan.

Lägg till följande `removeIdentity` kod till utloggningsknappen klicka på `Account.swift`.

```swift
// Logout
let logout = UIAlertAction(title: "Logout", style: .destructive, handler: { (action) -> Void in
    isLoggedIn = false;
    ////Hardcoded identity values
    let emailAddress = "testuser@gmail.com"
    let crmId = "112ca06ed53d3db37e4cea49cc45b71e"
    // Adobe Experience Platform - Remove Identity
    Identity.removeIdentity(item: IdentityItem(id: emailAddress), withNamespace: "Email")
    Identity.removeIdentity(item: IdentityItem(id: crmId), withNamespace: "lumaCrmId")
})
```

>[!NOTE]
>I exemplen ovan `crmId` och `emailAddress` är hårdkodade, men i ett verkligt program skulle värdena vara dynamiska.

## Validera med Assurance

1. Granska [installationsanvisningar](assurance.md) och koppla simulatorn eller enheten till Assurance.
1. I appen väljer du kontoikonen längst ned till höger.

   ![appkonto för luma](assets/mobile-identity-login.png)
1. Välj **Logga in** -knappen.
1. Du får möjlighet att ange användarnamn och lösenord, båda är valfria och du kan enkelt välja **Logga in**.

   ![inloggning för lumatapp](assets/mobile-identity-login-final.png)
1. Leta i webbgränssnittet för Assurance efter `Edge Identity Update Identities` från `com.adobe.griffon.mobile` leverantör.
1. Markera händelsen och granska data i `ACPExtensionEventData` -objekt. Du bör se de identiteter som du har uppdaterat.
   ![validera identitetsuppdatering](assets/mobile-identity-validate-assurance.png)

## Validera med identitetsdiagram

När du är klar med stegen i [Experience Platform lektion](platform.md)kan du även bekräfta det inspelade inslaget i visningsprogrammet för plattformsidentitetsdiagram:

![validera identitetsdiagram](assets/mobile-identity-validate.png)


Nästa: **[Profil](profile.md)**

>[!NOTE]
>
>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Mobile SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela med dig av dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)