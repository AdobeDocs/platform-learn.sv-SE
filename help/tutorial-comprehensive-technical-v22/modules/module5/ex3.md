---
title: Kundens AI - Instrumentpanel för bedömning och segmentering (predikt & Take Action)
description: Kundens AI - Instrumentpanel för bedömning och segmentering (predikt & Take Action)
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 57d6c714-5d41-4ac1-8e60-3000da45b76e
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 1%

---

# 5.3 Customer AI - Scoring Dashboard and Segmentation (Predict &amp; Take Action)

När kundens AI-instans har slutfört en modellkörning kan ni visualisera den benägenhetspoäng som utvärderas för att förutsäga att kunden genomför ett köp inom 30 dagar.

![AI](./images/caimodels.png)

>[!NOTE]
>
>Endast en kund-AI-instans med statusen **Lyckades** kan du förhandsgranska tjänstens insikter.

## 5.3.1 Förutsägbarhet

Nu ska vi granska den förväntade benägenheten som genereras av kundens AI-instansmodell. Klicka på instansnamnet för att visa kontrollpanelen.

![AI](./images/caimodels1.png)

Kundens AI-instrumentpanel visar sammanfattningen om poäng, fördelning av populationen och de faktorer som påverkar modellen.

![AI-beskrivning](./images/caidescription.png)

![Sammanfattning av instrumentpanel](./images/caidashboard.png)

Håll muspekaren över de inflytelserika faktorerna för att se hur datafördelningen ytterligare fördelar sig.

![Påverkansfaktorer](./images/caiinfluencefactors.png)

## 5.3.2 Verksamhetsåtgärder

### 5.3.2.1 Segmentera kunder

Med kundens AI-panel kan du definiera segment med ett enda klick. Klicka på **Skapa segment** på porträttkorten.

![Skapa ett segment](./images/caiinfluencefactors1.png)

Du ser att en segmentdefinition skapas automatiskt.

![Segmentregel](./images/caicreatesegment.png)

Ge segmentet ett namn enligt den här namnkonventionen: `--demoProfileLdap-- - Customer AI High Propensity`. Klicka **Spara**.

![Segmentregel](./images/caicreatesegment1.png)

Du kan nu använda det här segmentet för målinriktning med till exempel CDP, Journey Orchestration och Adobe Target i realtid.

### 5.3.2.2 Profilöversikt

Eftersom kundens AI-benägenhetspoäng blir en del av kundprofilen i realtid kan du se enskilda kunders poäng.

I Adobe Experience Platform går du till **Profiler** i den vänstra menyn och väljer **Bläddra**.

Sök efter en profil med hjälp av någon av identifierarna, till exempel **E-POST hbirkenshawa@businessweek.com**, som är tillgängliga i JSON-filen som du importerade. Klicka på **Profil-ID** för att öppna profilen.

![Profil](./images/profile1.png)

Då ser du det här:

![Profil](./images/profile2.png)

Gå till **Attribut**, som innehåller utdata från kundens AI-modell.

![Profil](./images/profile3.png)

Bläddra nedåt för att se hur väl dina kunder uppnår AI-modellen.

![Profil](./images/profile4.png)

Nästa steg: [Sammanfattning och fördelar](./summary.md)

[Gå tillbaka till modul 5](./intelligent-services.md)

[Gå tillbaka till Alla moduler](./../../overview.md)
