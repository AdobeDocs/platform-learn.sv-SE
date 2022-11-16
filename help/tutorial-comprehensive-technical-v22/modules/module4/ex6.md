---
title: Frågetjänst - Utforska datauppsättningen med Tablet
description: Frågetjänst - Utforska datauppsättningen med Tablet
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst, BI Expert
doc-type: tutorial
activity: develop
exl-id: 04209eb4-b054-4a2e-885e-61f601c3fc2c
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# 4.6 Query Service och Tableau

Öppna Tableu.

![start-tableau.png](./images/start-tableau.png)

I **Ansluta till en server** välj **PostgreSQL**:

![tableau-connect-postprogress.png](./images/tableau-connect-postgress.png)

Gå till Adobe Experience Platform **Frågor** och till **Autentiseringsuppgifter**.

![query-service-credentials.png](./images/query-service-credentials.png)

Från **Autentiseringsuppgifter** i Adobe Experience Platform, kopiera **Värd** och klistra in den i **Server** fält, kopiera **Databas** och klistra in den i **Databas** i Tableau kopierar du **Port** och klistra in den i fältet **Port** i Tableu gör samma sak för **Användarnamn** och **Lösenord**. Klicka på **Logga in**.

Logga in:

![tableau-connection-dialog.png](./images/tableau-connection-dialog.png)

Klicka på Sök (1) och ange **ldap** Identifiera tabellen i sökfältet från resultatuppsättningen och dra (3) den till den namngivna platsen **Dra tabeller hit**. När du är klar klickar du på **Blad 1** (3).

![tableau-drag-table.png](./images/tableau-drag-table.png)

För att visualisera data på kartan måste vi konvertera longitud och latitud till dimensioner. I **Åtgärder** välj **Latitud** (1) och öppna fältets listruta och välj **Konvertera till Dimension** (2). Gör på samma sätt för **Longitud** mått.

![tableau-convert-dimension.png](./images/tableau-convert-dimension.png)

Dra **Longitud** mäta till **Kolumner** och **Latitud** mät till **Rader**. Automatiskt kartan över **Belgien** visas med få punkter som representerar de städer som finns i datauppsättningen.

![tableau-drag-lon-lat.png](./images/tableau-drag-lon-lat.png)

Välj **Måttnamn** (1) öppnar du listrutan och väljer **Lägg till i blad** (2):

![tableau-select-measure-names.png](./images/tableau-select-measure-names.png)

Nu finns det en karta med punkter av olika storlek. Storleken anger antalet kundtjänstinteraktioner för den specifika staden. Navigera till den högra panelen och öppna om du vill ändra storlek på punkterna **Mätvärden** (med listruteikonen). Välj **Redigera storlekar**. Lek med olika storlekar.

![tableau-variable-size-dots.png](./images/tableau-vary-size-dots.png)

Visa data per **Ämne för samtal**, dra (1) **Ämne för samtal** dimension till **Sidor**. Navigera genom de olika **Utlysning** med **Ämne för samtal** (2) till höger på skärmen:

![tableau-call-topic-navigation.png](./images/tableau-call-topic-navigation.png)

Du har nu avslutat den här övningen.

Nästa steg: [4.7 Query Service API](./ex7.md)

[Gå tillbaka till modul 4](./query-service.md)

[Gå tillbaka till Alla moduler](../../overview.md)
