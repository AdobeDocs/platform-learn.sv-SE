---
title: Adobe Journey Optimizer - API för externt väder, SMS-åtgärd med mera - Definiera anpassade åtgärder
description: Adobe Journey Optimizer - API för externt väder, SMS-åtgärd med mera - Definiera anpassade åtgärder
kt: 5342
doc-type: tutorial
exl-id: d9bdc4c6-7539-4646-9b75-f397b792479f
source-git-commit: c531412a2c0a5c216f49560e01fb26b9b7e71869
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---

# 3.2.3 Definiera en anpassad åtgärd

I den här övningen skapar du en anpassad åtgärd för att skicka ett meddelande till en Slack-kanal.

Logga in på Adobe Journey Optimizer på [Adobe Experience Cloud](https://experience.adobe.com). Klicka på **Journey Optimizer**.

![ACOP](./../../../modules/ajo-b2c/module3.1/images/acophome.png)

Du omdirigeras till vyn **Hem** i Journey Optimizer. Kontrollera först att du använder rätt sandlåda. Sandlådan som ska användas kallas `--aepSandboxName--`. Du kommer sedan att vara i vyn **Hem** i din sandlåda `--aepSandboxName--`.

![ACOP](./../../../modules/ajo-b2c/module3.1/images/acoptriglp.png)

Du kommer nu att använda en befintlig Slack-kanal och skicka meddelanden till den Slack kanalen. Slack har ett lättanvänt API och du använder Adobe Journey Optimizer för att utlösa deras API.

![Demo](./images/slack.png)

Bläddra nedåt på den vänstra menyn och klicka på **Konfigurationer**. Klicka sedan på knappen **Hantera** under **Åtgärder**.

![Demo](./images/menuactions.png)

Sedan visas listan **Åtgärder**. Klicka på **Skapa åtgärd**.

![Demo](./images/acthome.png)

En tom åtgärdspopup visas.

![Demo](./images/emptyact.png)

Använd `--aepUserLdap--TextSlack` som namn för åtgärden.

Ange Beskrivning till: `Send Message to Slack`.

Använd följande för **URL-konfigurationen**:

- URL: `https://2mnbfjyrre.execute-api.us-west-2.amazonaws.com/prod`
- Metod: **POST**

>[!NOTE]
>
>Ovanstående URL hänvisar till en AWS Lambda-funktion som sedan vidarebefordrar din begäran till Slack-kanalen enligt ovan. Detta görs för att skydda tillgången till en kanal som ägs av Adobe. Om du har en egen Slack-kanal bör du skapa en Slack-app via [https://api.slack.com/](https://api.slack.com/). Sedan måste du skapa en inkommande webkrok i den Slack-appen och sedan ersätta den ovanstående URL:en med din inkommande webkroks-URL.

![Demo](./images/slackname.png)

Du behöver inte ändra rubrikfälten.

![Demo](./images/slackurl.png)

**Autentisering** ska anges till **Ingen autentisering**.

![Demo](./images/slackauth.png)

Under **Nyttolaster** måste du definiera vilka fält som ska skickas till Slack. Logiskt sett vill ni att Adobe Journey Optimizer och Adobe Experience Platform ska vara hjärnan i personaliseringen, så att texten som ska skickas till Slack ska definieras av Adobe Journey Optimizer och sedan skickas till Slack för exekvering.

Klicka på ikonen **Redigera nyttolast** för **Begäran**.

![Demo](./images/slackmsgp.png)

Då visas ett tomt popup-fönster.

![Demo](./images/slackmsgpopup.png)

Kopiera texten nedan och klistra in den i det tomma popup-fönstret.

```json
{
 "text": {
  "toBeMapped": true,
  "dataType": "string",
  "label": "textToSlack"
 }
}
```

Då ser du det här:

![Demo](./images/slackmsgpopup1.png)

Bläddra uppåt och klicka på **Spara** en gång till för att spara funktionsmakrot.

![Demo](./images/slackmsgpopup3.png)

Din anpassade åtgärd ingår nu i listan **Åtgärder**.

![Demo](./images/slackdone.png)

Du har definierat händelser, en extern datakälla och åtgärder. Nu ska vi konsolidera allt det på en enda resa.

Nästa steg: [3.2.4 Skapa din resa och dina meddelanden](./ex4.md)

[Gå tillbaka till modul 3.2](journey-orchestration-external-weather-api-sms.md)

[Gå tillbaka till Alla moduler](../../../overview.md)
