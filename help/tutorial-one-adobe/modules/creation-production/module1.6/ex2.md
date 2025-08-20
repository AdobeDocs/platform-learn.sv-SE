---
title: GenStudio for Performance Marketing Create your Amazon AWS S3 bucket
description: GenStudio for Performance Marketing Create your Amazon AWS S3 bucket
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
source-git-commit: 1dd8b487cbd16e438e9c006c34e458ddb82cce64
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 0%

---

# 1.6.2 Skapa din AWS S3-bucket

## 1.6.2.1 Skapa din S3-bucket

Gå till [https://console.aws.amazon.com](https://console.aws.amazon.com) och logga in.

>[!NOTE]
>
>Om du inte har något AWS-konto än skapar du ett nytt AWS-konto med din personliga e-postadress.

![ETL](./images/awshome.png)

När du har loggat in omdirigeras du till **AWS Management Console**.

![ETL](./images/awsconsole.png)

Sök efter **s3** i sökfältet. Klicka på det första sökresultatet: **S3 - Skalbar lagring i molnet**.

![ETL](./images/awsconsoles3.png)

Därefter visas startsidan för **Amazon S3**. Klicka på **Skapa pyts**.

![ETL](./images/s3home.png)

Använd namnet **på skärmen** Skapa pyts`--aepUserLdap---gspem-dam`.

![ETL](./images/bucketname.png)

Låt alla andra standardinställningar vara som de är. Bläddra nedåt och klicka på **Skapa hink**.

![ETL](./images/createbucket.png)

Då ser du att din bucket skapas och kommer att omdirigeras till Amazon S3-hemsida.

![ETL](./images/S3homeb.png)

## Ange behörigheter för att komma åt S3-bucket

Nästa steg är att konfigurera åtkomst till din S3-bucket.

Gå till [https://console.aws.amazon.com/iam/home](https://console.aws.amazon.com/iam/home) om du vill göra det.

Åtkomsten till AWS-resurser styrs av Amazon Identity and Access Management (IAM).

Du kommer nu att se den här sidan.

![ETL](./images/iam.png)

Klicka på **Användare** på den vänstra menyn. Sedan visas skärmen **Användare**. Klicka på **Skapa användare**.

![ETL](./images/iammenu.png)

Konfigurera sedan användaren:

- Användarnamn: använd `s3_--aepUserLdap--_gspem_dam`

Klicka på **Nästa**.

![ETL](./images/configuser.png)

Då visas den här behörighetsskärmen. Klicka på **Koppla profiler direkt**.

![ETL](./images/perm1.png)

Ange söktermen **s3** om du vill visa alla relaterade S3-principer. Välj principen **AmazonS3FullAccess**. Bläddra nedåt och klicka på **Nästa**.

![ETL](./images/perm2.png)

Granska konfigurationen. Klicka på **Skapa användare**.

![ETL](./images/review.png)

Då ser du det här. Klicka på **Visa användare**.

![ETL](./images/review1.png)

Klicka på **Säkerhetsuppgifter** och sedan på **Skapa åtkomstnyckel**.

![ETL](./images/cred.png)

Välj **Program som körs utanför AWS**. Bläddra nedåt och klicka på **Nästa**.

![ETL](./images/creda.png)

Klicka på **Skapa åtkomstnyckel**

![ETL](./images/credb.png)

Då ser du det här. Klicka på **Visa** för att visa din hemliga åtkomstnyckel:

![ETL](./images/cred1.png)

Din **hemliga åtkomstnyckel** visas nu.

>[!IMPORTANT]
>
>Lagra dina inloggningsuppgifter i en textfil på datorn.
>
> - Åtkomstnyckel-ID: ...
> - Hemlig åtkomstnyckel: ...
>
> När du klickar på **Klar** visas aldrig dina autentiseringsuppgifter igen!

Klicka på **Klar**.

![ETL](./images/cred2.png)

Du har nu skapat en AWS S3-bucket och du har skapat en användare med behörighet att komma åt den här bucket.

## 1.6.2.2 Överför Assets till din S3-bucket

Sök efter **s3** i sökfältet. Klicka på det första sökresultatet: **S3 - Skalbar lagring i molnet**.

![ETL](./images/bucket1.png)

Klicka för att öppna din nyligen skapade S3-bucket, som ska heta `--aepUserLdap---gspem-dam`.

![ETL](./images/bucket2.png)

Klicka på **Överför**.

![ETL](./images/bucket3.png)

Du borde se det här då.

![ETL](./images/bucket4.png)

Du kan hämta CitiSignal-bildfiler [här](./../../asset-mgmt/module2.2/images/CitiSignal_Neon_Rabbit.zip){target="_blank"}.

Exportera filerna till skrivbordet.

![ETL](./images/bucket5.png)

Ta de två bildfilerna i mappen och släpp dem i S3 bucket-överföringsfönstret. Klicka på **Överför**.

![ETL](./images/bucket6.png)

Du borde se det här då. Din S3-bucket, dina bildfiler och din IAM-användare är nu klara att användas av din externa DAM-app.

![ETL](./images/bucket7.png)

## Nästa steg

Gå till [Skapa din externa DAM-app](./ex3.md){target="_blank"}

Gå tillbaka till [GenStudio for Performance Marketing - utökningsbarhet](./genstudioext.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../overview.md){target="_blank"}
