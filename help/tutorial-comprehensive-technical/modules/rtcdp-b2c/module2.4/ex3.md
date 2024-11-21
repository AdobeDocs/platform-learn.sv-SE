---
title: Audience Activation till Microsoft Azure Event Hub - Konfigurera Event Hub RTCDP-målet i Adobe Experience Platform
description: Audience Activation till Microsoft Azure Event Hub - Konfigurera Event Hub RTCDP-målet i Adobe Experience Platform
kt: 5342
doc-type: tutorial
exl-id: 86bc3afa-16a9-4834-9119-ce02445cd524
source-git-commit: 216914c9d97827afaef90e21ed7d4f35eaef0cd3
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 0%

---

# 2.4.3 Konfigurera Azure Event Hub-målet i Adobe Experience Platform

## Identifiera obligatoriska Azure Connection-parametrar

Om du vill konfigurera ett Event Hub-mål i Adobe Experience Platform behöver du ditt:

- Namnutrymme för händelsehubbar
- Händelsehubb
- Azure SAS-nyckelnamn
- Azure SAS-nyckel

Händelsehubben och EventHub-namnområdet har definierats i den föregående övningen: [Konfigurera händelsehubben i Azure](./ex2.md)

### Namnutrymme för händelsehubbar

Om du vill söka efter ovanstående information i Azure Portal går du till [https://portal.azure.com/#home](https://portal.azure.com/#home). Kontrollera att du använder rätt Azure-konto.

Klicka på **Alla resurser** i din Azure-portal:

![2-01-azure-all-resources.png](./images/201azureallresources.png)

Leta reda på namnområdet **Event Hubs** i listan och klicka på det.

![2-01-azure-all-resources.png](./images/201azureallresources1.png)

Namnet på **Event Hubs-namnområdet** visas nu tydligt. Det ska likna `--aepUserLdap---aep-enablement`.

![2-01-azure-all-resources.png](./images/201azureallresources2.png)

### Händelsehubb

Klicka på **Enheter > Händelsehubbar** på sidan **Händelsehubbar för namnområde** för att visa en lista över händelsehubbar som har definierats i namnutrymmet för händelsehubbar, om du följde de namnkonventioner som användes i den föregående övningen kommer du att hitta en händelsehubb med namnet `--aepUserLdap---aep-enablement-event-hub`. Observera att du kommer att behöva det i nästa övning.

![2-04-event-hub-selected.png](./images/204eventhubselected.png)

### SAS-nyckelnamn

Klicka på **Inställningar > Principer för delad åtkomst** på sidan **Händelsehubb-namnområde**. Du ser en lista över principer för delad åtkomst. SAS-nyckeln som vi letar efter är **RootManageSharedAccessKey**, vilket är **SAS-nyckelnamnet. Skriv ner det.

![2-05-select-sas.png](./images/205selectsas.png)

### SAS-nyckelvärde

Klicka sedan på **RootManageSharedAccessKey** för att hämta SAS-nyckelvärdet. Och tryck på ikonen **Kopiera till Urklipp** för att kopiera **primärnyckeln**, i det här fallet `pqb1jEC0KLazwZzIf2gTHGr75Z+PdkYgv+AEhObbQEY=`.

![2-07-sas-key-value.png](./images/207saskeyvalue.png)

### Sammanfattning av målvärden

Nu bör du ha identifierat alla värden som behövs för att definiera Azure Event Hub-målet i Adobe Experience Platform CDP i realtid.

| Namn på målattribut | Värde för målattribut | Exempelvärde |
|---|---|---|
| sasKeyName | SAS-nyckelnamn | RootHanteraDeladÅtkomstnyckel |
| sasKey | SAS-nyckelvärde | pqb1jEC0KLazwZzIf2gTHGr75Z+PdkYgv+AEhObbQEY= |
| namespace | Namnutrymme för händelsehubbar | `--aepUserLdap---aep-enablement` |
| eventHubName | Händelsehubb | `--aepUserLdap---aep-enablement-event-hub` |

## Skapa Azure Event Hub-mål i Adobe Experience Platform

Logga in på Adobe Experience Platform via följande URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

När du har loggat in loggar du in på Adobe Experience Platform hemsida.

![Datainmatning](./../../../modules/datacollection/module1.2/images/home.png)

Innan du fortsätter måste du välja en **sandlåda**. Sandlådan som ska markeras har namnet ``--aepSandboxName--``. När du har valt rätt sandlåda ser du skärmändringen och nu befinner du dig i din dedikerade sandlåda.

![Datainmatning](./../../../modules/datacollection/module1.2/images/sb1.png)

Gå till **Destinationer** och gå sedan till **Katalog**. Välj **molnlagring**, gå till **Azure Event Hubs** och klicka på **Konfigurera**.

![2-08-list-destination.png](./images/208listdestinations.png)

Välj **Standardautentisering**. Fyll i anslutningsinformationen som du har samlat in i föregående övning. Klicka sedan på **Anslut till mål**.

![2-09-destination-values.png](./images/209destinationvalues.png)

Om dina autentiseringsuppgifter är korrekta visas en bekräftelse: **Ansluten**.

![2-09-destination-values.png](./images/209destinationvaluesa.png)

Du måste nu ange namn och beskrivning i formatet `--aepUserLdap---aep-enablement`. Ange **eventHubName** (se föregående övning, den ser ut så här: `--aepUserLdap---aep-enablement-event-hub`) och klicka på **Nästa**.

![2-10-create-destination.png](./images/210createdestination.png)

Du kan också välja en datastyrningspolicy. Klicka på **Spara och avsluta**.

![2-11-save-exit-activation.png](./images/211saveexitactivation.png)

Målet har nu skapats och är tillgängligt i Adobe Experience Platform.

![2-12-destination-created.png](./images/212destinationcreated.png)

Nästa steg: [2.4.4 Skapa en målgrupp](./ex4.md)

[Gå tillbaka till modul 2.4](./segment-activation-microsoft-azure-eventhub.md)

[Gå tillbaka till Alla moduler](./../../../overview.md)
