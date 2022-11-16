---
title: Segmentaktivering till Microsoft Azure Event Hub - Konfigurera din Microsoft Azure-miljö
description: Segmentaktivering till Microsoft Azure Event Hub - Konfigurera din Microsoft Azure-miljö
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 79711c1a-674c-4233-9c6c-af3bad6d0e0c
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 0%

---

# 13.0 Konfigurera miljön

## 13.0.1 Skapa en Azure-prenumeration

>[!NOTE]
>
>Om du redan har en Azure-prenumeration kan du hoppa över det här steget. Fortsätt med träning 13.0.2 i så fall.

Gå till [https://portal.azure.com](https://portal.azure.com) och logga in med ditt Azure-konto. Om du inte har någon, använd din personliga e-postadress för att skapa ditt Azure-konto.

![02-azure-portal-email.png](./images/02-azure-portal-email.png)

När inloggningen är klar visas följande skärm:

![03-azure-logged-in.png](./images/03-azure-logged-in.png)

Klicka på menyn till vänster och välj **Alla resurser** visas Azure-prenumerationsskärmen om du ännu inte prenumererar. I så fall väljer du **Börja med en kostnadsfri provversion av Azure**.

![04-azure-start-subscribe.png](./images/04-azure-start-subscribe.png)

Fyll i Azure-prenumerationsformuläret, ange din mobiltelefon och ditt kreditkort för aktivering (du har en kostnadsfri nivå i 30 dagar och du debiteras inte om du inte uppgraderar):

![05-azure-subscription-form.png](./images/05-azure-subscription-form.png)

När prenumerationsprocessen är klar är du redo att gå:

![06-azure-subscription-ok.png](./images/06-azure-subscription-ok.png)


## 13.0.2 Installera Visual Code Studio

Du använder Microsoft Visual Code Studio för att hantera ditt Azure-projekt. Du kan ladda ned den via [den här länken](https://code.visualstudio.com/download). Följ installationsanvisningarna för ditt operativsystem på samma webbplats.

## 13.0.3 Installera Visual Code Extensions

Installera Azure-funktioner för Visual Studio-kod från [https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions). Klicka på installationsknappen:

![07-azure-code-extension-install.png](./images/07-azure-code-extension-install.png)

Installera Azure-konto och logga in för Visual Studio-kod från [https://marketplace.visualstudio.com/items?itemName=ms-vscode.azure-account](https://marketplace.visualstudio.com/items?itemName=ms-vscode.azure-account). Klicka på installationsknappen:

![08-azure-account-extension-install.png](./images/08-azure-account-extension-install.png)

## 13.0.4 Installera node.js

>[!NOTE]
>
>Om du redan har node.js installerat kan du hoppa över det här steget. Fortsätt med träning 13.0.5 i så fall.

### macOS

Se till att du har [Homebreiska](https://brew.sh/) installeras först. Följ instruktionerna [här](https://brew.sh/).

![Nod](./images/brew.png)

Kör följande kommando när du har installerat Homebrew:

```javascript
brew install node
```

### Windows

Ladda ned [Windows Installer](https://nodejs.org/en/#home-downloadhead) direkt från [nodejs.org](https://nodejs.org/en/) webbplats.

## 13.0.5 Verifiera node.js-version

För den här modulen måste du ha node.js version 12 installerat. Andra versioner av node.js kan orsaka problem med övning 13.5.

Innan du fortsätter bör du verifiera din version av node.js nu.

Kör det här kommandot för att verifiera din node.js-version:

```javascript
node -v
```

Om du har en version under eller över 12 måste du uppgradera eller nedgradera.

### Uppgradera/nedgradera nod.js-version på macOS

Kontrollera att du har paketet **n** installerade.

Installera paketet **n** kör du det här kommandot:

```javascript
sudo npm install -g n
```

Om du har en version som är under eller över version 12 kör du det här kommandot för att uppgradera eller nedgradera:

```javascript
sudo n 12.6.0
```

### Uppgradera/nedgradera nod.js-version i Windows

Avinstallera node.js från Windows > Kontrollpanelen > Lägg till eller ta bort program.

Installera den version som krävs från [nodejs.org](https://nodejs.org/en/) webbplats.

## 13.0.6 Installera NPM-paket: förfrågan

Du måste installera paketet **förfrågan** som en del av installationen av node.js.

Installera paketet **förfrågan** kör du det här kommandot:

```javascript
npm install request
```


Nästa steg: [13.1 Konfigurera din Microsoft Azure EventHub-miljö](./ex1.md)

[Gå tillbaka till modul 13](./segment-activation-microsoft-azure-eventhub.md)

[Gå tillbaka till Alla moduler](./../../overview.md)
