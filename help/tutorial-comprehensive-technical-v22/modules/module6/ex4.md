---
title: CDP för realtid - Bygg ett segment och vidta åtgärder - Skicka segmentet till en S3-destination
description: CDP för realtid - Bygg ett segment och vidta åtgärder - Skicka segmentet till en S3-destination
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 5b0bcd69-7131-48a3-bd3e-773ba95cc42b
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '909'
ht-degree: 1%

---

# 6.4 Vidta åtgärder: skicka segmentet till en S3-destination

Adobe Experience Platform kan också dela målgrupper med e-postmarknadsföringsdestinationer som Salesforce Marketing Cloud, Oracle Eloqua, Oracle Responsys och Adobe Campaign.

Du kan använda FTP eller SFTP som en del av de dedikerade destinationerna för var och en av dessa destinationer för e-postmarknadsföring, eller så kan du använda AWS S3 för att utbyta kundlistor mellan Adobe Experience Platform och dessa destinationer för e-postmarknadsföring.

I den här modulen konfigurerar du ett sådant mål genom att använda en AWS S3-bucket.

## 6.4.1 Skapa din S3-bucket

Gå till [https://console.aws.amazon.com](https://console.aws.amazon.com) och logga in med det Amazon-konto du skapade tidigare.

![ETL](./images/awshome.png)

När du har loggat in omdirigeras du till **AWS Management Console**.

![ETL](./images/awsconsole.png)

I **Hitta tjänster** meny, söka efter **s3**. Klicka på det första sökresultatet: **S3 - Skalbar lagring i molnet**.

![ETL](./images/awsconsoles3.png)

Då ser du **Amazon S3** hemsida. Klicka **Skapa kryss**.

![ETL](./images/s3home.png)

I **Skapa kryss** måste du konfigurera två saker:

- Namn: använd namnet `aepmodulertcdp--demoProfileLdap--`. I den här övningen är Bucket-namnet **aepmodulertcdpvangeluw**
- Region: använd regionen **EU (Frankfurt) eu-central-1**

![ETL](./images/bucketname.png)

Låt alla andra standardinställningar vara som de är. Bläddra nedåt och klicka **Skapa bucket**.

![ETL](./images/createbucket.png)

Då ser du att din bucket skapas och kommer att omdirigeras till Amazon S3-hemsida.

![ETL](./images/S3homeb.png)

## 6.4.2 Ange behörigheter för att komma åt S3-bucket

Nästa steg är att konfigurera åtkomst till din S3-bucket.

Om du vill göra det går du till [https://console.aws.amazon.com/iam/home](https://console.aws.amazon.com/iam/home).

Åtkomsten till AWS-resurser styrs av Amazon Identity and Access Management (IAM).

Du kommer nu att se den här sidan.

![ETL](./images/iam.png)

Klicka på **Användare**. Då ser du **Användare** skärm. Klicka **Lägg till användare**.

![ETL](./images/iammenu.png)

Konfigurera sedan användaren:

- Användarnamn: use `s3_--demoProfileLdap--_rtcdp` som ett namn, så i det här exemplet är namnet `s3_vangeluw_rtcdp`.
- AWS åtkomsttyp: välj **Åtkomstnyckel - programmatisk åtkomst**.

Klicka **Nästa: Behörigheter**.

![ETL](./images/configuser.png)

Då visas den här behörighetsskärmen. Klicka **Koppla befintliga policyer direkt**.

![ETL](./images/perm1.png)

Ange söktermen **s3** för att se alla relaterade S3-policyer. Välj profil **AmazonS3FullAccess**. Klicka **Nästa: Taggar**.

![ETL](./images/perm2.png)

På **Taggar** -skärmen behöver du inte konfigurera något. Klicka **Nästa: Granska**.

![ETL](./images/perm3.png)

Granska konfigurationen. Klicka **Skapa användare**.

![ETL](./images/review.png)

Användaren har nu skapats och du ser dina autentiseringsuppgifter för att få åtkomst till din S3-miljö. Det här är enda gången som du ser dina autentiseringsuppgifter så skriv ned dem.

![ETL](./images/cred.png)

Klicka **Visa** för att se din hemliga åtkomstnyckel:

![ETL](./images/cred1.png)

>[!IMPORTANT]
>
>Lagra dina inloggningsuppgifter i en textfil på datorn.
>
> - Åtkomstnyckel-ID: ...
> - Hemlig åtkomstnyckel: ...
>
> När du har klickat **Stäng** kommer du aldrig att se dina inloggningsuppgifter igen!

Klicka **Stäng**.

![ETL](./images/close.png)

Du har nu skapat en AWS S3-bucket och du har skapat en användare med behörighet att komma åt den här bucket.

## 6.4.3 Konfigurera mål i Adobe Experience Platform

Gå till [Adobe Experience Platform](https://experience.adobe.com/platform). När du loggat in kommer du till Adobe Experience Platform hemsida.

![Dataintag](../module2/images/home.png)

Innan du fortsätter måste du välja en **sandlåda**. Sandlådan som ska markeras har namnet ``--aepSandboxId--``. Du kan göra detta genom att klicka på texten **[!UICONTROL Produktionsprodukt]** i den blå linjen ovanför skärmen. När du har valt lämplig [!UICONTROL sandlåda]kommer du att se skärmändringen och nu är du med på din [!UICONTROL sandlåda].

![Dataintag](../module2/images/sb1.png)

Gå till den vänstra menyn **Destinationer** och sedan gå till **Katalog**. Då ser du **Målkatalog**.

![RTCDP](./images/rtcdpmenudest.png)

Klicka **molnlagring** klickar du på **Konfigurera** knapp (eller på **Aktivera segment**, beroende på din miljö) på **Amazon S3** kort.

![RTCDP](./images/rtcdp2.png)

Beroende på din miljö kan du behöva klicka **+ Konfigurera nytt mål** för att börja skapa destinationen.

![RTCDP](./images/rtcdp2a.png)

Välj **Nytt konto** som kontotyp. Använd de S3-autentiseringsuppgifter som du fick i föregående steg:

| Åtkomstnyckel-ID | Nyckel för hemlig åtkomst |
|:-----------------------:| :-----------------------:|
| AKIA..... | Cm5Ln.... |

Klicka **Anslut till mål**.

![RTCDP](./images/rtcdpsfs3.png)

En visuell bekräftelse visas på att det här målet nu är anslutet.

![RTCDP](./images/rtcdpsfs3connected.png)

Du måste ange ett namn och en mapp så att Adobe Experience Platform kan ansluta till S3-bucket.

Använd följande som namngivningskonvention:

| Åtkomstnyckel-ID | Nyckel för hemlig åtkomst |
|:-----------------------:| :-----------------------:|
| Namn | `AWS - S3 - --demoProfileLdap--` |
| Beskrivning | `AWS - S3 - --demoProfileLdap--` |
| Buckennamn | `aepmodulertcdp--demoProfileLdap--` |
| Mappsökväg | / |

Klicka på **Nästa**.

![RTCDP](./images/rtcdpsfs3connect2.png)

Du kan nu även bifoga en datastyrningspolicy till ditt nya mål. Klicka på **Nästa**.

![RTCDP](./images/rtcdpsfs3connect2gov.png)

I listan med segment söker du efter det segment som du skapade i övning 1 och markerar det. Klicka på **Nästa**.

![RTCDP](./images/s3a.png)

Du kommer då att se det här. Om du vill kan du redigera schemat genom att klicka på **penna** ikon. **Skapa schema**.

![RTCDP](./images/s3bb.png)

Definiera ditt valschema. Välj **Exportera inkrementella filer** och ange frekvensen till **Varje timme** var **3 timmar**. Klicka **Skapa**.

![RTCDP](./images/s3bbc.png)

Du får den här då. Klicka på **Nästa**.

![RTCDP](./images/s3bbca.png)

Nu kan du välja attribut för exporten till AWS S3. Klicka **Lägg till nytt fält** och se till att fältet `--aepTenantId--.identification.core.ecid` läggs till och markeras som **Dedupliceringsnyckel**.

Du kan också lägga till så många andra fält som behövs.

När du har lagt till alla fält klickar du på **Nästa**.

![RTCDP](./images/s3c.png)

Granska konfigurationen. Klicka **Slutför** för att slutföra konfigurationen.

![RTCDP](./images/s3g.png)

Du kommer sedan tillbaka till skärmen Målaktivering och då ser du att ditt segment har lagts till i det här målet.

![RTCDP](./images/s3j.png)

Om du vill lägga till fler segmentexporter kan du klicka **Aktivera segment** för att starta om processen och lägga till fler segment.

![RTCDP](./images/s3k.png)

Nästa steg: [6.5 Vidta åtgärder: skicka segmentet till Adobe Target](./ex5.md)

[Gå tillbaka till modul 6](./real-time-cdp-build-a-segment-take-action.md)

[Gå tillbaka till Alla moduler](../../overview.md)
