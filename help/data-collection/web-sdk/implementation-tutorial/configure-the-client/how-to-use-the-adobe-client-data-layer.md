---
title: Så här använder du datalagret för klienten i Adobe
description: Så här använder du datalagret för klienten i Adobe
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 33a5db8c-e49b-4073-b4d7-4abe19537fcb
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 0%

---

# Så här använder du datalagret för klienten i Adobe

I [Vad är ett datalager?](whats-a-data-layer.md)har du lärt dig att det finns två saker att tänka på när du diskuterar datalager: behållaren och innehållet. Adobe-klientdatalagret är behållaren. Det bryr sig inte om hur du [strukturera dina data](../structuring-your-data.md) eller vilken information du vill lägga in i dina data. Data kan struktureras som [XDM](../structuring-your-data.md#xdm), som exemplen nedan visar, eller så kan du skapa en egen struktur helt och hållet.

I idealfallet ansvarar företagets tekniker för att föra in alla nödvändiga data i datalagret med kod på sidan. Marknadsföringsteamet hämtar sedan data från datalagret, helst med Adobe Experience Platform Tags.

## Överföra data till datalagret

Adobe Client Data Layer är en JavaScript-array. När du skapar Adobe-klientdatalagret börjar det tomt:

```js
window.adobeDataLayer = window.adobeDataLayer || [];
```

Om du vill placera data i datalagret anropar du `push` metod i datalagerarrayen:

```js
window.adobeDataLayer.push({
  "claims": {
    "ID": "CL10991306",
    "policyID": "IXP28113",
    "type": "automobile"
  }
});
```

Du kan när som helst överföra ytterligare data till datalagret genom att anropa `push` igen.

```js
window.adobeDataLayer.push({
  "claims": {
    "status": "approved",
    "benefitAmount": {
      "amount": 1827.90,
      "currencyCode": "USD"
    }
  }
});
```

## Förstå push-data

Om du implementerade de två föregående `push` -anrop får du två poster i datalagrets array. Datalagret är inte särskilt användbart i det här läget. Vanligtvis vill du komma åt det sammanslagna läget för datalagret, eller med andra ord ett enda objekt som är det kombinerade resultatet av alla data som du har överfört till datalagret. Vi kommer att lära oss att komma åt det här sammanfogade läget senare i självstudiekursen. För närvarande räcker det att förstå att datalagrets beräknade status efter våra två `push` Anrop skulle vara följande:

```json
{
  "claims": {
    "ID": "CL10991306",
    "policyID": "IXP28113",
    "type": "automobile",
    "status": "approved",
    "benefitAmount": {
      "amount": 1827.90,
      "currencyCode": "USD"
    }
  }
}
```

## Tar bort data

Ibland måste du ta bort datadelar från datalagret. Detta är särskilt vanligt i enkelsidiga program när användaren navigerar från en vy till nästa. Om användaren till exempel navigerar från en produktvy till en kontaktvy kan det vara bra att radera produktdata i datalagret eftersom det inte längre är relevant för den aktiva vyn.

Du kan ta bort data genom att trycka på värdet för `undefined` för den tangent som du vill ta bort. Om du vill ta bort `status` från datalagret ser koden ut så här:

```js
window.adobeDataLayer.push({
  "claims": {
    "status": undefined
  }
});
```

Datalagrets beräknade läge inkluderar inte längre `status`:

```json
{
  "claims": {
    "ID": "CL10991306",
    "policyID": "IXP28113",
    "type": "automobile",
    "benefitAmount": {
      "amount": 1827.90,
      "currencyCode": "USD"
    }
  }
}
```

## Överföra händelser till datalagret

Adobe-klientdatalagret används inte bara för att lagra data, utan även för att kommunicera vilka händelser som inträffar på sidan. Faktum är att du vanligtvis överför data till datalagret _som ett resultat_ om en händelse som inträffar på sidan. Dessa händelser omfattar (1) interaktionshändelser, som att öppna en chattbot eller skriva en sökterm i ett sökfält eller (2) icke-interaktionshändelser, som att visa en annons eller slutföra beräkningar av webbsidans prestanda.

Om du vill kommunicera om att en händelse har inträffat på sidan, inkluderar du en `event` -tangenten i objektet som du flyttar till datalagret. Du kanske vill meddela att en användare har angett en sökfråga i ett sökfält.

```js
window.adobeDataLayer.push({
  "event": "searchQueryEntered"
});
```

Senare får du lära dig hur du aktiverar regler i Adobe Experience Platform Tags när en viss händelse överförs till datalagret. Observera även att `event` key is _not_ ingår i det beräknade tillståndet. Den får särskild behandling av datalagret.

## Överföra händelser och data till datalagret

Att meddela avlyssnare att användaren har angett en sökfråga är praktiskt, men vad gör jag om du vill ange ytterligare information om händelsen? Du kanske vill ta med användarens sökfråga. Du kan tillhandahålla dessa data på ett av två sätt:

1. Ange data så att de **behålls** i datalagret som en del av datalagrets beräknade läge.
2. Ange data så att de **bevaras inte** i datalagret som en del av datalagrets beräknade läge.

Om du vill behålla data i datalagret beror vanligtvis på om du tänker referera till dessa data under den tid som användaren är på sidan. Om det inte gör det kan det bli ett rörigt datalager om data behålls i datalagret.

Här är ett exempel på hur du överför en händelse med ytterligare data som **behålls** i datalagret:

```js
window.adobeDataLayer.push({
  "event": "searchQueryEntered",
  "siteKnowledge": {
    "supportSiteSearch": {
      "term": "roller",
      "locationInPage": "topSearchBar"
    }
  }
});
```

Efter detta `push` äger rum, `siteKnowledge` kommer alltid att visas i datalagrets beräknade läge tills sidan tas bort från minnet (såvida du inte avsiktligt tar bort eller åsidosätter `siteKnowledge`).

Här följer ett exempel på hur du överför en händelse med ytterligare data som **bevaras inte** i datalagret:

```js
window.adobeDataLayer.push({
  "event": "searchQueryEntered",
  "eventInfo": {
    "siteKnowledge": {
      "supportSiteSearch": {
        "term": "roller",
        "locationInPage": "topSearchBar"
      }
    }
  }
});
```

Observera i det här exemplet att `siteKnowledge` är förpackad inuti `eventInfo`. The `eventInfo` key får särskild behandling av datalagret. Det talar om för datalagret att dessa data _bör_ inkluderas med händelsen som skickas till avlyssnare, men den _bör inte_ bevaras inuti datalagret. När avlyssnare (t.ex. Adobe Experience Platform-taggar) har underrättats om händelsen, glöms dessa data i stort sett bort. The `siteKnowledge` -tangenten visas aldrig i datalagrets beräknade läge.

Varje gång du ringer `push`kommer Adobe Client Data Layer att meddela alla avlyssnare. Senare får vi lära oss att lyssna på de här meddelandena från Adobe Experience Platform Tags och aktivera regler utifrån detta.
