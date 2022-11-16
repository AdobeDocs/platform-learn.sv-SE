---
title: Foundation - konfiguration av Adobe Experience Platform Data Collection och Web SDK-tillägget - Edge Network, Datastreams och Server Side Data Collection
description: Foundation - konfiguration av Adobe Experience Platform Data Collection och Web SDK-tillägget - Edge Network, Datastreams och Server Side Data Collection
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 6f7c540f-3804-483d-90f9-b26b4a252b8b
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 2%

---

# 1.2 Edge Network, DataStreams och Server Side Data Collection

## Kontext

I den här övningen ska du skapa en **Datastream**. A **Datastream** anger för Adobe Edge-servrarna var data ska skickas när de har samlats in via Web SDK. Vill du till exempel skicka data till Adobe Experience Platform? Adobe Analytics? Adobe Audience Manager? Adobe Target?

Datastreams hanteras alltid i användargränssnittet i Adobe Experience Platform Data Collection och är viktiga för Adobe Experience Platform datainsamling med Web SDK. Även om du implementerar Web SDK med en tagghanteringslösning som inte är Adobe måste du ändå skapa din datastream i Adobe Experience Platform Data Collection-användargränssnittet.

Du kommer att implementera Web SDK i webbläsaren i nästa övning. Då blir det tydligare för er hur de data som samlas in ser ut. För närvarande berättar vi bara för DataStream var vi ska vidarebefordra data.

## Skapa ett datastream

I [Utövning 0.2](./../module0/ex2.md) du redan har skapat en datastream, men vi har inte diskuterat bakgrunden och anledningen till att du var hos Datastream.

En dataström talar om för Adobe Edge-servrarna var data ska skickas när de har samlats in av Web SDK. Vill du till exempel skicka data till Adobe Experience Platform? Adobe Analytics? Adobe Audience Manager? Adobe Target? Datastreams hanteras i användargränssnittet i Adobe Experience Platform Data Collection och är avgörande för plattformsdatainsamling med Web SDK, oavsett om du implementerar Web SDK via Adobe Experience Platform Data Collection eller inte.

Låt oss titta på **[!UICONTROL Datastream]**:

Gå till [https://experience.adobe.com/launch/](https://experience.adobe.com/launch/).

Klicka **[!UICONTROL Datastreams]** eller **[!UICONTROL Datastreams (beta)]** i den vänstra menyn.

![Klicka på Datastream-ikonen i den vänstra navigeringen](./images/edgeconfig1.png)

Sök efter ditt datastream, som har namnet `--demoProfileLdap-- - Demo System Datastream`.

![Namnge datastream och spara](./images/edgeconfig2.png)

Då ser du detaljerna om din dataström.

![Namnge datastream och spara](./images/edgecfg1.png)

Klicka **...** nästa **Adobe Experience Platform** och klicka **Redigera**.

![Namnge datastream och spara](./images/edgecfg1a.png)

Du kommer då att se det här. För tillfället har du bara aktiverat Adobe Experience Platform. Konfigurationen ser ut ungefär som i konfigurationen nedan. (Beroende på din miljö och Adobe Experience Platform-instans kan namnet på sandlådan vara ett annat)

![Namnge datastream och spara](./images/edgecfg2.png)

Du bör tolka nedanstående fält så här:

För denna datastream...

- Alla data som samlas in lagras i `--aepSandboxId--` sandlåda i Adobe Experience Platform
- Alla Experience Event-data samlas som standard in i datauppsättningen **Demo System - händelsedatauppsättning för webbplats (Global v1.1)**
- Alla profildata samlas som standard in i datauppsättningen **Demonstrationssystem - profildatauppsättning för webbplats (Global v1.1)** (Inmatning av profildata internt med Web SDK stöds för närvarande inte av Web SDK och kommer att göras tillgängligt i ett senare skede)
- Om du vill använda **offer decisioning** för denna dataström måste du markera rutan för Offer decisioning. (Detta kommer att vara en del av [Modul 9](./../module9/offer-decisioning.md))
- Om du vill använda **Kantsegmentering** måste du markera kryssrutan för Kantsegmentering.
- Om du vill använda **Destinationer för personalisering** måste du markera kryssrutan för personaliseringsmål.

För närvarande behövs ingen annan konfiguration för din datastream.

Nästa steg: [1.3 Introduktion till Adobe Experience Platform Data Collection](./ex3.md)

[Gå tillbaka till modul 1](./data-ingestion-launch-web-sdk.md)

[Gå tillbaka till Alla moduler](./../../overview.md)
