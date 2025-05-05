---
title: Lägg till och konfigurera Web SDK-tillägget
description: Lär dig hur du lägger till och konfigurerar Web SDK-tillägget i taggegenskapen, så att du får de funktioner du behöver i fler lektioner för att slutföra migreringen.
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16758
source-git-commit: 7ae56d997884cf1558e72c0ad553df1c5d43c081
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---


# Lägg till och konfigurera Web SDK-tillägget

Lär dig hur du lägger till och konfigurerar Web SDK-tillägget i taggegenskapen för att få den funktionalitet du behöver i fler lektioner för att slutföra migreringen.
Följ de här stegen för att lägga till och konfigurera tillägget:

1. Navigera till Experience Platform Data Collection. Detta kan göras på ett av två sätt:
   1. Gå till [Adobe Experience Platform-gränssnittet](https://platform.adobe.com/) och välj sedan **[!UICONTROL Tags]** längst ned i den vänstra navigeringen.

      ![Åtkomsttaggar 1](assets/access-tags-1.jpg)
   1. Om du inte har tillgång till Platform kan du använda programväljaren (9 punkter) längst upp till höger i fönstret och välja Datainsamling (efter att du har loggat in på Experience.Adobe.com).

      ![Åtkomsttaggar 2](assets/access-tags-2.jpg)
1. Hitta och välj taggegenskapen som du migrerar till Web SDK.
1. Välj **[!UICONTROL Extensions]** i den vänstra navigeringen för taggegenskapen.
1. Välj **[!UICONTROL Catalog]** i den övre delen om du vill se en lista över alla tillgängliga tillägg.
1. Sök efter och välj tillägget **[!UICONTROL Adobe Experience Platform Web SDK]** och klicka sedan på **[!UICONTROL Install]** till höger.

   ![Hitta SDK-tillägget för webben](assets/find-the-websdk-extension.jpg){style="border:1px solid lightslategray"}

1. Konfigurationsinställningarna för tillägget visas. Leta reda på avsnittet Datastreams och ange den Experience Platform-sandlåda som du vill använda för den här migreringen (&quot;Miljölistrutor&quot; för alla tre miljöerna). Om du bara migrerar Adobe Analytics och inte skickar data till Adobe Experience Platform väljer du sandlådan **Produktion**. Om du ska skicka dessa beteendeanalysdata till Experience Platform för användning i programmen där, väljer du den sandlåda som du vill använda för det. Du kommer antagligen först att vilja välja en utvecklingssandlåda tills du är klar med migreringen och har lagt till/testat din plattformstjänst.
1. Det viktigaste är att du kopplar koden och inställningarna här i Taggar till Edge genom att välja de datastreams som du skapade i det föregående steget för produktions-, mellanlagrings- och utvecklingsmiljöer.

   ![Val av dataström](assets/choose-datastreams.jpg){style="border:1px solid lightslategray"}

1. Bläddra nedåt och lägg märke till att inställningarna för **Identitet** är markerade som standard. Låt de här kryssrutorna vara markerade, eftersom de hjälper dig att identifiera webbplatsbesökarna korrekt när du migrerar till Web SDK. Mer information finns i dokumentationen som är länkad till nedan.

1. Välj **[!UICONTROL Save]**.

>[!NOTE]
>
>Egenskapen Tags har nu en grundläggande installation och konfiguration av tillägget Web SDK. Vi kommer att använda delar av Web SDK-tillägget när vi skapar eller ändrar dataelement och regler under den här självstudiekursen för migrering, men vi kommer inte att ändra fler av alternativen för tilläggskonfiguration i självstudiekursen. Ytterligare konfigurationsobjekt kan och bör användas för ytterligare användningsfall. Detaljerad dokumentation om de här konfigurationerna finns i [Konfigurera SDK-taggtillägget för webben](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/client/web-sdk/web-sdk-extension-configuration).
