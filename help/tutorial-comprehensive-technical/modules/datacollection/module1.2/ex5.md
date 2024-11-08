---
title: Foundation - datainmatning - datainmatning från offlinekällor
description: Foundation - datainmatning - datainmatning från offlinekällor
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 0%

---

# 1.2.5 Data Landing Zone

I den här övningen är målet att konfigurera din Data Landing Zone Source-anslutning med Azure Blob-lagring.

Data Landing Zone är ett Azure Blob-lagringsgränssnitt som tillhandahålls av Adobe Experience Platform, vilket ger dig tillgång till en säker, molnbaserad fillagringsfunktion för att hämta filer till plattformen. Data Landing Zone har stöd för SAS-baserad autentisering och dess data skyddas med standardsäkerhetsmekanismer för Azure Blob-lagring vid vila och överföring. SAS-baserad autentisering ger dig säker åtkomst till din Data Landing Zone-behållare via en offentlig internetanslutning.

>[!NOTE]
>
> Adobe Experience Platform **tvingar en strikt TTL** (time-to-live) på sju dagar för alla filer som överförs till en Data Landing Zone-behållare. Alla filer tas bort efter sju dagar.


## 1.2.5.1 Krav

Om du vill kopiera blober eller filer till din Adobe Experience Platform Data Landing Zone använder du kommandoradsverktyget AzCopy. Du kan hämta en version för ditt operativsystem via [https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10).

![dlz-install-az-copy.png](./images/dlz-install-az-copy.png)

- Zippa upp den hämtade filen

![dlz-install-az-copy.png](./images/dlz1.png)

- Hämta exempeldatafilen global-context-websiteinteractions.csv, som innehåller exempel på webbplatsinteraktioner och spara den i den mapp där du packade upp **azcopy**.

![dlz-install-az-copy.png](./images/dlz2.png)

- Öppna ett terminalfönster och navigera till mappen på skrivbordet. Du bör se följande innehåll (azcopy och global-context-websiteinteractions.csv), till exempel på OSX:

![dlz-unzip-azcopy.png](./images/dlz-unzip-azcopy.png)

## 1.2.5.2 Ansluta Data Landing Zone till Adobe Experience Platform

Logga in på Adobe Experience Platform via följande URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

När du har loggat in loggar du in på Adobe Experience Platform hemsida.

![Datainmatning](./images/home.png)

Innan du fortsätter måste du välja en **sandlåda**. Sandlådan som ska markeras har namnet ``--module2sandbox--``. Du kan göra detta genom att klicka på texten **[!UICONTROL Production Prod]** i den blå raden ovanför skärmen. När du har valt rätt sandlåda ser du skärmändringen och nu befinner du dig i din dedikerade sandlåda.

![Datainmatning](./images/sb1.png)

Gå till **Källor** på den vänstra menyn. Sök efter **datalandning** i källkatalogen. På **Data Landing Zone**-kortet klickar du på **..** och väljer **Visa autentiseringsuppgifter**.

![dlz-view-credentials.png](./images/dlz-view-credentials.png)

Klicka på tp copy **SASUri**.

![dlz-copy-sas-uri.png](./images/dlz-copy-sas-uri.png)

## 1.2.5.3 Kopiera csv-filen till AEP-datalandningszonen

Du kommer nu att importera data till Adobe Experience Platform med Azure-kommandoradsverktyg med hjälp av AZCopy.

Öppna en terminal på platsen där du installerar azcopy och kör följande kommando för att kopiera en fil till AEP:s datalandningszon:

``./azcopy copy <your-local-file> <your SASUri>``

Se till att omge din SASUri med dubbla citattecken. Ersätt `<your-local-file>` med sökvägen till din lokala kopia av filen **global-context-websiteinteractions.csv** i azcopy-katalogen och ersätt `<your SASUri>` med värdet **SASUri** som du kopierade från Adobe Experience Platform-gränssnittet. Kommandot bör se ut så här:

```command
./azcopy copy global-context-websiteinteractions.csv "https://sndbxdtlnd2bimpjpzo14hp6.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-xxxxxxx-9843-4973-ae52-xxxxxxxx&sr=c&sp=racwdlm&sig=DN3kdhKzard%2BQwKASKg67Zxxxxxxxxxxxxxxxx"
```

När du har kört ovanstående kommando i terminalen visas följande:

![dlz-exec-copy-command.png](./images/dlz-exec-copy-command.png)

## 1.2.5.4 Söka efter filen i din Data Landing Zone

Gå till din Data Landing Zone i Adobe Experience Platform.

Välj **Källor**, sök efter **datalandning** och klicka på knappen **Inställningar** .

![dlz-inspect-datalanding-zone.png](./images/dlz-inspect-datalanding-zone.png)

Då öppnas Data Landing Zone. Du ser filen som du just överförde i datalandningszonens **valda data**-panel.

![dlz-datalanding-zone-open.png](./images/dlz-datalanding-zone-open.png)

## 1.2.5.5 Bearbeta filen

Markera filen och välj **Avgränsad** som dataformat. Sedan visas en förhandsgranskning av dina data. Klicka på **Nästa**.

![dlz-datalanding-select-file.png](./images/dlz-datalanding-select-file.png)

Nu kan du börja mappa överförda data så att de matchar XDM-schemat i datauppsättningen.

Välj **Befintlig datauppsättning** och välj datauppsättningen **Demo System - händelsedatauppsättning för webbplats (Global v1.1)**. Klicka på **Nästa**.

![dlz-target-dataset.png](./images/dlz-target-dataset.png)

Nu kan du mappa inkommande källdata från csv-filen till målfälten från datauppsättningens XDM-schema.

![dlz-start-mapping.png](./images/dlz-start-mapping.png)

>[!NOTE]
>
> Glöm inte de potentiella felen med mappningen. Du korrigerar mappningen i nästa steg.

## 1.2.5.6 Kartfält

Klicka först på knappen **Rensa alla mappningar**. Sedan kan du börja med en ren mappning.

![dlz-clear-mappings.png](./images/mappings1.png)

Klicka sedan på **Ny fälttyp** och välj **Lägg till nytt fält**.

![dlz-clear-mappings.png](./images/dlz-clear-mappings.png)

Om du vill mappa **ecid**-källfältet markerar du fältet **identities.ecid** och klickar på **Select**.

![dlz-map-identity.png](./images/dlz-map-identity.png)

Klicka sedan på **Mappa målfält**.

![dlz-map-select-target-field.png](./images/dlz-map-select-target-field.png)

Markera fältet ``--aepTenantId--``.identity.core.ecid i schemastrukturen.

![dlz-map-target-field.png](./images/dlz-map-target-field.png)

Du måste mappa några andra fält, klicka på **+ Ny fälttyp** följt av **Lägg till nytt fält** och lägga till fält för den här mappningen

| källa | target |
|---|---|
| resource.info.pagename | web.webPageDetails.name |
| tidsstämpel | tidsstämpel |
| tidsstämpel | _id |

![dlz-add-other-mapping.png](./images/dlz-add-other-mapping.png)

När skärmen är klar bör den se ut som på skärmen nedan. Klicka på **Nästa**.

![dlz-mapping-result.png](./images/dlz-mapping-result.png)

Klicka på **Nästa**.

![dlz-default-eduling.png](./images/dlz-default-scheduling.png)

Klicka på **Slutför**.

![dlz-import-finish.png](./images/dlz-import-finish.png)

## 1.2.5.7 Skärmdataflöde

Om du vill övervaka dataflödet går du till **Källor**, **Dataflöden** och klickar på dataflödet:

![dlz-monitor-dataflow.png](./images/dlz-monitor-dataflow.png)

Det kan ta några minuter att läsa in data. Statusen **Slutfört** visas när det är klart:

![dlz-monitor-dataflow-result.png](./images/dlz-monitor-dataflow-result.png)

Nästa steg: [Sammanfattning och förmåner](./summary.md)

[Gå tillbaka till modul 1.2](./data-ingestion.md)

[Gå tillbaka till Alla moduler](../../../overview.md)
