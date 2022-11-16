---
title: Foundation - datainmatning - datainmatning från offlinekällor
description: Foundation - datainmatning - datainmatning från offlinekällor
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 93d9f4ef-9cbd-4310-879e-d69106b70404
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '773'
ht-degree: 1%

---

# 2.5 Data Landing Zone

I den här övningen är målet att konfigurera din datakälla för Data Landing Zone med Azure Blob-lagring.

Data Landing Zone är ett Azure Blob-lagringsgränssnitt som tillhandahålls av Adobe Experience Platform, vilket ger dig tillgång till en säker, molnbaserad fillagringsfunktion för att hämta filer till plattformen. Data Landing Zone har stöd för SAS-baserad autentisering och dess data skyddas med standardsäkerhetsmekanismer för Azure Blob-lagring vid vila och överföring. SAS-baserad autentisering ger dig säker åtkomst till din Data Landing Zone-behållare via en offentlig internetanslutning.

>[!NOTE]
>
> Adobe Experience Platform **använder en strikt TTL-fil (time-to-live) på sju dagar** på alla filer som överförts till en Data Landing Zone-behållare. Alla filer tas bort efter sju dagar.


## 2.5.1 Krav

Om du vill kopiera blober eller filer till din Adobe Experience Platform Data Landing Zone använder du kommandoradsverktyget AzCopy. Du kan hämta en version för ditt operativsystem via [https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10).

![dlz-install-az-copy.png](./images/dlz-install-az-copy.png)

- Zippa upp den hämtade filen

![dlz-install-az-copy.png](./images/dlz1.png)

- Hämta exempeldatafilen [global-context-websiteinteractions.csv](../../assets/csv/data-ingestion/global-context-websiteinteractions.csv), som innehåller exempel på webbplatsinteraktioner och sparar den i den mapp där du packade upp **azcopy**.

![dlz-install-az-copy.png](./images/dlz2.png)

- Öppna ett terminalfönster och navigera till mappen på skrivbordet. Du bör se följande innehåll (azcopy och global-context-websiteinteractions.csv), till exempel på OSX:

![dlz-unzip-azcopy.png](./images/dlz-unzip-azcopy.png)

## 2.5.2 Ansluta Data Landing Zone till Adobe Experience Platform

Logga in på Adobe Experience Platform genom att gå till denna URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

När du loggat in kommer du till Adobe Experience Platform hemsida.

![Dataintag](./images/home.png)

Innan du fortsätter måste du välja en **sandlåda**. Sandlådan som ska markeras har namnet ``--module2sandbox--``. Du kan göra detta genom att klicka på texten **[!UICONTROL Produktionsprodukt]** i den blå linjen ovanför skärmen. När du har valt rätt sandlåda ser du skärmändringen och nu befinner du dig i din dedikerade sandlåda.

![Dataintag](./images/sb1.png)

Gå till den vänstra menyn **Källor**. Sök efter i källkatalogen **datalastning**. På **Datallandningszon** kort, klicka **...** och markera **Visa autentiseringsuppgifter**.

![dlz-view-credentials.png](./images/dlz-view-credentials.png)

Klicka på tp copy **SASUri**.

![dlz-copy-sas-uri.png](./images/dlz-copy-sas-uri.png)

## 2.5.3 Kopiera din csv-fil till din AEP-datalandningszon

Du kommer nu att importera data till Adobe Experience Platform med Azure-kommandoradsverktyg med hjälp av AZCopy.

Öppna en terminal på platsen där du installerar azcopy och kör följande kommando för att kopiera en fil till AEP:s datalandningszon:

``./azcopy copy <your-local-file> <your SASUri>``

Se till att omge din SASUri med dubbla citattecken. Ersätt `<your-local-file>` efter sökvägen till den lokala kopian av filen **global-context-websiteinteractions.csv** i azcopy-katalogen och ersätt `<your SASUri>` av **SASUri** värdet som du kopierade från användargränssnittet i Adobe Experience Platform. Kommandot bör se ut så här:

```command
./azcopy copy global-context-websiteinteractions.csv "https://sndbxdtlnd2bimpjpzo14hp6.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-xxxxxxx-9843-4973-ae52-xxxxxxxx&sr=c&sp=racwdlm&sig=DN3kdhKzard%2BQwKASKg67Zxxxxxxxxxxxxxxxx"
```

När du har kört ovanstående kommando i terminalen visas följande:

![dlz-exec-copy-command.png](./images/dlz-exec-copy-command.png)

## 2.5.4 Söka efter filen i din Data Landing Zone

Gå till din Data Landing Zone i Adobe Experience Platform.

Välj **Källor**, sök efter **datalastning** och klicka på **Inställningar** -knappen.

![dlz-inspect-datalanding-zone.png](./images/dlz-inspect-datalanding-zone.png)

Då öppnas Data Landing Zone. Du kommer att se filen som du just överförde i datalandningszonens **markera data** -panelen.

![dlz-datalanding-zone-open.png](./images/dlz-datalanding-zone-open.png)

## 2.5.5 Bearbeta filen

Markera filen och välj **Avgränsad** som dataformat. Sedan visas en förhandsgranskning av dina data. Klicka på **Nästa**.

![dlz-datalanding-select-file.png](./images/dlz-datalanding-select-file.png)

Nu kan du börja mappa överförda data så att de matchar XDM-schemat i datauppsättningen.

Välj **Befintlig datauppsättning** och markera datauppsättningen **Demo System - händelsedatauppsättning för webbplats (Global v1.1)**. Klicka på **Nästa**.

![dlz-target-dataset.png](./images/dlz-target-dataset.png)

Nu kan du mappa inkommande källdata från csv-filen till målfälten från datauppsättningens XDM-schema.

![dlz-start-mapping.png](./images/dlz-start-mapping.png)

>[!NOTE]
>
> Glöm inte potentiella fel med mappningen. Du korrigerar mappningen i nästa steg.

## 2.5.6 Kartfält

Först och främst klickar du på **Rensa alla mappningar** -knappen. Sedan kan du börja med en ren mappning.

![dlz-clear-mappings.png](./images/mappings1.png)

Klicka på **Ny fälttyp** och sedan markera **Lägg till nytt fält**.

![dlz-clear-mappings.png](./images/dlz-clear-mappings.png)

Så här mappar du **ecid** källfält, markera fältet **identiteter.ecid** och klicka **Välj**.

![dlz-map-identity.png](./images/dlz-map-identity.png)

Klicka på **Mappa målfält**.

![dlz-map-select-target-field.png](./images/dlz-map-select-target-field.png)

Markera fältet ``--aepTenantId--``.identify.core.ecid i schemastrukturen.

![dlz-map-target-field.png](./images/dlz-map-target-field.png)

Du måste mappa några andra fält, klicka **+ Ny fälttyp** följt av **Lägg till nytt fält** och lägg till fält för den här mappningen

| källa | target |
|---|---|
| resource.info.pagename | web.webPageDetails.name |
| tidsstämpel | tidsstämpel |
| tidsstämpel | _id |

![dlz-add-other-mapping.png](./images/dlz-add-other-mapping.png)

När skärmen är klar bör den se ut som nedan. Klicka på **Nästa**.

![dlz-mapping-result.png](./images/dlz-mapping-result.png)

Klicka på **Nästa**.

![dlz-default-eduling.png](./images/dlz-default-scheduling.png)

Klicka **Slutför**.

![dlz-import-finish.png](./images/dlz-import-finish.png)

## 2.5.7 Skärmdataflöde

Om du vill övervaka ditt dataflöde går du till **Källor**, **Dataflöden** och klicka på dataflödet:

![dlz-monitor-dataflow.png](./images/dlz-monitor-dataflow.png)

Det kan ta några minuter att läsa in data. När det är klart visas statusen **Lyckades**:

![dlz-monitor-dataflow-result.png](./images/dlz-monitor-dataflow-result.png)

Nästa steg: [Sammanfattning och fördelar](./summary.md)

[Gå tillbaka till modul 2](./data-ingestion.md)

[Gå tillbaka till Alla moduler](../../overview.md)
