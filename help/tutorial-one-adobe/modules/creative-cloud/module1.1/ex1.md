---
title: Komma igång med Firefly Services
description: Lär dig hur du använder Postman och Adobe I/O för att fråga Adobe Firefly Services API:er
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 52385c33-f316-4fd9-905f-72d2d346f8f5
source-git-commit: 219945c74c620b9a4b93cb2b7462137118d42d33
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 0%

---

# 1.1.1 Komma igång med Firefly Services

Lär dig hur du använder Postman och Adobe I/O för att fråga Adobe Firefly Services API:er.

## 1.1.1.1 Konfigurera ditt Adobe I/O-projekt

I den här övningen används Adobe I/O för att fråga mot Firefly Services API:er. Följ de här stegen för att konfigurera Adobe I/O.

1. Gå till [https://developer.adobe.com/console/home](https://developer.adobe.com/console/home){target="_blank"}.

![Adobe I/O Ny integrering](./images/iohome.png){zoomable="yes"}

1. Se till att du väljer rätt instans i skärmens övre högra hörn. Din instans är `--aepImsOrgName--`. Välj sedan **Skapa nytt projekt**.

![Adobe I/O Ny integrering](./images/iocomp.png){zoomable="yes"}

1. Välj **+ Lägg till i projekt** och välj **API**.

![Adobe I/O Ny integrering](./images/adobe_io_access_api.png){zoomable="yes"}

Skärmen bör se ut så här.

![Adobe I/O Ny integrering](./images/api1.png){zoomable="yes"}

1. Välj **Creative Cloud** och välj **Firefly - Firefly Services**. Välj sedan **Nästa**.

![Adobe I/O Ny integrering](./images/api3.png){zoomable="yes"}

1. Ange ett namn för dina autentiseringsuppgifter: `--aepUserLdap-- - Firefly Services OAuth credential`och välj **Nästa**.

![Adobe I/O Ny integrering](./images/api4.png){zoomable="yes"}

1. Välj standardprofilen **Standardkonfiguration för Firefly Services** och välj **Spara konfigurerat API**.

![Adobe I/O Ny integrering](./images/api9.png){zoomable="yes"}

Nu är Adobe I/O-integreringen klar.

![Adobe I/O Ny integrering](./images/api11.png){zoomable="yes"}

## 1.1.1.2 Ladda ned Postman-miljön

1. Välj **Hämta för Postman** och välj sedan **OAuth Server-till-Server** för att hämta en Postman-miljö.

![Adobe I/O Ny integrering](./images/iopm.png){zoomable="yes"}

1. Välj projektnamn.

![Adobe I/O Ny integrering](./images/api13.png){zoomable="yes"}

1. Välj **Redigera projekt**.

![Adobe I/O Ny integrering](./images/api14.png){zoomable="yes"}

1. Ange ett eget namn för integreringen: `--aepUserLdap-- Firefly`och välj **Spara**.

![Adobe I/O Ny integrering](./images/api15.png){zoomable="yes"}

Installationen av Adobe I/O-integreringen är nu klar.

![Adobe I/O Ny integrering](./images/api16.png){zoomable="yes"}

## 1.1.1.3 Postman-autentisering till Adobe I/O

1. Hämta och installera den aktuella versionen av Postman för ditt operativsystem på [Postman Downloads](https://www.postman.com/downloads/){target="_blank"}.

![Adobe I/O Ny integrering](./images/getstarted.png){zoomable="yes"}

1. Starta programmet.

I Postman finns det två koncept: Miljö och Samlingar.

- Miljöfilen innehåller alla dina miljövariabler som är mer eller mindre konsekventa. I miljön hittar du saker som IMSOrg i din Adobe-miljö, tillsammans med säkerhetsreferenser som ditt klient-ID och andra. Du hämtade miljöfilen under Adobe I/O-installationen tidigare och den har namnet **`oauth_server_to_server.postman_environment.json`**.

- Samlingen innehåller ett antal API-begäranden som du kan använda. Vi kommer att använda 2 samlingar
   - 1 Collection for Authentication to Adobe I/O
   - 1 Samling för övningar i denna modul

1. Hämta [postman-ff.zip](./../../../assets/postman/postman-ff.zip) till ditt lokala skrivbord.

![Adobe I/O Ny integrering](./images/pmfolder.png){zoomable="yes"}

I filen **postman.zip** finns följande filer:

    -`Adobe IO - OAuth.postman_collection.json`
    -`FF - Firefly Services Tech Insiders.postman_collection.json`

1. Zippa upp **postman-ff.zip** och lagra följande två filer i en mapp på skrivbordet:
- Adobe IO - OAuth.postman_collection.json
- FF - Firefly Services Tech Insiders.postman_collection.json
- oauth_server_to_server.postman_environment.json

![Adobe I/O Ny integrering](./images/pmfolder1.png){zoomable="yes"}

1. I Postman väljer du **Importera**.

![Adobe I/O Ny integrering](./images/postmanui.png){zoomable="yes"}

1. Välj **Filer**.

![Adobe I/O Ny integrering](./images/choosefiles.png){zoomable="yes"}

1. Välj de tre filerna i mappen och välj sedan **Öppna** och **Importera**.

![Adobe I/O Ny integrering](./images/selectfiles.png){zoomable="yes"}

![Adobe I/O Ny integrering](./images/impconfirm.png){zoomable="yes"}

Nu har du allt du behöver i Postman för att börja interagera med Firefly Services via API:erna.

## 1.1.1.4 Begär en åtkomsttoken

För att vara säker på att du är autentiserad måste du begära en åtkomsttoken.

1. Kontrollera att du har valt rätt miljö innan du kör en begäran genom att verifiera miljölistrutan i det övre högra hörnet. Den valda miljön bör ha ett namn som liknar det här, `--aepUserLdap-- Firefly Services OAuth Credential`.

![Postman](./images/envselemea1.png){zoomable="yes"}

Den valda miljön bör ha ett namn som liknar det här, `--aepUserLdap-- Firefly Services OAuth Credential`.

![Postman](./images/envselemea.png){zoomable="yes"}

Nu när din Postman-miljö och dina samlingar är konfigurerade och fungerar kan du autentisera från Postman till Adobe I/O.

1. I samlingen **Adobe IO - OAuth** markerar du begäran **POST - Get Access Token** och väljer **Skicka**.

Obs! Under **Frågeparametrar** refereras två variabler, `API_KEY` och `CLIENT_SECRET`. Dessa variabler hämtas från den valda miljön, `--aepUserLdap-- Firefly Services OAuth Credential`.

![Postman](./images/ioauth.png){zoomable="yes"}

Om det lyckas visas ett svar som innehåller en innehavartoken, en åtkomsttoken och ett giltighetsfönster i avsnittet **Brödtext** i Postman.

![Postman](./images/ioauthresp.png){zoomable="yes"}


Du bör se ett liknande svar som innehåller följande information:

| Nyckel | Värde |
|:-------------:| :---------------:| 
| token_type | **bärare** |
| access_token | **eyJhbGciOiJSU...** |
| förfaller_in | **86399** |

Adobe I/O **Bearer-token** har ett specifikt värde (den mycket långa access_token) och ett giltighetsfönster och är nu giltigt i 24 timmar. Det innebär att om du efter 24 timmar vill använda Postman för att autentisera till Adobe I/O måste du generera en ny token genom att köra denna begäran igen.

## 1.1.1.5 API för Firefly Services, bild 2

Nu kan du skicka din första förfrågan till Firefly Services API:er.

1. Välj begäran **POST - Firefly - T2I V3** i samlingen **FF - Firefly Services Tech Insiders** .

![Firefly](./images/ff1.png){zoomable="yes"}

1. Kopiera bild-URL:en från svaret och öppna den i webbläsaren för att visa bilden.

![Firefly](./images/ff2.png){zoomable="yes"}

Du bör se en vacker bild som visar `horses in a field`.

![Firefly](./images/ff3.png){zoomable="yes"}

Du kan spela runt med API-begäran innan du fortsätter med nästa övning.

## Nästa steg

Gå till [Optimera din Firefly-process med Microsoft Azure och försignerade URL:er](./ex2.md){target="_blank"}

Gå tillbaka till [Översikt över Adobe Firefly Services](./firefly-services.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../overview.md){target="_blank"}
