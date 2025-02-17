---
title: Frågetjänst - Komma igång
description: Frågetjänst - Komma igång
kt: 5342
doc-type: tutorial
exl-id: 07f91736-2fb8-4381-b076-50df33f051b1
source-git-commit: 1e3a8d585503eddad4c642a3b13d2b5f7ddc9943
workflow-type: tm+mt
source-wordcount: '647'
ht-degree: 0%

---

# 2.1.2 Komma igång

## Bekanta dig med Adobe Experience Platform användargränssnitt

Gå till [Adobe Experience Platform](https://experience.adobe.com/platform). När du har loggat in loggar du in på Adobe Experience Platform hemsida.

![Datainmatning](./../../../../modules/delivery-activation/datacollection/dc1.2/images/home.png)

Innan du fortsätter måste du välja en **sandlåda**. Sandlådan som ska markeras har namnet ``--aepSandboxName--``. När du har valt rätt [!UICONTROL sandbox] visas skärmändringen och nu är du i din dedikerade [!UICONTROL sandbox].

![Datainmatning](./../../../../modules/delivery-activation/datacollection/dc1.2/images/sb1.png)

## Utforska data på plattformen

Att samla in data från olika kanaler är en svår uppgift för alla varumärken. Och i den här övningen engagerar Citi Signal-kunder med Citi Signal på sin webbplats, på sin mobilapp, så samlas köpdata in av Citi Sigals Point of Sale-system och de har CRM- och Loyalty-data. Citi Signal använder Adobe Analytics och Adobe Launch för att samla in data på sin webbplats, i mobilappen och i POS-systemet, så dessa data strömmar redan till Adobe Experience Platform. Vi börjar med att utforska alla data för Citi Signal som redan finns i Adobe Experience Platform.

Gå till **Datauppsättningar** på den vänstra menyn.

![emea-website-interaction-dataset.png](./images/emeawebsiteinteractiondataset.png)

Citi Signal direktuppspelar data till Adobe Experience Platform och dessa data är tillgängliga i datamängden `Demo System - Event Dataset for Website (Global v1.1)`. Sök efter `Demo System - Event Dataset for Website`.

![emea-callcenter-interaction-dataset.png](./images/emeawebsiteinteractiondataset1.png)

Citi Signals Callcenter Interaction-data hämtas i datamängden `Demo System - Event Dataset for Call Center (Global v1.1)`. Sök efter `Demo System - Event Dataset for Call Center` data i sökrutan. Klicka på datauppsättningens namn för att öppna den.

![emea-callcenter-interaction-dataset.png](./images/emeacallcenterinteractiondataset.png)

När du har klickat på datauppsättningen får du en översikt över datauppsättningsaktiviteten, t.ex. kapslade och misslyckade batchar. Klicka på **Förhandsgranska datauppsättning** om du vill visa ett exempel på data som lagras i datauppsättningen `Demo System - Event Dataset for Call Center (Global v1.1)`.

![preview-interaction-dataset.png](./images/previewinteractiondataset.png)

Den vänstra panelen visar schemastrukturen för den här datauppsättningen och till höger visas ett exempel på de data som har importerats.

![explore-interaction-dataset.png](./images/exploreinteractiondataset.png)

Klicka på **Stäng** för att stänga fönstret **Förhandsgranska datauppsättning**.

## Introduktion till frågetjänsten

Du kommer åt frågetjänsten genom att klicka på **Frågor** i den vänstra menyn.

![select-queries.png](./images/selectqueries.png)

Genom att gå till **Logg** kan du se sidan Frågelista där du får en lista över alla frågor som har körts i organisationen, med den senaste överst.

![query-list.png](./images/querylist.png)

Klicka på en SQL-fråga i listan och observera informationen i den högra listen.

![click-sql-query.png](./images/clicksqlquery.png)

Du kan rulla fönstret för att se hela frågan eller klicka på ikonen som är markerad nedan för att kopiera hela frågan till anteckningsrutan. Du behöver inte kopiera frågan just nu.

![click-copy-query.png](./images/clickcopyquery.png)

Du kan inte bara se de frågor som har körts. Med det här användargränssnittet kan du skapa nya datauppsättningar från frågor. Dessa datauppsättningar kan länkas till Adobe Experience Platform kundprofil i realtid eller användas som indata för Adobe Experience Platform Data Science Workspace.

## Anslut PSQL-klienten till frågetjänsten

Frågetjänsten stöder klienter med en drivrutin för PostgreSQL. Här kommer vi att använda PSQL, ett kommandoradsgränssnitt och Power BI eller Tableau. Låt oss ansluta till PSQL.

Klicka på **Referenser**.

![queries-select-configuration.png](./images/queriesselectconfiguration.png)

Skärmen visas nedan. Skärmen innehåller serverinformation och autentiseringsuppgifter för autentisering till frågetjänsten. För närvarande fokuserar vi på skärmens högra sida som innehåller ett anslutningskommando för PSQL. Klicka på knappen Kopiera för att kopiera kommandot till Urklipp.

![copy-psql-connection.png](./images/copypsqlconnection.png)

För Windows: Öppna kommandoraden genom att trycka på Windows-tangenten, skriva cmd och sedan klicka på resultatet av kommandotolken.

![open-command-prompt.png](./images/opencommandprompt.png)

För macOS: Öppna terminal.app via spotlight-sökning:

![open-terminal-osx.png](./images/openterminalosx.png)

Klistra in det anslutningskommando som du har kopierat från användargränssnittet för frågetjänsten och tryck på Retur i kommandotolken:

Windows:

![command-prompt-connected.png](./images/commandpromptconnected.png)

MacOS:

![command-prompt-paste-osx.png](./images/commandpromptpasteosx.png)

Du är nu ansluten till frågetjänsten med PSQL.

I de följande övningarna kommer det att finnas en hel del interaktion med detta fönster. Vi kallar det ditt **PSQL-kommandoradsgränssnitt**.

Nu kan du börja skicka frågor.

## Nästa steg

Gå till [2.1.3 med frågetjänsten](./ex3.md){target="_blank"}

Gå tillbaka till [frågetjänsten](./query-service.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../../overview.md){target="_blank"}
