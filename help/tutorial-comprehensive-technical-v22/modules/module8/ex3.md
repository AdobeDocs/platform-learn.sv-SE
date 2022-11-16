---
title: Adobe Journey Optimizer - API för externt väder, SMS-åtgärd med mera - Definiera anpassade åtgärder
description: Adobe Journey Optimizer - API för externt väder, SMS-åtgärd med mera - Definiera anpassade åtgärder
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 7ee5aee9-3740-4eee-9f53-a44fdb564a00
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---

# 8.3 Definiera en anpassad åtgärd

I den här övningen ska du skapa två anpassade åtgärder genom att använda Adobe Journey Optimizer tillsammans.

Logga in på Adobe Journey Optimizer genom att gå till [Adobe Experience Cloud](https://experience.adobe.com). Klicka **Journey Optimizer**.

![ACOP](../module7/images/acophome.png)

Du omdirigeras till **Startsida**  i Journey Optimizer. Kontrollera först att du använder rätt sandlåda. Sandlådan som ska användas anropas `--aepSandboxId--`. Om du vill ändra från en sandlåda till en annan klickar du på **PRODUKTIONSprodukt (VA7)** och välj sandlådan i listan. I det här exemplet heter sandlådan **AEP-aktivering FY22**. Då är du i **Startsida** vy över din sandlåda `--aepSandboxId--`.

![ACOP](../module7/images/acoptriglp.png)

Bläddra nedåt i den vänstra menyn och klicka på **Konfigurationer**. Klicka sedan på **Hantera** knapp under **Åtgärder**.

![Demo](./images/menuactions.png)

Då ser du **Åtgärder** lista.

![Demo](./images/acthome.png)

Du definierar en åtgärd som skickar en text till en Slack-kanal.

## 8.3.1 Åtgärd: Skicka text till Slack Channel

Du kommer nu att använda en befintlig Slack-kanal och skicka meddelanden till den Slack-kanalen. Slack har ett lättanvänt API och vi använder Adobe Journey Optimizer för att utlösa deras API.

![Demo](./images/slack.png)

Klicka **Skapa åtgärd** för att börja lägga till en ny åtgärd.

![Demo](./images/adda.png)

En tom åtgärdspopup visas.

![Demo](./images/emptyact.png)

Använd som namn på åtgärden `--demoProfileLdap--TextSlack`. I det här exemplet är åtgärdsnamnet `vangeluwTextSlack`.

Ange Beskrivning till: `Send Text to Slack`.

![Demo](./images/slackname.png)

För **URL-konfiguration**, använd detta:

- URL: `https://2mnbfjyrre.execute-api.us-west-2.amazonaws.com/prod`
- Metod: **POST**

>[!NOTE]
>
>Ovanstående URL hänvisar till en AWS Lambda-funktion som sedan vidarebefordrar din begäran till Slack-kanalen enligt ovan. Detta görs för att skydda tillgången till en kanal som ägs av Adobe. Om du har en egen Slack-kanal bör du skapa en Slack-app via [https://api.slack.com/](https://api.slack.com/)måste du sedan skapa en inkommande webkrok i den Slack-appen och sedan ersätta ovanstående URL med din inkommande webkroks-URL.

Du behöver inte ändra rubrikfälten.

![Demo](./images/slackurl.png)

**Autentisering** ska anges till **Ingen autentisering**.

![Demo](./images/slackauth.png)

För **Åtgärdsparametrar** måste du definiera vilka fält som ska skickas till Slack. Logiskt sett vill vi att Adobe Journey Optimizer och Adobe Experience Platform ska vara hjärnan i personaliseringen, så att texten som ska skickas till Slack ska definieras av Adobe Journey Optimizer och sedan skickas till Slack för genomförande.

Så för **Åtgärdsparametrar** klickar du på **Redigera nyttolast** ikon.

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

Obs! genom att ange fälten nedan blir dessa fält tillgängliga från kundresan och du kan fylla i dem dynamiskt från resan:

**&quot;toBeMapped&quot;: true,**

**&quot;dataType&quot;: &quot;string&quot;,**

**&quot;label&quot;: &quot;textToSlack&quot;**

Då ser du det här:

![Demo](./images/slackmsgpopup1.png)

Klicka **Spara**.

![Demo](./images/twiliomsgpopup2.png)

Bläddra uppåt och klicka **Spara** en gång till för att spara din anpassade åtgärd.

![Demo](./images/slackmsgpopup3.png)

Din anpassade åtgärd ingår nu i **Åtgärder** lista.

![Demo](./images/slackdone.png)

Du har definierat händelser, en extern datakälla och åtgärder. Nu ska vi konsolidera allt det på en enda resa.

Nästa steg: [8.4 Skapa din resa och dina meddelanden](./ex4.md)

[Gå tillbaka till modul 8](journey-orchestration-external-weather-api-sms.md)

[Gå tillbaka till Alla moduler](../../overview.md)
