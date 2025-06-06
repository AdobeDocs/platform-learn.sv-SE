---
title: Komma igång med Workfront Fusion
description: Lär dig hur du använder Workfront Fusion och Adobe I/O för att hämta Adobe Firefly Services API:er
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 42e260e0-8af0-4d71-b634-48c1966bd912
source-git-commit: 4b38b40c47b5c373f74a85261adce46f291303a8
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 0%

---

# 1.2.1 Komma igång med Workfront Fusion

Lär dig hur du använder Workfront Fusion och Adobe I/O för att hämta Adobe Firefly Services API:er.

## 1.2.1.1 Skapa nytt scenario

Gå till [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Öppna **Workfront Fusion**.

![WF Fusion](./images/wffusion1.png)

Gå till **scenarier**.

![WF Fusion](./images/wffusion2.png)

Klicka på ikonen **+** för att skapa en ny mapp för ditt arbete.

![WF Fusion](./images/wffusion2a.png)

Namnge mappen `--aepUserLdap--` och välj **Spara**.

![WF Fusion](./images/wffusion2b.png)

Markera mappen och välj sedan **Skapa nytt scenario**.

![WF Fusion](./images/wffusion3.png)

Ett tomt scenario visas. Välj **verktyg** och välj **Ange flera variabler**.

![WF Fusion](./images/wffusion4.png)

Flytta ikonen **klocka** till **Ange flera variabler**.

![WF Fusion](./images/wffusion5.png)

Skärmen bör se ut så här.

![WF Fusion](./images/wffusion6.png)

Högerklicka på frågetecknet och välj **Ta bort modul**.

![WF Fusion](./images/wffusion7.png)

Högerklicka sedan på **Ange flera variabler** och välj **Inställningar**.

![WF Fusion](./images/wffusion8.png)

## 1.2.1.2 Konfigurera Adobe I/O-autentisering

Nu måste du konfigurera de variabler som behövs för att autentisera mot Adobe I/O. I föregående övning skapade du ett Adobe I/O-projekt. Variablerna i det Adobe I/O-projektet måste nu definieras i Workfront Fusion.

Följande variabler måste definieras:

| Nyckel | Värde |
|:-------------:| :---------------:| 
| `CONST_client_id` | ditt Adobe I/O-projekt klient-ID |
| `CONST_client_secret` | ditt Adobe I/O-projekt Client Secret |
| `CONST_scope` | ditt Adobe I/O-projekts omfång |

Du hittar dessa variabler genom att gå till [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects){target="_blank"} och öppna ditt Adobe I/O-projekt, som har namnet `--aepUserLdap-- One Adobe tutorial`.

![WF Fusion](./images/wffusion9.png)

I ditt projekt väljer du **OAuth Server-Server** för att se värdena för tangenterna ovan.

![WF Fusion](./images/wffusion10.png)

Med tangenterna och värdena ovan kan du konfigurera objektet **Set multiple variables** . Välj **Lägg till objekt**.

![WF Fusion](./images/wffusion11.png)

Ange **variabelnamnet**: **CONST_client_id** och dess **variabelvärde**, välj **Lägg till**.

![WF Fusion](./images/wffusion12.png)

Välj **Lägg till objekt**.

![WF Fusion](./images/wffusion13.png)

Ange **Variabelnamn**: **CONST_client_secrets** och dess **variabelvärde**, välj **Lägg till**.

![WF Fusion](./images/wffusion14.png)

Välj **Lägg till objekt**.

![WF Fusion](./images/wffusion15.png)

Ange **Variabelnamn**: **CONST_scope** och dess **Variabelvärde**, välj **Lägg till**.

![WF Fusion](./images/wffusion16.png)

Välj **OK**.

![WF Fusion](./images/wffusion17.png)

Håll pekaren över **Ange flera variabler** och välj den stora ikonen **+** om du vill lägga till ytterligare en modul.

![WF Fusion](./images/wffusion18.png)

Skärmen bör se ut så här.

![WF Fusion](./images/wffusion19.png)

Ange **http** i sökfältet. Välj **HTTP** för att öppna den.

![WF Fusion](./images/wffusion21.png)

Välj **Gör en förfrågan**.

![WF Fusion](./images/wffusion20.png)

| Nyckel | Värde |
|:-------------:| :---------------:| 
| `URL` | `https://ims-na1.adobelogin.com/ims/token/v3` |
| `Method` | `POST` |
| `Body Type` | `x-www-form-urlencoded` |

Välj **Lägg till objekt**.

![WF Fusion](./images/wffusion22.png)

Lägg till objekt för vart och ett av värdena nedan:

| Nyckel | Värde |
|:-------------:| :---------------:| 
| `client_id` | din fördefinierade variabel för `CONST_client_id` |
| `client_secret` | din fördefinierade variabel för `CONST_client_secret` |
| `scope` | din fördefinierade variabel för `CONST_scope` |
| `grant_type` | `client_credentials` |

Konfiguration för `client_id`:

![WF Fusion](./images/wffusion23.png)

Konfiguration för `client_secret`.

![WF Fusion](./images/wffusion25.png)

Konfiguration för `scope`.

![WF Fusion](./images/wffusion26.png)

Konfiguration för `grant_type`.

![WF Fusion](./images/wffusion28.png)

Rulla ned och markera rutan för **Analysera svar**. Välj **OK**.

![WF Fusion](./images/wffusion27.png)

Skärmen bör se ut så här. Välj **Kör en gång**.

![WF Fusion](./images/wffusion29.png)

När scenariot har körts bör skärmen se ut så här:

![WF Fusion](./images/wffusion30.png)

Markera ikonen **frågetecken** på objektet **Ange flera variabler** för att se vad som hände när objektet kördes.

![WF Fusion](./images/wffusion31.png)

Välj ikonen **frågetecken** på **HTTP - Gör en begäran** om du vill se vad som hände när objektet kördes. I **OUTPUT** ser du **access_token** som returneras av Adobe I/O.

![WF Fusion](./images/wffusion32.png)

Hovra över **HTTP - Gör en förfrågan** och välj ikonen **+** för att lägga till en till modul.

![WF Fusion](./images/wffusion33.png)

Sök efter `tools` i sökfältet. Välj **Verktyg**.

![WF Fusion](./images/wffusion34.png)

Välj **Ange flera variabler**.

![WF Fusion](./images/wffusion35.png)

Välj **Lägg till objekt**.

![WF Fusion](./images/wffusion36.png)

Ange **Variabelnamn** till `bearer_token`. Välj `access_token` som dynamiskt **variabelvärde**. Välj **Lägg till**.

![WF Fusion](./images/wffusion37.png)

Skärmen bör se ut så här. Välj **OK**.

![WF Fusion](./images/wffusion38.png)

Välj **Kör en gång** igen.

![WF Fusion](./images/wffusion39.png)

När scenariot körs väljer du ikonen **frågetecken** på det sista **Ange flera variabler** -objektet. Du bör se att access_token lagras i variabeln `bearer_token`.

![WF Fusion](./images/wffusion40.png)

Högerklicka sedan på det första objektet **Ange flera värden** och välj **Byt namn**.

![WF Fusion](./images/wffusion41.png)

Ange namnet **Initiera konstanter**. Välj **OK**.

![WF Fusion](./images/wffusion42.png)

Byt namn på det andra objektet till **Autentisera till Adobe I/O**. Välj **OK**.

![WF Fusion](./images/wffusion43.png)

Byt namn på det tredje objektet till **Ange Bearer-token**. Välj **OK**.

![WF Fusion](./images/wffusion44.png)

Skärmen bör se ut så här:

![WF Fusion](./images/wffusion45.png)

Ändra sedan namnet på ditt scenario till `--aepUserLdap-- - Adobe I/O Authentication`.

![WF Fusion](./images/wffusion46.png)

Välj **Spara**.

![WF Fusion](./images/wffusion47.png)

## Nästa steg

Gå till [Använd Adobe API:er i Workfront Fusion](./ex2.md){target="_blank"}

Gå tillbaka till [Creative Workflow Automation med Workfront Fusion](./automation.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../overview.md){target="_blank"}
