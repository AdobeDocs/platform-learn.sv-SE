---
title: Skapa segment
seo-title: Build segments | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Skapa segment
description: I den här lektionen ska vi skapa några segment baserat på profildata som vi har inhämtat i tidigare lektioner.
role: Data Architect
feature: Data Governance
jira: KT-4348
thumbnail: 4348-build-segments.jpg
exl-id: cd05e814-1ea7-48ba-adf6-1a71504c623e
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 0%

---

# Skapa segment

<!-- 30 min-->
I den här lektionen ska vi skapa några segment baserat på profildata som vi har inhämtat i tidigare lektioner.

När ni har kundprofiler i realtid kan ni skapa segment för individer som delar liknande egenskaper och som kan svara på liknande sätt som marknadsföringsstrategier. Byggstenarna för dessa segment är XDM-fälten som du skapade tidigare.

**Dataarkitekter** måste skapa segment utanför den här självstudiekursen och stödja sina kollegor i den här uppgiften.

Innan du börjar övningarna ska du titta på den här korta videon och lära dig mer om hur du skapar segment:
>[!VIDEO](https://video.tv.adobe.com/v/27254?learn=on&enablevpops)


## Behörigheter krävs

I lektionen [Konfigurera behörigheter](configure-permissions.md) ställer du in alla åtkomstkontroller som krävs för att slutföra den här lektionen, speciellt:

* Behörighetsobjekt **[!UICONTROL Profile Management]** > **[!UICONTROL Manage Segments]**, **[!UICONTROL View Segments]** och **[!UICONTROL Export Audience Segment]**
* Behörighetsobjekt **[!UICONTROL Profile Management]** > **[!UICONTROL View Profiles]** och **[!UICONTROL Manage Profiles]**
* Behörighetsobjekt **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* Användarrollåtkomst till produktprofilen `Luma Tutorial Platform`
* Åtkomst till produktprofilen `Luma Tutorial Platform` för utvecklare (för API)

## Bygg ett enkelt segment

Låt oss skapa ett enkelt segment för lojalitetsprogram för kunder med Guld- eller Platinumstatus

1. Gå till **[!UICONTROL Segments]** i den vänstra navigeringen i användargränssnittet för plattformen
1. Markera knappen **[!UICONTROL Create segment]**
1. Till vänster om schemaverktaren finns tre flikar för Attribut (postdata), Händelser (tidsseriedata) och Publiker
1. Markera kugghjulsikonen om du vill se hur segmentbyggaren som standard bara visar fält med data och låter dig ändra kopplingsprofilen
1. Gå till mappen **XDM Individual Profile > Lojalitet** på fliken Attribut (du kan också söka efter &quot;loyalty&quot;)
1. Dra och släpp `Tier` från attributfältsmenyn till segmentbyggarbetsytan
1. Välj `Tier` är lika med `Gold` eller `Platinum`
1. Välj **[!UICONTROL Refresh estimate]** om du vill se hur många profiler som är kvalificerade för ditt segment
1. Ange `Luma customers with level Gold or Above` som **[!UICONTROL Name]**
1. Välj **[!UICONTROL Save]**
   ![Segment](assets/segment-goldOrAbove.png)

<!--## Build a sequential segment-->

## Skapa ett dynamiskt segment

I den här övningen skapar vi ett segment för kunder som har köpt samma produkt två gånger inom 30 dagar. Med dynamiska segment kan du skala segmenteringen genom att använda fält som variabler.

1. Gå till **[!UICONTROL Segments]** i den vänstra navigeringen
1. Markera knappen **[!UICONTROL Create segment]**
1. Välj fliken **[!UICONTROL Events]**
1. Filtrera listan till `purchases`
1. Dra händelsetypen **[!UICONTROL Purchases]** till arbetsytan _två gånger_
1. Välj klockikonen mellan de två **[!UICONTROL Purchases]**-händelserna och välj &quot;inom 30 dagar&quot;
1. Bekräfta att din segmentdefinition vid den här tidpunkten är **Inkludera målgrupp som har minst en Inköpshändelse och inom 30 dagar har minst en Inköpshändelse**
   ![Två köp inom 30 dagar](assets/segment-twoPurchases.png)
1. Ändra nu händelsefiltret till `sku`
1. Dra SKU-fältet till den andra köphändelsen
   ![Två köp inom 30 dagar med SKU](assets/segment-twoPurchases-addSku.png)
1. Rensa händelsefiltret
1. I avsnittet **[!UICONTROL Browse Variables]** bör du se att det finns mappar för de två inköpshändelserna. Klicka för att utforska **[!UICONTROL Purchases 1]**\
   ![Två köp inom 30 dagar med SKU, bläddra i det första köpet](assets/segment-twoPurchases-browsePurchaseOne.png)
1. Gå ned i mappen **[!UICONTROL Product list items]**, markera fältet **[!UICONTROL SKU]** och dra det till höger om operanden **[!UICONTROL equals]**. När du hovrar över området släpper du det i avsnittet Lägg till för att jämföra operander
1. Namnge ditt segment `Bought same product within 30 days`
1. Bekräfta att målgruppsdefinitionen är **Inkludera målgrupp som har minst en Inköpshändelse och inom 30 dagar har minst en Inköpshändelse där ((SKU är lika med Inköp1 SKU))**
1. Markera knappen **[!UICONTROL Save]**

   ![Köpte samma produkt under de senaste 30 dagarna](assets/segment-boughtSameProduct.png)

## Skapa ett segment med flera enheter

Kommer du ihåg hur vi skapade relationen mellan `Luma Offline Purchase Events Schema` och `Luma Product Catalog Schema` i tidigare lektioner? Vi gjorde det så att vi kunde använda relationen i vårt schema med segmentering av flera enheter.

Med den avancerade segmenteringsfunktionen för flera enheter kan du skapa segment med hjälp av flera XDM-klasser för att utöka dina scheman. Det innebär att segmentbyggaren kan komma åt ytterligare fält som om de vore inbyggda i profildatalagret

Du skapar nästa segment genom att tillämpa relationen som du skapade mellan din `Luma Product Catalog Schema` och din `Luma Offline Purchase Events Schema`.

1. Gå till **[!UICONTROL Segments]** i den vänstra navigeringen
1. Markera knappen **[!UICONTROL Create segment]**
1. Välj fliken **[!UICONTROL Events]**
1. Filtrera listan till `purchases`
1. Dra händelsetypen **[!UICONTROL Purchases]** till arbetsytan
1. Välj listrutan med klockan ovanför händelsen och välj **[!UICONTROL in last 30 days]**
1. Filtrera listan **[!UICONTROL Events]** till `category` och dra sedan fältet **[!UICONTROL Product Category]** till **[!UICONTROL Purchases]**
1. Ändra operatorn till **[!UICONTROL starts with]** och ange `men` i textrutan
1. Ange `Purchased a Men's product in the last 30 days` som **[!UICONTROL Name]**
1. Bekräfta målgruppsdefinitionen `(Include audience who have at least 1 Purchases event where ((Product Category starts with men)) ) and occurs in last 30 day(s)`
1. Markera knappen **[!UICONTROL Save]**

   ![Köpte samma produkt under de senaste 30 dagarna](assets/segment-purchasedMens.png)

## Segmentering av grupper och strömning

Klicka på **[!UICONTROL Segments]** i den vänstra navigeringen och låt oss titta lite närmare på våra tre segment:

* Två av våra segment är gruppsegment och ett är ett direktuppspelningssegment.
* Som standard används direktuppspelningssegmentering när det är möjligt, vilket kvalificerar kunden för ett segment så fort de uppfyller kriterierna. När segmentdefinitioner är för komplexa för direktuppspelning, konverteras de automatiskt till batch. I det här fallet valde de två segmenten att gruppera eftersom kontrollfönstret för köphändelserna var större än sju dagar. En fullständig och aktuell lista över begränsningar för direktuppspelning finns i [dokumentationen](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/streaming-segmentation.html).
* Batchjobben körs enligt ett dagligt schema som kan stängas av.

![Köpte samma produkt under de senaste 30 dagarna](assets/segment-review.png)

## Ytterligare resurser

* [Dokumentation för segmenteringstjänsten](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html)
* [API-referens för segmenteringstjänst](https://www.adobe.io/experience-platform-apis/references/segmentation/)

Det finns mer att segmentera, särskilt när det gäller att aktivera segment. Dessa ämnen kommer att behandlas i en annan självstudiekurs.

Du har klarat alla övningar! Fortsätt till [slutsatsen](conclusion.md).
