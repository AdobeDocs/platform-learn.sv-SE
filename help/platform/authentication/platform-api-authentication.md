---
title: Autentisera och få åtkomst till Experience Platform-API:er
description: Lär dig hur du får tillgång till Adobe Experience Platform-API:er.
feature: API
role: Developer
level: Beginner
jira: KT-3688
thumbnail: 28832.jpeg
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: c1774670-436e-46dd-9c9b-177bfee5f749
source-git-commit: 42427df298e2c5ae734ce050e935378db51e66a1
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 5%

---

# Autentisera och få åtkomst [!DNL Experience Platform] API:er

Lär dig hur du kommer igång med Adobe Experience Platform API:er. Den här självstudiekursen vägleder dig genom processen att skapa inloggningsuppgifter och börja skapa API-begäranden för Experience Platform.

## Skapa ett projekt i Adobe Developer Console och exportera en Postman-miljö{#export-integration-details-to-postman}

[[!DNL Postman]](https://www.postman.com/) är ett tredjepartsprogram som hjälper utvecklare att snabbt och enkelt interagera med Adobe Experience Platform API:er.

[Adobe Developer Console&#39;s](https://developer.adobe.com/console/home) **Exportinformation för Postman** är ett enkelt sätt att exportera den kontoinformation som behövs för att få tillgång till och interagera med ett Experience Platform-API i en enda Postman-miljöfil, vilket eliminerar behovet av att kopiera och klistra in värden från Adobe Developer Console i Postman.

>[!IMPORTANT]
>
>Så här öppnar du [Adobe Developer Console](https://developer.adobe.com/console/home)måste du vara antingen en [Systemadministratör](https://helpx.adobe.com/enterprise/using/admin-roles.html) eller en [Utvecklare](https://helpx.adobe.com/enterprise/using/manage-developers.html#:~:text=Add%20developers%20to%20a%20single%20product%20profile&amp;text=In%20the%20Admin%20Console%2C%20navigate,in%20the%20upper%2Dright%20corner.) i [Adobe Admin Console](https://adminconsole.adobe.com).
>
> När du har skapat API-autentiseringsuppgifterna måste systemadministratören associera dem med en roll i Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/28832/?quality=12&learn=on)




## Generera en åtkomsttoken med Postman{#generate-an-access-token-with-postman}

Använd [Adobe Identity Management Service API:er](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims) för att få en Access Token för att få tillgång till Adobe Experience Platform API:er.

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)


## Interagera med Experience Platform API:er med Postman

Upptäck interaktionen med Adobe Experience Platform API:er med [Adobe-medföljande Experience Platform API Postman-samlingar](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform), som bygger på [Miljövariabler för Adobe Developer Console](#export-integration-details-to-postman) och [genererad åtkomsttoken](#generate-an-access-token-with-postman).

>[!VIDEO](https://video.tv.adobe.com/v/29704/?quality=12&learn=on)


## Resurser som refereras i dessa videoklipp

* [Adobe Developer Console](https://developer.adobe.com/console/home)
* [Adobe Experience Platform Postman Samples](https://github.com/adobe/experience-platform-postman-samples)
   * [Identity Management System Postman Collection för generering av åtkomsttoken](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/ims)
   * [Adobe Experience Platform API Postman Collections](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform)
* [Ladda ned Postman](https://www.postman.com/)
