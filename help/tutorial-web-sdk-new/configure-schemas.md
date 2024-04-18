---
title: Skapa ett XDM-schema för webbdata
description: Lär dig hur du skapar ett XDM-schema för webbdata i gränssnittet för datainsamling. Den här lektionen ingår i självstudiekursen Implementera Adobe Experience Cloud med Web SDK.
feature: Web SDK,Schemas
exl-id: 159f914a-43d4-4808-b6af-01136386e25c
source-git-commit: fe8b92c560c9676a44935005cc558388244d6aea
workflow-type: tm+mt
source-wordcount: '1457'
ht-degree: 0%

---

# Skapa ett XDM-schema för webbdata

Lär dig hur du skapar ett XDM-schema för webbdata i gränssnittet för datainsamling.

XDM-scheman (Experience Data Model) är byggstenar, principer och bästa praxis för datainsamling i Adobe Experience Platform.

Platform Web SDK använder ditt schema för att standardisera dina webbhändelsedata, skicka dem till Platform Edge Network och slutligen vidarebefordra data till alla Experience Cloud-program som konfigurerats i datastream. Det här steget är viktigt eftersom det definierar en standarddatamodell som krävs för inmatning av kundupplevelsedata i Experience Platform och möjliggör tjänster och applikationer som bygger på dessa standarder.

## Varför modellera data?

Företag har sitt eget språk för att kommunicera om sin domän. Bilhandlare hanterar fabriker, modeller och cylindrar. Flygbolagen hanterar flightnummer, tjänsteklass och platstilldelningar. Vissa av dessa villkor är unika för ett visst företag, andra delas av ett vertikalt företag i branschen och andra delas av nästan alla företag. För termer som delas av en bransch vertikalt eller till och med bredare, kan ni börja göra kraftfulla saker med era data när ni namnger och strukturerar dessa termer på ett gemensamt sätt.

Många företag hanterar till exempel beställningar. Vad händer om dessa företag tillsammans beslutar sig för att göra en beställning på ett liknande sätt? Tänk dig till exempel om datamodellen består av ett objekt med en `priceTotal` som representerade orderns totala pris? Vad händer om det objektet också har egenskaper med namnet `currencyCode` och `purchaseOrderNumber`? Orderobjektet kanske innehåller en egenskap med namnet `payments` som skulle vara en matris med betalningsobjekt. Varje objekt motsvarar en betalning för ordern. En kund kanske till exempel har betalat för en del av beställningen med ett presentkort och betalat för resten med kreditkort. Du kan börja skapa en modell som ser ut ungefär så här:

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

Det här är Adobe mål. [Experience Data Model](https://business.adobe.com/products/experience-platform/experience-data-model.html). XDM tillhandahåller preskriptiv modellering för data som är vanliga i branschen, samtidigt som du kan utöka modellen efter dina specifika behov. Adobe Experience Platform är byggt kring XDM och därför måste data som skickas till Experience Platform finnas i XDM. I stället för att fundera på var och hur ni kan omvandla era aktuella datamodeller till XDM innan ni skickar data till Experience Platform bör ni överväga att implementera XDM i hela organisationen så att översättningen sällan behöver ske.


>[!NOTE]
>
> I demonstrationssyfte bygger övningarna i den här lektionen upp ett exempelschema för att fånga innehåll som visas och produkter som köpts av kunder i [Luma Demo Site](https://luma.enablementadobe.com/content/luma/us/en.html). Du kan använda de här stegen för att skapa ett annat schema för dina egna syften, men vi rekommenderar att du först följer med när du skapar exempelschemat för att lära dig funktionerna i schemaredigeraren.

Ta en kurs om du vill veta mer om XDM-scheman [Modellera era kundupplevelsedata med XDM](https://experienceleague.adobe.com/?recommended=ExperiencePlatform-D-1-2021.1.xdm) eller se [XDM - systemöversikt](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=sv).

## Utbildningsmål

När lektionen är klar kan du:

* Skapa ett XDM-schema inifrån datainsamlingsgränssnittet
* Lägg till fältgrupper i XDM-schemat
* Skapa XDM-scheman för webbhändelsedata enligt vedertagna standarder

## Förutsättningar

Alla nödvändiga etablerings- och användarbehörigheter för datainsamling och Adobe Experience Platform som beskrivs på [översikt](overview.md) sida.

## Skapa ett XDM-schema

XDM-scheman är standardsättet att beskriva data i Experience Platform, vilket gör att alla data som överensstämmer med scheman kan återanvändas i en organisation utan konflikter, eller till och med delas mellan flera organisationer. Mer information finns i [Grunderna för schemakomposition](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=en).

I den här övningen skapar du ett XDM-schema med de rekommenderade baslinjefältgrupperna för att hämta webbhändelsedata på [Luma Demo Site](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"}:

1. Öppna [Gränssnitt för datainsamling](https://launch.adobe.com/){target="_blank"}
1. Kontrollera att du är i rätt sandlåda. Hitta sandlådan i det övre högra hörnet

   >[!NOTE]
   >
   >Om du använder ett plattformsbaserat program som Real-Time CDP eller Journey Optimizer rekommenderar vi att du använder en utvecklingssandlåda för den här kursen. Om du inte gör det använder du **[!UICONTROL Prod]** sandlåda.

1. Gå till **[!UICONTROL Schemas]** till vänster navigering
1. Välj **[!UICONTROL Create Schema]** överst till höger

   ![Skapa schema](assets/schema-xdm-create-schema.png)
1. Välj **[!UICONTROL Experience Event]** på följande skärm
1. Välj **[!UICONTROL Next]**

   ![Schemaupplevelsehändelse](assets/schema-experience-event.png)

1. Ange namnet på schemat under **[!UICONTROL Schema display name]** fält, i detta fall `Luma Web Event Data`

   >[!TIP]
   >
   >En vanlig namnkonvention för XDM-scheman är att namnge schemat efter datakällan.


1. Välj Slutför

   ![Schemaupplevelsehändelse - slut](assets/schema-name-schema.png)

## Lägg till fältgrupper

Som tidigare nämnts är XDM det centrala ramverket som standardiserar kundupplevelsedata genom att tillhandahålla gemensamma strukturer och definitioner för användning i Adobe Experience Platform-tjänster längre fram i kedjan. Genom att följa XDM-standarder _alla kundupplevelsedata_ kan införlivas i en gemensam representation. Med den här metoden kan ni få värdefulla insikter från kundåtgärder, definiera kundmålgrupper genom segment och uttrycka kundattribut för personalisering med hjälp av data från flera olika källor. Se [Bästa tillvägagångssätt för datamodellering](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/best-practices.html?lang=en) för mer information.

När det är möjligt bör du använda befintliga fältgrupper och följa en produktmedveten modell och namnkonventioner. För alla data som är specifika för din organisation och som inte passar in i de fördefinierade fältgrupperna ovan kan du skapa en anpassad fältgrupp. Se [Skapa ett schema med Schemaredigeraren](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html?lang=en#create) för mer detaljerade steg om anpassade scheman.

>[!TIP]
> 
>I den här övningen lägger du till de rekommenderade fördefinierade fältgrupperna för insamling av webbdata: _**[!UICONTROL AEP Web SDK ExperienceEvent]**_och_**[!UICONTROL Consumer Experience Event]**_.
>
>
> Om du bara implementerar **Adobe Analytics** med Web SDK och inte skicka data till **Experience Platform**, använder du [!UICONTROL Adobe Analytics ExperienceEvent Template] fältgrupp för att definiera XDM-schemat. Detta kommer att användas i [Konfigurationsanalys](setup-analytics.md) lektion.

1. I **[!UICONTROL Field groups]** avsnitt, markera **[!UICONTROL Add]**

   ![Ny fältgrupp](assets/schema-new-field-group.png)

1. Sök efter [!UICONTROL `AEP Web SDK ExperienceEvent`]
1. Markera rutan
1. Sök efter [!UICONTROL `Consumer Experience Event`]
1. Markera rutan
1. Välj **[!UICONTROL Add field groups]**

   ![Lägg till fältgrupp](assets/schema-add-field-group.png)

Observera att du har tillgång till de mest använda nyckelvärdepar som krävs för datainsamling på webben i båda fältgrupperna. The [!UICONTROL display name] av varje fält visas för marknadsförarna i segmentbygggränssnittet i plattformsbaserade program och du kan ändra visningsnamnet för standardfält efter behov. Du kan också ta bort fält som du inte vill ha. När du klickar på något av fältgruppsnamnen markeras vilka nyckelvärdepar som tillhör det. I exemplet nedan ser du vilka grupper som tillhör **[!UICONTROL Consumer Experience Event]**.

![Fältgrupper för schema](assets/schema-consumer-experience-event.png)

Den här lektionen är bara en startpunkt. När du skapar ett eget webbeventschema måste du utforska och dokumentera dina affärskrav. Den här processen påminner om att skapa en [Dokument för verksamhetskrav](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/implementation-basics/creating-a-business-requirements-document.html) och [Referens för lösningsdesign](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/implementation-basics/creating-and-maintaining-an-sdr.html) för en Adobe Analytics-implementering, men bör innehålla krav för _alla nedströmsdatamottagare_ som till exempel mål för plattform, mål och händelsespelare.


### identityMap-objektet

Det finns ett särskilt fält som används för att identifiera webbanvändare som kallas `[!UICONTROL identityMap]`.

![Webbhändelsedata för Luma](assets/schema-identityMap.png)

Det är ett måste-ha-objekt för alla webbrelaterade datainsamlingar eftersom det innehåller det Experience Cloud-ID som krävs för att identifiera användare på webben. Det är också nyckeln till att ange interna kund-ID:n för autentiserade användare. `[!UICONTROL identityMap]` diskuteras mer i [Konfigurera identiteter](configure-identities.md) lektion. Den inkluderas automatiskt i alla scheman med **[!UICONTROL XDM ExperienceEvent]** klassen.


>[!IMPORTANT]
>
> Det går att aktivera **[!UICONTROL Profile]** för ett schema innan du sparar schemat. **Gör inte** aktivera det nu. När ett schema har aktiverats för profilen kan det inte inaktiveras eller tas bort. Det går inte att ta bort fält från scheman just nu, även om det går att [Föråldrade fält i användargränssnittet](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/field-deprecation-ui.html?lang=en#deprecate). Dessa konsekvenser är viktiga att tänka på senare när du arbetar med egna data i produktionsmiljön.
>
>
>Den här inställningen diskuteras mer under [Konfigurera Experience Platform](setup-experience-platform.md) lektion.
>![Profilschema](assets/schema-profile.png)

Om du vill slutföra den här lektionen väljer du **[!UICONTROL Save]** överst till höger.

![Spara schema](assets/schema-select-save.png)


Nu kan du referera till det här schemat när du lägger till Web SDK-tillägget i taggegenskapen.


[Nästa: ](configure-identities.md)

>[!NOTE]
>
>Tack för att du lade ned din tid på att lära dig om Adobe Experience Platform Web SDK. Om du har frågor, vill dela allmän feedback eller har förslag på framtida innehåll kan du dela med dig av dem om detta [Experience League diskussionsinlägg](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
