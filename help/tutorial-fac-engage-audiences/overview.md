---
title: Engagera med målgrupper direkt från ert datalager med en översikt över federerad målgruppskomposition
description: Federated Audience Composition är en kraftfull funktion som gör det möjligt för dataarkitekter och datatekniker att strukturera och aktivera värdefulla målgrupper direkt från datalager som stöds.
breadcrumb-title: Översikt
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-overview.jpg
recommendations: catalog, noDisplay
last-substantial-update: 2025-08-11T00:00:00Z
exl-id: 9d5a2e40-6cda-4164-87db-1bfffe3438e3
source-git-commit: 93b787112134919444150974c7149dc10c2d0ca6
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 0%

---

# Engagera med målgrupper direkt från ert datalager med en översikt över federerad målgruppskomposition

FAC (Federated Audience Composition) är en modul för Adobe Real-Time Customer Data Platform (Real-Time CDP) och Adobe Journey Optimizer. Det finns också med Adobe Real-Time CDP Composable Audiences (en skräddarsydd lösning för kunder som Composable CDP). Det ger dataarkitekter och datatekniker möjlighet att strukturera och aktivera värdefulla målgrupper direkt från [supportade datalager](https://experienceleague.adobe.com/sv/docs/federated-audience-composition/using/start/access-prerequisites){target="_blank"}, utan att behöva kopiera eller flytta kunddata till Adobe Experience Platform (AEP). Den här sammanställningsbara CDP-metoden (en skräddarsydd lösning för kunder) är anpassad efter branschtrender, vilket gör att företag kan utnyttja sin datainfrastruktur för personaliserade digitala upplevelser samtidigt som datastyrningen upprätthålls.

## Affärskontext

SecurFinancial är ett ledande finansföretag. Det utnyttjar sin stora mängd kunddata från olika källor för att personalisera erbjudanden och kampanjer för ett stort antal segment. De planerar att använda Adobe Real-Time CDP Federated Audience Composition Module som gör att företag kan använda sitt datalager för datahantering samtidigt som de använder Adobe Experience Platform för att leverera personaliserade kundupplevelser. Några viktiga fördelar:

- **Åtkomst till lagerdata**: Skapa värdefulla målgrupper från datauppsättningar i datalager som stöds utan datareplikering.
- **Minimerad datarörelse**: Fråga data direkt i lagerstället, utan duplicering och bibehållen datastyrning.
- **Enhetliga arbetsflöden för upplevelser**: Kuratera och aktivera målgrupper inom Adobe Experience Platform för flerkanalsbruk.
- **Förbättrad personalisering**: Förbättra profiler och målgrupper med lagerattribut så att ni kan skapa upplevelser som triggas i realtid.

## Affärsscenario

SecurFinancial vill lansera en e-postkampanj för att återannonsera sina kunder som är kvalificerade för ett lån baserat på god kredit och som inte har något aktivt lån i sin SecurFinancial-portfölj. De inhämtar onlinebeteendedata i realtid, men de står inför utmaningar när det gäller att identifiera kundens förkvalificering, eftersom de är begränsade från att inhämta kreditinformation till AEP. För att kvalificera kvalificerade kunder utan att flytta begränsade data kommer de att använda Federated Audience Composition för att berika sin AEP-beteendepublik.

## Guide

Den här guiden visar hur vi stöder SecureFinancial Business-scenariot. Det handlar i synnerhet om hur vi exponerar målgrupper för system som behöver dessa målgrupper, inklusive ett S3-lagringskonto, en resa i Journey Optimizer för att driva en e-postkampanj och återmarknadsföring på plats för kunder som godkänts i förväg för ett lån.

Stegen innehåller:

1. Koppla Adobe Experience Platform till ett datalager för företag.
2. Skapa en målgrupp med Federated Audience Composition.
3. Mappa en federerad publik till en extern Amazon S3-destination.
4. Bygg en kundresa med hjälp av externa målgruppsdata.
5. Berika en målgrupp med federerade data.
6. Driv&quot;in-the-just&quot;-personalisering på Edge.

## Förhandskrav

Om du vill utföra liknande aktiviteter i din miljö måste du ha:

- Tillgång till ett Adobe Experience Platform-konto som tillhandahålls med Real-Time CDP eller Journey Optimizer.
- Behörigheter för systemadministratör eller möjlighet att konfigurera behörigheter.
- Bekanta dig med Adobe Experience Platform-koncept, som scheman, datauppsättningar och målgrupper (rekommenderas: fyll i [Introduktion till Adobe Experience Platform-spellista](https://experienceleague.adobe.com/sv/playlists/experience-platform-introduction?lang=en){target="_blank"} på Experience League).
- Åtkomst till ett [Enterprise-datalager](https://experienceleague.adobe.com/sv/docs/federated-audience-composition/using/start/access-prerequisites){target="_blank"} som stöds.
- Grundläggande kunskap i SQL för att fråga datalager.
- **Sandlådemiljöer**: Skapa en sandlåda i din organisations instans för att experimentera utan att påverka produktionsdata.
- **Data Warehouse Connection**: I den här självstudien används en Snowflake-anslutning, men du kan använda vilket [datalager](https://experienceleague.adobe.com/sv/docs/federated-audience-composition/using/start/access-prerequisites) som helst som stöds.

Först ska vi granska [High-level Architecture &amp; Flow for Federated Audience Composition](fac-architecture-and-flow.md).
