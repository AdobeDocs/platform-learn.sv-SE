---
title: Datainsamling och vidarebefordran av händelser - Vidarebefordra händelser till AWS ekosystem
description: Vidarebefordra händelser till AWS ekosystem
kt: 5342
doc-type: tutorial
exl-id: 87c2c85d-f624-4972-a9c6-32ddf8a39570
source-git-commit: c0537545e4a5d1f1ca21a13d934eb965a4f3aa66
workflow-type: tm+mt
source-wordcount: '1566'
ht-degree: 0%

---

# 2.5.5 Vidarebefordra event till AWS Kinesis &amp; AWS S3

>[!IMPORTANT]
>
>Det är valfritt att slutföra övningen och det kostar inte att använda AWS Kinesis. AWS erbjuder ett kostnadsfritt nivåkonto där du kan testa och konfigurera många tjänster utan kostnad, men AWS Kinesis ingår inte i det kostnadsfria nivåkontot. För att genomföra och testa denna övning kommer det att kosta att använda AWS Kinesis.

## Bra att veta

Adobe Experience Platform har stöd för olika Amazon-tjänster som mål.
Kinesis och S3 är båda [profilexportmål](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html?lang=en) och kan användas som en del av Adobe Experience Platform Real-Time CDP.
Du kan enkelt mata in värdefulla segmenthändelser och tillhörande profilattribut i valfritt system.

I den här övningen får du lära dig hur du konfigurerar en egen Amazon Kinesis-ström för att strömma händelsedata från Adobe Experience Platform Edge-ekosystemet till en molnlagringsplats, som Amazon S3. Detta är användbart om du vill samla in upplevelsehändelser från webb- och mobilsajter och överföra dem till datalagret för analys och operativ rapportering. I allmänhet importeras data batchvis med stora dagliga filimporter, men de visar inte offentliga http-slutpunkter som kan användas i samband med händelsevidarebefordran.

Stöd för ovanstående användningsfall innebär att strömmande data måste buffras eller placeras i en kö innan de skrivs till en fil. Man måste se till att inte öppna filen för skrivåtkomst i flera processer. Att delegera denna uppgift till ett dedikerat system är idealiskt för att skalas fint samtidigt som man säkerställer en hög servicenivå. Det är här Kinesis kommer till undsättningen.

Amazon Kinesis dataströmmar fokuserar på inmatning och lagring av dataströmmar. Kinesis Data Firehose fokuserar på att leverera dataströmmar till utvalda destinationer, till exempel S3-bucket.

Som en del av den här övningen..

- Utför en grundläggande konfiguration av en dataström från Kinesis
- Skapa en Firehows leveransström och använd S3-bucket som mål
- Konfigurera Amazon API-gateway som en rest API-slutpunkt för att ta emot händelsedata
- Vidarebefordra råa händelsedata från Adobe Edge till din Kinesis-ström

## Konfigurera din AWS S3-bucket

Gå till [https://console.aws.amazon.com](https://console.aws.amazon.com) och logga in med ditt Amazon-konto.

![ETL](./../../../modules/rtcdp-b2c/module2.3/images/awshome.png)

När du har loggat in omdirigeras du till **AWS Management Console**.

![ETL](./../../../modules/rtcdp-b2c/module2.3/images/awsconsole.png)

Sök efter **s3** på menyn **Hitta tjänster**. Klicka på det första sökresultatet: **S3 - Skalbar lagring i molnet**.

![ETL](./../../../modules/rtcdp-b2c/module2.3/images/awsconsoles3.png)

Därefter visas startsidan för **Amazon S3**. Klicka på **Skapa pyts**.

![ETL](./../../../modules/rtcdp-b2c/module2.3/images/s3home.png)

På skärmen **Skapa pyts** måste du konfigurera två saker:

- Namn: använd namnet `eventforwarding---aepUserLdap--`.

![ETL](./images/bucketname.png)

Låt alla andra standardinställningar vara som de är. Bläddra nedåt och klicka på **Skapa hink**.

![ETL](./images/createbucket.png)

Då ser du att din bucket skapas och kommer att omdirigeras till Amazon S3-hemsida.

![ETL](./images/S3homeb.png)

## Konfigurera AWS Kinesis dataström

Sök efter **kines** på menyn **Hitta tjänster**. Klicka på det första sökresultatet: **Kinesis - Arbeta med data för realtidsströmning**.

![ETL](./images/kinesis1.png)

Välj **Kinesis-dataströmmar**. Klicka på **Skapa dataström**.

![ETL](./images/kinesis2.png)

Använd `--aepUserLdap---datastream` för **dataströmsnamnet**.

![ETL](./images/kinesis3.png)

Du behöver inte ändra några andra inställningar. Bläddra nedåt och klicka på **Skapa dataström**.

![ETL](./images/kinesis4.png)

Då ser du det här. När dataströmmen har skapats kan du gå vidare till nästa övning.

![ETL](./images/kinesis5.png)

## Konfigurera AWS Firehose Delivery Stream

Sök efter **kines** på menyn **Hitta tjänster**. Klicka på **Kinesis Data Firehose**.

![ETL](./images/kinesis6.png)

Klicka på **Skapa Firefose-ström**.

![ETL](./images/kinesis7.png)

För **Source** väljer du **Amazon Kinesis-dataströmmar**. För **Mål** väljer du **Amazon S3**. Klicka på **Bläddra** för att välja dataström.

![ETL](./images/kinesis8.png)

Välj dataström. Klicka på **Välj**.

![ETL](./images/kinesis9.png)

Då ser du det här. Kom ihåg **Firehose-strömmens namn** som du behöver det senare.

![ETL](./images/kinesis10.png)

Bläddra nedåt tills du ser **målinställningar**. Klicka på **Bläddra** för att välja S3-bucket.

![ETL](./images/kinesis11.png)

Välj S3-bucket och klicka på **Välj**.

![ETL](./images/kinesis12.png)

Då ser du något sådant här. Uppdatera följande inställningar:

- Ny radavgränsare: inställd på **Aktiverad**
- Dynamisk partitionering: inställd på **Inte aktiverad**

![ETL](./images/kinesis13.png)

Bläddra lite till och klicka på **Skapa Firehose-ström**

![ETL](./images/kinesis15.png)

Efter några minuter skapas din Firefose-ström och **Aktiv**.

![ETL](./images/kinesis16.png)

## Skapa IAM-användare

Klicka på **Användare** på den vänstra AWS IAM-menyn. Sedan visas skärmen **Användare**. Klicka på **Skapa användare**.

![ETL](./images/iammenu.png)

Konfigurera sedan användaren:

- Användarnamn: använd `--aepUserLdap--_kinesis_forwarding`

Klicka på **Nästa**.

![ETL](./images/configuser.png)

Då visas den här behörighetsskärmen. Klicka på **Koppla profiler direkt**.

Ange söktermen **kinesbrandhose** om du vill visa alla relaterade principer. Välj principen **AmazonKinesisFirehoseFullAccess**. Bläddra nedåt och klicka på **Nästa**.

![ETL](./images/perm2.png)

Granska konfigurationen. Klicka på **Skapa användare**.

![ETL](./images/review.png)

Då ser du det här. Klicka på **Visa användare**.

![ETL](./images/review1.png)

Klicka på **Lägg till behörigheter** och klicka på **Skapa infogad profil**.

![ETL](./images/pol1.png)

Då ser du det här. Välj tjänsten **Kinesis**.

![ETL](./images/pol2.png)

Gå till **Skriv** och markera kryssrutan för **PutRecord**.

![ETL](./images/pol3.png)

Bläddra ned till **Resurser** och välj **Alla**. Klicka på **Nästa**.

![ETL](./images/pol4.png)

Namnge din princip så här: **Kinesis_PutRecord** och klicka på **Skapa princip**.

![ETL](./images/pol5.png)

Då ser du det här. Klicka på **Säkerhetsuppgifter**.

![ETL](./images/pol6.png)

Klicka på **Skapa åtkomstnyckel**.

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

Du har nu skapat en IAM-användare med rätt behörigheter, som du måste ange när du konfigurerar AWS-tillägget i egenskapen för händelsevidarebefordran.

## Uppdatera egenskapen för händelsevidarebefordran: Tillägg

När du har konfigurerat sekretess och dataelement kan du nu konfigurera tillägget för Google Cloud-plattformen i din händelsevidarebefordringsegenskap.

Gå till [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/), gå till **Händelsevidarebefordran** och öppna egenskapen för händelsevidarebefordran.

![Adobe Experience Platform Data Collection SSF](./images/prop1.png)

Gå sedan till **Tillägg** och till **Katalog**. Klicka på tillägget **AWS** och klicka på **Installera**.

![Adobe Experience Platform Data Collection SSF](./images/awsext1.png)

Ange de IAM-användarautentiseringsuppgifter som du skapade i föregående övning. Klicka på **Spara**.

![Adobe Experience Platform Data Collection SSF](./images/awsext2.png)

Därefter måste du konfigurera en regel som börjar vidarebefordra händelsedata till Kinesis.

## Uppdatera händelsevidarebefordringsegenskapen: Regel

Gå till **Regler** på den vänstra menyn. Klicka för att öppna regeln **Alla sidor** som du skapade i någon av de tidigare övningarna.

![Adobe Experience Platform Data Collection SSF](./images/rlaws1.png)

Då ser du det här. Klicka på ikonen **+** för att lägga till en ny åtgärd.

![Adobe Experience Platform Data Collection SSF](./images/rlaws2.png)

Då ser du det här. Gör följande val:

- Välj **tillägget**: **AWS**
- Välj **åtgärdstyp**: **Skicka data till Kinesis-dataström**
- Namn: **AWS - Skicka data till Kinesis dataström**

Nu bör du se det här:

![Adobe Experience Platform Data Collection SSF](./images/rlaws4.png)

Konfigurera sedan följande:

- Strömnamn: `--aepUserLdap---datastream`
- AWS Region: kontrollera region i AWS Data Stream Setup
- Partitionsnyckel: **0**

Här ser du AWS:

![Adobe Experience Platform Data Collection SSF](./images/partkey.png)

Du borde ha den här nu. Klicka sedan på dataelementikonen för fältet **Data**.

![Adobe Experience Platform Data Collection SSF](./images/rlaws5.png)

Välj **XDM-händelse** och klicka på **Markera**.

![Adobe Experience Platform Data Collection SSF](./images/rlaws5a.png)

Du får den här då. Klicka på **Behåll ändringar**.

![Adobe Experience Platform Data Collection SSF](./images/rlaws5b.png)

Då ser du det här. Klicka på **Spara**.

![Adobe Experience Platform Data Collection SSF](./images/rlaws7.png)

Gå till **Publiceringsflöde** om du vill publicera ändringarna.
Öppna utvecklingsbiblioteket genom att klicka på **Main**.

![Adobe Experience Platform Data Collection SSF](./images/rlaws11.png)

Klicka på knappen **Lägg till alla ändrade resurser** , varefter du ser ändringarna av regeln och dataelementet visas i det här biblioteket. Klicka sedan på **Spara och bygg för utveckling**. Ändringarna distribueras nu.

![Adobe Experience Platform Data Collection SSF](./images/rlaws13.png)

Efter några minuter ser du att distributionen är klar och klar att testas.

![Adobe Experience Platform Data Collection SSF](./images/rl14.png)

## Testa konfigurationen

Gå till [https://dsn.adobe.com](https://dsn.adobe.com). När du har loggat in med din Adobe ID ser du det här. Klicka på de tre punkterna **..** i webbplatsprojektet och klicka sedan på **Kör** för att öppna det.

![DSN](./../../datacollection/module1.1/images/web8.png)

Du kommer då att se din demowebbplats öppnas. Markera URL-adressen och kopiera den till Urklipp.

![DSN](../../gettingstarted/gettingstarted/images/web3.png)

Öppna ett nytt inkognito-webbläsarfönster.

![DSN](../../gettingstarted/gettingstarted/images/web4.png)

Klistra in webbadressen till demowebbplatsen, som du kopierade i föregående steg. Du ombeds sedan logga in med din Adobe ID.

![DSN](../../gettingstarted/gettingstarted/images/web5.png)

Välj kontotyp och slutför inloggningsprocessen.

![DSN](../../gettingstarted/gettingstarted/images/web6.png)

Därefter visas webbplatsen i ett inkognitivt webbläsarfönster. För varje övning måste du använda ett nytt, inkognitivt webbläsarfönster för att läsa in webbadressen till demowebbplatsen.

![DSN](../../gettingstarted/gettingstarted/images/web7.png)

Byt vy till **AWS**. Genom att öppna dataströmmen och gå in på fliken **Övervakning** ser du nu inkommande trafik.

![Adobe Experience Platform Data Collection Setup](./images/hookaws3.png)

När du sedan öppnar dataströmmen för Firefose och går till fliken **Övervakning** visas även inkommande trafik.

![Adobe Experience Platform Data Collection Setup](./images/hookaws4.png)

När du har tittat på S3-bucket kommer du nu att märka att filer skapas där som en följd av att du har lagt in data.

![Adobe Experience Platform Data Collection Setup](./images/hookaws5.png)

När du laddar ned en sådan fil och öppnar den med en textredigerare ser du att den innehåller XDM-nyttolasten från de händelser som vidarebefordrats.

![Adobe Experience Platform Data Collection Setup](./images/hookaws6.png)

>[!IMPORTANT]
>
>När konfigurationen fungerar som väntat ska du inte glömma bort att stänga av dataströmmen och datafältet i AWS Kinesis för att undvika att debiteras!

Nästa steg: [Sammanfattning och förmåner](./summary.md)

[Gå tillbaka till modul 2.5](./aep-data-collection-ssf.md)

[Gå tillbaka till Alla moduler](./../../../overview.md)

