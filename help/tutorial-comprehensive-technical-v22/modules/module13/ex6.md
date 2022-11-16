---
title: Segmentaktivering till Microsoft Azure Event Hub - åtgärd
description: Segmentaktivering till Microsoft Azure Event Hub - åtgärd
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 989dd2e4-597b-4b80-8b17-41aa6929ed64
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 0%

---

# 13.6 Heltäckande scenario

## 13.6.1 Starta Azure Event Hub-utlösaren

För att visa nyttolasten som skickas av Adobe Experience Platform CDP i realtid till vår Azure Event Hub när segment kvalificeras måste vi starta vår enkla Azure Event Hub-utlösarfunktion. Den här funktionen gör att nyttolasten&quot;dumpas&quot; till konsolen i Visual Studio Code. Men kom ihåg att den här funktionen kan utökas på alla sätt för att interagera med alla typer av miljöer med hjälp av dedikerade API:er och protokoll.

### Starta Visual Studio Code och starta projektet

Se till att Visual Studio Code-projektet är öppet och körs

Om du vill starta/stoppa/starta om din Azure-funktion i Visual Studio Code ska du läsa följande övningar:

- [Utgång 13.5.4 - Starta Azure Project](./ex5.md)
- [Utövning 13.5.5 - Stoppa Azure-projekt](./ex5.md)

Din Visual Studio-kod **Terminal** Jag vill nämna något liknande:

```code
[2022-02-23T05:03:41.429Z] Worker process started and initialized.
[2022-02-23T05:03:41.484Z] Debugger attached.
[2022-02-23T05:03:46.401Z] Host lock lease acquired by instance ID '000000000000000000000000D90C881B'.
```

![6-01-vsc-ready.png](./images/vsc31.png)

## 13.6.2 Läs in din Luma-webbplats

Gå till [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). När du har loggat in med din Adobe ID ser du det här. Klicka på webbplatsprojektet för att öppna det.

![DSN](../module0/images/web8.png)

Nu kan du följa nedanstående flöde för att komma åt webbplatsen. Klicka **Integreringar**.

![DSN](../module0/images/web1.png)

På **Integreringar** måste du välja den datainsamlingsegenskap som skapades i övning 0.1.

![DSN](../module0/images/web2.png)

Du kommer då att se din demowebbplats öppnas. Markera URL-adressen och kopiera den till Urklipp.

![DSN](../module0/images/web3.png)

Öppna ett nytt inkognito-webbläsarfönster.

![DSN](../module0/images/web4.png)

Klistra in webbadressen till demowebbplatsen, som du kopierade i föregående steg. Du ombeds sedan logga in med din Adobe ID.

![DSN](../module0/images/web5.png)

Välj kontotyp och slutför inloggningsprocessen.

![DSN](../module0/images/web6.png)

Därefter visas webbplatsen i ett inkognitivt webbläsarfönster. För varje demonstration måste du använda ett nytt, inkognitivt webbläsarfönster för att läsa in webbadressen till demowebbplatsen.

![DSN](../module0/images/web7.png)

## 13.6.3 Kvalificera för ert intresse för utrustningssegment

Navigera till **Utrustning** sida en gång, och **inte läsa in eller uppdatera den**. Den här åtgärden bör ge dig rätt att `--demoProfileLdap-- - Interest in Equipment` segment.

![6-04-luma-telco-nav-sport.png](./images/luma1.png)

Verifiera genom att öppna profilvisarpanelen. Du bör nu vara medlem i `--demoProfileLdap-- - Interest in Equipment`. Om dina segmentmedlemskap ännu inte har uppdaterats på panelen Profilvisningsprogram klickar du på knappen Läs in igen.

![6-05-luma-telco-nav-bredband.png](./images/luma2.png)

Växla tillbaka till Visual Studio Code och titta på **TERMINAL** bör du se en lista över segment för din **ECID**. Nyttolasten för aktiveringen levereras till händelsehubben så snart du är berättigad till `--demoProfileLdap-- - Interest in Equipment` segment.

När du tittar närmare på segmentets nyttolast ser du att `--demoProfileLdap-- - Interest in Equipment` är i status **realiserad**.

En segmentstatus för **realiserad** innebär att vår profil just har gått in i segmentet. Med **befintlig** status innebär att vår profil fortsätter att vara i segmentet.

![6-06-vsc-activation-real.png](./images/luma3.png)

## 13.6.4 Besök utrustningssidan en andra gång

Gör en hård uppdatering av **Utrustning** sida.

![6-07-back-to-Sport.png](./images/luma1.png)

Nu kan du växla tillbaka till Visual Studio Code och verifiera **TERMINAL** -fliken. Du kommer att se att vi fortfarande har ditt segment, men nu är det i status **befintlig** vilket innebär att vår profil fortsätter att vara i segmentet.

![6-08-vsc-activation-existing.png](./images/luma4.png)

## 13.6.5 Besök sportsidan en tredje gång

Om du vill gå tillbaka till **Idrott** för en tredje gång kommer ingen aktivering att ske eftersom det inte sker någon lägesändring från ett segment.

Segmentaktiveringar utförs bara när segmentets status ändras:

![6-09-segment-state-change.png](./images/6-09-segment-state-change.png)

Nästa steg: [Sammanfattning och fördelar](./summary.md)

[Gå tillbaka till modul 13](./segment-activation-microsoft-azure-eventhub.md)

[Gå tillbaka till Alla moduler](./../../overview.md)
