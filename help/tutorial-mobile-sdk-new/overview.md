---
title: Implementera Adobe Experience Cloud i självstudiekursen om mobilappar
description: Lär dig hur du implementerar Adobe Experience Cloud mobilappar. Den här självstudiekursen vägleder dig genom en implementering av Experience Cloud-program i ett exempel på en Swift-app.
recommendations: noDisplay,catalog
hide: true
source-git-commit: a2788110b1c43d24022672bb5ba0f36af66d962b
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 1%

---

# Implementera Adobe Experience Cloud i mobilappar, genomgång

Lär dig hur du implementerar Adobe Experience Cloud-program i din mobilapp med Adobe Experience Platform Mobile SDK.

Experience Platform Mobile SDK är en SDK på klientsidan som gör att kunder i Adobe Experience Cloud kan interagera med både Adobe-program och tredjepartstjänster via Adobe Experience Platform Edge Network. Se [Dokumentation för Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/) för mer detaljerad information.

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
   * [Adobe Experience Platform](platform.md)
   * [Skicka meddelanden med Journey Optimizer](journey-optimizer-push.md)
   * [Meddelanden i appen med Journey Optimizer](journey-optimizer-inapp.md)
   * [Erbjudanden med Journey Optimizer](journey-optimizer-offers.md)
   * [A/B-tester med Target](target.md)


>[!NOTE]
>
>En liknande självstudiekurs om flera lösningar finns tillgänglig för [Web SDK](../tutorial-web-sdk/overview.md).

## Förutsättningar

I den här lektionen antas du ha ett Adobe-ID och de behörigheter som krävs för att slutföra övningarna. Om du inte gör det bör du kontakta din Adobe-administratör för att begära åtkomst.

* I Datainsamling måste du ha:
   * **[!UICONTROL Plattformar]**—behörighetsobjekt **[!UICONTROL Mobil]**
   * **[!UICONTROL Egendomsrättigheter]**—behörighetsobjekt till **[!UICONTROL Utveckla]**, **[!UICONTROL Godkänn]**, **[!UICONTROL Publicera]**, **[!UICONTROL Hantera tillägg]** och **[!UICONTROL Hantera miljöer]**.
   * **[!UICONTROL Företagsrättigheter]**—behörighetsobjekt till **[!UICONTROL Hantera egenskaper]** och om du slutför den valfria push-meddelandelektionen, **[!UICONTROL Hantera appkonfigurationer]**

     Mer information om taggbehörigheter finns i [Användarbehörigheter för taggar](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html?lang=en){target="_blank"} i produktdokumentationen.
* I Experience Platform måste du ha:
   * **[!UICONTROL Datamodellering]**—behörighetsobjekt för att hantera och visa scheman.
   * **[!UICONTROL Identity Management]**—behörighetsobjekt för att hantera och visa identitetsnamnutrymmen.
   * **[!UICONTROL Datainsamling]**—behörighetsobjekt för att hantera och visa dataströmmar.

   * Om du använder ett plattformsbaserat program som Real-Time CDP, Journey Optimizer eller Customer Journey Analytics bör du även ha:
      * **[!UICONTROL Datahantering]**—behörighetsobjekt som ska hantera och visa datauppsättningar för att slutföra _valfria plattformsövningar_ (kräver en licens för ett plattformsbaserat program).
      * En utveckling **sandlåda** som du kan använda för den här självstudiekursen.

* För Adobe Analytics måste du veta vilken **rapportsviter** du kan använda för att slutföra den här självstudiekursen.

* För Adobe Target måste du ha behörighet, korrekt konfigurerad **roller**, **arbetsytor** och **egenskaper** enligt beskrivning [här](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=en).

* För Adobe Journey Optimizer måste du ha tillräcklig behörighet för att konfigurera **push-meddelandetjänst** och skapa en **appyta**, a **resa**, a **message** och **meddelandeförinställningar**. För Beslutshantering behöver du rätt behörighet för att **hantera erbjudanden** och **beslut** enligt beskrivning [här](https://experienceleague.adobe.com/docs/journey-optimizer/using/access-control/privacy/high-low-permissions.html?lang=en#decisions-permissions).

Alla Experience Cloud-kunder bör ha tillgång till de funktioner som krävs för att driftsätta Mobile SDK.


>[!NOTE]
>
>I den här självstudiekursen skapar du scheman, datauppsättningar, identiteter osv. Om du går igenom den här självstudiekursen med flera personer i en och samma sandlåda, eller om du använder ett delat konto, bör du överväga att lägga till eller föregå en identifiering som en del av namnkonventionen när du skapar dessa objekt. Lägg till exempel ` - <your name or initials>` till namnet på det objekt som du ska skapa.


## Hämta Luma-appen

Det finns två versioner av exempelappen att hämta. Båda versionerna kan hämtas/klonas från [Github](https://git.corp.adobe.com/rmaur/Luma). Du hittar två mappar:


1. [Starta](https://git.corp.adobe.com/rmaur/Luma){target="_blank"}: ett projekt utan kod eller med platshållarkod för merparten av SDK-koden för Experience Platform Mobile som du behöver använda för att slutföra övningarna i den här kursen.
1. [Slutför](https://git.corp.adobe.com/Luma){target="_blank"}: en version med fullständig implementering för referens.

>[!NOTE]
>
>Du kommer att använda iOS som plattform [!DNL Swift] som programmeringsspråk, [!DNL SwiftUI] som gränssnittets ramverk och [!DNL Xcode] som den integrerade utvecklingsmiljön. Många av de implementeringskoncept som beskrivs liknar dock andra utvecklingsplattformar. Och många har redan slutfört den här självstudiekursen så lite som till ingen tidigare erfarenhet av iOS/Swift(UI). Du behöver inte vara expert för att slutföra lektionerna, men du får ut mer av lektionerna om du enkelt kan läsa och förstå koden.


Kom så börjar vi!

>[!SUCCESS]
>
>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Mobile SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Nästa: **[Skapa ett XDM-schema](create-schema.md)**
