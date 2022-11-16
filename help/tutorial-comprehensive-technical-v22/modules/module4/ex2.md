---
title: Frågetjänst - Använda frågetjänsten
description: Frågetjänst - Använda frågetjänsten
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst, BI Expert
doc-type: tutorial
activity: develop
exl-id: dbf19991-cb09-43cf-887c-52996dfd2986
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 0%

---

# 4.2 Använda frågetjänsten

## Syfte

- Hitta och utforska datauppsättningar
- Lär dig hur du hanterar Experience Data Models-objekt och -attribut i dina frågor

## Kontext

Här får du lära dig hur du använder PSQL för att hämta information om tillgängliga datauppsättningar, hur du skriver frågor för Experience Data Model (XDM) och skriver dina första enkla rapporteringsfrågor med hjälp av datamängderna Frågetjänst och Citi Signal.

## 4.2.1 Grundläggande frågor

Här får du lära dig mer om metoderna för att hämta information om tillgängliga datauppsättningar och hur du hämtar data korrekt med en fråga från en XDM-datauppsättning.

Alla datauppsättningar som vi har utforskat via Adobe Experience Platform i början av 1 är också tillgängliga som tabeller via ett SQL-gränssnitt. Du kan använda **visa tabeller,** -kommando.

Kör **visa tabeller,** i **PSQL kommandoradsgränssnitt**. (glöm inte att avsluta kommandot med ett semikolon).

Kopiera kommandot **visa tabeller,** och klistra in vid kommandotolken:

![command-prompt-show-tables.png](./images/command-prompt-show-tables.png)

Följande resultat visas:

```text
aepenablementfy21:all=> show tables;
                            name                            |        dataSetId         |                            dataSet                             | description | resolved 
------------------------------------------------------------+--------------------------+----------------------------------------------------------------+-------------+----------
 demo_system_event_dataset_for_call_center_global_v1_1      | 5fd1a9dea30603194baeea43 | Demo System - Event Dataset for Call Center (Global v1.1)      |             | false
 demo_system_event_dataset_for_mobile_app_global_v1_1       | 5fd1a9de250e4f194bec84cd | Demo System - Event Dataset for Mobile App (Global v1.1)       |             | false
 demo_system_event_dataset_for_voice_assistants_global_v1_1 | 5fd1a9de49ee76194b85f73c | Demo System - Event Dataset for Voice Assistants (Global v1.1) |             | false
 demo_system_event_dataset_for_website_global_v1_1          | 5fd1a9dee3224d194cdfe786 | Demo System - Event Dataset for Website (Global v1.1)          |             | false
 demo_system_profile_dataset_for_loyalty_global_v1_1        | 5fd1a9de250e4f194bec84cc | Demo System - Profile Dataset for Loyalty (Global v1.1)        |             | false
 demo_system_profile_dataset_for_ml_predictions_global_v1_1 | 5fd1a9de241f58194b0cb117 | Demo System - Profile Dataset for ML Predictions (Global v1.1) |             | false
 demo_system_profile_dataset_for_mobile_app_global_v1_1     | 5fd1a9deddf353194a2e00b7 | Demo System - Profile Dataset for Mobile App (Global v1.1)     |             | false
 demo_system_profile_dataset_for_website_global_v1_1        | 5fd1a9de42a61c194dd7b810 | Demo System - Profile Dataset for Website (Global v1.1)        |             | false
 journey_step_events                                        | 5fd1a7f30268c5194bbb7e5e | Journey Step Events                                            |             | false
```

Tryck på blankstegstangenten i kolonet för att visa nästa sida i resultatuppsättningen, eller ange `q` för att återgå till kommandotolken.

Alla datauppsättningar i plattformen har sin motsvarande frågetjänsttabell. Du kan hitta en datamängds tabell via datauppsättningsgränssnittet:

![ui-dataset-tablename.png](./images/ui-dataset-tablename.png)

The `demo_system_event_dataset_for_website_global_v1_1` tabellen är frågetjänsttabellen som motsvarar `Demo System - Event Schema for Website (Global v1.1)` datauppsättning.

Om du vill ha information om var en produkt visades väljer vi **geo** information.

Kopiera programsatsen nedan och klistra in den när du uppmanas till det i **PSQL kommandoradsgränssnitt** och tryck på Retur:

```sql
select placecontext.geo
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
```

I frågeresultatet kommer du att märka att kolumner i Experience Data Model (XDM) kan vara komplexa typer och inte bara skalära typer. I frågan ovan vill vi identifiera geografiska platser där en **commerce.productViews** inträffade. Identifiera en **commerce.productViews** måste vi navigera i XDM-modellen med **.** (punkt).

```text
aepenablementfy21:all=> select placecontext.geo
aepenablementfy21:all-> from   demo_system_event_dataset_for_website_global_v1_1
aepenablementfy21:all-> where  eventType = 'commerce.productViews'
aepenablementfy21:all-> and placecontext.geo.countryCode <> ''
aepenablementfy21:all-> limit 1;
                  geo                   
----------------------------------------
 ("(57.4694803,-3.1269422)",Tullich,GB)
(1 row)
```

Observera att resultatet är ett platt objekt i stället för ett värde? The **placecontext.geo** objektet innehåller fyra attribut: schema, land och stad. När ett objekt deklareras som en kolumn returneras hela objektet som en sträng. XDM-schemat kan vara mer komplext än det du är van vid, men det är mycket kraftfullt och har utformats för att stödja många lösningar, kanaler och användningsfall.

Om du vill markera ett objekts enskilda egenskaper använder du **.** (punkt).

Kopiera programsatsen nedan och klistra in den när du uppmanas till det i **PSQL kommandoradsgränssnitt**:

```sql
select placecontext.geo._schema.longitude
      ,placecontext.geo._schema.latitude
      ,placecontext.geo.city
      ,placecontext.geo.countryCode
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
```

Resultatet av ovanstående fråga bör se ut så här.
Resultatet är nu ett inställt enkelt värde:

```text
aepenablementfy21:all=> select placecontext.geo._schema.longitude
aepenablementfy21:all->       ,placecontext.geo._schema.latitude
aepenablementfy21:all->       ,placecontext.geo.city
aepenablementfy21:all->       ,placecontext.geo.countryCode
aepenablementfy21:all-> from   demo_system_event_dataset_for_website_global_v1_1
aepenablementfy21:all-> where  eventType = 'commerce.productViews'
aepenablementfy21:all-> and placecontext.geo.countryCode <> ''
aepenablementfy21:all-> limit 1;
 longitude  |  latitude  |  city   | countrycode 
------------+------------+---------+-------------
 -3.1269422 | 57.4694803 | Tullich | GB
(1 row)
```

Oroa dig inte, det finns ett enkelt sätt att hitta vägen till en viss egenskap. Här nedan får du lära dig hur.

Du måste redigera en fråga, så vi öppnar först en redigerare.

I Windows

Klicka på **sök** ikon i verktygsfältet för fönster, skriv **anteckningsblock** i **sök** klickar du på **anteckningsblock** resultat:

![windows-start-notepad.png](./images/windows-start-notepad.png)

På Mac

Installera [Hakparenteser](https://github.com/adobe/brackets/releases/download/release-1.14/Brackets.Release.1.14.dmg) eller använd en annan textredigerare om du inte har den installerad och följ instruktionerna. Efter installationen kan du söka efter **Hakparenteser** genom Mac spotlight-sökning och öppna den.

Kopiera följande programsats till anteckningsblock eller hakparenteser:

```sql
select your_attribute_path_here
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
```

Gå tillbaka till användargränssnittet i Adobe Experience Platform (bör vara öppet i webbläsaren) eller navigera till [https://platform.adobe.com](https://platform.adobe.com).

Välj **Scheman**, ange `Demo System - Event Schema for Website (Global v1.1)` i **sök** fält och markera `Demo System - Event Schema for Website (Global v1.1) Schema` från listan.

![browse-schema.png](./images/browse-schema.png)

Utforska XDM-modellen för **Demonstrationssystem - händelseschema för webbplats (Global v1.1)** genom att klicka på ett objekt. Expandera trädet för **placecontext**, **geo** och **schema**. När du väljer det faktiska attributet **longitud** visas hela sökvägen i den markerade röda rutan. Om du vill kopiera attributets sökväg klickar du på ikonen för kopieringssökväg.

![explore-schema-for-path.png](./images/explore-schema-for-path.png)

Växla till din anteckningsruta/parenteser och ta bort **your_attribute_path_here** från första raden. Placera markören efter **välj** på första raden och klistra in (CTRL-V).

Kopiera den ändrade programsatsen från anteckningsblock/hakparenteser och klistra in den vid uppmaningen i **PSQL kommandoradsgränssnitt** och tryck på Enter.

Resultatet ska se ut så här:

```text
aepenablementfy21:all=> select placeContext.geo._schema.longitude
aepenablementfy21:all-> from   demo_system_event_dataset_for_website_global_v1_1
aepenablementfy21:all-> where  eventType = 'commerce.productViews'
aepenablementfy21:all-> and placecontext.geo.countryCode <> ''
aepenablementfy21:all-> limit 1;
 longitude  
------------
 -3.1269422
```

Nästa steg: [4.3 Frågor, frågor, frågor.. och bortvinningsanalys](./ex3.md)

[Gå tillbaka till modul 4](./query-service.md)

[Gå tillbaka till Alla moduler](../../overview.md)
