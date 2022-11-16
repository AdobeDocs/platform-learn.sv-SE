---
title: Hur mäts Slutförande?
description: Hur mäts Slutförande?
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst, Data Scientist, Orchestration Engineer, BI Expert, Marketer
doc-type: tutorial
activity: develop
exl-id: 49baf4dd-8827-46e8-a2f9-9aeac31f8ff9
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1092'
ht-degree: 3%

---

# Omfattande teknisk självstudiekurs för Adobe Experience Platform - Hur mäts slutförandet?

Du kan uppdatera din komplettering av den omfattande tekniska självstudiekursen för Adobe Experience Platform med det Chrome-tillägg som skapades.

När du har följt instruktionerna i modul 0 har du angett din organisations **Konfigurations-ID** i Chrome-tillägget och du har registrerat dig. Chrome-tillägget bör nu se ut så här. Klicka på den lila ikonen för att skicka in en modul.

![12](./assets/images/config1.png)

Då ser du det här:

![12](./assets/images/config2.png)

Genom att öppna listrutan kan du välja vilken modul du vill slutföra:

![12](./assets/images/adminhome.png)

För att slutföra en modul måste du tillhandahålla ett bevis på att du är klar.

Nedan visas det förväntade korrekturet för varje modul.

## Komma igång

Förväntat slutförandebevis för modulen **Komma igång** är ID:t för det Demo System-projekt för webben som du har skapat.

ID:t för Demo System-projektet för webbformat ser ut så här: `--demoProfileLdap-- - OCUC`.

![3](./assets/images/module0dtl.png)

Välj **Komma igång** i listrutan anger du **ID för Demo System-projektet** och klicka på **Skicka** - knapp.

![12](./assets/images/completemodule0dtl.png)

## Datainsamling och Web SDK

Förväntat slutförandebevis för modulen **Datainsamling och Web SDK** är namnet på datainsamlingsegenskapen för webben.

Namnet på egenskapen Datainsamling för webbformat ser ut så här: `--demoProfileLdap-- - Demo System (05/02/2022) (enablement) 1644046719474`.

![3](./assets/images/module1dtl.png)

Välj **Datainsamling och Web SDK** i listrutan anger du **Egenskapsnamn för datainsamling för webben** och klicka på **Skicka** - knapp.

![12](./assets/images/completemodule1dtl.png)

## Dataintag

Förväntat slutförandebevis för modulen **Dataintag** är datauppsättnings-ID för de två datauppsättningar som du har skapat.

Formatet för datauppsättnings-ID ser ut så här: **5f069724723ef41916a8b5d2**.

`--demoProfileLdap-- - Demo System - Event Dataset for Website`

![3](./assets/images/completemodule2seg.png)

`--demoProfileLdap-- - Demo System - Profile Dataset for Website`

![3](./assets/images/completemodule2seg1.png)

Välj **Dataintag** i listrutan anger du **Datauppsättnings-ID** för båda datauppsättningarna i indatafälten och klicka på **Skicka** - knapp.

![12](./assets/images/completemodule2dtl.png)

## Kundprofil i realtid

Förväntat slutförandebevis för modulen **Kundprofil i realtid** är **Segment-ID** för segmentet som du skapade via användargränssnittet, `--demoProfileLdap-- - Male customers with interest in Montana Wind Jacket`.

Formatet för segment-ID ser ut så här: **8cb7034d-d4ae-4d26-a61f-a76559c12457**.

![3](./assets/images/completemodule3seg.png)

Välj **Kundprofil i realtid** i listrutan anger du **Segment-ID** i inmatningsfältet och klicka på **Skicka** - knapp.

![12](./assets/images/completemodule3dtl.png)

## Frågetjänst

Förväntat slutförandebevis för modulen **Frågetjänst** är ditt datauppsättnings-ID `--demoProfileLdap--_callcenter_interaction_analysis` - datauppsättning som du får när du har slutfört modulen.

Formatet ser ut så här: **62076f68f14a9d194995d4e2**.

![12](./assets/images/completemodule7.png)

Välj **Frågetjänst** i listrutan anger du **Datauppsättnings-ID** i inmatningsfältet och klicka på **Skicka** - knapp.

![12](./assets/images/completemodule7dtl.png)

## Intelligenta tjänster

Förväntat slutförandebevis för modulen **Intelligenta tjänster** är ditt ID **Kundens AI-tjänst för produktköpsförmån**.

Formatet ser ut så här: **12729** och du kan hämta det från URL:en när du har öppnat tjänsten.

![12](./assets/images/completemodule10.png)

Välj **Intelligenta tjänster** i listrutan anger du **Kundens AI-tjänste-ID** i inmatningsfältet och klicka på **Skicka** - knapp.

![12](./assets/images/completemodule10dtl.png)

## Real-Time CDP

Förväntat slutförandebevis för modulen **Real-Time CDP** är ditt ID **Adobe Target Activity**.

Formatet ser ut så här: **111804**.

![12](./assets/images/vec4.png)

Välj **Real-Time CDP** i listrutan anger du **Adobe Target Activity ID** i inmatningsfältet och klicka på **Skicka** - knapp.

![12](./assets/images/completemodule11dtl.png)

## AJO: Orchestration

Förväntat slutförandebevis för modulen **AJO: Orchestration** är eventID för `--demoProfileLdap--AccountCreationEvent`.

Formatet ser ut så här: **227402c540eb8f8855c6b2333adf6d54d7153d9d7d56fa475a686081c57473 6**.

![12](./assets/images/ajoo.png)

Välj **AJO: Orchestration** i listrutan anger du ditt ** eventID** i inmatningsfältet och klickar på **Skicka** - knapp.

![12](./assets/images/completemodule6dtl.png)

## AJO: Anpassade åtgärder

Förväntat slutförandebevis för modulen **AJO: Anpassade åtgärder** är eventID för din händelse `--demoProfileLdap--GeofenceEntry`.

Formatet ser ut så här: **fa42ab7982ba55f039eacec24c1e32e5c51b310c67f0fa559ab49b89b63f4934**.

![12](./assets/images/jofinal.png)

Välj **AJO: Anpassade åtgärder** i listrutan anger du **eventID** i inmatningsfältet och klicka på **Skicka** - knapp.

![12](./assets/images/completemodule12dtl.png)

## AJO: Erbjudanden

Förväntat slutförandebevis för modulen **AJO: Erbjudanden** är ID:t för **Erbjudandebeslut** som du skapade.

Du hittar **ID för erbjudandebeslut** som ser ut så här **xcore:offer-activity:1122fcc4603ea499**, här:

![14](./assets/images/offers.png)

Välj **AJO: Erbjudanden** i listrutan anger du **ID för erbjudandebeslut** i inmatningsfältet och klicka på **Skicka** - knapp.

![12](./assets/images/completemodule14dtl.png)

## AJO: Händelser

Förväntat slutförandebevis för modulen **AJO: Händelser** är eventID för `--demoProfileLdap--StoreEntryEvent`.

Formatet ser ut så här: **e3a8f0bdc0b609667cd96a72a6b1e5aafa0ddaf6ccf121c574e6a2030860a633**.

![14](./assets/images/jojourneyid.png)

Välj **AJO: Händelser** i listrutan anger du **eventID** i inmatningsfältet och klicka på **Skicka** - knapp.

![12](./assets/images/completemodule23dtl.png)

## CJA

Förväntat slutförandebevis för modulen **CJA** är ID:t för ditt projekt `--demoProfileLdap-- - Omnichannel Analysis`.

Formatet ser ut så här: **6217344f6249ac70c726db60** hittar du den i URL:en när du har öppnat projektet.

![12](./assets/images/cjacompletion.png)

Välj **CJA** i listrutan anger du **Projekt-ID** i inmatningsfältet och klicka på **Skicka** - knapp.

![12](./assets/images/completemodule13dtl.png)

## CJA: BigQuery

Förväntat slutförandebevis för modulen **CJA: BigQuery** är ditt ID **BigQuery**-connection.

Du hittar **Anslutnings-ID för BigQuery** som ser ut så här **85a2394d-8b94-410c-a239-4d8b94b10c38**, här:

![14](./assets/images/bqid.png)

Välj **CJA: BigQuery** i listrutan anger du **Anslutnings-ID för BigQuery** i inmatningsfältet och klicka på **Skicka** - knapp.

![12](./assets/images/completemodule16dtl.png)

## RTCDP: EventHub

Förväntat slutförandebevis för modulen **RTCDP: EventHub** är ditt ID **Microsoft Azure Event Hub** mål i Adobe Experience Platform.

Du hittar **Mål-ID för Microsoft Azure Event Hub** som ser ut så här **fa3f7ce5-86fd-4096-bf7c-e586fdc096ba**, här:

![14](./assets/images/azuredestid.png)

Välj **RTCDP: EventHub** i listrutan anger du **Mål-ID för Microsoft Azure Event Hub** i inmatningsfältet och klicka på **Skicka** - knapp.

![12](./assets/images/completemodule18dtl.png)

## RTCDP-anslutningar

Förväntat slutförandebevis för modulen **RTCDP-anslutningar** är din **Egenskaps-ID för händelsevidarebefordran**.

Du hittar **Egenskaps-ID för händelsevidarebefordran** som ser ut så här **PR40f44184c88472e9c19d8d602aab0de**, här:

![14](./assets/images/launchssfid.png)

Välj **RTCDP-anslutningar** i listrutan anger du **Egenskaps-ID för händelsevidarebefordran** i inmatningsfältet och klicka på **Skicka** - knapp.

![12](./assets/images/completemodule21dtl.png)

## Apache Kafka

Förväntat slutförandebevis för modulen **Apache Kafka** är ID:t för din källkoppling `--demoProfileLdap-- - Kafka`.

ID:t ser ut så här **f843d50a-ee30-4ca8-a766-0e4f3d29a2f7** och du hittar den här:

![14](./assets/images/kafkaflowid.png)

Välj **Apache Kafka** i listrutan anger du **Flöde-ID** i inmatningsfältet och klicka på **Skicka** - knapp.

![12](./assets/images/completemodule24dtl.png)

[Gå tillbaka till Alla moduler](./overview.md)
