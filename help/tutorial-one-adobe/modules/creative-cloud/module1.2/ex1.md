---
title: Komma igång med Firefly Services
description: Komma igång med Firefly Services
kt: 5342
doc-type: tutorial
source-git-commit: 1229a57730076c49adcbc168b5d73f92ad7581c9
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 0%

---

# 1.2.1 Komma igång med Workfront Fusion

I den här övningen ska du använda Workfront Fusion och Adobe I/O för att ställa frågor till API:er för Adobe Firefly Services.

## 1.2.1.1 Skapa nytt scenario

Gå till [https://experience.adobe.com/](https://experience.adobe.com/). Klicka för att öppna **Workfront Fusion**.

![WF Fusion](./images/wffusion1.png)

Du borde se det här då. Gå till **scenarier**.

![WF Fusion](./images/wffusion2.png)

Klicka på **Skapa nytt scenario**.

![WF Fusion](./images/wffusion3.png)

Då ser du ett tomt scenario. Klicka på ikonen **tools** och välj **Ange flera variabler**.

![WF Fusion](./images/wffusion4.png)

Nu måste du flytta ikonen **klocka** till den nyligen tillagda **Ange flera variabler**.

![WF Fusion](./images/wffusion5.png)

Då ser du det här.

![WF Fusion](./images/wffusion6.png)

Högerklicka sedan på frågetecknet och välj **Ta bort modul**.

![WF Fusion](./images/wffusion7.png)

Högerklicka sedan på objektet **Ange flera variabler** och välj **Inställningar**.

![WF Fusion](./images/wffusion8.png)

## 1.2.1.2 Konfigurera autentisering med Adobe I/O

Nu måste du konfigurera de variabler som behövs för att autentisera mot Adobe I/O. I föregående övning skapade du ett Adobe I/O-projekt. Variablerna i det Adobe I/O-projektet måste nu definieras i Workfront Fusion.

Följande variabler måste definieras:

| Nyckel | Värde |
|:-------------:| :---------------:| 
| `CONST_client_id` | ditt Adobe I/O-projekt klient-ID |
| `CONST_client_secret` | ditt Adobe I/O-projekt Client Secret |
| `CONST_scope` | ditt Adobe I/O-projektomfång |

Du hittar dessa variabler genom att gå till [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects) och öppna ditt Adobe I/O-projekt, som har namnet `--aepUserLdap-- Firefly`.

![WF Fusion](./images/wffusion9.png)

Klicka på **OAuth ServerTo-Server** i ditt projekt för att se värdena för tangenterna ovan.

![WF Fusion](./images/wffusion10.png)

Med tangenterna och värdena ovan kan du konfigurera **Set multiple variables** -objektet. Klicka på **Lägg till objekt**.

![WF Fusion](./images/wffusion11.png)

Ange **variabelnamnet**: **CONST_client_id** och dess **variabelvärde**, klicka på **Lägg till**.

![WF Fusion](./images/wffusion12.png)

Klicka på **Lägg till objekt**.

![WF Fusion](./images/wffusion13.png)

Ange **variabelnamnet**: **CONST_client_secrets** och dess **variabelvärde**, klicka på **Lägg till**.

![WF Fusion](./images/wffusion14.png)

Klicka på **Lägg till objekt**.

![WF Fusion](./images/wffusion15.png)

Ange **variabelnamnet**: **CONST_scope** och dess **variabelvärde**, klicka på **Lägg till**.

![WF Fusion](./images/wffusion16.png)

Klicka på **OK**.

![WF Fusion](./images/wffusion17.png)

Håll pekaren över **Ange flera variabler** och klicka på den stora **+** -ikonen för att lägga till en annan modul.

![WF Fusion](./images/wffusion18.png)

Du borde se det här då.

![WF Fusion](./images/wffusion19.png)

Ange **http** i sökfältet. Välj **HTTP** för att öppna den.

![WF Fusion](./images/wffusion21.png)

och välj sedan **Gör en förfrågan**.

![WF Fusion](./images/wffusion20.png)

| Nyckel | Värde |
|:-------------:| :---------------:| 
| `URL` | `https://ims-na1.adobelogin.com/ims/token/v3` |
| `Method` | `POST` |
| `Body Type` | `x-www-form-urlencoded` |

Klicka på **Lägg till objekt**.

![WF Fusion](./images/wffusion22.png)

Lägg till objekt för vart och ett av värdena nedan:

| Nyckel | Värde |
|:-------------:| :---------------:| 
| `client_id` | din fördefinierade variabel för `CONST_client_id` |
| `client_secret` | din fördefinierade variabel för `CONST_client_secret` |
| `scope` | din fördefinierade variabel för `CONST_scope` |
| `grant_type` | `client_credentials` |

Konfiguration för `client_id`.

![WF Fusion](./images/wffusion23.png)

Konfiguration för `client_secret`.

![WF Fusion](./images/wffusion25.png)

Konfiguration för `scope`.

![WF Fusion](./images/wffusion26.png)

Konfiguration för `grant_type`.

![WF Fusion](./images/wffusion28.png)

Konfigurationsöversikt. Bläddra nedåt och markera kryssrutan för **Analysera svar**. Klicka på **OK**.

![WF Fusion](./images/wffusion27.png)

Du borde se det här då. Klicka på **Kör en gång**.

![WF Fusion](./images/wffusion29.png)

När scenariot har körts bör du se det här.

![WF Fusion](./images/wffusion30.png)

Klicka på ikonen **frågetecken** på objektet **Ange flera variabler** för att se vad som hände när objektet kördes.

![WF Fusion](./images/wffusion31.png)

Klicka på ikonen **frågetecken** på **HTTP - Gör en begäran** om du vill se vad som hände när objektet kördes. I **OUTPUT** ser du att **access_token** returneras av Adobe I/O.

![WF Fusion](./images/wffusion32.png)

Hovra över **HTTP - Gör en förfrågan** -objektet och klicka på ikonen **+** för att lägga till ytterligare en modul.

![WF Fusion](./images/wffusion33.png)

Sök efter `tools` i sökfältet. Välj **Verktyg**.

![WF Fusion](./images/wffusion34.png)

Välj **Ange flera variabler**.

![WF Fusion](./images/wffusion35.png)

Välj **Lägg till objekt**.

![WF Fusion](./images/wffusion36.png)

Ange **variabelnamnet** som `bearer_token`. Välj `access_token` som dynamiskt **variabelvärde**. Klicka på **Lägg till**.

![WF Fusion](./images/wffusion37.png)

Du borde ha den här då. Klicka på **OK**.

![WF Fusion](./images/wffusion38.png)

Klicka på *Kör en gång** igen.

![WF Fusion](./images/wffusion39.png)

När scenariot har körts klickar du på ikonen **frågetecken** på det sista **Ange flera variabler** -objektet. Du bör sedan se att access_token lagras i variabeln `bearer_token`.

![WF Fusion](./images/wffusion40.png)

Högerklicka sedan på det första objektet **Ange flera värden** och välj **Byt namn**.

![WF Fusion](./images/wffusion41.png)

Ange namnet **Initiera konstanter**. Klicka på **OK**.

![WF Fusion](./images/wffusion42.png)

Byt namn på det andra objektet och ange namnet till **Autentisera till Adobe I/O**. Klicka på **OK**.

![WF Fusion](./images/wffusion43.png)

Byt namn på det tredje objektet och ställ in namnet på **Ange Bearer-token**. Klicka på **OK**.

![WF Fusion](./images/wffusion44.png)

Du borde ha den här då.

![WF Fusion](./images/wffusion45.png)

Ändra sedan namnet på ditt scenario till `--aepUSerLdap-- - Adobe I/O Authentication`.

![WF Fusion](./images/wffusion46.png)

Klicka på **Spara**.

![WF Fusion](./images/wffusion47.png)

Nästa steg: [1.2.2 Använd Firefly-text till bild med Workfront Fusion](./ex2.md)

[Gå tillbaka till modul 1.2](./automation.md)

[Gå tillbaka till Alla moduler](./../../../overview.md)
