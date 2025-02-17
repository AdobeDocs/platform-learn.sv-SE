---
title: Audience Activation till Microsoft Azure Event Hub - Sammanfattning och fördelar
description: Audience Activation till Microsoft Azure Event Hub - Sammanfattning och fördelar
kt: 5342
doc-type: tutorial
exl-id: f081af11-3ea0-47cc-ae74-24a0e0231d66
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 1%

---

# Sammanfattning och fördelar

Grattis och tack för att du har lagt ned din tid på att lära dig om Microsoft Azure Event Hub och Adobe Experience Platform!
I den här modulen får du lära dig hur du konfigurerar en Azure Event Hub-instans och hur du ansluter den till Adobe Experience Platform.

## Fördelar

Låt oss lyfta fram fördelarna med att integrera Adobe Experience Platform med Microsoft Azure Event Hub:

- Med Microsoft Azure Event Hubs som Adobe Experience Platform-mål kan du hämta målgruppskvalifikationer i realtid och bearbeta dem med en Azure Event Hub-funktion. Med en sådan Azure Event Hub-funktion kan du skapa vilken typ av anpassad målgruppsaktiveringshanterare som helst och som sådan integrera alla typer av tredjepartsmål.

- Även om destinationer endast aktiveras av angivna målgrupper, kommer aktiveringsnyttolasten att inkludera alla målgrupper som den angivna profilen kvalificerar för.

- En målgrupp aktiverar bara en aktivering när dess status ändras. En profil som till exempel kvalificerar fyra gånger för en målgrupp under en period av tre månader, aktiveras bara de två första. Den första är en statusändring från till **realiserad**, den andra utlöses av en statusändring från **realiserad** till **befintlig**.

- När målgrupper aktiveras för kända profiler inkluderas en fullständig identitetskarta i aktiveringsnyttolasten. Din Azure-funktion kan använda någon av de tillgängliga identiteterna för att mappa målgrupperna till en profil som hanteras i ett tredjepartsprogram, samtidigt som programmets kundidentifierare används.

- I den här modulen har händelsehubbfunktionen distribuerats lokalt (felsökningsläge i Visual Studio Code), vilket ger dig många felsöknings- och felsökningsalternativ.

## Kolla in det här

- N/A

## Nästa steg

Gå tillbaka till [Real-Time CDP: Audience Activation till Microsoft Azure Event Hub](./segment-activation-microsoft-azure-eventhub.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../../overview.md){target="_blank"}
