---
title: Implementera Adobe Experience Cloud i självstudiekursen om mobilappar
description: Lär dig hur du implementerar Adobe Experience Cloud mobilappar. Den här självstudiekursen vägleder dig genom en implementering av Experience Cloud-program i ett exempel på en Swift-app.
recommendations: noDisplay,catalog
last-substantial-update: 2023-11-29T00:00:00Z
exl-id: daff4214-d515-4fad-a224-f7589b685b55
source-git-commit: 0d5914ee0e63719c0439f02a5aa2a1e1c1d11a2f
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 0%

---

# Implementera Adobe Experience Cloud i mobilappar, genomgång

Lär dig hur du implementerar Adobe Experience Cloud-program i din mobilapp med Adobe Experience Platform Mobile SDK.

Experience Platform Mobile SDK är en SDK på klientsidan som gör att kunder i Adobe Experience Cloud kan interagera med både Adobe-program och tredjepartstjänster via Adobe Experience Platform Edge Network. Se [Dokumentation för Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/home/) för mer detaljerad information.

![Arkitektur](assets/architecture.png)


Den här självstudiekursen vägleder dig genom implementeringen av Platform Mobile SDK i ett exempel på en app för återförsäljning som kallas Luma. The [Luma-app](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) har funktioner som gör att du kan bygga en realistisk implementering. När du är klar med den här självstudiekursen bör du vara redo att börja implementera alla marknadsföringslösningar via Experience Platform Mobile SDK i dina egna mobilappar.

Lektionerna är utformade för iOS och skrivna i Swift/SwiftUI, men många av begreppen gäller även för Android™.

När du är klar med självstudiekursen kan du:

* Skapa ett schema med standardfältgrupper och anpassade fältgrupper.
* Konfigurera en datastream.
* Konfigurera en mobil taggegenskap.
* Konfigurera en Experience Platform-datauppsättning (valfritt).
* Installera och implementera taggtillägg i en app.
* skicka Experience Cloud-parametrar korrekt till en [webbvy](web-views.md).
* Validera implementeringen med [Adobe Experience Platform Assurance](assurance.md).
* Lägg till följande Adobe Experience Cloud-program/tillägg:
   * [Adobe Experience Platform Edge (XDM)](events.md)
   * [Samling av livscykeldata](lifecycle-data.md)
   * [Godkännande](consent.md)
   * [Identitet](identity.md)
   * [Profil](profile.md)
   * [Platser](places.md)
   * [Analytics ](analytics.md)
   * [Experience Platform](platform.md)
   * [Skicka meddelanden med Journey Optimizer](journey-optimizer-push.md)
   * [Meddelanden i appen med Journey Optimizer](journey-optimizer-inapp.md)
   * [Beslutshantering med Journey Optimizer](journey-optimizer-offers.md)
   * [Target](target.md)


>[!NOTE]
>
>En liknande självstudiekurs om flera lösningar finns tillgänglig för [Web SDK](../tutorial-web-sdk/overview.md).

## Förutsättningar

I den här lektionen antas du ha ett Adobe-ID och de användarbehörigheter som krävs för att slutföra övningarna. Om du inte gör det bör du kontakta din Adobe-administratör för att begära åtkomst.

* I Datainsamling måste du ha:
   * **[!UICONTROL Plattformar]**—behörighetsobjekt **[!UICONTROL Mobil]**
   * **[!UICONTROL Egendomsrättigheter]**—behörighetsobjekt till **[!UICONTROL Utveckla]**, **[!UICONTROL Godkänn]**, **[!UICONTROL Publicera]**, **[!UICONTROL Hantera tillägg]** och **[!UICONTROL Hantera miljöer]**.
   * **[!UICONTROL Företagsrättigheter]**—behörighetsobjekt till **[!UICONTROL Hantera egenskaper]** och om du slutför den valfria push-meddelandelektionen, **[!UICONTROL Hantera appkonfigurationer]**

     Mer information om taggbehörigheter finns i [Användarbehörigheter för taggar](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html?lang=en){target="_blank"} i produktdokumentationen.
* I Experience Platform måste du ha:
   * **[!UICONTROL Datamodellering]**—behörighetsobjekt för att hantera och visa scheman.
   * **[!UICONTROL Identity Management]**—behörighetsobjekt för att hantera och visa identitetsnamnutrymmen.
   * **[!UICONTROL Datainsamling]**—behörighetsobjekt för att hantera och visa dataströmmar.

   * Om du använder en plattformsbaserad applikation som Real-Time CDP, Journey Optimizer eller Customer Journey Analytics, och kommer att göra de lektioner du behöver:
      * **[!UICONTROL Datahantering]**—behörighetsobjekt för att hantera och visa datauppsättningar.
      * En utveckling **sandlåda** som du kan använda för den här självstudiekursen.

   * För Journey Optimizer lektioner behöver du behörighet att konfigurera **push-meddelandetjänst** och skapa en **appyta**, a **resa**, a **message** och **meddelandeförinställningar**. För Beslutshantering behöver du rätt behörighet för att **hantera erbjudanden** och **beslut** enligt beskrivning [här](https://experienceleague.adobe.com/docs/journey-optimizer/using/access-control/privacy/high-low-permissions.html?lang=en#decisions-permissions).

* För Adobe Analytics måste du veta vilken **rapportsviter** du kan använda för att slutföra den här självstudiekursen.

* För Adobe Target måste du ha behörighet att skapa och aktivera aktiviteter.


>[!NOTE]
>
>Som en del av den här självstudiekursen skapar du scheman, datauppsättningar, identiteter och så vidare. Om flera personer går igenom den här självstudiekursen i en enda sandlåda bör du överväga att lägga till eller föregå en identifiering som en del av namnkonventionen när du skapar dessa objekt. Lägg till exempel ` - <your name or initials>` till namnet på det objekt som du ska skapa.

## Versionshantering

* 29 november 2023: Större översyn med nya exempelappar och nya lektioner för meddelanden i appen, beslutshantering och Adobe Target.
* 9 mars 2022: Första publiceringen

## Hämta Luma-appen

Det finns två versioner av exempelappen att hämta. Båda versionerna kan hämtas/klonas från [Github](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App). Du hittar två mappar:


1. [Starta](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"}: ett projekt utan kod eller med platshållarkod för merparten av SDK-koden för Experience Platform Mobile som du behöver använda för att slutföra övningarna i den här kursen.
1. [Slutför](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"}: en version med fullständig implementering för referens.

>[!NOTE]
>
>Du använder iOS [!DNL Swift] som programmeringsspråk, [!DNL SwiftUI] som gränssnittets ramverk och [!DNL Xcode] som den integrerade utvecklingsmiljön. Många av de implementeringskoncept som beskrivs liknar dock andra utvecklingsplattformar. Många har redan slutfört den här självstudiekursen med lite eller ingen tidigare erfarenhet av iOS/Swift(UI). Du behöver inte vara expert för att slutföra lektionerna, men du får ut mer av lektionerna om du enkelt kan läsa och förstå koden.


Du kan hämta den slutliga versionen av programmet från App Store.

[![Ladda ned](assets/download-app.svg)](https://apps.apple.com/us/app/luma-app/id6466588487)


Kom så börjar vi!

>[!SUCCESS]
>
>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Mobile SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Nästa: **[Skapa ett XDM-schema](create-schema.md)**
