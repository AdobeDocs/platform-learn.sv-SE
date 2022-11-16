---
title: Strömma data från Apache Kafka till Adobe Experience Platform
description: I den här modulen får du lära dig hur du konfigurerar ett eget Apache Kafka-kluster, definierar ämnen, producenter och konsumenter samt strömmar data till Adobe Experience Platform med Adobe Experience Platform Sink Connector for Kafka Connect.
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: e1e283b1-93b7-4d06-b9ed-beac48a99c3f
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---

# 15. Strömma data från Apache Kafka till Adobe Experience Platform

**Författare: [Vivek Tiwari](https://www.linkedin.com/in/vivek-tiwari-25092656/), [Nipun Nair](https://www.linkedin.com/in/nipunnair/), [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

I den här modulen får du lära dig hur du konfigurerar ett eget Apache Kafka-kluster, definierar ämnen, producenter och konsumenter samt strömmar data till Adobe Experience Platform med Adobe Experience Platform Sink Connector via Kafka Connect.

## Utbildningsmål

- Utför en grundläggande konfiguration av ett lokalt Kafka-kluster
- Skapa ett Kafka-tema, använd en Kafka-producent och en Kafka-konsument
- Konfigurera Kafka Connect och Adobe Experience Platform Sink Connector
- Skapa händelser manuellt och se vilka händelser som hämtas in i Adobe Experience Platform
- Använd ett befintligt Twitter-bibliotek från Kafka Connect för att strömma Twitter-data till Adobe Experience Platform

## Förutsättningar

- Java JDK11 eller senare måste vara installerat på datorn. Du kan hämta JDK här: [https://www.oracle.com/java/technologies/javase-jdk11-downloads.html](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html)
- Tillgång till Adobe Experience Platform

## Arkitektur - översikt

Titta närmare på arkitekturen nedan, som visar vilka komponenter som kommer att diskuteras och användas i den här modulen.

![Arkitektur - översikt](../../assets/images/architecturem24.png)

## Sandlåda att använda

Använd den här sandlådan för den här modulen: `--aepSandboxId--`.

>[!NOTE]
>
>Glöm inte att installera, konfigurera och använda Chrome-tillägget enligt referensen i [0.1 - Installera Chrome-tillägget för Experience League-dokumentationen](../module0/ex1.md)

## Utövningar

[15.1 Introduktion till Apache Kafka](./ex1.md)

I den här övningen får du lära dig grunderna i Apache Kafka

[15.2 Installera och konfigurera Kafka-klustret](./ex2.md)

I den här övningen hämtar, installerar och konfigurerar du det grundläggande Apache Kafka-klustret.

[15.3 Konfigurera slutpunkten för HTTP API-direktuppspelning i Adobe Experience Platform](./ex3.md)

I den här övningen konfigurerar du en HTTP API-källanslutning i Adobe Experience Platform.

[15.4 Installera och konfigurera Kafka Connect och Adobe Experience Platform Sink Connector](./ex4.md)

I den här övningen använder du Kafka Connect för att installera och använda Adobe Experience Platform Sink Connector och du skickar händelser till Adobe Experience Platform manuellt.

[Sammanfattning och fördelar](./summary.md)

Sammanfattning av den här modulen och en översikt över fördelarna.

>[!NOTE]
>
>Tack för att du lade ned din tid på att lära dig allt om Adobe Experience Platform. Om du har frågor kan du dela allmän feedback om dina förslag på framtida innehåll. Kontakta Wouter Van Geluwe direkt genom att skicka ett e-postmeddelande till **vangeluw@adobe.com**.

[Gå tillbaka till Alla moduler](../../overview.md)
