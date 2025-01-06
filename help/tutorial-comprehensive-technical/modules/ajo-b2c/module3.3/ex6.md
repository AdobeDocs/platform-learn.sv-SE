---
title: Offer decisioning - Testa ditt beslut med API:t
description: Testa ditt beslut med API:t
kt: 5342
doc-type: tutorial
exl-id: 75515a3e-5df8-42ed-95dc-daae60ee9c72
source-git-commit: fc24f3c9fb1683db35026dc53d0aaa055aa87e34
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 0%

---

# 3.3.6 Testa ditt beslut med API:t

## 3.3.6.1 Arbeta med Offer decisionings-API:t med Postman

Hämta [den här Postman-samlingen för Offer decisioning](./../../../assets/postman/postman_offer-decisioning.zip) till skrivbordet och zippa upp den. Då får du den här:

![OD API](./images/unzip.png)

Nu har du den här filen på skrivbordet:

- `_AJO- Decisioning Service.postman_collection.json`

In [Exercise 2.1.3 - Postman authentication to Adobe I/O](./../../../modules/rtcdp-b2c/module2.1/ex3.md) you installed Postman. Du måste använda Postman igen för den här övningen.

Öppna Postman och importera filen `_AJO- Decisioning Service.postman_collection.json`. Den här samlingen är sedan tillgänglig i Postman.

![Ny integrering för Adobe I/O](./images/postmanui.png)

Nu har du allt du behöver i Postman för att börja interagera med Adobe Experience Platform via API:erna.

Innan du kan använda nedanstående API:er måste du autentisera igen med samlingen **Adobe IO - OAuth** som du konfigurerade i Exercise 2.1.3.

![Ny integrering för Adobe I/O](./images/postmanui1.png)


### 3.3.6.2 Erbjudanden för kundprofil

Klicka för att öppna begäran **POST - Få erbjudanden för kundprofil**. Det första som ska uppdateras är variabeln **Header** för **x-sandbox-name**. Du bör ange det till `--aepSandboxName--`.

![OD API](./images/api23.png)

Det finns ett antal fält som måste uppdateras för den här begäran. Gå till **Body**.

- **xdm:placementId**
- **xdm:activityId**
- **xdm:id**
- **xdm:itemCount** (ändra det till ett valfritt värde)

![OD API](./images/api24.png)

Fältet **xdm:activityId** måste fyllas i. Du kan hämta det i användargränssnittet för Adobe Experience Platform enligt nedan.

![OD API](./images/activityid.png)

Fältet **[!UICONTROL xdm:placementId]** måste fyllas i. Du kan hämta det i användargränssnittet för Adobe Experience Platform enligt nedan. I exemplet nedan kan du se placementId för placeringen **[!UICONTROL Web - Image]**.

![OD API](./images/placementid.png)

För fältet **xdm:id** anger du e-postadressen till kundprofilen som du vill begära ett erbjudande för. Klicka på **[!UICONTROL Send]** när alla värden har angetts.

![OD API](./images/api24a.png)

Slutligen kommer ni att se resultatet av vilken typ av personaliserat erbjudande och vilka resurser som behöver visas för den här kunden. I det här exemplet begärdes två objekt och som du ser har två anpassade erbjudanden returnerats. 1 erbjudande för Apple Watch och ett annat erbjudande för Galaxy Watch 7.

![OD API](./images/api25.png)

Du har nu avslutat den här övningen.

Nästa steg: [Sammanfattning och förmåner](./summary.md)

[Gå tillbaka till modul 3.3](./offer-decisioning.md)

[Gå tillbaka till Alla moduler](./../../../overview.md)
