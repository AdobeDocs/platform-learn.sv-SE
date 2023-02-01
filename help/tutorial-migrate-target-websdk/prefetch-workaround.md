---
title: Tillfällig lösning för förhämtning | Migrera mål från at.js 2.x till Web SDK
description: Lär dig hur du implementerar en tillfällig lösning för att skicka parametrar med förhämtning
source-git-commit: d061d2492d6d5e8e7a8a6e03ce63b9b6cd3793d8
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# Tillfällig lösning för förhämtning

Alla Target-kunder som inte var i produktion med Experience Platform Web SDK före den 1 oktober 2022 gör en begäran till Target från Experience Platform Edge Network med läget prefetch. Med Förhämtning kan webbläsaren förinläsa och cachelagra Target-erbjudanden så att de kan användas när besökaren når rätt läge på sidan. Detta är fördelaktigt i Single Page Applications (SPA) eftersom den önskade användarupplevelsen kan återges så snabbt som möjligt, utan ytterligare nätverksbegäranden. Det finns dock viktiga konsekvenser för både SPA och icke-SPA implementeringar.

I stället för att räkna en besökare i en aktivitet när erbjudandeinnehållet levereras i nätverksbegäran, räknas nu besökare i aktiviteter när en `propositionDisplay` sendEvent-begäran görs av Web SDK. Dessa förfrågningar görs automatiskt av VEC-aktiviteter (Visual Experience Composer) när renderDecision är inställt på true och när upplevelsen har återgetts på sidan. Med anpassade omfång och när renderDecision är inställt på false måste propositionDisplay-begäranden initieras avsiktligt av implementeraren. Dessutom _Alla parametrar som används för andra ändamål än omedelbar aktivitetskvalifikation ska skickas via en `propositionDisplay`  event_.

## Varför behövs lösningen?

I många Target-implementeringar kan viktiga nätverksbegäranden ibland göras utan att någon förväntan om att någon aktivitet ska levereras förväntas. Till exempel kan förfrågningar göras till:

* Konvertering av postorder
* Ange profilparametrar
* Utlös profilskript
* Skicka enhetsparametrar för att fylla i Recommendations-katalogen

I förhämtningsläge fungerar dessa inte som förväntat. I förhämtningsläget importeras dessa data inte såvida de inte är en del av en `propositionDisplay`.

## Vad är lösningen?

Lösningen består av tre delar:

1. Definiera ett anpassat omfång som en del av `sendEvent`
1. Använd det anpassade omfånget i en formulärbaserad aktivitet (aktiviteten kan hantera standardinnehåll)
1. Använd en svarshanterare för att skapa en annan `sendEvent` för propositionDisplay och inkludera de parametrar du behöver för att hämta ordningen, ange profilparametrarna, utlösa profilskriptet, skicka enhetsparametrarna osv.

Här följer ett exempel på hur lösningen kan användas för att skicka en profilparameter:


```JavaScript
var data = {
    "__adobe": {
        "target": {
            "profile.gender": "male"
        }
    }
};
// Send the initial event with the data object and custom decision scope
alloy("sendEvent", {
    "renderDecisions": true,
    data,
    decisionScopes: ['profile-param-example']
}).then(function(result) {
    var propositions = result.propositions;
    var ctaProposition;
    if (propositions) {
        // Find the discount proposition, if it exists.
        for (var i = 0; i < propositions.length; i++) {
            var proposition = propositions[i];
            if (proposition.scope === "profile-param-example") {
                ctaProposition = proposition;
                break;
            }
        }
    }
    if (ctaProposition) {
        // Send a "decisioning.propositionDisplay" event signaling that the proposition has been rendered, and includes the data object again
        alloy("sendEvent", {
            xdm: {
                eventType: "decisioning.propositionDisplay",
                _experience: {
                    decisioning: {
                        propositions: [{
                            id: ctaProposition.id,
                            scope: ctaProposition.scope,
                            scopeDetails: ctaProposition.scopeDetails
                        }]
                    }
                }
            },
            data
        });
    }
});
```

När profilen anges som en del av propositionDisplay sparas den i besökarens profil och är tillgänglig i efterföljande förfrågningar. Samma metod kan användas för att rapportera information om orderkonvertering och enhetsparametrar.

I taggar använder du händelsetypen Send Event Complete för att utlösa en händelse som innehåller ytterligare sendEvent.

## Hur vet jag om min implementering använder förhämtningsläge?

Du måste öppna en kundtjänstbiljett för att ta reda på om ditt konto använder förhämtningsläge.


>[!NOTE]
>
>Vi vill hjälpa dig att lyckas med målmigreringen från at.js till Web SDK. Om du stöter på problem med din migrering eller känner att det saknas viktig information i den här guiden ber vi dig att meddela oss genom att publicera i [den här communitydiskussionen](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).