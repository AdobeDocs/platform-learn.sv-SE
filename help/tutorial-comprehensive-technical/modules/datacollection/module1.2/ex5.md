---
title: Foundation - datainmatning - datainmatning från offlinekällor
description: Foundation - datainmatning - datainmatning från offlinekällor
kt: 5342
doc-type: tutorial
exl-id: 21b84a77-4115-4ba7-b847-b236aa14bbdd
source-git-commit: 2f53c8da2cbe833120fa6555c65b8b753bfa4f8d
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 0%

---

# 1.2.5 Data Landing Zone

I den här övningen är målet att konfigurera din Data Landing Zone Source-anslutning med Azure Blob-lagring.

Data Landing Zone är ett Azure Blob-lagringsgränssnitt som tillhandahålls av Adobe Experience Platform, vilket ger dig tillgång till en säker, molnbaserad fillagringsfunktion för att hämta filer till plattformen. Data Landing Zone har stöd för SAS-baserad autentisering och dess data skyddas med standardsäkerhetsmekanismer för Azure Blob-lagring vid vila och överföring. SAS-baserad autentisering ger dig säker åtkomst till din Data Landing Zone-behållare via en offentlig internetanslutning.

>[!NOTE]
>
> Adobe Experience Platform **tvingar en strikt TTL** (time-to-live) på sju dagar för alla filer som överförs till en Data Landing Zone-behållare. Alla filer tas bort efter sju dagar.


## Förhandskrav

Om du vill kopiera blober eller filer till din Adobe Experience Platform Data Landing Zone använder du kommandoradsverktyget AzCopy. Du kan hämta en version för ditt operativsystem via [https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10), bläddra nedåt på sidan för att **hämta den portabla AzCopy-binärfilen** och välja lämplig version för ditt operativsystem.

![dlz-install-az-copy.png](./images/dlzinstallazcopy.png)

- Zippa upp den hämtade filen

![dlz-install-az-copy.png](./images/dlz1.png)

- Hämta exempeldatafilen [global-context-websiteinteractions.csv](./../../../assets/csv/data-ingestion/global-context-websiteinteractions.csv) som innehåller exempel på webbplatsinteraktioner och spara den i den mapp där du packade upp **azcopy**.

![dlz-install-az-copy.png](./images/dlz2.png)

- Öppna ett terminalfönster och navigera till mappen på skrivbordet. Du bör se följande innehåll (azcopy och global-context-websiteinteractions.csv), till exempel på OSX:

![dlz-unzip-azcopy.png](./images/dlzunzipazcopy.png)

## 1.2.5.2 Ansluta Data Landing Zone till Adobe Experience Platform

Logga in på Adobe Experience Platform via följande URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

När du har loggat in loggar du in på Adobe Experience Platform hemsida.

![Datainmatning](./images/home.png)

Innan du fortsätter måste du välja en **sandlåda**. Sandlådan som ska markeras har namnet ``--aepSandboxName--``.  När du har valt rätt sandlåda ser du skärmändringen och nu befinner du dig i din dedikerade sandlåda.

![Datainmatning](./images/sb1.png)

Gå till **Källor** på den vänstra menyn. Sök efter **datalandning** i källkatalogen.

![Datainmatning](./images/sourcesdlz.png)

Klicka på **Data Landing Zone** -kortet så visas inloggningsuppgifterna på den högra fliken.

![dlz-view-credentials.png](./images/dlzviewcredentials.png)

Klicka på ikonen för att kopiera **SASUri**.

![dlz-copy-sas-uri.png](./images/dlzcopysasuri.png)

## Kopiera csv-filen till AEP-datalandningszonen

Du kommer nu att importera data till Adobe Experience Platform med Azure-kommandoradsverktyg med hjälp av AZCopy.

Öppna en terminal på platsen där du installerar azcopy och kör följande kommando för att kopiera en fil till AEP:s datalandningszon:

``./azcopy copy <your-local-file> <your SASUri>``

Se till att omge din SASUri med dubbla citattecken. Ersätt `<your-local-file>` med sökvägen till din lokala kopia av filen **global-context-websiteinteractions.csv** i azcopy-katalogen och ersätt `<your SASUri>` med värdet **SASUri** som du kopierade från Adobe Experience Platform-gränssnittet. Kommandot bör se ut så här:

```command
./azcopy copy global-context-websiteinteractions.csv "https://sndbxdtlnd2bimpjpzo14hp6.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-xxxxxxx-9843-4973-ae52-xxxxxxxx&sr=c&sp=racwdlm&sig=DN3kdhKzard%2BQwKASKg67Zxxxxxxxxxxxxxxxx"
```

När du har kört ovanstående kommando i terminalen visas följande:

![dlz-exec-copy-command.png](./images/dlzexeccopycommand.png)

## Sök efter filen i din Data Landing Zone

Gå till din Data Landing Zone i Adobe Experience Platform.

Välj **Källor**, sök efter **datalandning** och klicka på knappen **Inställningar** .

![dlz-inspect-datalanding-zone.png](./images/dlzinspectdatalandingzone.png)

Då öppnas Data Landing Zone. Du ser filen som du just överförde i datalandningszonens **valda data**-panel.

![dlz-datalanding-zone-open.png](./images/dlzdatalandingzoneopen.png)

## Bearbeta filen

Markera filen och välj **Avgränsad** som dataformat. Sedan visas en förhandsgranskning av dina data. Klicka på **Nästa**.

![dlz-datalanding-select-file.png](./images/dlzdatalandingselectfile.png)

Nu kan du börja mappa överförda data så att de matchar XDM-schemat i datauppsättningen.

Välj **Befintlig datauppsättning** och välj datauppsättningen **Demo System - händelsedatauppsättning för webbplats (Global v1.1)**. Klicka på **Nästa**.

![dlz-target-dataset.png](./images/dlztargetdataset.png)

Nu kan du mappa inkommande källdata från csv-filen till målfälten från datauppsättningens XDM-schema.

![dlz-start-mapping.png](./images/dlzstartmapping.png)

>[!NOTE]
>
> Glöm inte de potentiella felen med mappningen. Du korrigerar mappningen i nästa steg.

## Kartfält

Klicka först på knappen **Rensa alla mappningar**. Sedan kan du börja med en ren mappning.

![dlz-clear-mappings.png](./images/mappings1.png)

Klicka sedan på **Ny fälttyp** och välj **Lägg till nytt fält**.

![dlz-clear-mappings.png](./images/dlzclearmappings.png)

Om du vill mappa **ecid**-källfältet markerar du fältet **identities.ecid** och klickar på **Select**.

![dlz-map-identity.png](./images/dlzmapidentity.png)

Klicka sedan på **Mappa målfält**.

![dlz-map-select-target-field.png](./images/dlzmapselecttargetfield.png)

Markera fältet ``--aepTenantId--``.identity.core.ecid i schemastrukturen.

![dlz-map-target-field.png](./images/dlzmaptargetfield.png)

Du måste mappa några andra fält, klicka på **+ Ny fälttyp** följt av **Lägg till nytt fält** och lägga till fält för den här mappningen

| källa | target |
|---|---|
| resource.info.pagename | web.webPageDetails.name |
| tidsstämpel | tidsstämpel |
| tidsstämpel | _id |

![dlz-add-other-mapping.png](./images/dlzaddothermapping.png)

När skärmen är klar bör den se ut som på skärmen nedan. Klicka på **Nästa**.

![dlz-mapping-result.png](./images/dlzmappingresult.png)

Klicka på **Nästa**.

![dlz-default-eduling.png](./images/dlzdefaultscheduling.png)

Klicka på **Slutför**.

![dlz-import-finish.png](./images/dlzimportfinish.png)

## Övervaka dataflöde

Om du vill övervaka dataflödet går du till **Källor**, **Dataflöden** och klickar på dataflödet:

![dlz-monitor-dataflow.png](./images/dlzmonitordataflow.png)

Det kan ta några minuter att läsa in data. Statusen **Slutfört** visas när det är klart:

![dlz-monitor-dataflow-result.png](./images/dlzmonitordataflowresult.png)

Nästa steg: [Sammanfattning och förmåner](./summary.md)

[Gå tillbaka till modul 1.2](./data-ingestion.md)

[Gå tillbaka till Alla moduler](../../../overview.md)
