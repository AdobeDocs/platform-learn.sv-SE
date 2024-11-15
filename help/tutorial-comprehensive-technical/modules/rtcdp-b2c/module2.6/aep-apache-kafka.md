---
title: Strömma data från Apache Kafka till Adobe Experience Platform
description: I den här modulen får du lära dig hur du konfigurerar ett eget Apache Kafka-kluster, definierar ämnen, producenter och konsumenter samt strömmar data till Adobe Experience Platform med Adobe Experience Platform Sink Connector for Kafka Connect.
kt: 5342
doc-type: tutorial
exl-id: 2b7010f3-ab31-4099-aecd-fd4e73b7e96e
source-git-commit: 0dbcda0cfc9f199a44c845c1b5caf00a8d740251
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---

# 2.6 Strömma data från Apache Kafka till Adobe Experience Platform

**Författare: [Vivek Tiwari](https://www.linkedin.com/in/vivek-tiwari-25092656/), [Nipun Nair](https://www.linkedin.com/in/nipunnair/), [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

I den här modulen får du lära dig hur du konfigurerar ett eget Apache Kafka-kluster, definierar ämnen, producenter och konsumenter samt strömmar data till Adobe Experience Platform med Adobe Experience Platform Sink Connector via Kafka Connect.

## Utbildningsmål

- Utför en grundläggande konfiguration av ett lokalt Kafka-kluster
- Skapa ett Kafka-tema, använd en Kafka-producent och en Kafka-konsument
- Konfigurera Kafka Connect och Adobe Experience Platform Sink Connector
- Skapa händelser manuellt och se vilka händelser som hämtas in i Adobe Experience Platform
- Använd ett befintligt Twitter Producer Library från Kafka Connect för att strömma Twitter till Adobe Experience Platform

## Förhandskrav

- Java JDK11 eller senare måste vara installerat på datorn. Du kan hämta JDK här: [https://www.oracle.com/java/technologies/javase-jdk11-downloads.html](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html)
- Tillgång till Adobe Experience Platform

>[!NOTE]
>
>Glöm inte att installera, konfigurera och använda Chrome-tillägget enligt [Installera Chrome-tillägget för Experience League-dokumentationen](../../gettingstarted/gettingstarted/ex1.md)

## Utövningar

[2.6.1 Introduktion till Apache Kafka](./ex1.md)

I den här övningen får du lära dig grunderna i Apache Kafka

[2.6.2 Installera och konfigurera Kafka-klustret](./ex2.md)

I den här övningen hämtar, installerar och konfigurerar du det grundläggande Apache Kafka-klustret.

[2.6.3 Konfigurera slutpunkten för HTTP API-direktuppspelning i Adobe Experience Platform](./ex3.md)

I den här övningen konfigurerar du en Source Connector för HTTP i Adobe Experience Platform.

[2.6.4 Installera och konfigurera Kafka Connect och Adobe Experience Platform Sink Connector](./ex4.md)

I den här övningen använder du Kafka Connect för att installera och använda Adobe Experience Platform Sink Connector och du skickar händelser till Adobe Experience Platform manuellt.

[Sammanfattning och fördelar](./summary.md)

Sammanfattning av den här modulen och en översikt över fördelarna.

>[!NOTE]
>
>Tack för att du lägger ned din tid på att lära dig allt om Adobe Experience Platform och dess program. Om du har frågor kan du dela allmän feedback om dina förslag på framtida innehåll. Kontakta Tech Insiders direkt genom att skicka ett e-postmeddelande till **techinsiders@adobe.com**.

[Gå tillbaka till Alla moduler](../../../overview.md)
