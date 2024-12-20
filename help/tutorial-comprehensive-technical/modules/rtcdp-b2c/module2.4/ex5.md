---
title: Segmentaktivering till Microsoft Azure Event Hub - Definiera en Azure-funktion
description: Segmentaktivering till Microsoft Azure Event Hub - Definiera en Azure-funktion
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 0%

---

# 2.4.5 Skapa ditt Microsoft Azure-projekt

## 2.4.5.1 Bekanta dig med Azure Event Hub-funktioner

Med Azure-funktioner kan du köra små kodbitar (kallas **funktioner**) utan att behöva oroa dig för programinfrastrukturen. Med Azure-funktioner ger molninfrastrukturen alla aktuella servrar du behöver för att ditt program ska kunna köras i stor skala.

En funktion är **utlöst** av en viss typ av händelse. De utlösare som stöds är bland annat att svara på dataändringar, svara på meddelanden (till exempel händelsehubbar), köra ett schema eller som ett resultat av en HTTP-begäran.

Azure-funktioner är en serverlös beräkningstjänst som gör att du kan köra händelseutlösad kod utan att explicit behöva etablera eller hantera infrastruktur.

Azure Event Hubs kan integreras med Azure-funktioner för en serverlös arkitektur.

## 2.4.5.2 Öppna Visual Studio-kod och logga in på Azure

Visual Studio Code gör det enkelt att ...

- definiera och binda Azure-funktioner till Event Hubs
- testa lokalt
- distribuera till Azure
- körning av fjärrloggfunktion

### Öppna Visual Studio-kod

Om du vill öppna Visual Studio Code anger du **visual** i operativsystemets sökning (Spotlight-sökning i OSX, Sök i Aktivitetsfältet i Windows). Om du inte hittar den måste du upprepa stegen som beskrivs i [Utför 0 - Förkrav](./ex0.md).

![visual-studio-code-icon.png](./images/visual-studio-code-icon.png)

### Logga in på Azure

När du loggar in med ditt Azure-konto som du använde för att registrera i [Utgång 0 - Krav](./ex0.md) kan du hitta och binda alla händelsehubbresurser med Visual Studio-koden.

Klicka på ikonen **Azure** i Visual Studio-koden. Om du inte har det alternativet kan något ha gått fel med installationen av de nödvändiga tilläggen.

Välj sedan **Logga in på Azure**:

![3-01-vsc-open.png](./images/3-01-vsc-open.png)

Du omdirigeras till webbläsaren för att logga in. Kom ihåg att välja det Azure-konto som du använde för att registrera.

![3-02-vsc-Pick-account.png](./images/3-02-vsc-pick-account.png)

När du ser följande skärm i webbläsaren loggas du in med Visual Code Studio:

![3-03-vsc-login-ok.png](./images/3-03-vsc-login-ok.png)

Återgå till Visual Code Studio (du ser namnet på din Azure-prenumeration, till exempel **Azure-prenumeration 1**):

![3-04-vsc-logged-in.png](./images/3-04-vsc-logged-in.png)

## 2.4.5.3 Skapa ett Azure-projekt

När du hovrar över **Azure-prenumerationen** visas en meny ovanför avsnittet och väljer **Skapa nytt projekt..**:

![3-05-vsc-create-project.png](./images/vsc2.png)

Välj en lokal mapp som du vill spara projektet i och klicka på **Välj**:

![3-06-vsc-select-folder.png](./images/vsc3.png)

Du kommer nu att ange guiden Skapa projekt. Välj **JavaScript** som språk för ditt projekt:

![3-07-vsc-select-language.png](./images/vsc4.png)

Välj **Azure Event Hub-utlösaren** som projektets första funktionsmall:

![3-08-vsc-function-template.png](./images/vsc5.png)

Ange ett namn för funktionen, använd följande format `--aepUserLdap---aep-event-hub-trigger` och tryck på Retur:

![3-09-vsc-function-name.png](./images/vsc6.png)

Välj **Skapa ny inställning för lokal app**:

![3-10-vsc-function-local-app-setting.png](./images/vsc7.png)

Välj ett namnutrymme för händelsehubb. Du bör se händelsehubben som du definierade i **Utgång 2**. I det här exemplet är händelsehubbens namnutrymme **vangeluw-aep-enablement**:

![3-11-vsc-function-select-namespace.png](./images/vsc8.png)

Markera din händelsehubb så ser du den händelsehubb som du definierade i **Utgång 2**. I mitt fall är det **vangeluw-aep-enablement-event-hub**:

![3-12-vsc-function-select-eventhub.png](./images/vsc9.png)

Välj **RootManageSharedAccessKey** som händelsehubbsprincip:

![3-13-vsc-function-select-even-thub-policy.png](./images/vsc10.png)

Ange om du vill använda **$Default**:

![3-14-vsc-eventhub-Consumer-group.png](./images/vsc11.png)

Välj **Lägg till på arbetsyta** om du vill öppna ditt projekt:

![3-15-vsc-project-add-to-workspace.png](./images/vsc12.png)

När du har skapat projektet klickar du på **index.js** för att öppna filen i redigeraren:

![3-16-vsc-open-index-js.png](./images/vsc13.png)

Nyttolasten som skickas av Adobe Experience Platform till din händelsehubb kommer att innehålla segment-ID:n:

```json
[{
"segmentMembership": {
"ups": {
"ca114007-4122-4ef6-a730-4d98e56dce45": {
"lastQualificationTime": "2020-08-31T10:59:43Z",
"status": "realized"
},
"be2df7e3-a6e3-4eb4-ab12-943a4be90837": {
"lastQualificationTime": "2020-08-31T10:59:56Z",
"status": "realized"
},
"39f0feef-a8f2-48c6-8ebe-3293bc49aaef": {
"lastQualificationTime": "2020-08-31T10:59:56Z",
"status": "realized"
}
}
},
"identityMap": {
"ecid": [{
"id": "08130494355355215032117568021714632048"
}]
}
}]
```

Ersätt koden i Visual Studio-kodens index.js med koden nedan. Den här koden körs varje gång CDP i realtid skickar segmentkvalifikationer till din Event Hub-destination. I vårt exempel handlar koden bara om att visa och förbättra den mottagna nyttolasten. Men du kan föreställa dig vilken funktion som helst för att bearbeta segmentens kvalifikationer i realtid.

```javascript
// Marc Meewis - Solution Consultant Adobe - 2020
// Adobe Experience Platform Enablement - Module 13

// Main function
// -------------
// This azure function is fired for each segment activated to the Adobe Exeperience Platform Real-time CDP Azure 
// Eventhub destination
// This function enriched the received segment payload with the name fo the segment. 
// You can replace this function with any logic that is require to process and deliver
// Adobe Experience Platform segments in real-time to any application or platform that 
// would need to act upon an AEP segment qualiification.
// 

module.exports = async function (context, eventHubMessages) {

    return new Promise (function (resolve, reject) {

        context.log('Message : ' + JSON.stringify(eventHubMessages, null, 2));

        resolve();

    });    

};
```

Resultatet bör se ut så här:

![3-16b-vsc-edit-index-js.png](./images/vsc1.png)

## 2.4.5.4 Kör Azure Project

Nu är det dags att köra projektet. I det här skedet distribuerar vi inte projektet till Azure. Vi kör den lokalt i felsökningsläge. Välj ikonen Kör och klicka på den gröna pilen.

![3-17-vsc-run-project.png](./images/vsc14.png)

Första gången du kör ditt projekt i felsökningsläge måste du koppla ett Azure-lagringskonto. Klicka sedan på **Välj lagringskonto**.

![3-17-vsc-run-project.png](./images/vsc15.png)

I listan över lagringskonton väljer du det som du har skapat som en del av [13.1.4 Konfigurera ditt Azure Storage-konto](./ex1.md). Ditt lagringskonto har namnet `--aepUserLdap--aepstorage`, till exempel: **mmeewisaepstorage**.

![3-22-vsc-select-storage-account.png](./images/vsc16.png)

Ditt projekt är nu igång och visas med en lista över händelser i händelsehubben. I nästa övning kommer du att visa hur man beter sig på Lumas demowebbplats som kommer att kvalificera sig för dessa segment. Du får därför en nyttolast för segmentkvalificering i terminalen för händelsehubbens utlösarfunktion:

![3-23-vsc-application-started.png](./images/vsc17.png)

## 2.4.5.5 Stoppa Azure Project

Om du vill stoppa projektet väljer du fliken **Terminal**, klickar i terminalfönstret och trycker på **CMD-C** i OSX eller **CTRL-C** i Windows:

![3-24-vsc-application-stop.png](./images/vsc18.png)

Nästa steg: [2.4.6 Heltäckande scenario](./ex6.md)

[Gå tillbaka till modul 2.4](./segment-activation-microsoft-azure-eventhub.md)

[Gå tillbaka till Alla moduler](./../../../overview.md)
