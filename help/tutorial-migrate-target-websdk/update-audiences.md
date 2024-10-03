---
title: Uppdatera målgrupper och profilskript - Migrera Target från at.js 2.x till Web SDK
description: Lär dig hur du uppdaterar Adobe Target målgrupper och profilskript för kompatibilitet med Experience Platform Web SDK.
exl-id: 2c0f85f7-6e8c-4d0b-8ed5-53897d06e563
source-git-commit: d4308b68d6974fe47eca668dd16555d15a8247c9
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# Uppdatera målgrupper och profilskript för kompatibilitet med Platform Web SDK

När du har slutfört de tekniska uppdateringarna för att migrera Target till Platform Web SDK kan du behöva uppdatera några av dina målgrupper, profilskript och aktiviteter för att säkerställa en smidig övergång.

Alla Target-parametrar måste skickas i XDM-format med en Platform Web SDK-implementering. Innan du publicerar ändringarna i produktionen bör du:

* Uppdatera målgrupper som använder mbox-parametrar
* Uppdatera profilskript som använder mbox-parametrar
* Uppdatera alla erbjudanden och aktiviteter med hjälp av ersättare för mbox-parametertoken (till exempel `${mbox.parameter_name}`)

## Justera målgrupper

Alla målgrupper som använder anpassade mbox-parametrar bör uppdateras så att de använder de nya XDM-parameternamnen. En anpassad parameter för `page_name` skulle till exempel troligen mappas till `web.webpagedetails.pageName`.

Ett sätt att säkerställa kompatibilitet med både at.js och Platform Web SDK är att uppdatera alla relevanta målgrupper så att `OR`-villkor används, vilket visas nedan:

![Så här uppdaterar du en målgrupp för kompatibilitet med plattformswebbsäkra DK](assets/target-audience-update.png){zoomable="yes"}

## Redigera profilskript

Profilskript ska uppdateras för att referera till nya XDM-parameternamn, som liknar målgrupper. Förutom ändringen av mbox-parameternamn finns det ingen skillnad i hur profilskript fungerar mellan en at.js och en Platform Web SDK-implementering.

Ett sätt att säkerställa kompatibilitet är att använda `OR`-villkor i din profilskriptkod.

Exempel på profilskript:

```Javascript
if(mbox.param('pageName') == 'Product Details'){
  return true
}
```

Uppdaterat profilskript för kompatibilitet med Platform Web SDK:

```Javascript
if((mbox.param('pageName') == 'Product Details') || (mbox.param('web.webPageDetails.pageName') =='Product Details')){
  return true
}
```

Mer information och bästa praxis finns i den dedikerade dokumentationen om [profilskript](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html).

## Uppdatera parametertoken för dynamiskt innehåll

Om du har erbjudanden, rekommendationer eller aktiviteter som använder [dynamisk innehållsersättning](https://experienceleague.adobe.com/docs/target/using/experiences/offers/passing-profile-attributes-to-the-html-offer.html) kan de behöva uppdateras för att ta hänsyn till de nya XDM-parameternamnen.

Beroende på hur du använder tokenersättning för mbox-parametrar kan du eventuellt förbättra din befintliga konfiguration så att den tar hänsyn till både gamla och nya parameternamn. I situationer där anpassad JavaScript-kod inte är möjlig, t.ex. i JSON-erbjudanden, bör du skapa kopior och göra uppdateringar när migreringen är klar och publicerad på produktionsplatsen.

Exempel på JSON-erbjudande:

```JSON
{
  "pageName" : "${mbox.page_name}",
  "layoutVariation" : "grid"
}
```

Exempel på JSON-erbjudande med parameternamn för Platform Web SDK:

```JSON
{
  "pageName" : "${mbox.web.webPagedDetails.pageName}",
  "layoutVariation" : "grid"
}
```

Om du väljer att göra justeringar efter migreringen för att ta hänsyn till de nya parameternamnen för XDM-mbox ska du se till att pausa alla aktiviteter som påverkas under migreringshändelsen för att förhindra aktivitetsvisningsfel för besökarna.

Läs sedan om hur du [validerar målimplementeringen](validate.md).

>[!NOTE]
>
>Vi vill hjälpa dig att lyckas med målmigreringen från at.js till Web SDK. Om du stöter på problem med din migrering eller om du känner att det saknas viktig information i den här guiden kan du meddela oss genom att publicera [den här communitydiskussionen](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
