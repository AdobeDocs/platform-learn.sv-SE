---
title: Skapa identiteter
description: Lär dig hur du skapar identiteter i XDM och använder dataelementet Identitetskarta för att hämta användar-ID:n. Den här lektionen ingår i självstudiekursen Implementera Adobe Experience Cloud med Web SDK.
feature: Tags
source-git-commit: f08866de1bd6ede50bda1e5f8db6dbd2951aa872
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 0%

---

# Skapa identiteter

Lär dig hur du fångar identiteter med Experience Platform Web SDK. Samla in både oautentiserade och autentiserade identitetsdata på [Luma demo site](https://luma.enablementadobe.com/content/luma/us/en.html). Lär dig hur du använder dataelementen som du skapade tidigare för att samla in autentiserade data med datatypen Platform Web SDK som kallas identitetskarta.

Det finns fyra nya typer av dataelement som introduceras av plattformens SDK-taggtillägg:

1. ID för händelsesammanslagning
1. Identitetskarta
1. Variabel
1. XDM-objekt

Den här lektionen fokuserar på dataelementet för identitetskartan. Du mappar dataelement som innehåller ett autentiserat användar-ID och autentiseringsstatus till XDM.

## Utbildningsmål

När lektionen är slut kan du:

* Förstå skillnaden mellan Experience Cloud ID (ECID) och ID för förstahandsenhet
* Förstå skillnaden mellan oautentiserade och autentiserade ID:n
* Skapa ett dataelement för identitetskarta

## Förutsättningar

Du har en förståelse för vad ett datalager är, och vet hur det [Luma demo site](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} datalager och veta hur du refererar till dataelement i taggar. Du måste ha utfört följande steg i självstudien:

* [Konfigurera ett XDM-schema](configure-schemas.md)
* [Konfigurera ett identitetsnamnutrymme](configure-identities.md)
* [Konfigurera ett datastream](configure-datastream.md)
* [Web SDK-tillägget är installerat i taggegenskapen](install-web-sdk.md)
* [Skapa dataelement](create-data-elements.md)

>[!IMPORTANT]
>
>The [Experience Cloud ID-tjänsttillägg](https://exchange.adobe.com/experiencecloud.details.100160.adobe-experience-cloud-id-launch-extension.html) behövs inte vid implementering av Adobe Experience Platform Web SDK eftersom ID-tjänstfunktionen är inbyggd i Platform Web SDK.

## EXPERIENCE CLOUD ID

The [Experience Cloud ID (ECID)](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=en) är ett delat ID-namnutrymme som används i Adobe Experience Platform- och Adobe Experience Cloud-program. ECID utgör grunden för kundidentiteten och är standardidentitet för digitala resurser. Detta gör ECID till den idealiska identifieraren för att spåra oautentiserade användarbeteenden eftersom det alltid finns.


<!-- FYI I commented this out because it was breaking the build - Jack
>[!TIP]
>
> When you use the Experience Platform Web SDK to set up Adobe applications on your digital properties, the ECID is generated at the Adobe Edge server level. As such, ECID is not viewable on the client-side network request payload. You can view the ECID by seeing the Preview tab of the network request, or by using the [Adobe Experience Platform Debugger Edge Trace](set-up-analytics.md#experience-cloud-id-validation).
>![View ECID](assets/validate-dev-console-ecid.png)
-->

Läs mer om hur [ECID:n spåras med Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en).

ECID anges med en kombination av cookies från första part och Platform Edge Network. Som standard anges cookies från första part av Web SDK. Om du vill ta hänsyn till webbläsarbegränsningar för cookies kan du välja att ställa in och hantera dina egna cookies från första part i stället. Dessa kallas för FPID (First-party device ID).

## FPID (First Party Device ID)

FPID är cookies från första part _du använder dina egna webbservrar_ som Adobe sedan använder för att ställa in ECID, i stället för att använda cookie-filen från Web SDK. Första parts-cookies är mest effektiva när de ställs in med en server som använder en DNS A-post (för IPv4) eller en AAAA-post (för IPv6), i motsats till en DNS CNAME- eller JavaScript-kod.

När en FPID-cookie har angetts kan dess värde hämtas och skickas till Adobe när händelsedata samlas in. Insamlade FPID används som startvärde för att generera ECID på Platform Edge Network, som även i fortsättningen är standardidentifierare i Adobe Experience Cloud-program.

Läs mer om [Första parts enhets-ID i Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/first-party-device-ids.html?lang=en)

>[!CAUTION]
>
> FPID är ett alternativt sätt att generera ECID genom att använda en cookie som angetts av webbservrarna. Det används inte för att identifiera autentiserade användare.

## Autentiserat ID

Som nämnts ovan tilldelas alla besökare av dina digitala resurser ett ECID av Adobe när de använder Platform Web SDK. Detta gör ECID till standardidentitet för att spåra oautentiserat digitalt beteende.

Du kan också skicka ett autentiserat användar-ID så att plattformen kan skapa [Identitetsdiagram](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/understanding-identity-and-identity-graphs.html?lang=en), kan Target ange sin tredje part. Detta görs genom att använda [!UICONTROL Identitetskarta] dataelementtyp.

Skapa [!UICONTROL Identitetskarta] dataelement:

1. Gå till **[!UICONTROL Dataelement]** och markera **[!UICONTROL Lägg till dataelement]**

1. **[!UICONTROL Namn]** dataelementet `identityMap.loginID`

1. Som **[!UICONTROL Tillägg]**, markera `Adobe Experience Platform Web SDK`

1. Som **[!UICONTROL Dataelementtyp]**, markera `Identity map`

1. Då visas ett skärmyta till höger i dialogrutan **[!UICONTROL Gränssnitt för datainsamling]** för att konfigurera identiteten:

   ![Gränssnitt för datainsamling](assets/identity-identityMap-setup.png)

1. Som  **[!UICONTROL Namnutrymme]** väljer du `lumaCrmId` namnutrymme som du tidigare skapade i [Konfigurera identiteter](configure-identities.md) lektion.

   >[!NOTE]
   >
   >    Om du inte ser dina `lumaCrmId` namnutrymme kontrollerar du att du även har skapat det i din standardproduktionssandlåda. Endast namnutrymmen som skapats i standardproduktionssandlådan visas för närvarande i listrutan för namnutrymme.

1. Efter **[!UICONTROL Namnutrymme]** är markerat måste ett ID anges. Välj `user.profile.attributes.username` dataelement som skapades tidigare i [Skapa dataelement](create-data-elements.md#create-data-elements-to-capture-the-data-layer) lektion, som hämtar ett ID när användare loggar in på Luma-webbplatsen.

   <!--  >[!TIP]
    >
    >You can verify the **[!UICONTROL Luma CRM ID]** is collected in a data element on the web property by going to the [Luma Demo site](https://luma.enablementadobe.com/content/luma/us/en.html), logging in, [switching the tag environment](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tag-property) to your own, and typing `_satellite.getVar("user.profile.attributes.username")` in the web browser developer console.
    >
    >   ![Data Element  ID ](assets/identity-data-element-customer-id.png)
    -->

1. Som **[!UICONTROL Autentiserat läge]**, markera **[!UICONTROL Autentiserad]**
1. Välj **[!UICONTROL Primär]**

1. Välj **[!UICONTROL Spara]**

   ![Gränssnitt för datainsamling](assets/identity-id-namespace.png)

>[!TIP]
>
> Adobe rekommenderar att du skickar identiteter som representerar en person, till exempel `Luma CRM Id`, som [!UICONTROL primär] identitet.
>
> Om identitetskartan innehåller personidentifieraren (t.ex. `Luma CRM Id`) blir personidentifieraren [!UICONTROL primär] identitet. I annat fall `ECID` blir [!UICONTROL primär] identitet.




<!--
1. Once the data element is configured in **[!UICONTROL Data Collection interface]**, it can be tested on the Luma web property like any other Data Element. Enter the following script in the browser developer console
   
   
   ```
   _satellite.getVar('identityMap.loginID')
   ```  

   ![Data Collection interface](assets/identity-consoleIdentityDataElement.png)
   
   >[!NOTE]
   >
   >ECID identifier will NOT populate in the Data Element, as this is configured already with Platform Web SDK.   
-->

I slutet av dessa steg bör du skapa följande dataelement:

| CORE-tilläggsdataelement | Webbsidedataelement för plattforms-SDK |
-----------------------------|-------------------------------
| `cart.orderId` | `identityMap.loginID` |
| `page.pageInfo.hierarchie1` | `xdm.variable.content` |
| `page.pageInfo.pageName` | |
| `page.pageInfo.server` | |
| `user.profile.attributes.loggedIn` | |
| `user.profile.attributes.username` | |

Med dessa dataelement på plats är du redo att börja skicka data till Platform Edge Network via XDM-objektet genom att skapa en regel i taggar.

[Nästa: ](create-tag-rule.md)

>[!NOTE]
>
>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Web SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela med dig av dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
