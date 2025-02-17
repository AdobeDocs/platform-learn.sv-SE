---
title: Frågetjänst - Utforska datauppsättningen med Tablet
description: Frågetjänst - Utforska datauppsättningen med Tablet
kt: 5342
doc-type: tutorial
exl-id: 33ab854d-fad7-497c-affa-f58e4299c0b3
source-git-commit: 1e3a8d585503eddad4c642a3b13d2b5f7ddc9943
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# 2.1.7 Query Service och Tableau

Öppna Tableu.

![start-tableau.png](./images/starttableau.png)

I **Anslut till en server** klickar du på **Mer** och sedan på **PostgreSQL**.

![tableau-connect-postprogress.png](./images/tableauconnectpostgress.png)

Om du inte har använt PostgeSQL med Tableau än kan du se det här. Klicka på **Hämta drivrutin**.

![tableau-connect-postprogress.png](./images/tableauconnectpostgress1.png)

Följ instruktionerna för att hämta och installera PostgreSQL-drivrutinen.

![tableau-connect-postprogress.png](./images/tableauconnectpostgress2.png)

När du är klar med installationen av drivrutinen avslutar du och startar om Tableau Desktop. Efter omstarten går du till **Anslut till en server** igen, klickar på **Mer** och sedan på **PostgreSQL** igen.

![tableau-connect-postprogress.png](./images/tableauconnectpostgress.png)

Då ser du det här.

![tableau-connect-postprogress.png](./images/tableauconnectpostgress3.png)

Gå till Adobe Experience Platform, till **Frågor** och till **Referenser**.

![query-service-credentials.png](./images/queryservicecredentials.png)

Kopiera **Host** från sidan **Credentials** i Adobe Experience Platform och klistra in den i fältet **Server**, kopiera **Database** och klistra in den i fältet **Database** i Tablet, kopiera **Port** och klistra in den i fältet **Port** i Tablet u gör du samma för **Användarnamn** och **Lösenord**. Klicka sedan på **Logga in**.

![tableau-connection-dialog.png](./images/tableauconnectiondialog.png)

I listan med tillgängliga tabeller letar du reda på tabellen som du skapade i föregående övning, som kallas `--aepUserLdap--_callcenter_interaction_analysis`. Dra den till arbetsytan.

![tableau-drag-table.png](./images/tableaudragtable.png)

Då ser du det här. Klicka på **Uppdatera nu**.

![tableau-drag-table.png](./images/tableaudragtable1.png)

Du kommer då att se data från AEP bli tillgängliga i Tableau. Klicka på **Blad 1** för att börja arbeta med data.

![tableau-drag-table.png](./images/tableaudragtable2.png)

Om du vill visualisera data på kartan måste du konvertera longitud och latitud till dimensioner. I **Mått** högerklickar du på **Latitude** och väljer **Konvertera till Dimension** på menyn. Gör på samma sätt för måttet **Longitude**.

![table-convert-dimension.png](./images/tableauconvertdimension.png)

Dra måttet **Longitude** till **Columns** och måttet **Latitude** till **Rows**. Kartan för **Belgien** visas automatiskt med få punkter som representerar städerna i datauppsättningen.

![tableau-drag-lon-lat.png](./images/tableaudraglonlat.png)

Välj **Måttnamn** och klicka på **Lägg till i blad**.

![tableau-select-measure-names.png](./images/selectmeasurenames.png)

Nu finns det en karta med punkter av olika storlek. Storleken anger antalet kundtjänstinteraktioner för den specifika staden. Om du vill ändra storleken på punkterna går du till den högra panelen och öppnar **Måttvärden** (med listruteikonen). Välj **Redigera storlekar** i listrutan. Lek med olika storlekar.

![tableau-variable-size-dots.png](./images/tableauvarysizedots.png)

Om du vill visa data per **Anropa ämne** ytterligare drar du dimensionen **Anropa ämne** till **Sidor**. Navigera genom de olika **samtalsämnena** med hjälp av **anropsämnet** till höger på skärmen:

![tableau-call-topic-navigation.png](./images/tableaucalltopicnavigation.png)

Du har nu avslutat den här övningen.

## Nästa steg

Gå till [2.1.8 Query Service API](./ex8.md){target="_blank"}

Gå tillbaka till [frågetjänsten](./query-service.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../../overview.md){target="_blank"}
