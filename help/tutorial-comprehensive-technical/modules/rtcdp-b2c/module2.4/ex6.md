---
title: Segmentaktivering till Microsoft Azure Event Hub - åtgärd
description: Segmentaktivering till Microsoft Azure Event Hub - åtgärd
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 0%

---

# 2.4.6 Heltäckande scenario

## 2.4.6.1 Starta Azure Event Hub-utlösaren

För att visa nyttolasten som skickas av Adobe Experience Platform CDP i realtid till vår Azure Event Hub när segment kvalificeras måste vi starta vår enkla Azure Event Hub-utlösarfunktion. Den här funktionen gör att nyttolasten&quot;dumpas&quot; till konsolen i Visual Studio Code. Men kom ihåg att den här funktionen kan utökas på alla sätt för att interagera med alla typer av miljöer med hjälp av dedikerade API:er och protokoll.

### Starta Visual Studio Code och starta projektet

Se till att du har Visual Studio Code-projektet öppet och igång

Om du vill starta/stoppa/starta om din Azure-funktion i Visual Studio Code ska du läsa följande övningar:

- [Utgång 13.5.4 - Starta Azure Project](./ex5.md)
- [Utövning 13.5.5 - Stoppa Azure-projekt](./ex5.md)

Din Visual Studio-kods **Terminal** ska nämna något liknande:

```code
[2022-02-23T05:03:41.429Z] Worker process started and initialized.
[2022-02-23T05:03:41.484Z] Debugger attached.
[2022-02-23T05:03:46.401Z] Host lock lease acquired by instance ID '000000000000000000000000D90C881B'.
```

![6-01-vsc-ready.png](./images/vsc31.png)

## 2.4.6.2 Läs in din Luma-webbplats

Gå till [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). När du har loggat in med din Adobe ID ser du det här. Klicka på webbplatsprojektet för att öppna det.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web8.png)

Nu kan du följa nedanstående flöde för att komma åt webbplatsen. Klicka på **Integrationer**.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web1.png)

På sidan **Integrationer** måste du välja den datainsamlingsegenskap som skapades i övning 0.1.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web2.png)

Du kommer då att se din demowebbplats öppnas. Markera URL-adressen och kopiera den till Urklipp.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web3.png)

Öppna ett nytt inkognito-webbläsarfönster.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web4.png)

Klistra in webbadressen till demowebbplatsen, som du kopierade i föregående steg. Du ombeds sedan logga in med din Adobe ID.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web5.png)

Välj kontotyp och slutför inloggningsprocessen.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web6.png)

Därefter visas webbplatsen i ett inkognitivt webbläsarfönster. För varje demonstration måste du använda ett nytt, inkognitivt webbläsarfönster för att läsa in webbadressen till demowebbplatsen.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web7.png)

## 2.4.6.3 Kvalificera för ert intresse för utrustningssegmentet

Navigera till sidan **Utrustning** en gång och **läs inte in eller uppdatera den igen**. Den här åtgärden bör kvalificera dig för ditt `--aepUserLdap-- - Interest in Equipment`-segment.

![6-04-luma-telco-nav-sport.png](./images/luma1.png)

Verifiera genom att öppna profilvisarpanelen. Du bör nu vara medlem i `--aepUserLdap-- - Interest in Equipment`. Om dina segmentmedlemskap ännu inte har uppdaterats på panelen Profilvisningsprogram klickar du på knappen Läs in igen.

![6-05-luma-telco-nav-bredband.png](./images/luma2.png)

Växla tillbaka till Visual Studio Code och titta på fliken **TERMINAL**. Du bör se en lista över segment för ditt specifika **ECID**. Den här aktiveringsnyttolasten levereras till händelsehubben så snart du kvalificerar dig för `--aepUserLdap-- - Interest in Equipment`-segmentet.

När du tittar närmare på segmentets nyttolast ser du att `--aepUserLdap-- - Interest in Equipment` har statusen **realiserad**.

En segmentstatus på **realiserad** innebär att vår profil just har öppnat segmentet. Statusen **existing** innebär att vår profil fortsätter att vara i segmentet.

![6-06-vsc-activation-real.png](./images/luma3.png)

## 2.4.6.4 Besök utrustningssidan en andra gång

Gör en hård uppdatering av sidan **Utrustning**.

![6-07-back-to-sport.png](./images/luma1.png)

Växla tillbaka till Visual Studio-kod och kontrollera fliken **TERMINAL**. Du kommer att se att vi fortfarande har ditt segment, men nu har statusen **befintlig**, vilket innebär att vår profil fortsätter att vara i segmentet.

![6-08-vsc-activation-existing.png](./images/luma4.png)

## 2.4.6.5 Besök sportsidan en tredje gång

Om du skulle besöka sidan **Sport** en tredje gång, kommer ingen aktivering att göras eftersom det inte finns någon lägesändring från ett segment.

Segmentaktiveringar utförs bara när segmentets status ändras:

![6-09-segment-state-change.png](./images/6-09-segment-state-change.png)

Nästa steg: [Sammanfattning och förmåner](./summary.md)

[Gå tillbaka till modul 2.4](./segment-activation-microsoft-azure-eventhub.md)

[Gå tillbaka till Alla moduler](./../../../overview.md)
