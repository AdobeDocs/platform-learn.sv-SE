---
title: PostBuster - anställda i Adobe
description: PostBuster - anställda i Adobe
doc-type: multipage-overview
exl-id: 01e30878-e1a9-4f46-bcf2-0074686ec1b5
source-git-commit: 54303033e23a28c45e9ef6c7a85135b21b3e29dc
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# PostBuster

>[!IMPORTANT]
>
>Instruktionerna nedan är endast avsedda för anställda i Adobe.

## Installera PostBuster

Gå till [https://adobe.service-now.com/esc?id=adb_esc_kb_article&amp;sysparm_article=KB0020542](https://adobe.service-now.com/esc?id=adb_esc_kb_article&amp;sysparm_article=KB0020542).

Klicka för att hämta den senaste versionen av **PostBuster**.

![PostBuster](./assets/images/pb1.png)

Hämta rätt version för ditt operativsystem.

![PostBuster](./assets/images/pb2.png)

När nedladdningen är klar och har installerats öppnar du PostBuster. Du borde se det här då. Klicka på **Importera**.

![PostBuster](./assets/images/pb3.png)

Hämta [postbuster.json.zip](./assets/postman/postbuster.json.zip) och extrahera den på skrivbordet.

![PostBuster](./assets/images/pbpb.png)

Klicka på **Välj en fil**.

![PostBuster](./assets/images/pb4.png)

Markera filen **postbuster.json**. Klicka på **Öppna**.

![PostBuster](./assets/images/pb5.png)

Du borde se det här då. Klicka på **Skanna**.

![PostBuster](./assets/images/pb6.png)

Klicka på **Importera**.

![PostBuster](./assets/images/pb7.png)

Du borde se det här då. Klicka för att öppna den importerade samlingen.

![PostBuster](./assets/images/pb8.png)

Nu ser du din samling. Du måste fortfarande konfigurera en miljö för vissa miljövariabler.

![PostBuster](./assets/images/pb9.png)

Klicka på **Grundmiljö** och sedan på ikonen **redigera** .

![PostBuster](./assets/images/pb10.png)

Du borde se det här då.

![PostBuster](./assets/images/pb11.png)

Kopiera miljöplatshållaren nedan och klistra in den i **basmiljön**.

```json
{
	"CLIENT_SECRET": "",
	"API_KEY": "",
	"ACCESS_TOKEN": "",
	"SCOPES": [
		"openid",
		"AdobeID",
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

![PostBuster](./assets/images/pb12.png)

När du har gått igenom modulen **Firefly-tjänster** bör din miljö se ut så här. Du behöver inte göra detta nu, det kommer att behandlas i ett senare skede.

![PostBuster](./assets/images/pb13.png)

>[!NOTE]
>
>![Tech Insiders](./assets/images/techinsiders.png){width="50px" align="left"}
>
>Om du har frågor kan du dela allmän feedback om dina förslag på framtida innehåll. Kontakta Tech Insiders direkt genom att skicka ett e-postmeddelande till **techinsiders@adobe.com**.

[Gå tillbaka till Alla moduler](./overview.md)
