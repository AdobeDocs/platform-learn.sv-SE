---
title: Frågetjänst - Utforska datauppsättningen med Tablet
description: Frågetjänst - Utforska datauppsättningen med Tablet
kt: 5342
doc-type: tutorial
exl-id: 29525740-fe1f-4770-bcc9-f2ad499a2cb5
source-git-commit: b53ee64ae8438b8f48f842ed1f44ee7ef3e813fc
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# 5.1.7 Query Service och Tableau

Öppna Tableu.

![start-tableau.png](./images/start-tableau.png)

I **Anslut till en server** väljer du **PostgreSQL**:

![tableau-connect-postprogress.png](./images/tableau-connect-postgress.png)

Gå till Adobe Experience Platform, till **Frågor** och till **Referenser**.

![query-service-credentials.png](./images/query-service-credentials.png)

Kopiera **Host** från sidan **Credentials** i Adobe Experience Platform och klistra in den i fältet **Server**, kopiera **Database** och klistra in den i fältet **Database** i Tablet, kopiera **Port** och klistra in den i fältet **Port** i Tablet u gör du samma för **Användarnamn** och **Lösenord**. Klicka sedan på **Logga in**.

Logga in:

![tableau-connection-dialog.png](./images/tableau-connection-dialog.png)

Klicka på sök (1) och ange din **ldap** i sökfältet, identifiera tabellen i resultatuppsättningen och dra (3) den till platsen **Dra tabeller hit**. När du är klar klickar du på **Blad 1** (3).

![tableau-drag-table.png](./images/tableau-drag-table.png)

För att visualisera data på kartan måste vi konvertera longitud och latitud till dimensioner. I **Mått** markerar du **Latitude** (1) och öppnar fältets listruta och väljer **Konvertera till Dimension** (2). Gör på samma sätt för måttet **Longitude**.

![table-convert-dimension.png](./images/tableau-convert-dimension.png)

Dra måttet **Longitude** till **Columns** och måttet **Latitude** till **Rows**. Kartan för **Belgien** visas automatiskt med få punkter som representerar städerna i datauppsättningen.

![tableau-drag-lon-lat.png](./images/tableau-drag-lon-lat.png)

Välj **Måttnamn** (1), öppna listrutan och välj **Lägg till i blad** (2):

![tableau-select-measure-names.png](./images/tableau-select-measure-names.png)

Nu finns det en karta med punkter av olika storlek. Storleken anger antalet kundtjänstinteraktioner för den specifika staden. Om du vill ändra storleken på punkterna går du till den högra panelen och öppnar **Måttvärden** (med listruteikonen). Välj **Redigera storlekar** i listrutan. Lek med olika storlekar.

![tableau-variable-size-dots.png](./images/tableau-vary-size-dots.png)

Om du vill visa data per **Anropa ämne** ytterligare drar du (1) dimensionen **Anropa ämne** till **Sidor**. Navigera genom de olika **samtalsämnena** med hjälp av **anropsämnet** (2) till höger på skärmen:

![tableau-call-topic-navigation.png](./images/tableau-call-topic-navigation.png)

Du har nu avslutat den här övningen.

Nästa steg: [5.1.8 API för frågetjänst](./ex8.md)

[Gå tillbaka till modul 5.1](./query-service.md)

[Gå tillbaka till Alla moduler](../../../overview.md)
