---
title: Adobe Journey Optimizer - API för externt väder, SMS-åtgärd med mera - Definiera anpassade åtgärder
description: Adobe Journey Optimizer - API för externt väder, SMS-åtgärd med mera - Definiera anpassade åtgärder
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 0%

---

# 3.2.3 Definiera en anpassad åtgärd

I den här övningen ska du skapa två anpassade åtgärder genom att använda Adobe Journey Optimizer tillsammans.

Logga in på Adobe Journey Optimizer på [Adobe Experience Cloud](https://experience.adobe.com). Klicka på **Journey Optimizer**.

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acophome.png)

Du omdirigeras till vyn **Hem** i Journey Optimizer. Kontrollera först att du använder rätt sandlåda. Sandlådan som ska användas kallas `--aepSandboxName--`. Om du vill ändra från en sandlåda till en annan klickar du på **PRODUKTIONSprodukt (VA7)** och väljer sandlådan i listan. I det här exemplet heter sandlådan **AEP Enablement FY22**. Du kommer sedan att vara i vyn **Hem** i din sandlåda `--aepSandboxName--`.

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acoptriglp.png)

Bläddra nedåt på den vänstra menyn och klicka på **Konfigurationer**. Klicka sedan på knappen **Hantera** under **Åtgärder**.

![Demo](./images/menuactions.png)

Sedan visas listan **Åtgärder**.

![Demo](./images/acthome.png)

Du definierar en åtgärd som skickar en text till en Slack-kanal.

## 3.2.3.1 Åtgärd: Skicka text till Slack Channel

Du kommer nu att använda en befintlig Slack-kanal och skicka meddelanden till den Slack-kanalen. Slack har ett lättanvänt API och vi använder Adobe Journey Optimizer för att utlösa deras API.

![Demo](./images/slack.png)

Klicka på **Skapa åtgärd** för att börja lägga till en ny åtgärd.

![Demo](./images/adda.png)

En tom åtgärdspopup visas.

![Demo](./images/emptyact.png)

Använd `--aepUserLdap--TextSlack` som namn för åtgärden. I det här exemplet är åtgärdsnamnet `vangeluwTextSlack`.

Ange Beskrivning till: `Send Text to Slack`.

![Demo](./images/slackname.png)

Använd följande för **URL-konfigurationen**:

- URL: `https://2mnbfjyrre.execute-api.us-west-2.amazonaws.com/prod`
- Metod: **POST**

>[!NOTE]
>
>Ovanstående URL hänvisar till en AWS Lambda-funktion som sedan vidarebefordrar din begäran till Slack-kanalen enligt ovan. Detta görs för att skydda tillgången till en kanal som ägs av Adobe. Om du har en egen Slack-kanal bör du skapa en Slack-app via [https://api.slack.com/](https://api.slack.com/). Sedan måste du skapa en inkommande webkrok i den Slack-appen och sedan ersätta den ovanstående URL:en med din inkommande webkroks-URL.

Du behöver inte ändra rubrikfälten.

![Demo](./images/slackurl.png)

**Autentisering** ska anges till **Ingen autentisering**.

![Demo](./images/slackauth.png)

För **åtgärdsparametrarna** måste du definiera vilka fält som ska skickas till Slack. Logiskt sett vill vi att Adobe Journey Optimizer och Adobe Experience Platform ska vara hjärnan i personaliseringen, så att texten som ska skickas till Slack ska definieras av Adobe Journey Optimizer och sedan skickas till Slack för genomförande.

För **åtgärdsparametrarna** klickar du på ikonen **Redigera nyttolast** .

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

Obs! Genom att ange fälten nedan blir dessa fält tillgängliga från kundresan och du kan fylla i dem dynamiskt från resan:

**&quot;toBeMapped&quot;: true,**

**&quot;dataType&quot;: &quot;string&quot;,**

**&quot;label&quot;: &quot;textToSlack&quot;**

Då ser du det här:

![Demo](./images/slackmsgpopup1.png)

Klicka på **Spara**.

![Demo](./images/twiliomsgpopup2.png)

Bläddra uppåt och klicka på **Spara** en gång till för att spara din anpassade åtgärd.

![Demo](./images/slackmsgpopup3.png)

Din anpassade åtgärd ingår nu i listan **Åtgärder**.

![Demo](./images/slackdone.png)

Du har definierat händelser, en extern datakälla och åtgärder. Nu ska vi konsolidera allt det på en enda resa.

Nästa steg: [3.2.4 Skapa din resa och dina meddelanden](./ex4.md)

[Gå tillbaka till modul 8](journey-orchestration-external-weather-api-sms.md)

[Gå tillbaka till Alla moduler](../../../overview.md)
