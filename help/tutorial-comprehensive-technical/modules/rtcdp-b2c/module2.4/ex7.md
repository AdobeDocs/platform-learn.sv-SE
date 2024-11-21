---
title: Audience Activation till Microsoft Azure Event Hub - åtgärd
description: Audience Activation till Microsoft Azure Event Hub - åtgärd
kt: 5342
doc-type: tutorial
exl-id: f5b224bf-60b9-46e0-abdb-9d96a7e8c59f
source-git-commit: b4a7144217a68bc0b1bc70b19afcbc52e226500f
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---

# 2.4.7 Heltäckande scenario

## Starta Azure Event Hub-utlösaren

För att visa nyttolasten som skickas av Adobe Experience Platform CDP i realtid till vår Azure Event Hub när målgrupper kvalificerar sig måste vi starta vår enkla Azure Event Hub-utlösarfunktion. Den här funktionen gör att nyttolasten&quot;dumpas&quot; till konsolen i Visual Studio Code. Men kom ihåg att den här funktionen kan utökas på alla sätt för att interagera med alla typer av miljöer med hjälp av dedikerade API:er och protokoll.

### Starta Visual Studio Code och starta projektet

Se till att du har Visual Studio Code-projektet öppet och igång

Om du vill starta/stoppa/starta om din Azure-funktion i Visual Studio Code ska du läsa föregående övning.

Din Visual Studio-kods **Terminal** ska nämna något liknande:

```code
[2024-11-20T20:07:12.316Z] Debugger listening on ws://127.0.0.1:9229/86c8e251-8e2f-4c65-a063-cda77edbf2ca
[2024-11-20T20:07:12.318Z] For help, see: https://nodejs.org/en/docs/inspector
[2024-11-20T20:07:12.343Z] Worker process started and initialized.
[2024-11-20T20:07:12.359Z] Debugger attached.

Functions:

        vangeluw-aep-event-hub-trigger: eventHubTrigger

For detailed output, run func with --verbose flag.
[2024-11-20T20:07:18.150Z] Host lock lease acquired by instance ID '000000000000000000000000000C19D8'.
```

## Läs in din Citi Signal-webbplats

Gå till [https://dsn.adobe.com](https://dsn.adobe.com). När du har loggat in med din Adobe ID ser du det här. Klicka på de tre punkterna **..** i webbplatsprojektet och klicka sedan på **Kör** för att öppna det.

![DSN](./../../datacollection/module1.1/images/web8.png)

Du kommer då att se din demowebbplats öppnas. Markera URL-adressen och kopiera den till Urklipp.

![DSN](../../gettingstarted/gettingstarted/images/web3.png)

Öppna ett nytt inkognito-webbläsarfönster.

![DSN](../../gettingstarted/gettingstarted/images/web4.png)

Klistra in webbadressen till demowebbplatsen, som du kopierade i föregående steg. Du ombeds sedan logga in med din Adobe ID.

![DSN](../../gettingstarted/gettingstarted/images/web5.png)

Välj kontotyp och slutför inloggningsprocessen.

![DSN](../../gettingstarted/gettingstarted/images/web6.png)

Därefter visas webbplatsen i ett inkognitivt webbläsarfönster. För varje övning måste du använda ett nytt, inkognitivt webbläsarfönster för att läsa in webbadressen till demowebbplatsen.

![DSN](../../gettingstarted/gettingstarted/images/web7.png)

## Kvalificera för er målgrupp

Gå till sidan **Planer**. Den här åtgärden kvalificerar dig för målgruppen `--aepUserLdap-- - Interest in Plans`.

![6-04-luma-telco-nav-sport.png](./images/cs1.png)

Verifiera genom att öppna profilvisarpanelen. Du bör nu vara medlem i `--aepUserLdap-- - Interest in Plans`. Om målgruppsmedlemskapen ännu inte har uppdaterats på din profilvisarpanel klickar du på knappen Läs in igen.

![6-05-luma-telco-nav-bredband.png](./images/cs2.png)

Växla tillbaka till Visual Studio Code och titta på fliken **TERMINAL**. Du bör se en lista över målgrupper för ditt specifika **ECID**. Den här aktiveringsnyttolasten levereras till händelsehubben så snart du kvalificerar dig för målgruppen `--aepUserLdap-- - Interest in Plans`.

![6-06-vsc-activation-real.png](./images/cs3.png)

När du tittar närmare på målgruppsnyttolasten kan du se att `--aepUserLdap-- - Interest in Plans` har statusen **realiserad**.

```json
{
  "identityMap": {
    "ecid": [
      {
        "id": "36281682065771928820739672071812090802"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "94db5aed-b90e-478d-9637-9b0fad5bba11": {
        "createdAt": 1732129904025,
        "lastQualificationTime": "2024-11-21T07:33:52Z",
        "mappingCreatedAt": 1732130611000,
        "mappingUpdatedAt": 1732130611000,
        "name": "vangeluw - Interest in Plans",
        "status": "realized",
        "updatedAt": 1732129904025
      }
    }
  }
}
```

En målgruppsstatus på **realiserad** innebär att din profil är en del av målgruppen, medan statusen **avslutad** innebär att vår profil har tagits bort från målgruppen.

Nästa steg: [Sammanfattning och förmåner](./summary.md)

[Gå tillbaka till modul 2.4](./segment-activation-microsoft-azure-eventhub.md)

[Gå tillbaka till Alla moduler](./../../../overview.md)
