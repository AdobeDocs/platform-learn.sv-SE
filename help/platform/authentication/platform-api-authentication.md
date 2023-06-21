---
title: Autentisera och få åtkomst till Experience Platform-API:er
description: Lär dig hur du får tillgång till Adobe Experience Platform-API:er.
role: Developer
feature: API
kt: 3688
thumbnail: 28832.jpeg
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: c1774670-436e-46dd-9c9b-177bfee5f749
source-git-commit: 60f509ef55ce121f572466a8f13953dba982a0ce
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 7%

---

# Autentisera och få åtkomst [!DNL Experience Platform] API:er

Om du vill göra förfrågningar till Adobe Experience Platform API:er måste du ha ett Experience Platform-utvecklarkonto.

## Skapa ett projekt i Adobe Developer Console och exportera en Postman-miljö

[[!DNL Postman]](https://www.postman.com/) är ett verktyg som gör att utvecklare snabbt och enkelt kan interagera med Adobe Experience Platform API:er.

Adobe Developer Console&#39;s **Exportinformation för Postman** är ett enkelt sätt att exportera all kontoinformation som behövs för att få åtkomst till och interagera med ett Experience Platform-API i en enda Postman-miljöfil, vilket eliminerar behovet av att kopiera och klistra in värden från Adobe Developer Console i Postman.

>[!VIDEO](https://video.tv.adobe.com/v/28832/?quality=12&learn=on)

>[!IMPORTANT]
>
>När du har skapat API-autentiseringsuppgifterna måste en systemadministratör på ditt företag associera autentiseringsuppgifterna med en Experience Platform-roll.


## Generera en åtkomsttoken med Postman

Använd [Adobe Identity Management Service API:er](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims) för att få en Access Token för att få tillgång till Adobe Experience Platform API:er.

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)


## Interagera med Experience Platform API:er med Postman

Upptäck interaktionen med Adobe Experience Platform API:er med [Adobe-medföljande Experience Platform API Postman-samlingar](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform), som bygger på [Miljövariabler för Adobe Developer Console](#export-adobe-io-integration-details-to-postman) och [genererad åtkomsttoken](#generate-an-access-token-with-postman).

>[!VIDEO](https://video.tv.adobe.com/v/29704/?quality=12&learn=on)


## Ytterligare resurser

* [Adobe Developer Console](https://developer.adobe.com/console/home)
* [Adobe Experience Platform Postman Samples](https://github.com/adobe/experience-platform-postman-samples)
   * [Identity Management System Postman Collection för generering av åtkomsttoken](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims)
   * [Adobe Experience Platform API Postman Collections](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)
* [Ladda ned Postman](https://www.postman.com/)
