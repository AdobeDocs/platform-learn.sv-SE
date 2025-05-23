---
title: Skapa identiteter för Platform Web SDK
description: Lär dig hur du skapar identiteter i XDM och använder dataelementet Identitetskarta för att hämta användar-ID:n. Den här lektionen ingår i självstudiekursen Implementera Adobe Experience Cloud med Web SDK.
feature: Web SDK, Tags, Identities
jira: KT-15402
exl-id: 7ca32dc8-dd86-48e0-8931-692bcbb2f446
source-git-commit: a8431137e0551d1135763138da3ca262cb4bc4ee
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 0%

---

# Skapa identiteter

Lär dig hur du fångar identiteter med Adobe Experience Platform Web SDK. Hämta både oautentiserade och autentiserade identitetsdata på [demowebbplatsen för Luma](https://luma.enablementadobe.com/content/luma/us/en.html). Lär dig hur du använder dataelementen som du skapade tidigare för att samla in autentiserade data med datatypen Platform Web SDK som kallas identitetskarta.

Den här lektionen fokuserar på det dataelement för identitetskartan som finns i taggtillägget Adobe Experience Platform Web SDK. Du mappar dataelement som innehåller ett autentiserat användar-ID och autentiseringsstatus till XDM.

## Utbildningsmål

När lektionen är slut kan du:

* Förstå relationen mellan Experience Cloud ID (ECID) och FPID (First Party Device ID)
* Förstå skillnaden mellan oautentiserade och autentiserade ID:n
* Skapa ett dataelement för identitetskarta

## Förhandskrav

Du har en förståelse för vad ett datalager är, har lärt dig mer om datalagret [Luma demo ](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} och vet hur du refererar till dataelement i taggar. Du måste ha slutfört föregående lektioner i självstudien:

* [Konfigurera ett XDM-schema](configure-schemas.md)
* [Konfigurera ett identitetsnamnutrymme](configure-identities.md)
* [Konfigurera ett datastream](configure-datastream.md)
* [Web SDK-tillägget är installerat i taggegenskapen](install-web-sdk.md)
* [Skapa dataelement](create-data-elements.md)


## EXPERIENCE CLOUD ID

[Experience Cloud ID (ECID)](https://experienceleague.adobe.com/sv/docs/experience-platform/identity/features/ecid) är ett delat ID-namnområde som används i Adobe Experience Platform- och Adobe Experience Cloud-program. ECID utgör grunden för kundidentiteten och är standardidentitet för digitala resurser. ECID är den idealiska identifieraren för att spåra oautentiserade användarbeteenden eftersom det alltid finns.

<!-- FYI I commented this out because it was breaking the build - Jack
>[!TIP]
>
> When you use the Experience Platform Web SDK to set up Adobe applications on your digital properties, the ECID is generated at the Adobe Edge server level. As such, ECID is not viewable on the client-side network request payload. You can view the ECID by seeing the Preview tab of the network request, or by using the [Adobe Experience Platform Debugger Edge Trace](set-up-analytics.md#experience-cloud-id-validation).
>![View ECID](assets/validate-dev-console-ecid.png)
-->

Läs mer om hur [ECID:n spåras med Platform Web SDK](https://experienceleague.adobe.com/sv/docs/experience-platform/edge/identity/overview).

ECID anges med en kombination av cookies från första part och Platform Edge Network. Som standard anges cookies för identitet från första part av Web SDK på klientsidan. Om du vill ta hänsyn till webbläsarbegränsningar för cookie-intervall kan du välja att ange egna cookies på serversidan för förstapartidentitet i stället. Dessa identitetscookies kallas för FPID (First-party device ID).

>[!IMPORTANT]
>
>Tjänsttillägget [Experience Cloud ID](https://exchange.adobe.com/apps/ec/100160/adobe-experience-cloud-id-launch-extension) behövs inte när Adobe Experience Platform Web SDK implementeras eftersom ID-tjänstfunktionen är inbyggd i Platform Web SDK.

## FPID (First Party Device ID)

FPID är cookies från första part _du anger med dina egna webbservrar_ som Adobe sedan använder för att skapa ECID, i stället för att använda cookie-filen från första part som anges av Web SDK. Webbläsarstödet kan variera, men cookies från första part kan vara mer varaktiga när de anges av en server som använder en DNS A-post (för IPv4) eller en AAA-post (för IPv6), i motsats till när de anges av en DNS CNAME- eller JavaScript-kod.

När en FPID-cookie har angetts kan dess värde hämtas och skickas till Adobe när händelsedata samlas in. Insamlade FPID används som startvärde för att generera ECID på Platform Edge Network, som även fortsättningsvis är standardidentifierare i Adobe Experience Cloud-program.

Även om FPID inte används i den här självstudiekursen bör du använda FPID i din egen Web SDK-implementering. Läs mer om [Första parts enhets-ID i plattformens webb-SDK](https://experienceleague.adobe.com/sv/docs/experience-platform/edge/identity/first-party-device-ids)

>[!CAUTION]
>
> FPID är ett alternativt sätt att generera ECID genom att använda en cookie som angetts av webbservrarna. Det används inte för att identifiera autentiserade användare.

## Autentiserat ID

Som nämnts ovan tilldelas alla besökare av dina digitala resurser ett ECID av Adobe när de använder Platform Web SDK. ECID är standardidentitet för att spåra oautentiserat digitalt beteende.

Du kan också skicka ett autentiserat användar-ID så att plattformen kan skapa [identitetsdiagram](https://experienceleague.adobe.com/sv/docs/platform-learn/tutorials/identities/understanding-identity-and-identity-graphs) och mål kan ange sitt [tredjeparts-ID](https://experienceleague.adobe.com/sv/docs/target/using/audiences/visitor-profiles/3rd-party-id). Inställningen av det autentiserade ID:t görs med dataelementtypen [!UICONTROL Identity Map].

Så här skapar du dataelementet [!UICONTROL Identity Map]:

1. Gå till **[!UICONTROL Data Elements]** och välj **[!UICONTROL Add Data Element]**

1. **[!UICONTROL Name]** dataelementet `identityMap.loginID`

1. Som **[!UICONTROL Extension]** väljer du `Adobe Experience Platform Web SDK`

1. Som **[!UICONTROL Data Element Type]** väljer du `Identity map`

1. Ett skärmyta visas till höger i **[!UICONTROL Data Collection interface]** så att du kan konfigurera identiteten:

   ![Gränssnitt för datainsamling](assets/identity-identityMap-setup.png)

1. Som **[!UICONTROL Namespace]** väljer du namnutrymmet `lumaCrmId` som du tidigare skapade i lektionen [Konfigurera identiteter](configure-identities.md). Om den inte visas i listrutan skriver du in den.

1. När **[!UICONTROL Namespace]** har valts måste ett ID anges. Markera dataelementet `user.profile.attributes.username` som skapades tidigare i lektionen [Skapa dataelement](create-data-elements.md#create-data-elements-to-capture-the-data-layer) som hämtar ett ID när användare är inloggade på Luma-webbplatsen.

   <!--  >[!TIP]
    >
    >You can verify the **[!UICONTROL Luma CRM ID]** is collected in a data element on the web property by going to the [Luma Demo site](https://luma.enablementadobe.com/content/luma/us/en.html), logging in, [switching the tag environment](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tag-property) to your own, and typing `_satellite.getVar("user.profile.attributes.username")` in the web browser developer console.
    >
    >   ![Data Element  ID ](assets/identity-data-element-customer-id.png)
    -->

1. Som **[!UICONTROL Authenticated state]** väljer du **[!UICONTROL Authenticated]**
1. Välj **[!UICONTROL Primary]**

1. Välj **[!UICONTROL Save]**

   ![Gränssnitt för datainsamling](assets/identity-id-namespace.png)

>[!TIP]
>
> Adobe rekommenderar att du skickar identiteter som representerar en person, till exempel `Luma CRM Id`, som [!UICONTROL primary]-identitet.
>
> Om identitetskartan innehåller personidentifieraren (till exempel `Luma CRM Id`) blir personidentifieraren [!UICONTROL primary]-identiteten. Annars blir `ECID` [!UICONTROL primary]-identiteten.




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

| Dataelement för kärntillägg | Dataelement för plattforms-SDK-tillägg |
-----------------------------|-------------------------------
| `cart.orderId` | `data.variable` |
| `cart.productInfo` | `identityMap.loginID` |
| `cart.productInfo.purchase` | `xdm.variable.content` |
| `page.pageInfo.hierarchie1` | |
| `page.pageInfo.pageName` | |
| `page.pageInfo.server` | |
| `product.category` | |
| `product.productInfo.sku` | |
| `product.productInfo.title` | |
| `user.profile.attributes.loggedIn` | |
| `user.profile.attributes.username` | |

Med dessa dataelement på plats kan du börja skicka data till Platform Edge Network genom att skapa en regel i taggar.

[Nästa: ](create-tag-rule.md)

>[!NOTE]
>
>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Web SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela dem i det här [Experience League-diskussionsinlägget](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
