---
title: Installera och konfigurera Kafka-klustret
description: Installera och konfigurera Kafka-klustret
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: adffeead-9bcb-4632-9a2c-c6da1c40b7f2
source-git-commit: be5a7dec47a83a14d74024015a15a9c24d04cd95
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 0%

---

# 2.6.2 Installera och konfigurera Kafka-klustret

## Ladda ned Apache Kafka

Gå till [https://kafka.apache.org/downloads](https://kafka.apache.org/downloads) och hämta den senaste versionen. Välj den senaste binära versionen, i det här fallet **3.9.0**. Nedladdningen startar.

![Kafka](./images/kafka1.png)

Skapa en mapp med namnet **Kafka_AEP** på skrivbordet och placera den hämtade filen i den katalogen.

![Kafka](./images/kafka3.png)

Öppna ett **Terminal**-fönster genom att högerklicka på mappen och klicka på **Ny terminal i mappen**.

![Kafka](./images/kafka4.png)

Kör det här kommandot i terminalfönstret för att dekomprimera den hämtade filen:

`tar -xvf kafka_2.13-3.9.0.tgz`

>[!NOTE]
>
>Kontrollera att ovanstående kommando matchar den version av filen som du hämtade. Om din version är nyare måste du uppdatera ovanstående kommando så att det matchar den versionen.

![Kafka](./images/kafka5.png)

Då ser du det här:

![Kafka](./images/kafka6.png)

När du har dekomprimerat filen har du nu en katalog som den här:

![Kafka](./images/kafka7.png)

I den katalogen visas följande underkataloger:

![Kafka](./images/kafka8.png)

Gå tillbaka till terminalfönstret. Ange följande kommando:

`cd kafka_2.13-3.9.0`

>[!NOTE]
>
>Kontrollera att ovanstående kommando matchar den version av filen som du hämtade. Om din version är nyare måste du uppdatera ovanstående kommando så att det matchar den versionen.

![Kafka](./images/kafka9.png)

Ange sedan kommandot `bin/kafka-topics.sh`.

![Kafka](./images/kafka10a.png)

Du bör då se detta svar. Detta innebär att Kafka är korrekt installerat och att Java fungerar bra. (Påminnelse: du behöver Java 23 JDK installerat för att det här ska fungera! Du kan se vilken Java-version du har installerat med kommandot `java -version`.)

![Kafka](./images/kafka10.png)

## Starta Kafka

För att kunna starta Kafka måste du starta Kafka Zookeeper och Kafka i den här ordningen.

Öppna ett **Terminal**-fönster genom att högerklicka på mappen **kafka_2.13-3.9.0** och klicka på **Ny terminal i mappen**.

![Kafka](./images/kafka11.png)

Ange det här kommandot:

`bin/zookeeper-server-start.sh config/zookeeper.properties`

![Kafka](./images/kafka12.png)

Då ser du det här:

![Kafka](./images/kafka13.png)

Håll det här fönstret öppet medan du går igenom övningarna!

Öppna ett nytt **Terminal**-fönster genom att högerklicka på mappen **kafka_2.13-3.9.0** och klicka på **Ny terminal i mappen**.

![Kafka](./images/kafka11.png)

Ange det här kommandot:

`bin/kafka-server-start.sh config/server.properties`

![Kafka](./images/kafka14.png)

Då ser du det här:

![Kafka](./images/kafka15.png)

Håll det här fönstret öppet medan du går igenom övningarna!

## Skapa ett Kafka-ämne

Öppna ett **Terminal**-fönster genom att högerklicka på mappen **kafka_2.13-3.9.0** och klicka på **Ny terminal i mappen**.

![Kafka](./images/kafka11.png)

Ange det här kommandot om du vill skapa ett nytt Kafka-ämne med namnet **aeptest**. Det här avsnittet kommer att användas för testning i den här övningen.

`bin/kafka-topics.sh --create --topic aeptest --bootstrap-server localhost:9092`

Därefter visas en bekräftelse:

![Kafka](./images/kafka17a.png)

Ange det här kommandot om du vill skapa ett nytt Kafka-ämne med namnet **aep**. Det här avsnittet kommer att användas av Adobe Experience Platform Sink Connector som du kommer att konfigurera i nästa övningar.

`bin/kafka-topics.sh --create --topic aep --bootstrap-server localhost:9092`

En liknande bekräftelse visas:

![Kafka](./images/kafka17.png)

## Skapa händelser

Gå tillbaka till terminalfönstret där du skapade ditt första Kafka-avsnitt och ange följande kommando:

`bin/kafka-console-producer.sh --broker-list 127.0.0.1:9092 --topic aeptest`

![Kafka](./images/kafka18.png)

Då ser du det här. Varje ny rad som följs av att du trycker på Retur-knappen resulterar i att ett nytt meddelande skickas till ämnet **aeptest**.

![Kafka](./images/kafka19.png)

Ange `Hello AEP` och tryck på Retur. Din första händelse har skickats till din lokala Kafka-instans till ämnet **aeptest**.

![Kafka](./images/kafka20.png)

Ange `Hello AEP again.` och tryck på Retur.

Ange `AEP Data Collection is the best.` och tryck på Retur.

Du har nu producerat 3 händelser i ämnet **aeptest**. Dessa händelser kan nu användas av ett program som behöver dessa data.

![Kafka](./images/kafka21.png)

Klicka på `Control` och `C` samtidigt på tangentbordet för att stänga din producent.

![Kafka](./images/kafka22.png)

## Förbrukningshändelser

I samma terminalfönster som du använde för att skapa händelser anger du följande kommando:

`bin/kafka-console-consumer.sh --bootstrap-server 127.0.0.1:9092 --topic aeptest --from-beginning`

Du kommer då att se alla meddelanden som har producerats i föregående övning för ämnet **aeptest** visas i konsumenten. Så här fungerar Apache Kafka: en producent skapar händelser i en pipeline och en konsument konsumerar dessa händelser.

![Kafka](./images/kafka23.png)

Klicka på `Control` och `C` samtidigt på tangentbordet för att stänga din producent.

![Kafka](./images/kafka24.png)

I den här övningen har du gått igenom alla grunderna för att konfigurera ett lokalt Kafka-kluster, skapa ett Kafka-ämne, producera händelser och konsumera händelser.

Målet med den här modulen är att simulera vad som skulle hända om en riktig organisation redan har implementerat ett Apache Kafka-kluster och vill strömma data från sitt Kafka-kluster till Adobe Experience Platform.

För att underlätta en sådan implementering skapades en Adobe Experience Platform Sink Connector som kan implementeras med Kafka Connect. Dokumentationen för den Adobe Experience Platform Sink Connector finns här: [https://github.com/adobe/experience-platform-streaming-connect](https://github.com/adobe/experience-platform-streaming-connect).

I nästa övning kommer du att implementera allt du behöver för att använda Adobe Experience Platform Sink Connector inifrån ditt eget lokala Kafka-kluster.

Stäng terminalfönstret.

Du har gjort klart den här övningen.

Nästa steg: [2.6.3 Konfigurera HTTP API-slutpunkt i Adobe Experience Platform](./ex3.md)

[Gå tillbaka till modul 2.6](./aep-apache-kafka.md)

[Gå tillbaka till Alla moduler](../../../overview.md)
