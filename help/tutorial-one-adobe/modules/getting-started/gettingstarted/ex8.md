---
title: Komma igång - Postman-konfiguration
description: Komma igång - Postman-konfiguration
kt: 5342
doc-type: tutorial
source-git-commit: 431f7696df12c8c133aced57c0f639c682304dee
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---

# Alternativ 2: PostBuster-konfiguration

>[!IMPORTANT]
>
>Om du inte är Adobe-anställd följer du instruktionerna för att [installera Postman](./ex7.md). Instruktionerna nedan är endast avsedda för Adobe-anställda. Om du redan har konfigurerat Postman hoppar du över den här övningen och går till [Program för att installera](./ex9.md).

## Installera PostBuster

Gå till [https://adobe.service-now.com/esc?id=adb_esc_kb_article&amp;sysparm_article=KB0020542](https://adobe.service-now.com/esc?id=adb_esc_kb_article&amp;sysparm_article=KB0020542).

Klicka för att hämta den senaste versionen av **PostBuster**.

![PostBuster](./images/pb1.png)

Hämta rätt version för ditt operativsystem.

![PostBuster](./images/pb2.png)

När nedladdningen är klar och har installerats öppnar du PostBuster. Du borde se det här då. Klicka på **Importera**.

![PostBuster](./images/pb3.png)

Hämta [postbuster.json.zip](./../../../assets/postman/postbuster.json.zip) och extrahera den på skrivbordet.

![PostBuster](./images/pbpb.png)

Klicka på **Välj en fil**.

![PostBuster](./images/pb4.png)

Markera filen **postbuster.json**. Klicka på **Öppna**.

![PostBuster](./images/pb5.png)

Du borde se det här då. Klicka på **Skanna**.

![PostBuster](./images/pb6.png)

Klicka på **Importera**.

![PostBuster](./images/pb7.png)

Du borde se det här då. Klicka för att öppna den importerade samlingen.

![PostBuster](./images/pb8.png)

Nu ser du din samling. Du måste fortfarande konfigurera en miljö för vissa miljövariabler.

![PostBuster](./images/pb9.png)

Klicka på **Grundmiljö** och sedan på ikonen **redigera** .

![PostBuster](./images/pb10.png)

Du borde se det här då.

![PostBuster](./images/pb11.png)

Kopiera miljöplatshållaren nedan och klistra in den i **basmiljön**.

```json
{
	"CLIENT_SECRET": "",
	"API_KEY": "",
	"ACCESS_TOKEN": "",
	"SCOPES": [
		"openid",
		"AdobeID",
		"read_organizations", 
		"additional_info.projectedProductContext", 
		"session",
		"ff_apis",
		"firefly_api"
	],
	"TECHNICAL_ACCOUNT_ID": "",
	"IMS": "ims-na1.adobelogin.com",
	"IMS_ORG": "",
	"access_token": "",
	"IMS_TOKEN": "",
	"AZURE_STORAGE_URL": "",
	"AZURE_STORAGE_CONTAINER": "",
	"AZURE_STORAGE_SAS_READ": "",
	"AZURE_STORAGE_SAS_WRITE": ""
}
```

Du borde ha den här då.

![PostBuster](./images/pb12.png)

## Ange dina Adobe I/O-variabler

Gå till [https://developer.adobe.com/console/home](https://developer.adobe.com/console/home){target="_blank"} och öppna projektet.

![Adobe I/O Ny integrering](./images/iopr.png){zoomable="yes"}

Gå till **OAuth Server-to-Server**.

![Adobe I/O Ny integrering](./images/iopbvar1.png){zoomable="yes"}

Du måste nu kopiera följande värden från ditt Adobe I/O-projekt och klistra in dem i din PostBuster-basmiljö.

- Klient-ID
- Klienthemlighet (klicka på **Hämta klienthemlighet**)
- Tekniskt konto-ID
- Organisations-ID (bläddra nedåt för att hitta ditt organisations-ID)

![Adobe I/O Ny integrering](./images/iopbvar2.png){zoomable="yes"}

Kopiera variablerna ovan en i taget och klistra in dem i din **basmiljö** i PostBuster.

| Variabelnamn i Adobe I/O | Variabelnamn i PostBuster-basmiljö |
|:-------------:| :---------------:| 
| Klient-ID | `API_KEY` |
| Klienthemlighet | `CLIENT_SECRET` |
| Tekniskt konto-ID | `TECHNICAL_ACCOUNT_ID` |
| Organisations-ID | `IMS_ORG` |

När du har kopierat variablerna på en av dem bör PostBuster-basmiljön se ut så här:

![Adobe I/O Ny integrering](./images/iopbvar3.png){zoomable="yes"}

I samlingen **Adobe IO - OAuth** markerar du begäran **POST - Get Access Token** och väljer **Skicka**.

Du bör se ett liknande svar som innehåller följande information:

| Nyckel | Värde |
|:-------------:| :---------------:| 
| token_type | **bärare** |
| access_token | **eyJhbGciOiJS...** |
| förfaller_in | **86399** |

Adobe I/O **Bearer-token** har ett specifikt värde (den mycket långa access_token) och ett giltighetsfönster och är nu giltigt i 24 timmar. Det innebär att om du efter 24 timmar vill använda Postman för att interagera med Adobe API:er måste du generera en ny token genom att köra denna begäran igen.

![Adobe I/O Ny integrering](./images/iopbvar4.png){zoomable="yes"}

PostBuster-miljön är nu konfigurerad och fungerar. Du har nu slutfört modulen Komma igång.

## Nästa steg

Gå till [Program som ska installeras](./ex9.md){target="_blank"}

Gå tillbaka till [Komma igång](./getting-started.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../overview.md){target="_blank"}