---
title: Konfigurera AEM CS-miljön
description: Konfigurera AEM CS-miljön
kt: 5342
doc-type: tutorial
exl-id: 62715072-0257-4d07-af1a-8becbb793459
source-git-commit: 15adbf950115f0b6bb6613e69a60b310f25de058
workflow-type: tm+mt
source-wordcount: '1178'
ht-degree: 0%

---

# 1.1.2 Konfigurera AEM CS-miljön

## 1.1.2.1 Konfigurera GitHub-repo

Gå till [https://github.com](https://github.com){target="_blank"}. Klicka på **Logga in**.

![AEMCS](./images/aemcssetup1.png)

Ange dina inloggningsuppgifter. Klicka på **Logga in**.

![AEMCS](./images/aemcssetup2.png)

När du har loggat in visas din GitHub-instrumentpanel.

![AEMCS](./images/aemcssetup3.png)

Gå till [https://github.com/adobe-rnd/aem-boilerplate-xcom](https://github.com/adobe-rnd/aem-boilerplate-xcom){target="_blank"}. Då ser du det här. Klicka på **Använd den här mallen** och sedan på **Skapa en ny databas**.

![AEMCS](./images/aemcssetup4.png)

Använd **som** databasnamn`citisignal-aem-accs`. Ange synligheten till **Privat**. Klicka på **Skapa databas**.

![AEMCS](./images/aemcssetup5.png)

Efter några sekunder har du skapat databasen.

![AEMCS](./images/aemcssetup6.png)

Gå sedan till [https://github.com/apps/aem-code-sync](https://github.com/apps/aem-code-sync){target="_blank"}. Klicka på **Installera** eller **Konfigurera**.

![AEMCS](./images/aemcssetup7.png)

Klicka på knappen **Fortsätt** bredvid ditt GitHub-användarkonto.

![AEMCS](./images/aemcssetup8.png)

Klicka på **Konfigurera** bredvid ditt GitHub-användarkonto.

![AEMCS](./images/aemcssetup8a.png)

Klicka på **Välj bara databaser** och lägg sedan till databasen som du just har skapat.

![AEMCS](./images/aemcssetup9.png)

Bläddra nedåt och klicka på **Spara**.

![AEMCS](./images/aemcssetup9a.png)

Du får då den här bekräftelsen.

![AEMCS](./images/aemcssetup10.png)

## 1.1.2.2 Uppdatera filen fstab.yaml

Öppna filen `fstab.yaml` genom att klicka på den i GitHub-repon.

![AEMCS](./images/aemcssetup11.png)

Klicka på ikonen **redigera** .

![AEMCS](./images/aemcssetup12.png)

Du måste nu uppdatera värdet för fältet **url** på rad 3.

![AEMCS](./images/aemcssetup13.png)

Du måste ersätta det aktuella värdet med URL:en för din specifika AEM Sites CS-miljö i kombination med inställningarna för GitHub-repon.

Detta är det aktuella värdet för URL:en: `https://author-p130360-e1272151.adobeaemcloud.com/bin/franklin.delivery/adobe-rnd/aem-boilerplate-xcom/main`.

Det finns tre delar av URL:en som behöver uppdateras

`https://XXX/bin/franklin.delivery/YYY/ZZZ/main`

XXX bör ersättas av URL:en till AEM CS Author environment.

YYY ska ersättas med ditt GitHub-användarkonto.

ZZZ ska ersättas med namnet på GitHub-databasen som du använde i föregående övning.

Du kan hitta URL:en till din AEM CS-redigeringsmiljö genom att gå till [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. Klicka på ditt **program** för att öppna det.

![AEMCS](./images/aemcs6.png)

Klicka sedan på de 3 punkterna **..** på fliken **Miljö** och klicka på **Visa detaljer**.

![AEMCS](./images/aemcs9.png)

Du kommer då att se din miljöinformation, inklusive URL:en för din **författarmiljö** . Kopiera URL-adressen.

![AEMCS](./images/aemcs10.png)

XXX = `author-p166717-e1786231.adobeaemcloud.com`

För GitHub-användarkontonamnet hittar du det enkelt i webbläsarens URL. I det här exemplet är användarkontonamnet `woutervangeluwe`.

YYY = `woutervangeluwe`

![AEMCS](./images/aemcs11.png)

För GitHub-databasnamnet kan du även hitta det i webbläsarfönstret som du har öppnat i GitHub. I det här fallet är databasnamnet `citisignal`.

ZZZ = `citisignal-aem-accs`

![AEMCS](./images/aemcs12.png)

Dessa tre värden tillsammans leder till den nya URL-adressen som måste konfigureras i filen `fstab.yaml`.

`https://author-p166717-e1786231.adobeaemcloud.com/bin/franklin.delivery/woutervangeluwe/citisignal-aem-accs/main`

Klicka på **Verkställ ändringar..**.

![AEMCS](./images/aemcs13.png)

Klicka på **Verkställ ändringar**.

![AEMCS](./images/aemcs14.png)

Filen `fstab.yaml` har uppdaterats.

## 1.1.2.3 Överför CitiSignal-resurser och -plats

Gå till [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. Klicka på ditt **program** för att öppna det.

![AEMCS](./images/aemcs6.png)

Klicka sedan på URL:en till din författarmiljö.

![AEMCS](./images/aemcssetup18.png)

Klicka på **Logga in med Adobe**.

![AEMCS](./images/aemcssetup19.png)

Därefter visas din författarmiljö.

![AEMCS](./images/aemcssetup20.png)

URL:en ser ut så här: `https://author-p166717-e1786231.adobeaemcloud.com/ui#/aem/aem/start.html?appId=aemshell`

Du måste nu komma åt **CRX Package Manager**-miljön i AEM. Det gör du genom att ta bort `ui#/aem/aem/start.html?appId=aemshell` från URL:en och ersätta den med `crx/packmgr`, vilket innebär att URL:en ska se ut så här nu:
`https://author-p166717-e1786231.adobeaemcloud.com/crx/packmgr`.
Tryck på **Enter** för att läsa in pakethanterarmiljön

![AEMCS](./images/aemcssetup22.png)

Klicka sedan på **Överför paket**.

![AEMCS](./images/aemcssetup21.png)

Klicka på **Bläddra** för att hitta det paket som ska överföras.

Paketet som ska överföras kallas **citisign-assets.zip** och kan hämtas här: [https://one-adobe-tech-insiders.s3.us-west-2.amazonaws.com/one-adobe/citisignal_aem_accs.zip](https://one-adobe-tech-insiders.s3.us-west-2.amazonaws.com/one-adobe/citisignal_aem_accs.zip){target="_blank"}.

![AEMCS](./images/aemcssetup23.png)

Markera paketet `citisignal_aem_accs.zip` och klicka på **Öppna**.

![AEMCS](./images/aemcssetup24.png)

Klicka sedan på **OK**.

![AEMCS](./images/aemcssetup25.png)

Paketet kommer sedan att överföras. Klicka sedan på **Installera** på det paket som du just överförde.

![AEMCS](./images/aemcssetup27.png)

Klicka på **Installera**.

![AEMCS](./images/aemcssetup28.png)

Efter några minuter installeras ditt paket.

![AEMCS](./images/aemcssetup29.png)

Du kan nu stänga det här fönstret.

## 1.1.2.4 Publicera CitiSignal-resurser

Gå till [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. Klicka på ditt **program** för att öppna det.

![AEMCS](./images/aemcs6.png)

Klicka sedan på URL:en till din författarmiljö.

![AEMCS](./images/aemcssetup18.png)

Klicka på **Logga in med Adobe**.

![AEMCS](./images/aemcssetup19.png)

Därefter visas din författarmiljö. Klicka på **Assets**.

![AEMCS](./images/aemcsassets1.png)

Klicka på **Filer**.

![AEMCS](./images/aemcsassets2.png)

Klicka för att markera mappen **CitiSignal** och klicka sedan på **Hantera publikation**.

![AEMCS](./images/aemcsassets3.png)

Klicka på **Nästa**.

![AEMCS](./images/aemcsassets4.png)

Klicka på **Publicera**.

![AEMCS](./images/aemcsassets5.png)

Dina resurser har nu publicerats.

## 1.1.2.5 Publicera CitiSignal-webbplats

Klicka på produktnamnet **Adobe Experience Manager** i det övre vänstra hörnet av skärmen och klicka sedan på **pilen** bredvid **Assets**.

![AEMCS](./images/aemcssetup30a.png)

Klicka sedan på **Webbplatser**.

![AEMCS](./images/aemcssetup30.png)

Du bör sedan se webbplatsen **CitiSignal** som skapades när paketet installerades tidigare.

![AEMCS](./images/aemcssetup31.png)

Om du vill länka din plats till GitHub-databasen som du skapade tidigare måste du skapa en **Edge Delivery Services-konfiguration**.

Det första steget att göra det är att skapa en **molnkonfiguration**.

Det gör du genom att klicka på **Adobe Experience Manager**-produktnamnet i det övre vänstra hörnet av skärmen, klicka på **verktygsikonen** och sedan på **Allmänt** . Klicka för att öppna **Konfigurationsläsaren**.

![AEMCS](./images/aemcssetup31a.png)

Du borde se det här då. Klicka på **Skapa**

![AEMCS](./images/aemcssetup31b.png)

Ställ in fälten **Titel** och **Namn** på `CitiSignal`. Aktivera kryssrutan för **molnkonfigurationer**.

Klicka på **Skapa**.

![AEMCS](./images/aemcssetup31c.png)

Du borde ha den här då.

![AEMCS](./images/aemcssetup31d.png)

Därefter måste du uppdatera några fält i den **molnkonfiguration** som du nyss skapade.

Det gör du genom att klicka på produktnamnet **Adobe Experience Manager** i det övre vänstra hörnet på skärmen, klicka på ikonen **tools** och sedan välja **molntjänster** . Klicka för att öppna **Edge Delivery Services Configuration**.

![AEMCS](./images/aemcssetup32.png)

Välj **CitiSignal**, klicka på **Skapa** och välj **Konfiguration**.

![AEMCS](./images/aemcssetup31e.png)

Du måste nu fylla i fälten **Organisation** och **Platsnamn**. Om du vill göra det måste du först ha en sökväg till URL:en för din GitHub-databas.

![AEMCS](./images/aemcssetup31f.png)

- **Organisation**: använd namnet på din GitHub-organisation, i det här exemplet är det `woutervangeluwe`
- **Platsnamn**: använd namnet på GitHub-databasen som ska vara `citisignal-aem-accs`.

Klicka på **Spara och stäng**.

![AEMCS](./images/aemcssetup33.png)

Du borde ha den här då. Markera kryssrutan framför din nya Edge Cloud-konfiguration och klicka på **Publicera**.

![AEMCS](./images/aemcssetup34.png)

## 1.1.2.6 Uppdatera filsökvägar.json

Öppna filen `paths.json` genom att klicka på den i GitHub-repon.

![AEMCS](./images/aemcssetupjson1.png)

Klicka på ikonen **redigera** .

![AEMCS](./images/aemcssetupjson2.png)

Du måste nu uppdatera ersättningstexten `aem-boilerplate-commerce` med `CitiSignal` på raderna 3, 4, 5, 6, 7 och 10.

Klicka på **Verkställ ändringar**.

![AEMCS](./images/aemcssetupjson3.png)

Klicka på **Verkställ ändringar**.

![AEMCS](./images/aemcssetupjson4.png)

Filen `paths.json` har uppdaterats.

## 1.1.2.7 Publicera CitiSignal-webbplats

Klicka på **Adobe Experience Manager**-produktnamnet i skärmens övre vänstra hörn och välj sedan **Webbplatser**.

![AEMCS](./images/aemcssetup38.png)

Klicka sedan på kryssrutan framför **CitiSignal**. Klicka sedan på **Hantera publikation**.

![AEMCS](./images/aemcssetup39.png)

Klicka på **Nästa**.

![AEMCS](./images/aemcssetup40.png)

Klicka på **Inkludera underordnade inställningar**.

![AEMCS](./images/aemcssetup41.png)

Klicka för att markera kryssrutan **Inkludera underordnade** och klicka sedan för att avmarkera de andra kryssrutorna. Klicka på **OK**.

![AEMCS](./images/aemcssetup42.png)

Klicka på **Publicera**.

![AEMCS](./images/aemcssetup43.png)

Du kommer då att skickas tillbaka hit. Klicka på **CitiSignal**, markera kryssrutan framför **index** och klicka sedan på **Redigera**.

![AEMCS](./images/aemcssetup44.png)

Din webbplats öppnas sedan i **Universal Editor**.

![AEMCS](./images/aemcssetup45.png)

Du kan nu komma åt din webbplats genom att gå till `main--citisignal-aem-accs--XXX.aem.page` och/eller `main--citisignal-aem-accs--XXX.aem.live` efter att du ersatt XXX med ditt GitHub-användarkonto, som i det här exemplet är `woutervangeluwe`.

I det här exemplet blir den fullständiga URL:en följande:
`https://main--citisignal-aem-accs--woutervangeluwe.aem.page` och/eller `https://main--citisignal-aem-accs--woutervangeluwe.aem.live`.

Det kan ta en stund innan alla resurser visas korrekt, eftersom de måste publiceras först.

Då ser du det här:

![AEMCS](./images/aemcssetup46.png)

## 1.1.2.8 Testa sidprestanda

Gå till [https://pagespeed.web.dev/](https://pagespeed.web.dev/){target="_blank"}. Ange din URL och klicka på **Analysera**.

![AEMCS](./images/aemcssetup48.png)

Då ser du att er webbplats, både i mobilvisualisering och i datorvisualisering, får högsta poäng:

**Mobil**:

![AEMCS](./images/aemcssetup49.png)

**Skrivbord**:

![AEMCS](./images/aemcssetup50.png)

Nästa steg: [Utveckla ett anpassat block](./ex3.md){target="_blank"}

Gå tillbaka till [Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./aemcs.md){target="_blank"}

[Gå tillbaka till alla moduler](./../../../overview.md){target="_blank"}
