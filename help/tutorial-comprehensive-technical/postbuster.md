---
title: PostBuster - anställda i Adobe
description: PostBuster - anställda i Adobe
doc-type: multipage-overview
exl-id: a798e9d7-bb99-4390-885f-5fbd2ef4cee9
source-git-commit: 9c1b30dc0fcca6b4324ec7c8158699fa273cdc90
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# PostBuster

>[!IMPORTANT]
>
>Instruktionerna nedan är endast avsedda för anställda i Adobe.

>[!IMPORTANT]
>
>Genom att följa instruktionerna nedan har du alla nödvändiga API-samlingar tillgängliga som kommer att användas i dessa övningar:
>
>- [2.1.3 Visa din egen kundprofil i realtid - API](./modules/rtcdp-b2c/module2.1/ex3.md)
>- [2.3.6 Destinations SDK](./modules/rtcdp-b2c/module2.3/ex6.md)
>- [3.3.6 Testa ditt beslut med API](./modules/ajo-b2c/module3.3/ex6.md)
>- [5.1.8 Query Service API](./modules/datadistiller/module5.1/ex8.md)

## Installera PostBuster

Gå till [https://adobe.service-now.com/esc?id=adb_esc_kb_article&sysparm_article=KB0020542](https://adobe.service-now.com/esc?id=adb_esc_kb_article&sysparm_article=KB0020542).

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

Välj filen **aep_tutorial.json**. Klicka på **Öppna**.

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
	"QS_QUERY_ID": "",
	"SANDBOX_NAME": ""
}
```

Du borde ha den här då.

![PostBuster](./assets/images/pb12.png)

När du har skapat ett Adobe IO-projekt bör miljön se ut så här. Du behöver inte göra detta nu, det kommer att behandlas i ett senare skede.

![PostBuster](./assets/images/pb13.png)

>[!NOTE]
>
>![Tech Insiders](./assets/images/techinsiders.png){width="50px" align="left"}
>
>Om du har frågor kan du dela allmän feedback om dina förslag på framtida innehåll. Kontakta Tech Insiders direkt genom att skicka ett e-postmeddelande till **techinsiders@adobe.com**.

[Gå tillbaka till Alla moduler](./overview.md)
