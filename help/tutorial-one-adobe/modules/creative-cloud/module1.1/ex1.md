---
title: Komma igång med Firefly Services
description: Komma igång med Firefly Services
kt: 5342
doc-type: tutorial
exl-id: 52385c33-f316-4fd9-905f-72d2d346f8f5
source-git-commit: 608fc570f9aa172db3578664e793f35fb3f1bf50
workflow-type: tm+mt
source-wordcount: '929'
ht-degree: 0%

---

# 1.1.1 Komma igång med Firefly Services

I den här övningen använder du Postman och Adobe I/O för att fråga Adobe Firefly Services API:er.

## Konfigurera ditt Adobe I/O-projekt

I den här övningen kommer du att använda Adobe I/O intensivt för att fråga mot API:er för Firefly Services. Följ stegen nedan för att konfigurera Adobe I/O.

Gå till [https://developer.adobe.com/console/home](https://developer.adobe.com/console/home)

![Ny integrering för Adobe I/O](./images/iohome.png)

Se till att du väljer rätt instans i skärmens övre högra hörn. Din instans är `--aepImsOrgName--`. Klicka på **Skapa nytt projekt**.

![Ny integrering för Adobe I/O](./images/iocomp.png)

Välj **+ Lägg till i projekt** och välj **API**.

![Ny integrering för Adobe I/O](./images/adobe_io_access_api.png)

Då ser du det här:

![Ny integrering för Adobe I/O](./images/api1.png)

Markera **Creative Cloud** och klicka på **Firefly - Firefly-tjänster**. Klicka på **Nästa**.

![Ny integrering för Adobe I/O](./images/api3.png)

Du kommer att se det här. Ange ett namn för dina autentiseringsuppgifter: `--aepUserLdap-- - Firefly Services OAuth credential`. Klicka på **Nästa**.

![Ny integrering för Adobe I/O](./images/api4.png)

Därefter måste du välja en produktprofil som definierar vilka behörigheter som är tillgängliga för den här integreringen.

Markera profilen **Standardkonfiguration för Firefly Services**.

Klicka på **Spara konfigurerat API**.

![Ny integrering för Adobe I/O](./images/api9.png)

Integreringen av Adobe I/O är nu klar.

![Ny integrering för Adobe I/O](./images/api11.png)

Klicka på knappen **Hämta för Postman** och sedan på **OAuth Server-to-Server** för att hämta en Postman-miljö.

![Ny integrering för Adobe I/O](./images/iopm.png)

IO-projektet har för närvarande ett generiskt namn. Du måste ge integreringen ett eget namn. Klicka på **Projekt X** (eller liknande namn) som anges

![Ny integrering för Adobe I/O](./images/api13.png)

Klicka på **Redigera projekt**.

![Ny integrering för Adobe I/O](./images/api14.png)

Ange ett namn för din integrering: `--aepUserLdap-- Firefly`.

Klicka på **Spara**.

![Ny integrering för Adobe I/O](./images/api15.png)

Konfigurationen av integreringen med Adobe I/O är nu klar.

![Ny integrering för Adobe I/O](./images/api16.png)

## Postman-autentisering till Adobe I/O

Gå till [https://www.postman.com/downloads/](https://www.postman.com/downloads/).

Hämta och installera den aktuella versionen av Postman för ditt operativsystem.

![Ny integrering för Adobe I/O](./images/getstarted.png)

Starta programmet när du har installerat Postman.

I Postman finns det två koncept: Miljö och Samlingar.

- Miljöfilen innehåller alla dina miljövariabler som är mer eller mindre konsekventa. I miljön hittar du saker som IMSOrg i Adobe-miljön, tillsammans med säkerhetsreferenser som ditt klient-ID och andra. Miljöfilen är den som du hämtade under Adobe I/O-konfigurationen i den tidigare övningen och har följande namn: **`oauth_server_to_server.postman_environment.json`**.

- Samlingen innehåller ett antal API-begäranden som du kan använda. Vi kommer att använda 2 samlingar
   - 1 samling för autentisering till Adobe I/O
   - 1 Samling för övningar i denna modul

Hämta filen [postman.zip](./../../../assets/postman/postman-ff.zip) till ditt lokala skrivbord.

![Ny integrering för Adobe I/O](./images/pmfolder.png)

I den här **postman.zip**-filen hittar du följande filer:

- `Adobe IO - OAuth.postman_collection.json`
- `FF - Firefly Services Tech Insiders.postman_collection.json`

Zippa upp filen **postman-ff.zip** och lagra dessa två filer i en mapp på skrivbordet tillsammans med den hämtade Postman-miljön från Adobe I/O, som är filen `oauth_server_to_server.postman_environment.json`. Du måste ha dessa tre filer i den mappen:

![Ny integrering för Adobe I/O](./images/pmfolder1.png)

Gå tillbaka till Postman. Klicka på **Importera**.

![Ny integrering för Adobe I/O](./images/postmanui.png)

Klicka på **filer**.

![Ny integrering för Adobe I/O](./images/choosefiles.png)

Navigera till mappen på skrivbordet där du extraherade de två hämtade filerna. Markera de här tre filerna samtidigt och klicka på **Öppna**.

![Ny integrering för Adobe I/O](./images/selectfiles.png)

När du har klickat på **Öppna** visas en översikt i Postman över miljön och de samlingar du håller på att importera. Klicka på **Importera**.

![Ny integrering för Adobe I/O](./images/impconfirm.png)

Nu har du allt du behöver i Postman för att börja interagera med Firefly Services via API:erna.

Det första du behöver göra är att se till att du är rätt autentiserad. Du måste begära en åtkomsttoken för att kunna autentiseras.

Kontrollera att du har valt rätt miljö innan du kör någon begäran. Du kan kontrollera den valda miljön genom att verifiera listrutan Miljö i det övre högra hörnet.

Den valda miljön bör ha ett namn som liknar det här, `--aepUserLdap-- Firefly Services OAuth Credential`.

![Postman](./images/envselemea.png)

Din Postman-miljö och dina samlingar är nu konfigurerade och fungerar. Nu kan du autentisera från Postman till Adobe I/O.

I samlingen **Adobe IO - OAuth** markerar du begäran med namnet **POST - Get Access Token**. Du kommer att referera till två variabler under **Params**, `API_KEY` och `CLIENT_SECRET`. Dessa variabler hämtas från den valda miljön, `--aepUserLdap-- Firefly Services OAuth Credential`.

Klicka på **Skicka**.

![Postman](./images/ioauth.png)

När du har klickat på **Skicka** visas ett svar i avsnittet **Brödtext** i Postman:

![Postman](./images/ioauthresp.png)

Om konfigurationen lyckades bör du se ett liknande svar som innehåller följande information:

| Nyckel | Värde |
|:-------------:| :---------------:| 
| token_type | **bärare** |
| access_token | **eyJhbGciOiJSU...** |
| förfaller_in | **86399** |

Adobe I/O har gett dig en **innehavartoken**, med ett specifikt värde (mycket lång access_token) och ett förfallofönster.

Den token vi har fått gäller nu i 24 timmar. Det innebär att om du efter 24 timmar vill använda Postman för att autentisera till Adobe I/O måste du generera en ny token genom att köra denna begäran igen.

## Firefly Services API, Text 2-bild

Nu kan du skicka din första förfrågan till Firefly Services API:er.

I samlingen **FF - Firefly Services Tech Insiders** väljer du begäran med namnet **POST - Firefly - T2I V3**. I avsnittet **Brödtext** visas ett standardmeddelande med texten `Horses in a field`. Klicka på **Skicka** om du vill att Firefly Services ska generera den bilden.

![Firefly](./images/ff1.png)

Då ser du ett liknande svar som innehåller en bild-URL. Kopiera bild-URL:en och öppna den i webbläsaren.

![Firefly](./images/ff2.png)

Nu visas en vacker bild som visar `horses in a field`.

![Firefly](./images/ff3.png)

Du kan spela runt med API-begäran innan du fortsätter med nästa övning.

Nästa steg: [1.1.2 Begär bilder med specifikationer](./ex2.md)

[Gå tillbaka till modul 1.1](./firefly-services.md)

[Gå tillbaka till Alla moduler](./../../../overview.md)
