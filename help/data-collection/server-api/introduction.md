---
title: Grundläggande introduktion till API:er
description: En introduktion till Application Programming Interfaces
activity: understand
doc-type: article
feature-set: Experience Platform
feature: Server API,API,Data Collection,Integrations
level: Beginner
role: User, Data Engineer, Developer
solution: Data Collection
topic: Integrations
exl-id: 9607e641-b0d5-49c1-b319-32ed0720e715
source-git-commit: ac07d62cf4bfb6a9a8b383bbfae093304d008b5f
workflow-type: tm+mt
source-wordcount: '2086'
ht-degree: 0%

---

# API 101 - En grundläggande introduktion till API:er

API står för Application Programming Interface. Det betyder precis vad det står - det finns gränssnitt mellan programmen och dessa gränssnitt gör att dessa program kan kommunicera. När programmerare utvecklar program behöver de ofta programvaran för att kunna kommunicera med andra program- eller maskinvaruprogram. API:t definierar vad, hur, när, var och varför för dessa meddelanden och interaktioner.

API:er är ett sätt att lösa affärsutmaningar med programvara. I de flesta företag är det en samarbetssatsning. Samarbete är alltid enklare med en gemensam förståelse av viktiga termer, begrepp och steg.

Om du funderar på att klicka på en länk på en webbsida använder webbläsaren ett antal API:er när du klickar på länken. Webbläsaren känner igen klickljudet, begär den sida som du vill besöka, hämtar sidan via Internet och visar den sedan på skärmen. Det finns många mindre steg däremellan, men webbläsaren är programvara som kommunicerar och interagerar med en mängd olika API:er bara för att visa en webbsida. I den här artikeln ska vi lyfta fram termer, koncept och steg som är viktiga när du använder eller diskuterar API:er.

I slutet av den här artikeln bör du ha en tydlig förståelse för dessa grundläggande termer, begrepp och steg. API-dokumentationen kan vara omfattande, och diskussioner om hur du använder API:er för att hantera specifika användningsfall kan bli mycket detaljerade. Att navigera i dokumentation och diskutera API:er är enklare och mer produktivt med tydliga grundläggande funktioner och delad förståelse.

>[!NOTE]
>
> Även om det finns många API:er kommer fokus här att ligga på webb- och webbläsarAPI:er: i princip när ett program interagerar med ett annat via Internet.

## API - termer och begrepp

Vad betyder ett ord eller en fras och hur kan jag tänka på det enkelt och enkelt? I ett API betyder&quot;programdelen&quot; ett program eller program. Delen &quot;Programmeringsgränssnitt&quot; avser hur och var ett program interagerar med ett annat program för vissa syften. När du klickar på en länk i vårt exempel på webbsida skickar webbläsaren en begäran till en server för webbsidan.

![Bild av hyperlänk med mål-URL](../assets/api101-link-destination.png)

I den här skärmbilden hovrar musmarkören över länken Adobe Experience Platform. Längst ned finns webbläsarens statusfält som visar &quot;adressen&quot; till sidan som webbläsaren kommer att få. Med andra ord: om du klickar på länken Adobe Experience Platform visas en uppmaning om att &quot;hämta den sidan åt mig så att jag kan se den här på skärmen&quot;.

När användaren klickar på en länk skickar webbläsaren en begäran till en server om att hämta en sida. Detta är en `GET`-begäran, en av de förfrågningsmetoder som vanligtvis används med webb-API:er. En sak som webbläsaren behöver fylla i är sidan &quot;address&quot; - var finns den på webben?

### Delar av en URL

![Webbläsaradressfältet med URL](../assets/api101-address-bar.png)

De flesta webbläsare har ett adressfält som visar en del av eller hela adressen för en webbsida. När webbläsaren&quot;hämtar&quot; sidan för länken som vi klickade på visas&quot;adressen&quot; för sidan i det här adressfältet. Så vad är &quot;adressen&quot; för en webbsida?

`https://business.adobe.com/se/products/experience-platform/adobe-experience-platform.html` ovan är adressen till en sida på webben och kallas URL eller Uniform Resource Locator. URL-adresser kan referera till en sida som den här, en bildfil, en video eller andra filtyper.

![Delar av en URL](../assets/api101-url-parts.jpg)

Den här adressen, URL:en, har specifika delar som är mycket relevanta för webb- och webbläsarAPI:er.

**Schema**

`scheme` ovan kallas även `protocol` med webb-API:er och är vanligtvis antingen `http` eller `https`. HTTP- eller HyperText Transfer Protocol är hur resurser som webbsidor överförs från en webbserver till en webbläsare. HTTPS är den säkra versionen, där överföringen sker via Internet med säkerhet som är avsedd att förhindra störningar av resursen som överförs. Det är vanligt att visa en liten låsikon i webbläsarens adressfält när du visar en sida via HTTPS.

För webb-API:er sker överföringen av dessa resurser via HTTP-begäranden, med andra ord via HTTP.

**Värdar och domäner**

`business.adobe.com` är värddatorn för resursen som begärs. När du klickar på vår exempellänk använder webbläsaren den här delen av URL:en för att hitta servern där sidan finns. Det är inte alltid exakt likadant som webbservern, men på en grundläggande nivå kan vi tänka på det som den server där webbläsaren kommer att få den begärda sidan.

Domännamn är en del av domännamnssystemet, som kallas DNS. De flesta människor ser `adobe.com` eller `example.com` som ett &quot;domännamn&quot;, men det finns delar som är relevanta för API:er. `www.adobe.com` och `business.adobe.com` kan kallas domännamn, men delarna `www.` och `business.` kallas underdomäner. API:er interagerar ofta med en URL som innehåller en underdomän som `api.example.com` eller `sub.www.example.com`.

Det är mycket vanligt att termen _host_ refererar till ett fullständigt domännamn inklusive alla underdomäner som `business.adobe.com`. Det är också vanligt att visa termerna _domän_ eller _domännamn_ när du refererar till en värd utan underdomän som `adobe.com`. Det är inte viktigt att memorera de specifika villkoren för varje del och variant av en värd här. Men det är viktigt att vara medveten om att dessa termer används ofta, så att ni kan klargöra alla relevanta detaljer för ert företag och era diskussioner.

**Ursprung**

Origin är en annan term som du bör vara medveten om att den är närbesläktad med delar av en URL. På en grundläggande nivå är en origo ungefär `scheme` plus `host` plus `domain` som `https://business.adobe.com/se`. Olika värden representerar ofta olika ursprung som `https://business.adobe.com/se` och `http://business.adobe.com/se` är inte samma ursprung eftersom de har olika scheman. `https://www.adobe.com` och `https://business.adobe.com/se` är inte heller samma ursprung i många användningsområden på grund av de olika underdomänerna.

**Sökväg**

Den sista biten i URL-exemplet ovan är `path` till resursen - sidan i vårt exempel. Delen `/products/experience-platform/` representerar vanligtvis mappar eller kataloger på webbservern. På samma sätt som vi har mappar eller kataloger på våra datorer för dokument och foton har vi också mappar på webbservrar för att ordna innehåll. Slutligen är delen `/adobe-experience-platform.html` filens namn, webbsidan.

Det finns andra mer detaljerade delar av en URL som markeras i nästa del av den här serien.

### Tredjeparts-API:er

Webb-API:er kallas ibland för tredjeparts-API:er. Tänk på detta som de parter som är inblandade i en transaktion. I vårt länkexempel är du - eller mer specifikt din webbläsare - den första parten i sidförfrågan. Webbservern är den andra parten. Var är den tredje?

Det är vanligt att en webbsida innehåller innehåll eller resurser från andra värdar eller källor. När webbläsaren börjar visa sidan gör den i så fall ytterligare en uppsättning förfrågningar till de andra värdarna, eller&quot;tredje part&quot;, som har dessa resurser. Detta är mycket vanligt, särskilt för mediematerial som videor eller bilder, men också för data som behöver uppdateras när de visas eller används. Att få aktuell tid på dygnet, aktuellt väder eller ett personligt välkomstmeddelande för en viss person är exempel på när ett tredjeparts-API kan tillhandahålla rätt resurs vid rätt tidpunkt. Det är vanligt att dessa förfrågningar kommer från dessa tredjeparts-API:er.

## Vanliga användningsområden för webb-API:er

Förutom när det gäller tid på dygnet, vädret eller personaliserat innehåll finns det många användningsområden för webb-API:er. Plattformar för sociala medier som Twitter, TikTok, Facebook, LinkedIn, Snapchat, Pinterest och andra har en mängd olika API:er som programmerare kan använda med sina program. Adobe har förstås också [ett stort antal API:er](https://developer.adobe.com/apis) som programmerare använder så att deras program kan interagera med Adobe produkter och tjänster. Programvaruprodukter och -tjänster har åtkomst till andra programvaruprodukter och -tjänster via dessa API:er.

## Exempel-API:er

Webbläsar-API:er gör att programmerare kan interagera med webbläsarens funktioner direkt. Med Battery API kan programvaran kontrollera batteristatus för en enhet så att den kan varna dig vid behov. Med Clipboard API kan du kopiera eller klistra in programvara med enhetens urklipp. Med fullskärms-API:t kan programmet visa alternativet att utöka vyn till hela skärmen på enheten, som YouTube.

Adobe Experience Platform Data Access API är ett webb-API som gör att programmerare kan få åtkomst till och hämta datauppsättningsfiler från Adobe Experience Platform så att de kan använda kundprofildata i sina egna program. Det är mycket vanligt att API:er som detta är en del av en programautomatiseringsprocess där programvara programmeras för att utföra en sekvens med olika API:er i kombination. Detta kan ofta vara en betydande kostnadsbesparing jämfört med att manuellt utföra samma steg.

## API-slutpunkter

När programmerare&quot;använder&quot; en webbläsare eller ett webb-API i sina program begär de vanligtvis att få skicka eller ta emot resurser, som vår exempelwebbläsare som begär en webbsida. I API-dokumentationen visas ofta slutpunkter för dessa begäranden, till exempel: `https://platform.adobe.io/data/foundation/export/files/{dataSetFileId}`. Detta är det specifika mönstret eller slutpunkten för det API för plattformsdataåtkomst som en programmerare använder för att hämta en datauppsättningsfil.

`{dataSetFileId}` omgiven av klammerparenteserna representerar ett värde som programmeraren måste skicka i begäran. URL:en i den faktiska API-begäran ser ut ungefär som `https://platform.adobe.io/data/foundation/export/files/xyz123brb` där `xyz123brb` måste vara ett giltigt ID för den datauppsättningsfil som programmeraren vill ta emot.

På samma sätt som webbläsaren hämtar en sida på en viss URL, hämtar API-begäranden resurser från eller skickar resurser till en specifik slutpunkt som den här datauppsättningsexemplet.

## HTTP-begärandemetoder

Nu bör det vara tydligt att webb-API:er begär resurser som webbsidor eller datauppsättningar. Precis som de flesta programvarubegrepp följer dessa HTTP-begäranden repeterbara mönster. En begäran skickas från ett programvaruprogram till ett annat program som utvärderar begäran och sedan svarar: webbläsaren begär en sida från en webbserver och svarar med sidinnehållet.

Hela processen från begäran till svar omfattar många mindre och mycket detaljerade steg, men förfrågningsmetoderna är enkla. Begärandemetoder definierar den åtgärd som begärs.

**`GET`**

Begärandemetoden `GET` används när du begär ett svar som tillhandahåller en resurs, till exempel webbsidan och datauppsättningsexempel. När vi klickar på en länk i en webbläsare eller trycker på en länk på en mobil enhet gör vi en `GET`-begäran bakom scenerna.

**`POST`**

Metoden `POST` skickar data med begäran. Det kan te sig konstigt att en&quot;begäran&quot; skickar data, men idén är att när API-begäran görs, uppmanas slutpunkten (den mottagande programvaran) att acceptera begäran och, när det gäller en `POST`, att även acceptera de data som skickas. De data som skickas skrivs vanligtvis till ett datalager, som en databas eller fil, så att de kan sparas.

**`PUT`**

`PUT`-förfrågningsmetoden liknar `POST` eftersom den skickar data, men om de data som skickas redan finns vid slutpunkten uppdaterar en `PUT` befintliga data genom att ersätta dem. En `POST` uppdateras inte, den skickar bara, så flera `POST`-begäranden kan skapa flera poster av skickade data i stället för att uppdatera befintliga poster.

**`PATCH`**

Begärandemetoden `PATCH` används för att skicka data som uppdaterar en del av en befintlig post, som när vi ändrar vår adress genom att uppdatera vår kontoprofil. Med en `POST`-begäran kunde en extra profil skapas och med en `PUT` kunde den befintliga profilen ersättas, men med metoden `PATCH` uppdaterar vi bara den relevanta delen av den befintliga posten, som vår adress.

**`DELETE`**

Begärandemetoden `DELETE` tar bort en resurs som anges i begäran, som om vi klickar på en länk för att ta bort hela vår kontoprofil.

Det finns flera andra, men det här är en lista över de vanligaste metoderna när du arbetar med API:er.

### Exempel på begäran

Nu när du har de grundläggande villkoren, begreppen och stegen som ingår i API:erna kan vi titta på en exempelbegäran om API i praktiken.

Sidan från webbläsarexemplet har URL:en `https://business.adobe.com/se/products/experience-platform/adobe-experience-platform.html`. När du klickar på länken Adobe Experience Platform gör webbläsaren en `GET`-begäran för den här sidan. Eftersom vi har webbläsaren att göra jobbet åt oss behöver vi bara klicka, men om en programmerare vill att det ska ske i ett programvaruprogram måste de ange all information som krävs för att API-begäran ska lyckas.

Så här kan det se ut i koden:

```js
fetch(
  "https://business.adobe.com/se/products/experience-platform/adobe-experience-platform.html",
  {
    headers: {
      accept:
        "text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9",
      "accept-language": "en-US,en;q=0.9",
      "sec-ch-ua":
        '" Not A;Brand";v="99", "Chromium";v="101", "Microsoft Edge";v="101"',
      "sec-fetch-dest": "document",
      "sec-fetch-mode": "navigate",
      "sec-fetch-site": "none",
      "sec-fetch-user": "?1",
      "upgrade-insecure-requests": "1",
    },
    referrerPolicy: "strict-origin-when-cross-origin",
    body: null,
    method: "GET",
    mode: "cors",
    credentials: "include",
  }
);
```

I koden ovan kan du se `URL` som webbläsaren begär, och längst ned finns förfrågningsmetoden `method: "GET"`. De andra kodraderna är också en del av begäran, men ligger utanför artikelns omfång.


*[API]: Application Programming Interface
*[URL]: Uniform Resource Locator
*[HTTP]: HyperText Transfer Protocol
*[DNS]: DNS
