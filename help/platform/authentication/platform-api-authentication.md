---
title: Autentisera och få åtkomst till Experience Platform-API:er
description: Lär dig hur du får tillgång till Adobe Experience Platform-API:er.
role: Developer
feature: API
kt: 3688
thumbnail: 28832.jpeg
exl-id: c1774670-436e-46dd-9c9b-177bfee5f749
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 5%

---

# Autentisera och få åtkomst [!DNL Experience Platform] API:er

För att kunna anropa Adobe Experience Platform API:er måste du först få tillgång till ett Experience Platform-utvecklarkonto.

Stegvisa instruktioner om hur du får tillgång till ett utvecklarkonto finns på [Självstudiekurs om autentisering med Experience Platform API](https://www.adobe.com/go/platform-api-authentication-en).

## Skapa och exportera Experience Platform API till Postman

[Postman](https://www.getpostman.com/) är ett verktyg som gör att utvecklare snabbt och enkelt kan interagera med Adobe Experience Platform API:er.

Adobe Developer Console&#39;s **Exportinformation för Postman** är ett enkelt sätt att exportera all kontoinformation som behövs för att få åtkomst till och interagera med ett Experience Platform-API i en enda Postman-miljöfil, vilket eliminerar behovet av att kopiera och klistra in värden från Adobe Developer Console i Postman.

>[!VIDEO](https://video.tv.adobe.com/v/28832/?quality=12&learn=on)

## Generera en åtkomsttoken med Postman

Använd [Adobe Identity Management Service API:er](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims) för att få en Access Token för åtkomst till Adobe Experience Platform API:er för icke-produktionsanvändning

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)

>[!WARNING]
>
> Som noterades i Postman-samlingen för generering av token för Adobe I/O Access är de angivna genereringsmetoderna lämpliga för icke-produktionsbruk. Lokal signering läser in ett JavaScript-bibliotek från en tredjepartsvärd och fjärrsignering skickar den privata nyckeln till en webbtjänst som ägs och drivs av Adobe. Även om Adobe inte lagrar den här privata nyckeln bör produktionsnycklar aldrig delas med någon.

## Interagera med Adobe I/O API:er med Postman

Utforska interaktion med Adobe I/O API:er med [Adobe-medföljande Experience Platform API Postman-samlingar](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform), som bygger på [Miljövariabler för Adobe I/O](#export-adobe-io-integration-details-to-postman) och [genererad åtkomsttoken](#generate-an-access-token-with-postman).

>[!VIDEO](https://video.tv.adobe.com/v/29704/?quality=12&learn=on)

Observera att Postman-samlingar som tillhandahålls av Adobe kanske inte finns för alla Adobe I/O API:er, men de [Experience Platform API Postman-samlingar](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform) kan användas som guide för hur du definierar egna Postman-samlingar för dessa användningsområden.

## Ytterligare resurser

* [Adobe I/O Console](https://console.adobe.io)
* [Adobe Experience Platform Postman Samples](https://github.com/adobe/experience-platform-postman-samples)
   * [Generering av Adobe I/O Access-token för Postman Collection](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims)
   * [Adobe Experience Platform API:er Postman Collections](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)
* [Ladda ned Postman](https://www.getpostman.com/)
