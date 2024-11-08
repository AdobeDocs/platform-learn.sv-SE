---
title: Segmentaktivering till Microsoft Azure Event Hub - Sammanfattning och fördelar
description: Segmentaktivering till Microsoft Azure Event Hub - Sammanfattning och fördelar
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 1%

---

# Sammanfattning och fördelar

Grattis och tack för att du har lagt ned din tid på att lära dig om Microsoft Azure Event Hub och Adobe Experience Platform!
I den här modulen får du lära dig hur du konfigurerar en Azure Event Hub-instans och hur du ansluter den till Adobe Experience Platform.

## Fördelar

Låt oss lyfta fram fördelarna med att integrera Adobe Experience Platform med Microsoft Azure Event Hub:

- Med Microsoft Azure Event Hubs som Adobe Experience Platform-mål kan du hämta segmentkvalificeringar i realtid och bearbeta dem med en Azure Event Hub-funktion. Med en sådan Azure Event Hub-funktion kan du skapa vilken typ av anpassad segmentaktiveringshanterare som helst och som sådan integrera alla typer av tredjepartsmål.

- Även om destinationer endast aktiveras av angivna segment, kommer aktiveringsnyttolasten att inkludera alla segment som den angivna profilen kvalificerar för.

- Ett segment aktiverar bara en aktivering när dess status ändras. En profil som exempelvis kvalificerar fyra gånger för ett segment under en period av tre månader, aktiveras bara de två första. Den första är en statusändring från till **realiserad**, den andra utlöses av en statusändring från **realiserad** till **befintlig**.

- När du aktiverar segment för kända profiler inkluderas en fullständig identitetskarta i aktiveringsnyttolasten. Din Azure-funktion kan använda någon av de tillgängliga identiteterna för att mappa segmenten till en profil som hanteras i ett tredjepartsprogram, samtidigt som programmets kundidentifierare används.

- I den här modulen har händelsehubbfunktionen distribuerats lokalt (felsökningsläge i Visual Studio Code), vilket ger dig många felsöknings- och felsökningsalternativ.

## Kolla in det här

- N/A

[Gå tillbaka till modul 2.4](./segment-activation-microsoft-azure-eventhub.md)

[Gå tillbaka till Alla moduler](./../../../overview.md)
