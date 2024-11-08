---
title: Segmentaktivering till Microsoft Azure Event Hub - Konfigurera din Microsoft Azure-miljö
description: Segmentaktivering till Microsoft Azure Event Hub - Konfigurera din Microsoft Azure-miljö
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# 2.4.0 Konfigurera miljön

## 2.4.0.1 Skapa en Azure-prenumeration

>[!NOTE]
>
>Om du redan har en Azure-prenumeration kan du hoppa över det här steget. Fortsätt med träning 13.0.2 i så fall.

Gå till [https://portal.azure.com](https://portal.azure.com) och logga in med ditt Azure-konto. Om du inte har någon, använd din personliga e-postadress för att skapa ditt Azure-konto.

![02-azure-portal-email.png](./images/02-azure-portal-email.png)

När inloggningen är klar visas följande skärm:

![03-azure-logged-in.png](./images/03-azure-logged-in.png)

Klicka på menyn till vänster och välj **Alla resurser**. Azure-prenumerationsskärmen visas om du inte har prenumererat ännu. I så fall väljer du **Starta med en kostnadsfri Azure-utvärderingsversion**.

![04-azure-start-subscribe.png](./images/04-azure-start-subscribe.png)

Fyll i Azure-prenumerationsformuläret, ange din mobiltelefon och ditt kreditkort för aktivering (du har en kostnadsfri nivå i 30 dagar och du debiteras inte om du inte uppgraderar):

![05-azure-subscription-form.png](./images/05-azure-subscription-form.png)

När prenumerationsprocessen är klar är du redo att gå:

![06-azure-subscription-ok.png](./images/06-azure-subscription-ok.png)


## 2.4.0.2 Installera Visual Code Studio

Du använder Microsoft Visual Code Studio för att hantera ditt Azure-projekt. Du kan hämta den via [den här länken](https://code.visualstudio.com/download). Följ installationsanvisningarna för ditt operativsystem på samma webbplats.

## 2.4.0.3 Installera Visual Code Extensions

Installera Azure-funktionerna för Visual Studio-kod från [https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions). Klicka på installationsknappen:

![07-azure-code-extension-install.png](./images/07-azure-code-extension-install.png)

Installera Azure-konto och logga in för Visual Studio-kod från [https://marketplace.visualstudio.com/items?itemName=ms-vscode.azure-account](https://marketplace.visualstudio.com/items?itemName=ms-vscode.azure-account). Klicka på installationsknappen:

![08-azure-account-extension-install.png](./images/08-azure-account-extension-install.png)

## 2.4.0.4 Installera node.js

>[!NOTE]
>
>Om du redan har node.js installerat kan du hoppa över det här steget. Fortsätt med träning 13.0.5 i så fall.

### macOS

Kontrollera att du har [Homebrew](https://brew.sh/) installerat först. Följ instruktionerna [här](https://brew.sh/).

![Nod](./images/brew.png)

Kör följande kommando när du har installerat Homebrew:

```javascript
brew install node
```

### Windows

Hämta [Windows Installer](https://nodejs.org/en/#home-downloadhead) direkt från webbplatsen [nodejs.org](https://nodejs.org/en/).

## 2.4.0.5 Verifiera version av node.js

För den här modulen måste du ha node.js version 12 installerat. Andra versioner av node.js kan orsaka problem med övning 13.5.

Kontrollera din version av node.js nu innan du fortsätter.

Kör det här kommandot för att verifiera din node.js-version:

```javascript
node -v
```

Om du har en version under eller över 12 måste du uppgradera eller nedgradera.

### Uppgradera/nedgradera nod.js-version på macOS

Kontrollera att du har installerat paketet **n**.

Kör följande kommando för att installera paketet **n**:

```javascript
sudo npm install -g n
```

Om du har en version som är under eller över version 12 kör du det här kommandot för att uppgradera eller nedgradera:

```javascript
sudo n 12.6.0
```

### Uppgradera/nedgradera nod.js-version i Windows

Avinstallera node.js från Windows > Kontrollpanelen > Lägg till eller ta bort program.

Installerar den version som krävs från webbplatsen [nodatums.org](https://nodejs.org/en/).

## 2.4.0.6 Installera NPM-paket: begäran

Du måste installera paketet **request** som en del av installationen av node.js.

Kör följande kommando för att installera paketet **request**:

```javascript
npm install request
```


Nästa steg: [2.4.1 Konfigurera din Microsoft Azure EventHub-miljö](./ex1.md)

[Gå tillbaka till modul 2.4](./segment-activation-microsoft-azure-eventhub.md)

[Gå tillbaka till Alla moduler](./../../../overview.md)
