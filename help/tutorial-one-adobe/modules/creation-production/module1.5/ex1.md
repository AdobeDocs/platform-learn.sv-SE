---
title: Komma igång med Frame.io
description: Komma igång med Frame.io
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
source-git-commit: efb4ecf90a27d00d256c1648e78c6e295199733e
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 0%

---

# 1.5.1 Komma igång med Frame.io

>[!NOTE]
>
> Skärmbilden nedan visar att en viss miljö används. När du går igenom den här självstudiekursen är det troligt att din miljö har ett annat namn. När du registrerade dig för den här självstudiekursen fick du den information om miljön som du skulle använda. Följ dessa instruktioner.

Gå till [https://next.frame.io/](https://next.frame.io/). Kontrollera att du är inloggad i miljön `--aepImsOrgName--`.

![Frame.io](./images/frameio1.png)

Om du inte är inloggad i den högra miljön klickar du på logotypen i det nedre vänstra hörnet och klickar för att välja den miljö du behöver använda.

![Frame.io](./images/frameio2.png)

## 1.5.1.1 Skapa din arbetsyta och ditt projekt

Klicka på **+ Ny Workspace**.

![Frame.io](./images/frameio3.png)

Använd `--aepUserLdap--` som arbetsytans namn. Klicka på **Spara**.

![Frame.io](./images/frameio4.png)

Arbetsytan har skapats. Sedan ska du skapa ett nytt projekt. Klicka på **+ Nytt projekt**.

![Frame.io](./images/frameio5.png)

Välj **Tom** och använd namnet `CitiSignal`. Klicka på **Skapa nytt projekt**.

![Frame.io](./images/frameio6.png)

Ditt projekt har skapats. Nu måste du överföra resurser i ditt projekt. Klicka på **Överför**.

![Frame.io](./images/frameio7.png)

Hämta följande filer: [https://tech-insiders.s3.us-west-2.amazonaws.com/Frame.io_Assets.zip](https://tech-insiders.s3.us-west-2.amazonaws.com/Frame.io_Assets.zip) till skrivbordet och zippa upp dem på skrivbordet.

![Frame.io](./images/frameio8.png)

Markera alla filer och klicka på **Öppna**.

>[!NOTE]
>
>Som du kan se i skärmbilden är mappen **Ljudeffekter** inte markerad just nu. Detta beror på att den manuella överföringen inte stöder överföring av mappar. Om några minuter installerar du appen Frame.io Transfer, som du använder för att överföra mappen och dess filer.

![Frame.io](./images/frameio9.png)

Efter några minuter visas dina filer i Frame.io.

![Frame.io](./images/frameio10.png)

Du har nu överfört filer manuellt, men det finns ett bättre och snabbare sätt att överföra och hämta filer till och från Frame.io. Det bästa sättet att göra det är att använda appen Frame.io Transfer.

## 1.5.1.2 Hämta och konfigurera överföringsappen Frame.io

Gå till [https://frame.io/transfer](https://frame.io/transfer) och hämta datorversionen.

![Frame.io](./images/frameio11.png)

Installera programmet och öppna det sedan.

![Frame.io](./images/frameio12.png)

När programmet öppnas måste du logga in. Klicka på **logga in**.

![Frame.io](./images/frameio13.png)

Ange e-postadressen för ditt Adobe-konto och klicka på **Kör**.

![Frame.io](./images/frameio14.png)

När autentiseringen är klar klickar du på **appen Open Frame.io Transfer**.

![Frame.io](./images/frameio15.png)

Du borde se det här då. Välj rätt miljö genom att klicka för att öppna listrutan.

![Frame.io](./images/frameio16.png)

Välj den miljö som du behöver använda för den här självstudiekursen, som är `--aepImsOrgName--`.

![Frame.io](./images/frameio17.png)

Du bör sedan se arbetsytan och projektet som du skapade tidigare, tillsammans med filerna som du överförde manuellt.

Klicka på **Överför**.

![Frame.io](./images/frameio18.png)

Gå till mappen som du använde tidigare och som innehåller de uppzippade filerna som du laddade ned tidigare. Markera mappen **Ljudeffekter** och klicka på **Överför**.

![Frame.io](./images/frameio19.png)

Dina filer kommer sedan att överföras.

![Frame.io](./images/frameio20.png)

När du har överfört den visas den nya mappen i Frame.io.

![Frame.io](./images/frameio21.png)

## 1.5.1.3 Konfigurera Adobe Premiere Pro Beta

Du har redan installerat Adobe Premiere Pro Beta som en del av modulen Komma igång. Om du vill använda Frame.io i kombination med Adobe Premiere Pro Beta kan du använda det plugin-program som har utvecklats för den här integreringen.

Öppna Creative Cloud-appen och sök efter `frame.io`.

![Frame.io](./images/frameio23.png)

Bläddra nedåt i sökresultaten för att hitta plugin-programmet **Frame.io V4 Comments**. Klicka på den.

![Frame.io](./images/frameio24.png)

Du borde se det här då. Klicka på **Installera**.

![Frame.io](./images/frameio25.png)

Om Adobe Premiere Pro Beta är öppet måste du **Stäng** det innan du kan installera plugin-programmet.

![Frame.io](./images/frameio26.png)

Klicka på **OK**. Plugin-programmet installeras nu.

![Frame.io](./images/frameio27.png)

När plugin-programmet är installerat öppnar du Adobe Premiere Pro Beta på datorn.

![Frame.io](./images/frameio22.png)

## Nästa steg

Gå till [-](./ex1.md){target="_blank"}

Gå tillbaka till [Effektivisera arbetsflödet med Frame.io](./frameio.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../overview.md){target="_blank"}
