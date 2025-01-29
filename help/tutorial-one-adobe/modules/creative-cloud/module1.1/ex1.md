---
title: Komma igång med Firefly Services
description: Lär dig hur du använder Postman och Adobe I/O för att ställa frågor till API:er för Adobe Firefly Services
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 52385c33-f316-4fd9-905f-72d2d346f8f5
source-git-commit: 8e410ad378d61f23d1d880d12e57f9d5e4e523c1
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 0%

---

# Komma igång med Firefly Services

Lär dig hur du använder Postman och Adobe I/O för att hämta API:er för Adobe Firefly Services.

## Konfigurera ditt Adobe I/O-projekt

I den här övningen används Adobe I/O för att fråga mot API:er för Firefly Services. Följ de här stegen för att konfigurera Adobe I/O.

1. Gå till [https://developer.adobe.com/console/home](https://developer.adobe.com/console/home){target="_blank"}.

![Ny integrering för Adobe I/O](./images/iohome.png)

1. Se till att du väljer rätt instans i skärmens övre högra hörn. Din instans är `--aepImsOrgName--`. Välj sedan **Skapa nytt projekt**.

![Ny integrering för Adobe I/O](./images/iocomp.png)

1. Välj **+ Lägg till i projekt** och välj **API**.

![Ny integrering för Adobe I/O](./images/adobe_io_access_api.png)

Skärmen bör se ut så här.

![Ny integrering för Adobe I/O](./images/api1.png)

1. Markera **Creative Cloud** och välj **Firefly - Firefly-tjänster**. Välj sedan **Nästa**.

![Ny integrering för Adobe I/O](./images/api3.png)

1. Ange ett namn för dina autentiseringsuppgifter: `--aepUserLdap-- - Firefly Services OAuth credential`och välj **Nästa**.

![Ny integrering för Adobe I/O](./images/api4.png)

1. Markera standardprofilen **Standardkonfiguration för Firefly Services** och välj **Spara konfigurerat API**.

![Ny integrering för Adobe I/O](./images/api9.png)

Integreringen av Adobe I/O är nu klar.

![Ny integrering för Adobe I/O](./images/api11.png)

## Ladda ned Postman

1. Välj **Hämta för Postman** och välj sedan **OAuth Server-till-Server** för att hämta en Postman-miljö.

![Ny integrering för Adobe I/O](./images/iopm.png)

1. Välj projektnamn.

![Ny integrering för Adobe I/O](./images/api13.png)

1. Välj **Redigera projekt**.

![Ny integrering för Adobe I/O](./images/api14.png)

1. Ange ett eget namn för integreringen: `--aepUserLdap-- Firefly`och välj **Spara**.

![Ny integrering för Adobe I/O](./images/api15.png)

Konfigurationen av integreringen med Adobe I/O är nu klar.

![Ny integrering för Adobe I/O](./images/api16.png)

## Postman-autentisering till Adobe I/O

1. Hämta och installera den aktuella versionen av Postman för ditt operativsystem på [Postman Downloads](https://www.postman.com/downloads/){target="_blank"}.

![Ny integrering för Adobe I/O](./images/getstarted.png)

1. Starta programmet.

I Postman finns det två koncept: Miljö och Samlingar.

- Miljöfilen innehåller alla dina miljövariabler som är mer eller mindre konsekventa. I miljön hittar du saker som IMSOrg i Adobe-miljön, tillsammans med säkerhetsreferenser som ditt klient-ID och andra. Du hämtade miljöfilen under Adobe I/O-installationen tidigare och den har namnet **`oauth_server_to_server.postman_environment.json`**.

- Samlingen innehåller ett antal API-begäranden som du kan använda. Vi kommer att använda 2 samlingar
   - 1 samling för autentisering till Adobe I/O
   - 1 Samling för övningar i denna modul

1. Hämta [postman.zip](./../../../assets/postman/postman-ff.zip) till ditt lokala skrivbord.

![Ny integrering för Adobe I/O](./images/pmfolder.png)

I filen **postman.zip** finns följande filer:

    -`Adobe IO - OAuth.postman_collection.json`
    -`FF - Firefly Services Tech Insiders.postman_collection.json`

1. Zippa upp **postman-ff.zip** och lagra följande två filer i en mapp på skrivbordet:
- Adobe IO - OAuth.postman_collection.json
- FF - Firefly Services Tech Insiders.postman_collection.json
- oauth_server_to_server.postman_environment.json

![Ny integrering för Adobe I/O](./images/pmfolder1.png)

1. I Postman väljer du **Importera**.

![Ny integrering för Adobe I/O](./images/postmanui.png)

1. Välj **Filer**.

![Ny integrering för Adobe I/O](./images/choosefiles.png)

1. Välj de tre filerna i mappen och välj sedan **Öppna** och **Importera**.

![Ny integrering för Adobe I/O](./images/selectfiles.png)

![Ny integrering för Adobe I/O](./images/impconfirm.png)

Nu har du allt du behöver i Postman för att börja interagera med Firefly Services via API:erna.

## Begär en åtkomsttoken

För att vara säker på att du är autentiserad måste du begära en åtkomsttoken.

1. Kontrollera att du har valt rätt miljö innan du kör en begäran genom att verifiera miljölistrutan i det övre högra hörnet. Den valda miljön bör ha ett namn som liknar det här, `--aepUserLdap-- Firefly Services OAuth Credential`.

![Postman](./images/envselemea1.png)

Den valda miljön bör ha ett namn som liknar det här, `--aepUserLdap-- Firefly Services OAuth Credential`.

![Postman](./images/envselemea.png)

Nu när din Postman-miljö och dina samlingar är konfigurerade och fungerar kan du autentisera från Postman till Adobe I/O.

1. I samlingen **Adobe IO - OAuth** markerar du begäran med namnet **POST - Get Access Token** och väljer **Skicka**.

Obs! Under **Frågeparametrar** refereras två variabler, `API_KEY` och `CLIENT_SECRET`. Dessa variabler hämtas från den valda miljön, `--aepUserLdap-- Firefly Services OAuth Credential`.

![Postman](./images/ioauth.png)

Om det lyckas visas ett svar som innehåller en innehavartoken, en åtkomsttoken och ett giltighetsfönster i avsnittet **Brödtext** i Postman.

![Postman](./images/ioauthresp.png)


Du bör se ett liknande svar som innehåller följande information:

| Nyckel | Värde |
|:-------------:| :---------------:| 
| token_type | **bärare** |
| access_token | **eyJhbGciOiJSU...** |
| förfaller_in | **86399** |

Adobe I/O **Bearer-token** har ett specifikt värde (den mycket långa access_token) och ett giltighetsfönster och är nu giltigt i 24 timmar. Det innebär att om du efter 24 timmar vill använda Postman för att autentisera till Adobe I/O måste du generera en ny token genom att köra denna begäran igen.

## Firefly Services API, Text 2-bild

Nu kan du skicka din första begäran till Firefly Services API:er.

1. Markera begäran med namnet **POST - Firefly - T2I V3** i samlingen **FF - Firefly Services Tech Insiders** .

![Firefly](./images/ff1.png)

1. Kopiera bild-URL:en från svaret och öppna den i webbläsaren för att visa bilden.

![Firefly](./images/ff2.png)

Du bör se en vacker bild som visar `horses in a field`.

![Firefly](./images/ff3.png)

Du kan spela runt med API-begäran innan du fortsätter med nästa övning.

## Nästa steg

Gå till [Optimera din Firefly-process med Microsoft Azure och försignerade URL:er](./ex2.md){target="_blank"}

Gå tillbaka till [Översikt över Adobe Firefly Services](./firefly-services.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../overview.md){target="_blank"}
