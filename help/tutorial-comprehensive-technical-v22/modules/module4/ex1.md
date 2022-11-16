---
title: Frågetjänst - Komma igång
description: Frågetjänst - Komma igång
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst, BI Expert
doc-type: tutorial
activity: develop
exl-id: dae257d2-8c94-4558-b9ce-eca38a88667b
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 0%

---

# 4.1 Komma igång

## 4.1.1 Bekanta dig med Adobe Experience Platform användargränssnitt

Gå till [Adobe Experience Platform](https://experience.adobe.com/platform). När du loggat in kommer du till Adobe Experience Platform hemsida.

![Dataintag](../module2/images/home.png)

Innan du fortsätter måste du välja en **sandlåda**. Sandlådan som ska markeras har namnet ``--module7sandbox--``. Du kan göra detta genom att klicka på texten **[!UICONTROL Produktionsprodukt]** i den blå linjen ovanför skärmen. När du har valt lämplig [!UICONTROL sandlåda]kommer du att se skärmändringen och nu är du med på din [!UICONTROL sandlåda].

![Dataintag](../module2/images/sb1.png)


## 4.1.2 Utforska data på plattformen

Att samla in data från olika kanaler är en svår uppgift för alla varumärken. Och i den här övningen engagerar Citi Signal-kunder med Citi Signal på sin webbplats, på sin mobilapp, så samlas köpdata in av Citi Sigals Point of Sale-system och de har CRM- och Loyalty-data. Citi Signal använder Adobe Analytics och Adobe Launch för att samla in data på sin webbplats, i mobilappen och i POS-systemet, så dessa data flödar redan till Adobe Experience Platform. Vi börjar med att utforska alla data för Citi Signal som redan finns i Adobe Experience Platform.

Gå till den vänstra menyn **Datauppsättningar**.

![emea-website-interaction-dataset.png](./images/emea-website-interaction-dataset.png)

Citi Signal strömmar data till Adobe Experience Platform och dessa data finns i `Demo System - Event Dataset for Website (Global v1.1)` datauppsättning. Sök efter `Demo System - Event Dataset for Website`.

![emea-callcenter-interaction-dataset.png](./images/emea-website-interaction-dataset1.png)

Citi Signals Callcenter Interaction-data hämtas i `Demo System - Event Dataset for Call Center (Global v1.1)` datauppsättning. Sök efter `Demo System - Event Dataset for Call Center` data i sökrutan. Klicka på datauppsättningens namn för att öppna den.

![emea-callcenter-interaction-dataset.png](./images/emea-callcenter-interaction-dataset.png)

När du har klickat på datauppsättningen får du en översikt över datauppsättningsaktiviteten, t.ex. kapslade och misslyckade batchar.

![preview-interaction-dataset.png](./images/preview-interaction-dataset.png)

Klicka på **Förhandsgranska datauppsättning** för att se exempel på data som lagras i `Demo System - Event Dataset for Call Center (Global v1.1)` datauppsättning. Den vänstra panelen visar schemastrukturen för den här datauppsättningen.

![explore-interaction-dataset.png](./images/explore-interaction-dataset.png)

Klicka på **Stäng** för att stänga **Förhandsgranska datauppsättning** -fönstret.

## 4.1.3 Introduktion till Query Service

Adobe Experience Platform Query Service öppnas genom att man klickar på **Frågor** i den vänstra menyn.

![select-queries.png](./images/select-queries.png)

Genom att gå till **Logg** På sidan Frågelista visas en lista med alla frågor som har körts i organisationen, med den senaste överst.

![query-list.png](./images/query-list.png)

Klicka på en SQL-fråga i listan och observera informationen i den högra listen.

![click-sql-query.png](./images/click-sql-query.png)

Du kan rulla fönstret för att se hela frågan eller klicka på ikonen som är markerad nedan för att kopiera hela frågan till anteckningsrutan. Du behöver inte kopiera frågan just nu.

![click-copy-query.png](./images/click-copy-query.png)

Du kan inte bara se de frågor som har körts. Med det här användargränssnittet kan du skapa nya datauppsättningar från frågor. Dessa datauppsättningar kan länkas till Adobe Experience Platform kundprofil i realtid eller användas som indata för Adobe Experience Platform Data Science Workspace.

## 4.1.4 Anslut PSQL-klienten till frågetjänsten

Frågetjänsten stöder klienter med en drivrutin för PostgreSQL. Här kommer vi att använda PSQL, ett kommandoradsgränssnitt och Power BI eller Tableau. Låt oss ansluta till PSQL.

Klicka på **Autentiseringsuppgifter**.

![queries-select-configuration.png](./images/queries-select-configuration.png)

Skärmen visas nedan. Konfigurationsskärmen innehåller serverinformation och autentiseringsuppgifter för autentisering till frågetjänsten. För närvarande fokuserar vi på skärmens högra sida som innehåller ett anslutningskommando för PSQL. Klicka på knappen Kopiera för att kopiera kommandot till Urklipp.

![copy-psql-connection.png](./images/copy-psql-connection.png)

För Windows: Öppna kommandoraden genom att trycka på Windows-tangenten och skriva cmd och sedan klicka på resultatet av kommandotolken.

![open-command-prompt.png](./images/open-command-prompt.png)

För macOS: Öppna terminal.app via spotlight-sökning:

![open-terminal-osx.png](./images/open-terminal-osx.png)

Klistra in det anslutningskommando som du har kopierat från användargränssnittet för frågetjänsten och tryck på Retur i kommandotolken:

Windows:

![command-prompt-connected.png](./images/command-prompt-connected.png)

macOS:

![command-prompt-paste-osx.png](./images/command-prompt-paste-osx.png)

Du är nu ansluten till frågetjänsten med PSQL.

I de följande övningarna kommer det att finnas en hel del interaktion med detta fönster. Vi kallar det **PSQL kommandoradsgränssnitt**.

Nu kan du börja skicka frågor.

Nästa steg: [4.2 Använda frågetjänsten](./ex2.md)

[Gå tillbaka till modul 4](./query-service.md)

[Gå tillbaka till Alla moduler](../../overview.md)
