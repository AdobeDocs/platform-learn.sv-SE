---
title: Intelligenta tjänster - kundens AI skapar en ny instans (Konfigurera)
description: Kund-AI - Skapa en ny instans (Konfigurera)
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: d9377c97-efed-427a-a063-aa9c6bd1a78a
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 1%

---

# 5.2 Customer AI - Create a New Instance (Konfigurera)

Kunds-AI fungerar genom att analysera befintliga data om kundupplevelsehändelser för att förutsäga bortfall eller konverteringsbenägenhetspoäng. Genom att skapa en ny instans av kundens AI kan marknadsförarna definiera mål och åtgärder.

## 5.2.1 Konfigurera en ny AI-instans för kunder

I Adobe Experience Platform klickar du på **Tjänster** i den vänstra menyn. The **Tjänster** webbläsaren visas och alla tillgängliga tjänster visas. Klicka på Kortet för Kundens AI **Öppna**.

![Tjänstnavigering](./images/navigatetoservice.png)

Klicka **Skapa instans**.

![Skapa ny instans](./images/createnewinstance.png)

Du kommer då att se det här.

![Skapa ny instans](./images/custai1.png)

Ange nödvändig information för kundens AI-instans:

- Namn: use `--demoProfileLdap-- Product Purchase Propensity`
- Beskrivning: använd: **Förutspå sannolikheten för att kunder köper en produkt**
- Typ av benägenhet: välj **Konvertering**

![Installationssida 1](./images/setuppage1.png)

Klicka på **Nästa**.

![Installationssida 1](./images/next.png)

Du kommer då att se det här. Välj den datauppsättning som du skapade i föregående övning med namnet `--demoProfileLdap - Demo System - Customer Experience Event Dataset`. Klicka på **Nästa**.

![Installationssida 1](./images/custai2.png)

Välj **Kommer att inträffa** och definiera fältet **commerce.purchase.value** som målvariabel.

![Definiera CAI-mål](./images/caidefinegoal.png)

Klicka på **Nästa**.

![Installationssida 1](./images/next.png)

Ange sedan att schemat ska köras **Vecka** och ange tiden så nära den aktuella tiden som möjligt. Kontrollera att växlingsknappen **Aktivera bakgrundsmusik för profil** är aktiverat.

![Definiera CAI-förskott](./images/caiadvancepage.png)

Klicka **Slutför**.

![Installationssida 1](./images/finish.png)

Du kommer då att se den här popup-rutan. Klicka **OK**.

![Installationssida 1](./images/finish1.png)

När du har konfigurerat instansen kan du se den i kundens AI-instanslista och även förhandsgranska sammanfattningen av konfigurations- och körningsinformationen genom att klicka på kundens AI-instansrad. I sammanfattningspanelen visas även felinformation om fel hittas.

![Sammanfattning av instansinställningar](./images/caiinstancesummary.png)

>[!NOTE]
>
>Du kan ändra alla definitioner och attribut så länge som kundens AI-instans status är antingen **Väntar på utbildning** eller **Fel**

Nästa steg: [5.3 Customer AI - Scoring Dashboard and Segmentation (Predict &amp; Take Action)](./ex3.md)

[Gå tillbaka till modul 5](./intelligent-services.md)

[Gå tillbaka till Alla moduler](./../../overview.md)
