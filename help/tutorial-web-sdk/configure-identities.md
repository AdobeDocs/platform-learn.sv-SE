---
title: Konfigurera ett identitetsnamnutrymme
description: Lär dig hur du konfigurerar identitetsnamnutrymmen som ska användas med Adobe Experience Platform Web SDK. Den här lektionen är en del av självstudiekursen Implementera Adobe Experience Cloud med Web SDK.
feature: Identities
exl-id: 7719dff4-6b30-4fa0-acae-7491c3208f15
source-git-commit: 2b5013ea01bf4e2388a6e1fc046b1685945be238
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 1%

---

# Konfigurera ett identitetsnamnutrymme

Lär dig hur du konfigurerar identitetsnamnutrymmen som ska användas med Adobe Experience Platform Web SDK.

The [Adobe Experience Platform Identity Service](https://experienceleague.adobe.com/docs/id-service/using/home.html) ställer in ett gemensamt besökar-ID för alla Adobe-lösningar för att underlätta för Experience Cloud, som målgruppsdelning mellan olika lösningar. Du kan också skicka dina egna kund-ID:n till tjänsten för att möjliggöra målinriktning mellan olika enheter och integrering med andra system, som CRM-systemet (Customer Relationship Management).

Om din webbplats redan använder Experience Cloud ID-tjänsten på din webbplats (antingen via Visitor API eller Experience Cloud ID Service Tag-tillägget) och du vill fortsätta använda den när du migrerar till Adobe Experience Platform Web SDK, måste du använda den senaste versionen av Visitor API eller Experience Cloud ID Service Tag-tillägget. Se [ID-migrering](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en) för mer information.

>[!NOTE]
>
> I demonstrationssyfte kan du använda övningarna i den här lektionen för att fånga identitetsinformationen för en fiktiv kund som är inloggad på [Luma Demo Site](https://luma.enablementadobe.com/content/luma/us/en.html) med hjälp av inloggningsuppgifterna, **användare: test@adobe.com / lösenord: test**. Du kan använda de här stegen för att skapa en annan identitet för dina egna syften, men om du vill lära dig funktionerna i identitetskartan i gränssnittet för datainsamling rekommenderar vi att du följer med för att hämta exempelidentiteten.

## Utbildningsmål

När lektionen är klar kan du:

* Identitetsnamnutrymmen
* Skapa ett anpassat identitetsnamnutrymme för att hämta ett internt CRM-ID


## Förutsättningar

Du måste ha slutfört tidigare lektioner:

* [Konfigurera behörigheter](configure-permissions.md)
* [Konfigurera scheman](configure-schemas.md)

>[!IMPORTANT]
>
>The [Experience Cloud ID-tillägg](https://exchange.adobe.com/experiencecloud.details.100160.adobe-experience-cloud-id-launch-extension.html) behövs inte när du implementerar Adobe Experience Platform Web SDK, eftersom JavaScript-biblioteket för Web SDK innehåller funktioner för tjänsten för besöks-ID.

## Skapa ett identitetsnamnutrymme

I den här övningen skapar du ett ID-namnutrymme för Lumas anpassade identitetsfält, `lumaCrmId`. Identitetsnamnutrymmen spelar en viktig roll när det gäller att skapa kundprofiler i realtid, eftersom två matchande värden i samma namnutrymme gör att två datakällor kan bilda ett identitetsdiagram.

Titta på den här korta videon om du vill veta mer om din identitet i Adobe Experience Platform innan du börjar övningarna:
>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

Skapa nu ett namnutrymme för Luma CRM-ID:

1. Öppna [Gränssnitt för datainsamling](https://launch.adobe.com/){target=&quot;_blank&quot;}
1. Välj den sandlåda som du använder för självstudiekursen

   >[!NOTE]
   >
   >Om du använder ett plattformsbaserat program som CDP i realtid rekommenderar vi att du använder en utvecklingssandlåda för den här självstudiekursen. Om du inte gör det använder du **[!UICONTROL Prod]** sandlåda.

1. Välj **[!UICONTROL Identiteter]** i den vänstra navigeringen
1. Välj **[!UICONTROL Bläddra]**

   En lista med identitetsnamnutrymmen visas i sidans huvudgränssnitt med namn, identitetssymboler, senaste uppdateringsdatum och om de är standardnamnutrymmen eller anpassade namnutrymmen. Den högra listen innehåller information om identitetsgrafens styrka.

1. Välj **[!UICONTROL Skapa namnutrymme för identitet]**

   ![Visa identiteter](assets/configure-identities-screen.png)

1. Ange följande information och välj **[!UICONTROL Skapa]**.

   | Fält | Värde |
   |---------------|-----------|
   | Visningsnamn | Luma CRM-ID |
   | Identitetssymbol | lumaCrmId |
   | Typ | Enhets-ID |


   ![Skapa namnutrymmen](assets/identities-create-namespace.png)


   Identitetsnamnutrymmet fylls i i **[!UICONTROL Identiteter]** skärm.

   ![Skapa namnutrymmen](assets/configure-identities-namespace-lumaCrmId.png)


>[!INFO]
>
> I [Skapa dataelement](create-data-elements.md) lektionen lär du dig hur du använder det här namnutrymmet när du skickar identiteter till Platform Edge Network.

## Skapa identitetsnamnutrymmet i din produktionssandlåda

På grund av en aktuell begränsning i Web SDK-tillägget måste även identitetsnamnutrymmen skapas i produktionssandlådan för att kunna använda namnutrymmet för att skicka data till en utvecklingssandlåda. Om du har använt en utvecklingssandlåda för den här självstudiekursen skapar du även `Luma CRM ID` namnutrymme i din produktionssandlåda.

## Ytterligare resurser

* [Identitetstjänstens dokumentation](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=sv)
* [Identitetstjänstens API](https://www.adobe.io/experience-platform-apis/references/identity-service/)

Nu när identiteter finns på plats kan datastream konfigureras.

[Nästa: ](configure-datastream.md)

>[!NOTE]
>
>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Web SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela med dig av dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
