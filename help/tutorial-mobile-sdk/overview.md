---
title: Implementera Adobe Experience Cloud i självstudiekursen om mobilappar
description: Lär dig hur du implementerar Adobe Experience Cloud mobilappar. I den här självstudiekursen får du hjälp med att implementera Experience Cloud-program i ett exempel på en Swift-app.
recommendations: noDisplay,catalog
exl-id: daff4214-d515-4fad-a224-f7589b685b55
source-git-commit: 4bccc95ff94e9377b65771268e82b1900c003fc1
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 1%

---

# Implementera Adobe Experience Cloud i mobilappar, genomgång

Lär dig hur du implementerar Adobe Experience Cloud-program i din mobilapp med Adobe Experience Platform Mobile SDK.

Experience Platform Mobile SDK är en SDK på klientsidan som gör att kunder i Adobe Experience Cloud kan interagera med både Adobe-program och tredjepartstjänster via Adobe Experience Platform Edge Network. Se [Dokumentation för Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/) för mer detaljerad information.

![bygginställningar](assets/data-collection-mobile-sdk.png)


Den här självstudiekursen vägleder dig genom implementeringen av Platform Mobile SDK i ett exempel på en app för återförsäljning som kallas Luma. The [Luma-app](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) har funktioner som gör att du kan bygga en realistisk implementering. När du är klar med den här självstudiekursen bör du vara redo att börja implementera alla era marknadsföringslösningar via Platform Mobile SDK i dina egna mobilappar.

Lektionerna är utformade för iOS och skrivna i Swift, men många av begreppen gäller även för Android™.

När du är klar med den här självstudiekursen kan du:

* Skapa ett schema med standardfältgrupper och anpassade fältgrupper.
* Konfigurera en datastream.
* Konfigurera en mobil taggegenskap.
* Konfigurera en Experience Platform-datauppsättning (valfritt).
* Installera och implementera taggtillägg i en app.
* Lägg till följande Adobe Experience Cloud-program/tillägg:
   * [Adobe Experience Platform Edge (XDM)](events.md)
   * [Samling av livscykeldata](lifecycle-data.md)
   * [Adobe Analytics via XDM](analytics.md)
   * [Godkännande](consent.md)
   * [Identitet](identity.md)
   * [Profil](profile.md)
   * [Adobe Experience Platform](platform.md)
   * [Skicka meddelanden med Journey Optimizer](journey-optimizer-push.md)
* Korrekt skicka Experience Cloud-parametrar till en [webbvy](web-views.md).
* Validera implementeringen med [Adobe Experience Platform Assurance](assurance.md).

>[!NOTE]
>
>En liknande självstudiekurs om flera lösningar finns tillgänglig för [Web SDK](../tutorial-web-sdk/overview.md).

## Förutsättningar

I den här lektionen antas du ha ett Adobe-ID och de behörigheter som krävs för att slutföra övningarna. Om du inte gör det bör du kontakta din Adobe-administratör för att begära åtkomst.

* I Datainsamling måste du ha:
   * **[!UICONTROL Plattformar]**—behörighetsobjekt **[!UICONTROL Mobil]**
   * **[!UICONTROL Egendomsrättigheter]**—behörighetsobjekt till **[!UICONTROL Utveckla]**, **[!UICONTROL Godkänn]**, **[!UICONTROL Publicera]**, **[!UICONTROL Hantera tillägg]** och **[!UICONTROL Hantera miljöer]**.
   * **[!UICONTROL Företagsrättigheter]**—behörighetsobjekt till **[!UICONTROL Hantera egenskaper]** och, om du slutför den valfria push-meddelandelektionen, **[!UICONTROL Hantera appkonfigurationer]**

      Mer information om taggbehörigheter finns i [Användarbehörigheter för taggar](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html?lang=en){target="_blank"} i produktdokumentationen.
* I Experience Platform måste du ha:
   * **[!UICONTROL Datamodellering]**—behörighetsobjekt för att hantera och visa scheman.
   * **[!UICONTROL Identity Management]**—behörighetsobjekt för att hantera och visa identitetsnamnutrymmen.
   * **[!UICONTROL Datainsamling]**—behörighetsobjekt för att hantera och visa dataströmmar.

   * Om du använder ett plattformsbaserat program som Real-Time CDP, Journey Optimizer eller Customer Journey Analytics bör du även ha:
      * **[!UICONTROL Datahantering]**—behörighetsobjekt som ska hantera och visa datauppsättningar för att slutföra _valfria plattformsövningar_ (kräver en licens för ett plattformsbaserat program).
      * En utveckling **sandlåda** som du kan använda för den här självstudiekursen.
* För Adobe Analytics måste du veta vilken **rapportsviter** du kan använda för att slutföra den här självstudiekursen.

Alla Experience Cloud-kunder bör ha tillgång till de funktioner som krävs för att driftsätta Mobile SDK.

Du måste också känna till [!DNL Swift]. Du behöver inte vara expert för att slutföra lektionerna, men du får ut mer av dem om du enkelt kan läsa och förstå koden.

## Ladda ned Luma-appen

Det finns två versioner av exempelappen att hämta.

1. [Tom](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"} - version utan Experience Cloud-kod för att slutföra övningarna i kursen
1. [Fullt implementerad](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"} - version med fullständig Experience Cloud-implementering som referens.

Kom så börjar vi!


Nästa: **[Skapa ett XDM-schema](create-schema.md)**

>[!NOTE]
>
>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Mobile SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela med dig av dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)