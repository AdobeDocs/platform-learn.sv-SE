---
title: Aktivera stöd för flera domäner | Migrera mål från at.js 2.x till Web SDK
description: Lär dig hur du konfigurerar Adobe Target för olika domäner och mobilappar till webbläsarscenarier med Experience Platform Web SDK.
source-git-commit: 287ebcb275c4fca574dbd6cdf7e07ba4268bddb5
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---

# Aktivera korsdomänsprofiler för besökare

Platform Web SDK har stöd för delning av besökar-ID, vilket gör att kunderna kan leverera personaliserade upplevelser på ett mer korrekt sätt i alla domäner. Med den här funktionen kan ni leverera enhetlig personalisering över olika domäner och förbättra noggrannheten i besökarens aktivitetsrapportering, utan att förlita er på cookies från tredje part.

## Förutsättningar

Om du vill använda delning av domänöverskridande ID måste du använda Platform Web SDK version 2.11.0 eller senare. Den här funktionen är även kompatibel med VisitorAPI.js version 1.7.0 eller senare.

Delning av domänöverskridande ID fungerar genom att lägga till en särskild `adobe_mc` frågesträngsparameter till måldomänens URL. Den här parametern används för att ange besökar-ID i stället för att generera ett nytt ID eller använda ett befintligt ID.

Måldomänen måste använda något av dessa bibliotek för delning av domänöverskridande ID för att bearbeta `adobe_mc` och dela besökar-ID:t på rätt sätt.

## Jämförelse av tillvägagångssätt

Innan du implementerar måste du först kontrollera om din befintliga implementering använder `visitor.appendVisitorIDsTo()` funktion. All anpassad kod som använder den här funktionen bör uppdateras för att använda den nya `appendIdentityToUrl` Web SDK, kommando.

| VisitorAPI.js | Platform Web SDK |
| --- | --- |
| `visitor.appendVisitorIDsTo(*url*)` | `alloy("appendIdentityToUrl", { url: *url* })` |

## Använda `appendIdentityToURL` kommando

För delning av domänöverskridande ID har Web SDK version 2.11.0 stöd för `appendIdentityToUrl` -kommando. När kommandot används genereras `adobe_mc` frågesträngsparameter.

Kommandot accepterar ett objekt med en egenskap, `url`och returnerar ett objekt med egenskaps-URL:en.

Det här kommandot väntar inte på någon uppdatering av medgivandet. Om samtycke inte har angetts returneras URL:en oförändrad.

Om inget ECID anges `/acquire` slutpunkten anropas för att generera ett ECID.

Nedan visas ett exempel på hur du kan implementera delning av domänöverskridande ID.

Den här koden lägger till en händelseavlyssnare för alla klickningar på sidan. Om klickningen var på en länk till en matchande domän, i det här fallet adobe.com eller behance.com, lägger den till identiteten i URL:en och dirigerar om användaren dit.

```Javascript
document.addEventListener("click", event => {
  const anchor = event.target.closest("a");
  if (!anchor || !anchor.href) {
    return;
  }
  const url = new URL(anchor.href);
  if (!url.hostname.endsWith("adobe.com") && !url.hostname.endsWith("behance.com")) {
    return;
  }
  event.preventDefault();
  alloy("appendIdentityToUrl", { url: anchor.href }).then(result => {
    document.location = result.url;
  });
});
```

>[!TIP]
>
>När du använder taggfunktionen (tidigare Launch) för att implementera Web SDK kan delning av domänöverskridande ID göras utan anpassad kod. Se [dedikerad dokumentation](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/id-sharing.html#tags-extension) för mer information.

>[!NOTE]
>
>Platform Web SDK har också stöd för delning av mobil-till-webb-ID för användning av inbyggda mobilappar. Mer information finns i den dedikerade dokumentationen om [delning av mobil-till-webb och domänövergripande ID](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/id-sharing.html).

Lär dig sedan hur du [uppdatera målgrupper och profilskript](update-audiences.md) för att säkerställa kompatibilitet med Platform Web SDK.

>[!NOTE]
>
>Vi vill hjälpa dig att lyckas med målmigreringen från at.js till Web SDK. Om du stöter på problem med din migrering eller känner att det saknas viktig information i den här guiden ber vi dig att meddela oss genom att publicera i [den här communitydiskussionen](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).