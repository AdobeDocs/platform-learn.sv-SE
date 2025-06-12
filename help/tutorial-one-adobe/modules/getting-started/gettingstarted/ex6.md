---
title: Komma igång - Adobe I/O
description: Komma igång - Adobe I/O
kt: 5342
doc-type: tutorial
exl-id: 00f17d4f-a2c8-4e8e-a1ff-556037a60629
source-git-commit: a1da1c73cbddacde00211190a1ca3d36f7a2c329
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 0%

---

# Konfigurera ditt Adobe I/O-projekt

## Skapa ett Adobe I/O-projekt

I den här övningen används Adobe I/O för att fråga olika Adobe-slutpunkter. Följ de här stegen för att konfigurera Adobe I/O.

Gå till [https://developer.adobe.com/console/home](https://developer.adobe.com/console/home){target="_blank"}.

![Adobe I/O Ny integrering](./images/iohome.png)

Se till att du väljer rätt instans i skärmens övre högra hörn. Din instans är `--aepImsOrgName--`.

>[!NOTE]
>
> På skärmbilden nedan visas en viss organisation som valts. När du går igenom den här självstudiekursen är det troligt att din organisation har ett annat namn. När du registrerade dig för den här självstudiekursen fick du den information om miljön som du skulle använda. Följ dessa instruktioner.

Välj sedan **Skapa nytt projekt**.

![Adobe I/O Ny integrering](./images/iocomp.png)

### FIREFLY SERVICES API

>[!IMPORTANT]
>
>Beroende på vilken utbildningsväg du valt kanske du inte har tillgång till Firefly Services API. Du har bara åtkomst till Firefly Services API om du är på utbildningsvägen **Firefly**, **Workfront Fusion**, **ALL** eller när du deltar i ett **direktsänt, personligt seminarium**. Du kan hoppa över det här steget om du inte är på någon av dessa inlärningsvägar.

Du borde se det här då. Välj **+ Lägg till i projekt** och välj **API**.

![Adobe I/O Ny integrering](./images/adobe_io_access_api.png)

Skärmen bör se ut så här.

![Adobe I/O Ny integrering](./images/api1.png)

Markera **Creative Cloud** och välj **Firefly - Firefly Services**. Välj sedan **Nästa**.

![Adobe I/O Ny integrering](./images/api3.png)

Ange ett namn för dina autentiseringsuppgifter: `--aepUserLdap-- - One Adobe OAuth credential` och välj **Nästa**.

![Adobe I/O Ny integrering](./images/api4.png)

Välj standardprofilen **Standardkonfiguration för Firefly Services** och välj **Spara konfigurerat API**.

![Adobe I/O Ny integrering](./images/api9.png)

Du borde se det här då.

![Adobe I/O Ny integrering](./images/api10.png)

### PHOTOSHOP SERVICES API

>[!IMPORTANT]
>
>Beroende på vilken utbildningsväg du valt kanske du inte har tillgång till Photoshop Services API. Du har bara åtkomst till Photoshop Services API om du är på utbildningsvägen **Firefly**, **Workfront Fusion**, **ALL** eller när du deltar i ett **direktsänt, personligt seminarium**. Du kan hoppa över det här steget om du inte är på någon av dessa inlärningsvägar.
>
>Välj **+ Lägg till i projekt** och välj sedan **API**.

![Azure Storage](./images/ps2.png)

Markera **Creative Cloud** och välj **Photoshop - Firefly Services**. Välj **Nästa**.

![Azure Storage](./images/ps3.png)

Välj **Nästa**.

![Azure Storage](./images/ps4.png)

Därefter måste du välja en produktprofil som definierar vilka behörigheter som är tillgängliga för den här integreringen.

Välj **Standardkonfiguration för Firefly Services** och **Standardkonfiguration för Creative Cloud Automation Services**.

Välj **Spara konfigurerat API**.

![Azure Storage](./images/ps5.png)

Du borde se det här då.

![Adobe I/O Ny integrering](./images/ps7.png)

### ADOBE EXPERIENCE PLATFORM API

>[!IMPORTANT]
>
>Beroende på vilken utbildningsväg du valt kanske du inte har tillgång till Adobe Experience Platform API. Du har bara åtkomst till Adobe Experience Platform API om du är på utbildningsvägen **AEP + appar**, **ALL** eller om du deltar i en **personlig**-workshop. Du kan hoppa över det här steget om du inte är på någon av dessa inlärningsvägar.

Välj **+ Lägg till i projekt** och välj sedan **API**.

![Azure Storage](./images/aep1.png)

Välj **Adobe Experience Platfrom** och välj **Experience Platform API**. Välj **Nästa**.

![Azure Storage](./images/aep2.png)

Välj **Nästa**.

![Azure Storage](./images/aep3.png)

Därefter måste du välja en produktprofil som definierar vilka behörigheter som är tillgängliga för den här integreringen.

Välj **Adobe Experience Platform - Alla användare - PROD**.

>[!NOTE]
>
>Namnet på produktprofilen för AEP beror på hur miljön konfigurerades. Om du inte ser produktprofilen ovan kan du ha en produktprofil som kallas **Standardåtkomst för produktion**. Om du är osäker på vilken du ska välja frågar du AEP systemadministratör.

Välj **Spara konfigurerat API**.

![Azure Storage](./images/aep4.png)

Du borde se det här då.

![Adobe I/O Ny integrering](./images/aep5.png)

### Frame.io API

>[!IMPORTANT]
>
>Beroende på vilken utbildningsväg du valt kanske du inte har tillgång till Frame.io API. Du har bara åtkomst till Frame.io API om du är på utbildningsvägen **Workfront Fusion**, **ALL** eller om du deltar i en **personlig**-workshop. Du kan hoppa över det här steget om du inte är på någon av dessa inlärningsvägar.

Välj **+ Lägg till i projekt** och välj sedan **API**.

![Azure Storage](./images/fiops2.png)

Markera **Creative Cloud** och välj **API:t Frame.io**. Välj **Nästa**.

![Azure Storage](./images/fiops3.png)

Välj **Server-till-server-autentisering** och klicka sedan på **Nästa**.

![Azure Storage](./images/fiops4.png)

Välj **OAuth Server-to-Server** och klicka sedan på **Nästa**.

![Azure Storage](./images/fiops5.png)

Därefter måste du välja en produktprofil som definierar vilka behörigheter som är tillgängliga för den här integreringen.

Välj **Default Frame.io Enterprise - Prime Configuration** och klicka på **Spara konfigurerat API**.

![Azure Storage](./images/fiops6.png)

Du borde se det här då.

![Adobe I/O Ny integrering](./images/fiops7.png)

### Projektnamn

Klicka på projektnamnet.

![Adobe I/O Ny integrering](./images/api13.png){zoomable="yes"}

Välj **Redigera projekt**.

![Adobe I/O Ny integrering](./images/api14.png){zoomable="yes"}

Ange ett eget namn för integreringen: `--aepUserLdap-- One Adobe tutorial` och välj **Spara**.

![Adobe I/O Ny integrering](./images/api15.png){zoomable="yes"}

Installationen av ditt Adobe I/O-projekt är nu klar.

![Adobe I/O Ny integrering](./images/api16.png){zoomable="yes"}

## Nästa steg

Gå till [Alternativ 1: Postman-konfiguration](./ex7.md){target="_blank"}

Gå till [Alternativ 2: PostBuster-konfiguration](./ex8.md){target="_blank"}

Gå tillbaka till [Komma igång](./getting-started.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../overview.md){target="_blank"}
