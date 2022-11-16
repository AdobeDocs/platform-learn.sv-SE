---
title: offer decisioning - Testa ditt beslut med API:t
description: Testa ditt beslut med API:t
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 0091c31f-0b54-4d40-a82b-3bf688db8a1f
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 0%

---

# 9.6 Testa ditt beslut med API:t

## 9.6.1 Arbeta med Offer decisionings-API:t med Postman

Hämta [denna Postman Collection för Offer decisioning](./../../assets/postman/postman_offer-decisioning.zip) till datorn och packa upp den. Då får du den här:

![OD API](./images/unzip.png)

Nu har du den här filen på skrivbordet:

- [!UICONTROL _Modul 14 - Beslutstjänst.postman_collection.json]

I [Exercise 3.3.3 - Postman-autentisering till Adobe I/O](./../../modules/module3/ex3.md) du installerade Postman. Du måste använda Postman igen för den här övningen.

Öppna Postman. Klicka **[!UICONTROL Importera]**.

![Adobe I/O New Integration](./images/postmanui.png)

Klicka på **[!UICONTROL Överför filer]**.

![Adobe I/O New Integration](./images/pm1.png)

Markera filen **[!UICONTROL _Modul 14 - Beslutstjänst.postman_collection.json]** och klicka **[!UICONTROL Öppna]**.

![Adobe I/O New Integration](./images/pm2.png)

Den här samlingen är sedan tillgänglig i Postman.

![Adobe I/O New Integration](./images/pm3.png)

Nu har du allt du behöver i Postman för att börja interagera med Adobe Experience Platform via API:erna.

### 9.6.1.1 Listbehållare

Klicka för att öppna begäran **[!UICONTROL GET - listbehållare]**.

Under **[!UICONTROL Parametrar]** kommer du att se det här:

- egenskap: `_instance.parentName==aepenablementfy22`

I den parametern **[!UICONTROL aepenablementfy22]** är namnet på den sandlåda som används i Adobe Experience Platform. Sandlådan som du bör använda är `--aepSandboxId--`. Ersätta texten **[!UICONTROL aepenablementfy22]** av `--aepSandboxId--`.

När du har ersatt namnet på sandlådan klickar du på **[!UICONTROL Skicka]**.

![OD API](./images/api2.png)

Detta är svaret, som visar behållaren för erbjudandet för den sandlåda som du angav. Please copy the **[!UICONTROL container instanceId]** som anges nedan och skriva ned den i en textfil på datorn. Du måste använda den här **[!UICONTROL container instanceId]** till nästa övning!

![OD API](./images/api3.png)

### 9.6.1.2 Listplaceringar

Klicka för att öppna begäran **[!UICONTROL GET - listplaceringar]**. Klicka **[!UICONTROL Skicka]**.

![OD API](./images/api4.png)

Du ser nu alla tillgängliga placeringar i erbjudandebehållaren. De placeringar du ser har definierats i användargränssnittet i Adobe Experience Platform, som du kan se i [Utövning 9.1.3](./ex1.md).

![OD API](./images/api5.png)

### 9.6.1.3 Regler för beslut om förteckningen

Klicka för att öppna begäran **[!UICONTROL GET - regler för listbeslut]**. Klicka **[!UICONTROL Skicka]**.

![OD API](./images/api6.png)

I svaret visas beslutsreglerna som du definierade i användargränssnittet för Adobe Experience Platform, som du kan se i [Utövning 9.1.4](./ex1.md).

![OD API](./images/api7.png)

### 9.6.1.4 Förteckning över personaliserade erbjudanden

Klicka för att öppna begäran **[!UICONTROL GET - lista personaliserade erbjudanden]**. Klicka **[!UICONTROL Skicka]**.

![OD API](./images/api8.png)

Svaret visar de personaliserade erbjudanden som du har definierat i Adobe Experience Platform användargränssnitt i [Utövning 9.2.1](./ex2.md).

![OD API](./images/api9.png)

### 9.6.1.5 Lista över återkopplingserbjudanden

Klicka för att öppna begäran **[!UICONTROL GET - Visa lista över reservalternativ]**. Klicka **[!UICONTROL Skicka]**.

![OD API](./images/api10.png)

I svaret visas det reserverbjudande som du definierade i användargränssnittet för Adobe Experience Platform i [Utövning 9.2.2](./ex2.md).

![OD API](./images/api11.png)

### 9.6.1.6 Listsamlingar

Klicka för att öppna begäran **[!UICONTROL GET - listsamlingar]**.

![OD API](./images/api12.png)

I svaret visas den samling som du definierade i användargränssnittet för Adobe Experience Platform i [Utövning 9.2.3](./ex2.md).

![OD API](./images/api13.png)

### 9.6.1.7 Få detaljerade erbjudanden om kundprofiler

Klicka för att öppna begäran **[!UICONTROL POST - Få detaljerade erbjudanden för kundprofil]**. Denna begäran liknar den föregående, men returnerar faktiskt information som bild-URL:er, text osv.

![OD API](./images/api23.png)

För denna begäran, som i föregående övning som har liknande krav, måste du ange värden för **[!UICONTROL xdm:placementId]** och **[!UICONTROL xdm:activityId]** för att hämta information om specifika erbjudanden för en kund.

Fältet **[!UICONTROL xdm:activityId]** måste fyllas i. Du kan hämta det i användargränssnittet för Adobe Experience Platform enligt nedan.

![OD API](./images/activityid.png)

Fältet **[!UICONTROL xdm:placementId]** måste fyllas i. Du kan hämta det i användargränssnittet för Adobe Experience Platform enligt nedan. I exemplet nedan kan du se placementId för placeringen **[!UICONTROL Webb - bild]**.

![OD API](./images/placementid.png)

Gå till **[!UICONTROL Brödtext]** och ange e-postadressen till den kund som du vill begära ett erbjudande för. Klicka **[!UICONTROL Skicka]**.

![OD API](./images/api24.png)

Slutligen kommer ni att se resultatet av vilket personaliserat erbjudande och vilka resurser som behöver visas för den här kunden.

![OD API](./images/api25.png)

Du har nu avslutat den här övningen.

Nästa steg: [Sammanfattning och fördelar](./summary.md)

[Gå tillbaka till modul 9](./offer-decisioning.md)

[Gå tillbaka till Alla moduler](./../../overview.md)
