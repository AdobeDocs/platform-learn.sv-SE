---
title: Sammansättning av avancerad målgruppsarkitektur och högnivåflöde
seo-title: Federated Audience Composition High-level Architecture & Flow | Engage with Audiences from your Data Warehouse using Federated Audience Composition
breadcrumb-title: Sammansättning av avancerad målgruppsarkitektur och högnivåflöde
description: Översikt över arkitekturen och flödet i Federated Audience Composition.
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-high-level-architecture.jpg
source-git-commit: dd5f594a54a9cab8ef78d36d2cf15a9b5f2b682a
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---


# Sammansättning av avancerad målgruppsarkitektur och högnivåflöde

Innan vi går vidare till att stödja affärsscenariot för SecurFinancial kommer vi att granska den övergripande arkitekturen och flödet för denna sammanställningsbara CDP-strategi.

Med modulen för federerad målgruppskomposition i Adobe Experience Platform utökas åtkomsten till datalageruppsättningar utan att underliggande data kopieras, vilket minimerar dataförflyttning och duplicering.

Detta ger också den sammansättningsbara arkitektur som behövs, som redan har slutfört det datahanteringsarbete som krävs på sitt lager och vill använda ett nollkopieringsmönster där Adobe Experience Platform blir engagemangsmotorn.

Det gör att företag snabbt kan bearbeta information som lagras i ett eller flera datalager. Det eliminerar behovet av att importera data till Adobe Experience. Dessutom ger det åtkomst till nya datauppsättningar som finns i företagens datalager men som hittills inte varit tillgängliga för kundupplevelsearbetsflöden. Exemplen kan omfatta historiska transaktioner eller personuppgifter som kommer att vara användbara på aggregerad målgruppsnivå för kundengagemang.

![fac-architecture](assets/fac-architecture.png)

Nu går vi vidare till att skapa en [Data Warehouse-anslutning](data-warehouse-connection.md).

