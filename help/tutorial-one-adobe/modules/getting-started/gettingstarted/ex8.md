---
title: Komma igång - Postman-konfiguration
description: Komma igång - Postman-konfiguration
kt: 5342
doc-type: tutorial
exl-id: fc1ee238-cce8-40a9-aba7-3605019a0077
source-git-commit: 899cb9b17702929105926f216382afcde667a1b6
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---

# Alternativ 2: PostBuster-konfiguration

>[!IMPORTANT]
>
>Om du inte är Adobe-anställd följer du instruktionerna för att [installera Postman](./ex7.md){target="_blank"}. Instruktionerna nedan är endast avsedda för Adobe-anställda.

## Video

I den här videon får du en förklaring och demonstration av alla steg som ingår i övningen.

>[!VIDEO](https://video.tv.adobe.com/v/3476496?quality=12&learn=on)

## Installera PostBuster

Gå till [https://adobe.service-now.com/esc?id=adb_esc_kb_article&amp;sysparm_article=KB0020542](https://adobe.service-now.com/esc?id=adb_esc_kb_article&sysparm_article=KB0020542){target="_blank"}.

Klicka för att hämta den senaste versionen av **PostBuster**.

![PostBuster](./images/pb1.png)

Hämta rätt version för ditt operativsystem.

![PostBuster](./images/pb2.png)

När nedladdningen är klar och har installerats öppnar du PostBuster. Du borde se det här då. Klicka på **Importera**.

![PostBuster](./images/pb3.png)

Hämta [postbuster.json.zip](./../../../assets/postman/postbuster.json.zip){target="_blank"} och extrahera den på skrivbordet.

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

Kopiera miljöplatshållaren nedan och klistra in den i **basmiljön** genom att ersätta det som finns där.

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
		"firefly_api",
		"frame.s2s.all"
	],
	"TECHNICAL_ACCOUNT_ID": "",
	"IMS": "ims-na1.adobelogin.com",
	"IMS_ORG": "",
	"access_token": "",
	"IMS_TOKEN": "",
	"AZURE_STORAGE_URL": "",
	"AZURE_STORAGE_CONTAINER": "",
	"AZURE_STORAGE_SAS_READ": "",
	"AZURE_STORAGE_SAS_WRITE": "",
	"FRAME_IO_BASE_URL": "https://api.frame.io",
	"FRAME_IO_ACCOUNT_ID": "",
	"FRAME_IO_WORKSPACE_ID": ""
}
```

Du borde ha den här då.

![PostBuster](./images/pb12.png)

## Ange dina Adobe I/O-variabler

Gå till [https://developer.adobe.com/console/home](https://developer.adobe.com/console/home){target="_blank"} och öppna projektet.

![Adobe I/O Ny integrering](./images/iopr.png)

Gå till **OAuth Server-to-Server**.

![Adobe I/O Ny integrering](./images/iopbvar1.png)

Du måste nu kopiera följande värden från ditt Adobe I/O-projekt och klistra in dem i din PostBuster-basmiljö.

- Klient-ID
- Klienthemlighet (klicka på **Hämta klienthemlighet**)
- Tekniskt konto-ID
- Organisations-ID (bläddra nedåt för att hitta ditt organisations-ID)

![Adobe I/O Ny integrering](./images/iopbvar2.png)

Kopiera variablerna ovan en i taget och klistra in dem i din **basmiljö** i PostBuster.

| Variabelnamn i Adobe I/O | Variabelnamn i PostBuster-basmiljö |
|:-------------:| :---------------:| 
| Klient-ID | `API_KEY` |
| Klienthemlighet | `CLIENT_SECRET` |
| Tekniskt konto-ID | `TECHNICAL_ACCOUNT_ID` |
| Organisations-ID | `IMS_ORG` |

När du har kopierat variablerna en och en bör PostBuster-basmiljön se ut så här.

Klicka på **Stäng**.

![Adobe I/O Ny integrering](./images/iopbvar3.png)

I samlingen **Adobe IO - OAuth** markerar du begäran **POST - Get Access Token** och väljer **Skicka**.

![Adobe I/O Ny integrering](./images/iopbvar3a.png)

Du bör se ett liknande svar som innehåller följande information:

| Nyckel | Värde |
|:-------------:| :---------------:| 
| token_type | **bärare** |
| access_token | **eyJhbGciOiJS...** |
| förfaller_in | **86399** |

Adobe I/O **Bearer-token** har ett specifikt värde (den mycket långa access_token) och ett giltighetsfönster och är nu giltigt i 24 timmar. Det innebär att om du efter 24 timmar vill använda Postman för att interagera med Adobe API:er måste du generera en ny token genom att köra denna begäran igen.

![Adobe I/O Ny integrering](./images/iopbvar4.png)

PostBuster-miljön är nu konfigurerad och fungerar. Du har nu avslutat den här övningen.

## Nästa steg

Gå till [Program som ska installeras](./ex9.md){target="_blank"}

Gå tillbaka till [Komma igång](./getting-started.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../overview.md){target="_blank"}
