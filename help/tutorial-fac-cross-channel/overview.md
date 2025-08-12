---
title: Lås upp flerkanalsinsikter med Federated Audience Composition
description: Federated Audience Composition är en kraftfull funktion som gör det möjligt för dataarkitekter och datatekniker att skapa och berika målgrupper direkt från externa datalager.
breadcrumb-title: Översikt
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-overview.jpg
recommendations: catalog, noDisplay
last-substantial-update: 2025-08-11T00:00:00Z
source-git-commit: a5ae2695763bc3d6dce786861dcbc15f3422c035
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 0%

---


# Översikt

Federated Audience Composition är en kraftfull funktion för Adobe Real-Time Customer Data Platform (Real-Time CDP) och Adobe Journey Optimizer. Det gör det möjligt för dataarkitekter och datatekniker att skapa och berika målgrupper direkt från [stödda](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/access-prerequisites){target="_blank"} externa datalager utan att replikera data till Adobe Experience Platform. Den här självstudiekursen ger praktisk vägledning så att tekniska användare kan koppla samman informationslager på företagsnivå, skapa och berika målgrupper och aktivera dem för personaliserade marknadsföringsupplevelser.

## Utbildningsmål

När du är klar med den här självstudiekursen gör du följande:

- Lär dig hur du ansluter Adobe Experience Platform till ett företagsdatalager.
- Lär dig skapa och hantera målgrupper med Federated Audience Composition.
- Upptäck hur ni kan förbättra befintliga målgrupper med lagerdata.
- Mappa externa målgrupper till externa mål som Amazon S3.
- Bygg kundresor med hjälp av externa målgruppsdata.
- Validera data och processer med praktiska övningar och demonstrationer.

Den här självstudiekursen är utformad för dataarkitekter och datatekniker som arbetar med Real-Time CDP eller Journey Optimizer. Det förutsätter att man känner till Adobe Experience Platform och grundläggande datalagerkoncept.

## Affärskontext

SecurFinancial är ett ledande finansföretag. Det utnyttjar sin stora mängd kunddata från olika källor för att personalisera erbjudanden och kampanjer för ett stort antal segment. De planerar att använda Adobe Real-Time CDP Federated Audience Composition-funktionen, som gör att företag kan använda sitt befintliga datalager samtidigt som de använder Adobe Experience Platform-program för att leverera personaliserade kundupplevelser. Några viktiga fördelar:

- **Åtkomst till lagerdata**: Skapa värdefulla målgrupper från datauppsättningar i datalager som stöds utan datareplikering.
- **Minimerad dataförflyttning**: Fråga data direkt i lagerstället, minska dubbletter och upprätthålla datastyrning.
- **Enhetliga arbetsflöden för upplevelser**: Kuratera och aktivera målgrupper inom Adobe Experience Platform för flerkanalsbruk.
- **Förbättrad personalisering**: Förbättra profiler och målgrupper med lagerattribut så att ni kan skapa upplevelser som triggas i realtid.

## Affärsscenario

SecurFinancial vill lansera en e-postkampanj för att återannonsera sina kunder som är kvalificerade för ett lån baserat på god kredit och som inte har något aktivt lån i sin SecurFinancial-portfölj. Även om de inhämtar onlinebeteendedata i realtid är det svårt att identifiera kundens förkvalificering, eftersom de inte längre behöver inhämta kreditinformation till AEP. För att kvalificera kvalificerade kunder utan att flytta begränsade data kommer de att använda Federated Audience Composition för att berika sin AEP-beteendepublik.



## Förhandskrav

Se till att du har:

- Tillgång till ett Adobe Experience Platform-konto som tillhandahålls med Real-Time CDP eller Journey Optimizer.
- Behörigheter för systemadministratör eller möjlighet att konfigurera behörigheter.
- Bekanta dig med Adobe Experience Platform-koncept, som scheman, datauppsättningar och målgrupper (rekommenderas: fyll i [Introduktion till Adobe Experience Platform-spellista](https://experienceleague.adobe.com/en/playlists/experience-platform-introduction?lang=en){target="_blank"} på Experience League).
- Tillgång till ett datalager för företag som stöds (t.ex. Amazon Redshift, Azure Synapse Analytics, Snowflake eller Google BigQuery).
- Grundläggande kunskap i SQL för att fråga datalager.

## Använda denna självstudiekurs

Den här självstudiekursen är utformad för tekniska användare. Lektionerna bygger på varandra, så fyll i dem i ordning om inget annat anges.

## Tekniska anteckningar

- **Sandlådemiljöer**: Skapa en sandlåda i din organisations Real-Time CDP-instans för att experimentera utan att påverka produktionsdata.
- **Data Warehouse Connection**: I den här självstudien används en Snowflake-anslutning, men du kan använda vilket [molnlager](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/access-prerequisites) som helst.

Börja med lektionen [Data Warehouse Connection](data-warehouse-connection.md) för att börja konfigurera din miljö.
