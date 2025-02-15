---
title: Komma igång med Firefly Services
description: Lär dig hur du använder Postman och Adobe I/O för att fråga Adobe Firefly Services API:er
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 52385c33-f316-4fd9-905f-72d2d346f8f5
source-git-commit: 5ee9c3b7cde5444ecceca4b01cc275d6263d8a59
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---

# 1.1.1 Komma igång med Firefly Services

Lär dig hur du använder Postman och Adobe I/O för att fråga Adobe Firefly Services API:er.

## 1.1.1.1 Krav

Innan du fortsätter med den här övningen måste du ha slutfört installationen av [ditt Adobe I/O-projekt](./../../../modules/getting-started/gettingstarted/ex6.md), och du måste också ha konfigurerat ett program för interaktion med API:er, som [Postman](./../../../modules/getting-started/gettingstarted/ex7.md) eller [PostBuster](./../../../modules/getting-started/gettingstarted/ex8.md).

## 1.1.1.2 Adobe I/O - access_token

I samlingen **Adobe IO - OAuth** markerar du begäran **POST - Get Access Token** och väljer **Skicka**. Svaret ska innehålla en ny **accestoken**.

![Postman](./images/ioauthresp.png){zoomable="yes"}

## 1.1.1.3 API för Firefly Services, bild 2

Nu när du har en giltig och ny access_token kan du skicka din första begäran till API:er för Firefly Services.

Välj begäran **POST - Firefly - T2I V3** i samlingen **FF - Firefly Services Tech Insiders** .

![Firefly](./images/ff1.png){zoomable="yes"}

Kopiera bild-URL:en från svaret och öppna den i webbläsaren för att visa bilden.

![Firefly](./images/ff2.png){zoomable="yes"}

Du bör se en vacker bild som visar `horses in a field`.

![Firefly](./images/ff3.png){zoomable="yes"}

Du kan spela runt med API-begäran innan du fortsätter med nästa övning.

## Nästa steg

Gå till [Optimera din Firefly-process med Microsoft Azure och försignerade URL:er](./ex2.md){target="_blank"}

Gå tillbaka till [Översikt över Adobe Firefly Services](./firefly-services.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../overview.md){target="_blank"}
