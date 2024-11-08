---
title: Introduktion till Apache Kafka
description: Introduktion till Apache Kafka
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 0%

---

# 2.6.1 Introduktion till Apache Kafka

## 2.6.1.1 Inledning

Alla organisationer börjar på ett mycket enkelt sätt ur ett dataperspektiv. En organisations ekosystem av data börjar med ett källsystem och ett mål. Källsystemet skickar data till målsystemet, och det är det. Lätt, eller hur?
Om det bara vore så enkelt. Organisationerna växer snabbt och växer snabbare än den enkla konfigurationen och antalet källsystem och målsystem. Alla dessa olika källor och destinationer måste utbyta data med varandra, och allt blir snabbt mycket komplext.
Om en organisation till exempel har fyra källor och sex mål och alla dessa program behöver tala med varandra måste ni skapa 24 integreringar.. Var och en av dessa integreringar har sina egna svårigheter:

- protokoll: hur data transporteras (TCP, HTTP, REST, FTP, ...)
- dataformat: hur tolkas data (binärt, CSV, JSON, Parquet, ...)
- dataschema och datautveckling: vad är datamodellen och hur kommer den att utvecklas?

Varje gång du ansluter ett källsystem till ett målsystem ökar dessutom belastningen på dessa system från den anslutningen.

Hur löser du det här? Det är där Apache Kafka kommer in i bilden. Med Apache Kafka kan en organisation koppla ihop dataströmmar och system genom att tillhandahålla ett gemensamt, distribuerat meddelandesystem med hög genomströmning. Source-system skickar sina data till Apache Kafka, och målsystemen använder data från Apache Kafka.

Tänk på alla typer av datakällor som företag måste hantera:

- webbplatshändelser
- mobilappshändelser
- POS-händelser
- CRM-data
- callcenter-data
- transaktionshistoria
- ...

Och tänk på alla typer av destinationer som företag använder i sina ekosystem och som alla kan behöva data från dessa källsystem:

- CRM
- Data Lake
- e-postsystem
- granskning
- analys
- ...

Apache Kafka skapades av LinkedIn och är nu ett öppen källkodsprojekt som huvudsakligen underhålls av Confluent.
Apache Kafka har en distribuerad, flexibel arkitektur som är feltolerant. Den kan skalas vågrätt till 100-tal mäklare och kan skalas till miljontals meddelanden per sekund. Den ger höga prestanda med latenser på mindre än 10 ms, vilket är idealiskt för användning i realtid.

Några exempel:

- Meddelandesystem
- Aktivitetsspårning
- Samla in mätvärden från många olika platser
- Insamling av programloggar
- Direktuppspelningsbearbetning (med Kafka Streams API eller Spark)
- Frikoppling av systemberoenden
- Integrering med Spark, Flink, Storm, Hadoop och många andra Big Data-tekniker.

Till exempel:

- Netflix använder Kafka för att tillämpa rekommendationer i realtid medan du tittar på tv-program
- Uber använder Kafka för att samla in användar-, taxi- och resedata i realtid för att beräkna och förutse efterfrågan och beräkna extra priser i realtid
- LinkedIn använder Kafka för att förhindra skräppost, samla in användarinteraktioner för att ge bättre anslutningsrekommendationer i realtid

I samtliga dessa fall används Kafka endast som en transportmekanism. Kafka är mycket bra på att flytta data mellan program.

## 2.6.1.2 Kafka-terminologi

### Meddelande

Ett meddelande är ett meddelande som skickas från ett system till Kafka. Ett meddelande innehåller en nyttolast och en nyttolast innehåller dataelement. En upplevelsehändelse som skickas från en webbplats till Adobe Experience Platform betraktas till exempel som ett meddelande.

### Ämne, partitioner, förskjutningar

Ett ämne är en särskild dataström som liknar en tabell i en databas. Du kan ha så många ämnen som du vill och ett ämne identifieras av dess namn. Ämnen delas upp i partitioner. Varje partition ordnas och varje meddelande i en partition får ett inkrementellt ID, som kallas **offset**. Meddelanden lagras i ett ämne på en partition och refereras med en förskjutning. Meddelanden sparas endast under en begränsad tid (standardinställningen är 1 vecka). När ett meddelande har skrivits till en partition kan det inte ändras längre.

### Mäklare

En mäklare liknar en server. Kafka består av flera mäklare (servrar). Varje mäklare identifieras med ett ID och innehåller vissa ämnespartitioner.

### Replikering

Kafka är ett distribuerat system. En av de viktiga sakerna i ett distribuerat system är att data lagras på ett säkert sätt och därför behövs replikering. När en mäklare (server) går ner bör en annan mäklare (server) ändå kunna ge åtkomst till meddelanden som ursprungligen lagrades på den mäklare som gick ned. Replikeringen skapar kopior av meddelanden för flera förmedlare för att säkerställa att inga data går förlorade.

### Producenter

Hur skickas data till Kafka? Det är en producents roll. En producent ansluter till ett källsystem och tar data från källsystemet, och skriver sedan dessa data till ämnen på partitioner. Beroende på hur Kafka-klustret är konfigurerat vet tillverkarna automatiskt vilken mäklare och partition de ska skriva till. I ett distribuerat system med flera mäklare och replikeringsstrategier kommer en producent att lagra data slumpmässigt över flera mäklare, vilket innebär att den automatiskt utför belastningsutjämning.

### Meddelandenycklar

Producenterna kan välja att skicka en nyckel med meddelandet. En nyckel kan vara vilken sträng som helst, ett tal osv. Om ingen nyckel anges skickas ett meddelande slumpmässigt till mäklare. Om en nyckel skickas kommer alla meddelanden för den nyckeln alltid att gå till samma partition. En meddelandenyckel som sådan används för att sortera meddelanden baserat på ett specifikt fält.

### Konsumenter

Konsumenterna läser data från ett Apache Kafka-avsnitt och delar sedan dessa data med målsystemen. Konsumenterna vet vilken mäklare de ska läsa från. Data läses av en konsument i ordning inom varje partition. Konsumenterna läser data i konsumentgrupper.

### Zookeeper

ZooKeeper är i princip en tjänst för distribuerade system som erbjuder ett hierarkiskt nyckelvärdenhetslager, som används för att tillhandahålla en distribuerad konfigurationstjänst, synkroniseringstjänst och namnregister för stora distribuerade system. Zookeeper måste vara igång innan du kan använda Apache Kafka, och Zookeeper är en sorts mästare för Kafka, som hanterar distribuerade tjänster i serverdelen medan Kafka producerar och konsumerar händelser.

Du har gjort klart den här övningen.

Nästa steg: [2.6.2 Installera och konfigurera Kafka-klustret](./ex2.md)

[Gå tillbaka till modul 2.6](./aep-apache-kafka.md)

[Gå tillbaka till Alla moduler](../../../overview.md)
