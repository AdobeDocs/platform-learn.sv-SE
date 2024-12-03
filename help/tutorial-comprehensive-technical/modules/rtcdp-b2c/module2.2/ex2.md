---
title: Intelligenta tjänster - kundens AI skapar en ny instans (Konfigurera)
description: Kund-AI - Skapa en ny instans (Konfigurera)
kt: 5342
doc-type: tutorial
exl-id: 067f3fa2-5c1e-4861-b26a-4315cad73a85
source-git-commit: b53ee64ae8438b8f48f842ed1f44ee7ef3e813fc
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---

# 2.2.2 Kund-AI - Skapa en ny instans (Konfigurera)

Kunds-AI fungerar genom att analysera befintliga data om kundupplevelsehändelser för att förutsäga bortfall eller konverteringsbenägenhetspoäng. Genom att skapa en ny instans av kundens AI kan marknadsförarna definiera mål och åtgärder.

## Konfigurera en ny AI-instans för kund

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

Klicka på **Spara och fortsätt**.

![Konfigurationssida 1](./images/setuppage1.png)

Då ser du det här. Markera den datauppsättning som du skapade i föregående övning med namnet `--demoProfileLdap - Demo System - Customer Experience Event Dataset`. Klicka på **Lägg till**.

![Konfigurationssida 1](./images/custai2.png)

Då ser du det här. du måste definiera fältet **Identitet**. Klicka på **Inget**.

![Konfigurationssida 1](./images/custai2a.png)

På popup-menyn väljer du **Identitetskarta (identityMap)** och sedan namnområdet **Demo System - CRMID (crmId)**. Klicka sedan på **Spara**.

![Konfigurationssida 1](./images/custai2b.png)

Klicka på **Spara och fortsätt**.

![Konfigurationssida 1](./images/custai2c.png)

Välj **Kommer att inträffa** i din specifika datauppsättning och definiera fältet **commerce.purchase.value** som målvariabel.

![Definierar CAI-mål](./images/caidefinegoal.png)

Ange sedan att schemat ska köra **Veckovis** och ange att tiden ska vara så nära den aktuella tiden som möjligt. Kontrollera att alternativet **Aktivera bakgrundsmusik för profilen** är aktiverat. Klicka på **Spara och fortsätt**.

![Definiera CAI-förskott](./images/caiadvancepage.png)

När du har konfigurerat instansen kan du se den i kundens AI-tjänstlista och du kan även förhandsgranska sammanfattningen av konfigurations- och körningsinformationen genom att klicka på kundens AI-instansrad. I sammanfattningspanelen visas även felinformation om fel hittas.

![Sammanfattning av instanskonfiguration](./images/caiinstancesummary.png)

>[!NOTE]
>
>Du kan ändra alla definitioner och attribut så länge som kundens AI-instansstatus är antingen **Väntar på utbildning** eller **Fel**

När modellen är klar ser du det här.

![Sammanfattning av instanskonfiguration](./images/caiinstancesummary1.png)


Nästa steg: [2.2.3 Kundens AI - Bedömningsinstrumentpanel och segmentering (predikt och åtgärd)](./ex3.md)

[Gå tillbaka till modul 2.2](./intelligent-services.md)

[Gå tillbaka till Alla moduler](./../../../overview.md)
