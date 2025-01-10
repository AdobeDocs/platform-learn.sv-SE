---
title: Skapa ett Cloud Manager-program
description: Skapa ett Cloud Manager-program
kt: 5342
doc-type: tutorial
source-git-commit: 89611537cad42082af1b9aa753752d5450f103a5
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 0%

---

# 2.1.2 Konfigurera AEM CS-miljö

## 2.1.2.1 Konfigurera GitHub-repo

Gå till [https://github.com](https://github.com). Klicka på **Logga in**.

![AEMCS](./images/aemcssetup1.png)

Ange dina inloggningsuppgifter. Klicka på **Logga in**.

![AEMCS](./images/aemcssetup2.png)

När du har loggat in visas din GitHub-instrumentpanel.

![AEMCS](./images/aemcssetup3.png)

Gå till [https://github.com/AdobeDevXSC/citisignal-one](https://github.com/AdobeDevXSC/citisignal-one). Då ser du det här. Klicka på **Använd den här mallen** och sedan på **Skapa en ny databas**.

![AEMCS](./images/aemcssetup4.png)

Använd **Databasnamnet** före `citisignal`. Ange synligheten till **Privat**. Klicka på **Skapa databas**.

![AEMCS](./images/aemcssetup5.png)

Efter några sekunder har du skapat databasen.

![AEMCS](./images/aemcssetup6.png)

Gå sedan till [https://github.com/apps/aem-code-sync](https://github.com/apps/aem-code-sync). Klicka på **Konfigurera**.

![AEMCS](./images/aemcssetup7.png)

Klicka på ditt GitHub-konto.

![AEMCS](./images/aemcssetup8.png)

Klicka på **Välj bara databaser** och lägg sedan till databasen som du just har skapat. Klicka sedan på **Installera**.

![AEMCS](./images/aemcssetup9.png)

Du får då den här bekräftelsen.

![AEMCS](./images/aemcssetup10.png)

## 2.1.2.2 Uppdatera filen fstab.yaml

Öppna filen `fstab.yaml` genom att klicka på den i GitHub-repon.

![AEMCS](./images/aemcssetup11.png)

Klicka på ikonen **redigera** .

![AEMCS](./images/aemcssetup12.png)

Du måste nu uppdatera värdet för fältet **url** på rad 4.

![AEMCS](./images/aemcssetup13.png)

Du måste ersätta det aktuella värdet med URL:en för AEM CS-miljön i kombination med inställningarna för GitHub-repon.

Detta är det aktuella värdet för URL:en: `https://author-p131639-e1282833.adobeaemcloud.com/bin/franklin.delivery/adobedevxsc/citisignal-one/main`.

Det finns tre delar av URL:en som behöver uppdateras

`https://XXX/bin/franklin.delivery/YYY/ZZZ/main`

XXX bör ersättas med URL:en till AEM CS-redigeringsmiljö.

YYY ska ersättas med ditt GitHub-användarkonto.

ZZZ ska ersättas med namnet på GitHub-databasen som du använde i föregående övning.

Du kan hitta URL:en till AEM CS-redigeringsmiljö genom att gå till [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com). Klicka på ditt **program** för att öppna det.

![AEMCS](./images/aemcs6.png)

Klicka sedan på de 3 punkterna **..** på fliken **Miljö** och klicka på **Visa detaljer**.

![AEMCS](./images/aemcs9.png)

Du kommer då att se din miljöinformation, inklusive URL:en för din **författarmiljö** . Kopiera URL-adressen.

![AEMCS](./images/aemcs10.png)

XXX = `author-p148073-e1511503.adobeaemcloud.com`

För GitHub-användarkontonamnet hittar du det enkelt i webbläsarens URL. I det här exemplet är användarkontonamnet `woutervangeluwe`.

YYY = `woutervangeluwe`

![AEMCS](./images/aemcs11.png)

För GitHub-databasnamnet kan du även hitta det i webbläsarfönstret som du har öppnat i GitHub. I det här fallet är databasnamnet `citisignal`.

ZZZ = `citisignal`

![AEMCS](./images/aemcs12.png)

Dessa tre värden tillsammans leder till den nya URL-adressen som måste konfigureras i filen `fstab.yaml`.

`https://author-p148073-e1511503.adobeaemcloud.com/bin/franklin.delivery/woutervangeluwe/citisignal/main`

Klicka på **Verkställ ändringar..**.

![AEMCS](./images/aemcs13.png)

Klicka på **Verkställ ändringar**.

![AEMCS](./images/aemcs14.png)

Filen `fstab.yaml` har uppdaterats.

## 2.1.2.3 Överföra CitiSignal-resurser

Gå till [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com). Klicka på ditt **program** för att öppna det.

![AEMCS](./images/aemcs6.png)

Klicka sedan på URL:en till din författarmiljö.

![AEMCS](./images/aemcssetup18.png)

Klicka på **Logga in med Adobe**.

![AEMCS](./images/aemcssetup19.png)

Därefter visas din författarmiljö.

![AEMCS](./images/aemcssetup20.png)

URL:en ser ut så här: `https://author-p148073-e1511503.adobeaemcloud.com/ui#/aem/aem/start.html?appId=aemshell`

Du måste nu komma åt **CRX Package Manager** -miljön i AEM. Det gör du genom att ta bort `ui#/aem/aem/start.html?appId=aemshell` från URL:en och ersätta den med `crx/packmgr`, vilket innebär att URL:en ska se ut så här nu:
`https://author-p148073-e1511503.adobeaemcloud.com/crx/packmgr`.
Tryck på **Enter** för att läsa in pakethanterarmiljön

![AEMCS](./images/aemcssetup22.png)

Klicka sedan på **Överför paket**.

![AEMCS](./images/aemcssetup21.png)

Klicka på **Bläddra** för att hitta det paket som ska överföras.

Paketet som ska överföras kallas **citisign-assets.zip** och kan hämtas här: [https://tech-insiders.s3.us-west-2.amazonaws.com/one-adobe/citisignal-assets.zip](https://tech-insiders.s3.us-west-2.amazonaws.com/one-adobe/citisignal-assets.zip).

![AEMCS](./images/aemcssetup23.png)

Markera paketet och klicka på **Öppna**.

![AEMCS](./images/aemcssetup24.png)

Klicka sedan på **OK**.

![AEMCS](./images/aemcssetup25.png)

Paketet kommer sedan att överföras.

![AEMCS](./images/aemcssetup26.png)

Klicka sedan på **Installera** på det paket som du just överförde.

![AEMCS](./images/aemcssetup27.png)

Klicka på **Installera**.

![AEMCS](./images/aemcssetup28.png)

Efter några minuter installeras ditt paket.

![AEMCS](./images/aemcssetup29.png)

Du kan nu stänga det här fönstret.


## 2.1.2.4 Publish CitiSignal-material

Gå till [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com). Klicka på ditt **program** för att öppna det.

![AEMCS](./images/aemcs6.png)

Klicka sedan på URL:en till din författarmiljö.

![AEMCS](./images/aemcssetup18.png)

Klicka på **Logga in med Adobe**.

![AEMCS](./images/aemcssetup19.png)

Därefter visas din författarmiljö. Klicka på **Webbplatser**.

![AEMCS](./images/aemcsassets1.png)

Klicka på **Filer**.

![AEMCS](./images/aemcsassets2.png)

Klicka för att markera mappen **CitiSignal** och klicka sedan på **Hantera publikation**.

![AEMCS](./images/aemcsassets3.png)

Klicka på **Nästa**.

![AEMCS](./images/aemcsassets4.png)

Klicka på **Publish**.

![AEMCS](./images/aemcsassets5.png)

Dina resurser har nu publicerats.

## 2.1.2.5 Skapa CitiSignal-webbplats

Gå till [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com). Klicka på ditt **program** för att öppna det.

![AEMCS](./images/aemcs6.png)

Klicka sedan på URL:en till din författarmiljö.

![AEMCS](./images/aemcssetup18.png)

Klicka på **Logga in med Adobe**.

![AEMCS](./images/aemcssetup19.png)

Därefter visas din författarmiljö. Klicka på **Webbplatser**.

![AEMCS](./images/aemcssetup30.png)

Klicka på **Skapa** och sedan på **Plats från mall**.

![AEMCS](./images/aemcssetup31.png)

Klicka på **Importera**.

![AEMCS](./images/aemcssetup32.png)

Nu måste du importera en förkonfigurerad mall för platsen. Du kan hämta mallen [här](./../../../assets/aem/citisignal-edge-delivery-services-template-0.0.4.zip). Spara filen på skrivbordet.

Markera sedan filen `citisignal-edge-delivery-services-template-0.0.4.zip` och klicka på **Öppna**.

![AEMCS](./images/aemcssetup33.png)

Då ser du det här. Klicka för att välja mallen som du just överförde och klicka sedan på **Nästa**.

![AEMCS](./images/aemcssetup34.png)

Nu måste du fylla i några detaljer.

- Platstitel: använd **CitiSignal**
- Platsnamn: använd **citisign-one**
- GitHub-URL: kopiera URL:en för GitHub-repo som du använde tidigare

![AEMCS](./images/aemcssetup35.png)

Du får den här då. Klicka på **Skapa**.

![AEMCS](./images/aemcssetup36.png)

Webbplatsen håller på att skapas. Det här kan ta några minuter. Klicka på **OK**.

![AEMCS](./images/aemcssetup37.png)

Uppdatera skärmen efter några minuter så ser du din nya CitiSignal-webbplats.

![AEMCS](./images/aemcssetup38.png)

## 2.1.2.6 Webbplatsen Publish CitiSignal

Klicka sedan på kryssrutan framför **CitiSignal**. Klicka sedan på **Hantera publikation**.

![AEMCS](./images/aemcssetup39.png)

Klicka på **Nästa**.

![AEMCS](./images/aemcssetup40.png)

Klicka på **Inkludera underordnade inställningar**.

![AEMCS](./images/aemcssetup41.png)

Klicka för att markera kryssrutan **Inkludera underordnade** och klicka sedan för att avmarkera de andra kryssrutorna. Klicka på **OK**.

![AEMCS](./images/aemcssetup42.png)

Klicka på **Publish**.

![AEMCS](./images/aemcssetup43.png)

Du kommer då att skickas tillbaka hit. Navigera till **CitiSignal** > **us** > **en**. Klicka i kryssrutan framför **index** och klicka sedan på **Redigera**.

![AEMCS](./images/aemcssetup44.png)

Din webbplats öppnas sedan i **Universal Editor**.

![AEMCS](./images/aemcssetup45.png)

Du kan nu även navigera till din webbplats genom att gå till `main--citisignal--woutervangeluwe.aem.live/us/en`



[Gå tillbaka till modul 2.1](./aemcs.md)

[Gå tillbaka till Alla moduler](./../../../overview.md)
