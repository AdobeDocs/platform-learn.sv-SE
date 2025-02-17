---
title: Strömma data från Apache Kafka till Adobe Experience Platform
description: I den här modulen får du lära dig hur du konfigurerar ett eget Apache Kafka-kluster, definierar ämnen, producenter och konsumenter samt strömmar data till Adobe Experience Platform med Adobe Experience Platform Sink Connector for Kafka Connect.
kt: 5342
doc-type: tutorial
exl-id: 28c63675-272e-46ff-88fc-6cd4096d66ca
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---

# 2.6 Strömma data från Apache Kafka till Adobe Experience Platform

I den här modulen får du lära dig hur du konfigurerar ett eget Apache Kafka-kluster, definierar ämnen, producenter och konsumenter samt strömmar data till Adobe Experience Platform med Adobe Experience Platform Sink Connector via Kafka Connect.

## Utbildningsmål

- Utför en grundläggande konfiguration av ett lokalt Kafka-kluster
- Skapa ett Kafka-tema, använd en Kafka-producent och en Kafka-konsument
- Konfigurera Kafka Connect och Adobe Experience Platform Sink Connector
- Skapa händelser manuellt och se vilka händelser som hämtas in i Adobe Experience Platform
- Använd ett befintligt Twitter-bibliotek från Kafka Connect för att strömma Twitter-data till Adobe Experience Platform

## Förhandskrav

- Java JDK23 eller senare måste vara installerat på datorn. Du kan hämta JDK här: [https://www.oracle.com/java/technologies/javase-jdk11-downloads.html](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html)
- Tillgång till Adobe Experience Platform

>[!NOTE]
>
>Glöm inte att installera, konfigurera och använda Chrome-tillägget enligt [Installera Chrome-tillägget för Experience League-dokumentationen](../../../getting-started/gettingstarted/ex1.md)

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

![Tech Insiders](./../../../../assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>Tack för att du lägger ned din tid på att lära dig allt om Adobe Experience Platform och dess program. Om du har frågor kan du dela allmän feedback om dina förslag på framtida innehåll. Kontakta Tech Insiders direkt genom att skicka ett e-postmeddelande till **techinsiders@adobe.com**.

[Gå tillbaka till Alla moduler](./../../../../overview.md)
