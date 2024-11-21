---
title: Audience Activation till Microsoft Azure Event Hub - Definiera en Azure-funktion
description: Audience Activation till Microsoft Azure Event Hub - Definiera en Azure-funktion
kt: 5342
doc-type: tutorial
exl-id: c39fea54-98ec-45c3-a502-bcf518e6fd06
source-git-commit: 216914c9d97827afaef90e21ed7d4f35eaef0cd3
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 0%

---

# 2.4.6 Skapa ditt Microsoft Azure-projekt

## Bekanta dig med Azure Event Hub-funktioner

Med Azure-funktioner kan du köra små kodbitar (kallas **funktioner**) utan att behöva oroa dig för programinfrastrukturen. Med Azure-funktioner ger molninfrastrukturen alla aktuella servrar du behöver för att ditt program ska kunna köras i stor skala.

En funktion är **utlöst** av en viss typ av händelse. De utlösare som stöds är bland annat att svara på dataändringar, svara på meddelanden (till exempel händelsehubbar), köra ett schema eller som ett resultat av en HTTP-begäran.

Azure-funktioner är en serverlös beräkningstjänst som gör att du kan köra händelseutlösad kod utan att explicit behöva etablera eller hantera infrastruktur.

Azure Event Hubs kan integreras med Azure-funktioner för en serverlös arkitektur.

## Öppna Visual Studio-kod och logga in på Azure

Visual Studio Code gör det enkelt att ...

- definiera och binda Azure-funktioner till Event Hubs
- testa lokalt
- distribuera till Azure
- körning av fjärrloggfunktion

### Öppna Visual Studio-kod

### Logga in på Azure

När du loggar in med ditt Azure-konto som du använde för att registrera dig i den tidigare övningen kan du hitta och binda alla Event Hub-resurser med Visual Studio Code.

Öppna Visual Studio-kod och klicka på ikonen **Azure** .

Välj sedan **Logga in på Azure**:

![3-01-vsc-open.png](./images/301vscopen.png)

Du omdirigeras till webbläsaren för att logga in. Kom ihåg att välja det Azure-konto som du använde för att registrera.

När du ser följande skärm i webbläsaren loggas du in med Visual Code Studio:

![3-03-vsc-login-ok.png](./images/303vscloginok.png)

Återgå till Visual Code Studio (du ser namnet på din Azure-prenumeration, till exempel **Azure-prenumeration 1**):

![3-04-vsc-logged-in.png](./images/304vscloggedin.png)

## Skapa ett Azure-projekt

Klicka på **Skapa funktionsprojekt..**:

![3-05-vsc-create-project.png](./images/vsc2.png)

Välj en lokal mapp som du vill spara projektet i och klicka på **Välj**:

![3-06-vsc-select-folder.png](./images/vsc3.png)

Du kommer nu att ange guiden Skapa projekt. Klicka på **JavaScript** som språk för ditt projekt:

![3-07-vsc-select-language.png](./images/vsc4.png)

Välj sedan **Modell v4**.

![3-07-vsc-select-language.png](./images/vsc4a.png)

Välj **Azure Event Hub-utlösaren** som projektets första funktionsmall:

![3-08-vsc-function-template.png](./images/vsc5.png)

Ange ett namn för funktionen, använd följande format `--aepUserLdap---aep-event-hub-trigger` och tryck på Retur:

![3-09-vsc-function-name.png](./images/vsc6.png)

Välj **Skapa ny inställning för lokal app**:

![3-10-vsc-function-local-app-setting.png](./images/vsc7.png)

Klicka för att markera det namnutrymme för händelsehubben som du skapade tidigare, med namnet `--aepUserLdap---aep-enablement`.

![3-11-vsc-function-select-namespace.png](./images/vsc8.png)

Klicka sedan på händelsehubben som du skapade tidigare, med namnet `--aepUserLdap---aep-enablement-event-hub`.

![3-12-vsc-function-select-eventhub.png](./images/vsc9.png)

Klicka för att välja **RootManageSharedAccessKey** som händelsehubbsprincip:

![3-13-vsc-function-select-even-thub-policy.png](./images/vsc10.png)

Välj **Lägg till på arbetsyta** om du vill öppna ditt projekt:

![3-15-vsc-project-add-to-workspace.png](./images/vsc12.png)

Du kan då få ett sådant här meddelande. I så fall klickar du på **Ja, jag litar på författarna**.

![3-15-vsc-project-add-to-workspace.png](./images/vsc12a.png)

När du har skapat projektet klickar du på **index.js** för att öppna filen i redigeraren:

![3-16-vsc-open-index-js.png](./images/vsc13.png)

Nyttolasten som skickas av Adobe Experience Platform till din Event Hub kommer att innehålla publikens ID:

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

Ersätt koden i Visual Studio-kodens index.js med koden nedan. Den här koden körs varje gång CDP i realtid skickar målgruppskvalifikationer till din Event Hub-destination. I vårt exempel handlar koden bara om att visa och förbättra den mottagna nyttolasten. Men du kan föreställa dig vilken funktion som helst för att bearbeta målgruppskvalifikationer i realtid.

```javascript
// Marc Meewis - Solution Consultant Adobe - 2020
// Adobe Experience Platform Enablement - Module 2.4

// Main function
// -------------
// This azure function is fired for each audience activated to the Adobe Exeperience Platform Real-time CDP Azure 
// Eventhub destination
// This function enriched the received audience payload with the name of the audience. 
// You can replace this function with any logic that is require to process and deliver
// Adobe Experience Platform audiences in real-time to any application or platform that 
// would need to act upon an AEP audience qualification.
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

## Kör Azure Project

Nu är det dags att köra projektet. I det här skedet distribuerar vi inte projektet till Azure. Vi kör den lokalt i felsökningsläge. Välj ikonen Kör och klicka på den gröna pilen.

![3-17-vsc-run-project.png](./images/vsc14.png)

Första gången du kör ditt projekt i felsökningsläge måste du koppla ett Azure-lagringskonto, klicka på **Välj lagringskonto** och sedan välja lagringskontot som du skapade tidigare, som har namnet `--aepUserLdap--aepstorage`.

Ditt projekt är nu igång och visas med en lista över händelser i händelsehubben. I nästa övning kommer du att visa hur ni beter er er på CitiSignal Demo-webbplatsen som kommer att kvalificera er för målgrupper. Därför får du en målgruppsklassificeringsnyttolast i terminalen för händelsehubbens utlösarfunktion.

![3-24-vsc-application-stop.png](./images/vsc18.png)

## Stoppa Azure Project

Gå till **CALL STACK** i VSC, klicka på pilen i det projekt som körs och klicka sedan på **Stopp** för att stoppa projektet.

![3-24-vsc-application-stop.png](./images/vsc17.png)

Nästa steg: [2.4.7 Heltäckande scenario](./ex7.md)

[Gå tillbaka till modul 2.4](./segment-activation-microsoft-azure-eventhub.md)

[Gå tillbaka till Alla moduler](./../../../overview.md)
