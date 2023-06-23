---
title: Strukturera data
description: Strukturera data
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: d300429a-5a66-4b61-97cb-b934fc8e8291
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# Strukturera data

Företag har sitt eget språk för att kommunicera om sin domän. Bilhandlare hanterar fabriker, modeller och cylindrar. Flygbolagen hanterar flightnummer, tjänsteklass och platstilldelningar. Vissa av dessa villkor är unika för ett visst företag, andra delas av ett vertikalt företag i branschen och andra delas av nästan alla företag. För termer som delas av en bransch vertikalt eller till och med bredare, kan ni börja göra kraftfulla saker med era data när ni namnger och strukturerar dessa termer på ett gemensamt sätt.

Många företag hanterar till exempel beställningar. Vad händer om dessa företag tillsammans beslutar sig för att göra en beställning på ett liknande sätt. Tänk dig till exempel om datamodellen består av ett objekt med en `priceTotal` som representerar orderns totala pris. Vad händer om det objektet också har egenskaper med namnet `currencyCode` och `purchaseOrderNumber`. Orderobjektet kanske innehåller en egenskap med namnet `payments` som skulle vara en matris med betalningsobjekt. Varje objekt motsvarar en betalning för ordern. En kund kanske till exempel har betalat för en del av beställningen med ett presentkort och betalat för resten med kreditkort. Du kan börja skapa en modell som ser ut ungefär så här:

```json
{
  "order": {
    "priceTotal": 89.50,
    "currencyCode": "EUR",
    "purchaseOrderNumber": "JWN20192388410012",
    "payments": [
      {
        "paymentType": "gift_card",
        "paymentAmount": 50
      },
      {
        "paymentType": "credit_card",
        "paymentAmount": 39.50
      }
    ]
  }
}
```

Om alla företag som hanterar beställningar beslutar sig för att modellera sina beställningsdata på ett konsekvent sätt för termer som är vanliga i branschen kan magiska saker börja hända. Information skulle kunna utbytas smidigare både inom och utanför er organisation i stället för att man hela tiden tolkar och översätter data (utkast och evar, vem som helst?). Maskinininlärning kan enklare förstå vad dina data är _medel_ och tillhandahålla användbara insikter. Användargränssnitt för relevanta data kan bli mer intuitiva. Dina data kan integreras smidigt med partners och leverantörer som följer samma modellering.

## XDM

Det här är Adobe mål [Experience Data Model](https://business.adobe.com/products/experience-platform/experience-data-model.html). XDM tillhandahåller preskriptiv modellering för data som är vanliga i branschen, samtidigt som du kan utöka modellen efter dina specifika behov. Adobe Experience Platform är byggt kring XDM och därför måste data som skickas till Experience Platform finnas i XDM. I stället för att fundera på var och hur ni kan omvandla era aktuella datamodeller till XDM innan ni skickar data till Experience Platform bör ni överväga att implementera XDM i hela organisationen så att översättningen sällan behöver ske.
