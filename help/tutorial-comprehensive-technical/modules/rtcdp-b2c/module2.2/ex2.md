---
title: Intelligenta tjänster - kundens AI skapar en ny instans (Konfigurera)
description: Kund-AI - Skapa en ny instans (Konfigurera)
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---

# 2.2.2 Kund-AI - Skapa en ny instans (Konfigurera)

Kunds-AI fungerar genom att analysera befintliga data om kundupplevelsehändelser för att förutsäga bortfall eller konverteringsbenägenhetspoäng. Genom att skapa en ny instans av kundens AI kan marknadsförarna definiera mål och åtgärder.

## 2.2.2.1 Konfigurera en ny AI-instans för kund

Klicka på **Tjänster** i den vänstra menyn i Adobe Experience Platform. Webbläsaren **Services** visas och visar alla tillgängliga tjänster. Klicka på **Öppna** på kortet för kundens AI.

![Tjänstnavigering](./images/navigatetoservice.png)

Klicka på **Skapa instans**.

![Skapa ny instans](./images/createnewinstance.png)

Då ser du det här.

![Skapa ny instans](./images/custai1.png)

Ange nödvändig information för kundens AI-instans:

- Namn: använd `--aepUserLdap-- Product Purchase Propensity`
- Beskrivning: använd: **Förutse sannolikheten för att kunder ska köpa en produkt**
- Proportionstyp: välj **Konvertering**

![Konfigurationssida 1](./images/setuppage1.png)

Klicka på **Nästa**.

![Konfigurationssida 1](./images/next.png)

Då ser du det här. Markera den datauppsättning som du skapade i föregående övning med namnet `--demoProfileLdap - Demo System - Customer Experience Event Dataset`. Klicka på **Nästa**.

![Konfigurationssida 1](./images/custai2.png)

Välj **Kommer att inträffa** och definiera fältet **commerce.purchase.value** som målvariabel.

![Definierar CAI-mål](./images/caidefinegoal.png)

Klicka på **Nästa**.

![Konfigurationssida 1](./images/next.png)

Ange sedan att schemat ska köra **Veckovis** och ange att tiden ska vara så nära den aktuella tiden som möjligt. Kontrollera att alternativet **Aktivera bakgrundsmusik för profilen** är aktiverat.

![Definiera CAI-förskott](./images/caiadvancepage.png)

Klicka på **Slutför**.

![Konfigurationssida 1](./images/finish.png)

Du kommer då att se den här popup-rutan. Klicka på **OK**.

![Konfigurationssida 1](./images/finish1.png)

När du har konfigurerat instansen kan du se den i kundens AI-instanslista och även förhandsgranska sammanfattningen av konfigurations- och körningsinformationen genom att klicka på kundens AI-instansrad. I sammanfattningspanelen visas även felinformation om fel hittas.

![Sammanfattning av instanskonfiguration](./images/caiinstancesummary.png)

>[!NOTE]
>
>Du kan ändra alla definitioner och attribut så länge som kundens AI-instansstatus är antingen **Väntar på utbildning** eller **Fel**

Nästa steg: [2.2.3 Kundens AI - Bedömningsinstrumentpanel och segmentering (predikt och åtgärd)](./ex3.md)

[Gå tillbaka till modul 2.2](./intelligent-services.md)

[Gå tillbaka till Alla moduler](./../../../overview.md)
