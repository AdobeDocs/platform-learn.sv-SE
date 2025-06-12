---
title: Konfigurera AEM CS-miljön
description: Konfigurera AEM CS-miljön
kt: 5342
doc-type: tutorial
exl-id: 62715072-0257-4d07-af1a-8becbb793459
source-git-commit: 457e7d0dec233edf75717fb9930585a3511bdc65
workflow-type: tm+mt
source-wordcount: '991'
ht-degree: 0%

---

# 1.1.3 Konfigurera AEM CS-miljön

## 1.1.3.1 Konfigurera GitHub-repo

Gå till [https://github.com](https://github.com){target="_blank"}. Klicka på **Logga in**.

![AEMCS](./images/aemcssetup1.png){zoomable="yes"}

Ange dina inloggningsuppgifter. Klicka på **Logga in**.

![AEMCS](./images/aemcssetup2.png){zoomable="yes"}

När du har loggat in visas din GitHub-instrumentpanel.

![AEMCS](./images/aemcssetup3.png){zoomable="yes"}

Gå till [https://github.com/AdobeDevXSC/citisignal-one](https://github.com/AdobeDevXSC/citisignal-one){target="_blank"}. Då ser du det här. Klicka på **Använd den här mallen** och sedan på **Skapa en ny databas**.

![AEMCS](./images/aemcssetup4.png){zoomable="yes"}

Använd `citisignal` som **databasnamn**. Ange synligheten till **Privat**. Klicka på **Skapa databas**.

![AEMCS](./images/aemcssetup5.png){zoomable="yes"}

Efter några sekunder har du skapat databasen.

![AEMCS](./images/aemcssetup6.png){zoomable="yes"}

Gå sedan till [https://github.com/apps/aem-code-sync](https://github.com/apps/aem-code-sync){target="_blank"}. Klicka på **Konfigurera**.

![AEMCS](./images/aemcssetup7.png){zoomable="yes"}

Klicka på ditt GitHub-konto.

![AEMCS](./images/aemcssetup8.png){zoomable="yes"}

Klicka på **Välj bara databaser** och lägg sedan till databasen som du just har skapat. Klicka sedan på **Installera**.

![AEMCS](./images/aemcssetup9.png){zoomable="yes"}

Du får då den här bekräftelsen.

![AEMCS](./images/aemcssetup10.png){zoomable="yes"}

## 1.1.3.2 Uppdatera filen fstab.yaml

Öppna filen `fstab.yaml` genom att klicka på den i GitHub-repon.

![AEMCS](./images/aemcssetup11.png){zoomable="yes"}

Klicka på ikonen **redigera** .

![AEMCS](./images/aemcssetup12.png){zoomable="yes"}

Du måste nu uppdatera värdet för fältet **url** på rad 4.

![AEMCS](./images/aemcssetup13.png){zoomable="yes"}

Du måste ersätta det aktuella värdet med URL:en för din specifika AEM CS-miljö i kombination med inställningarna för GitHub-repon.

Detta är det aktuella värdet för URL:en: `https://author-p131639-e1282833.adobeaemcloud.com/bin/franklin.delivery/adobedevxsc/citisignal-one/main`.

Det finns tre delar av URL:en som behöver uppdateras

`https://XXX/bin/franklin.delivery/YYY/ZZZ/main`

XXX bör ersättas av URL:en till AEM CS Author environment.

YYY ska ersättas med ditt GitHub-användarkonto.

ZZZ ska ersättas med namnet på GitHub-databasen som du använde i föregående övning.

Du kan hitta URL:en till din AEM CS-redigeringsmiljö genom att gå till [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. Klicka på ditt **program** för att öppna det.

![AEMCS](./images/aemcs6.png){zoomable="yes"}

Klicka sedan på de 3 punkterna **..** på fliken **Miljö** och klicka på **Visa detaljer**.

![AEMCS](./images/aemcs9.png){zoomable="yes"}

Du kommer då att se din miljöinformation, inklusive URL:en för din **författarmiljö** . Kopiera URL-adressen.

![AEMCS](./images/aemcs10.png){zoomable="yes"}

XXX = `author-p148073-e1511503.adobeaemcloud.com`

För GitHub-användarkontonamnet hittar du det enkelt i webbläsarens URL. I det här exemplet är användarkontonamnet `woutervangeluwe`.

YYY = `woutervangeluwe`

![AEMCS](./images/aemcs11.png){zoomable="yes"}

För GitHub-databasnamnet kan du även hitta det i webbläsarfönstret som du har öppnat i GitHub. I det här fallet är databasnamnet `citisignal`.

ZZZ = `citisignal`

![AEMCS](./images/aemcs12.png){zoomable="yes"}

Dessa tre värden tillsammans leder till den nya URL-adressen som måste konfigureras i filen `fstab.yaml`.

`https://author-p148073-e1511503.adobeaemcloud.com/bin/franklin.delivery/woutervangeluwe/citisignal/main`

Klicka på **Verkställ ändringar..**.

![AEMCS](./images/aemcs13.png){zoomable="yes"}

Klicka på **Verkställ ändringar**.

![AEMCS](./images/aemcs14.png){zoomable="yes"}

Filen `fstab.yaml` har uppdaterats.

## 1.1.3.3 Överför CitiSignal-resurser

Gå till [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. Klicka på ditt **program** för att öppna det.

![AEMCS](./images/aemcs6.png){zoomable="yes"}

Klicka sedan på URL:en till din författarmiljö.

![AEMCS](./images/aemcssetup18.png){zoomable="yes"}

Klicka på **Logga in med Adobe**.

![AEMCS](./images/aemcssetup19.png){zoomable="yes"}

Därefter visas din författarmiljö.

![AEMCS](./images/aemcssetup20.png){zoomable="yes"}

URL:en ser ut så här: `https://author-p148073-e1511503.adobeaemcloud.com/ui#/aem/aem/start.html?appId=aemshell`

Du måste nu komma åt **CRX Package Manager**-miljön i AEM. Det gör du genom att ta bort `ui#/aem/aem/start.html?appId=aemshell` från URL:en och ersätta den med `crx/packmgr`, vilket innebär att URL:en ska se ut så här nu:
`https://author-p148073-e1511503.adobeaemcloud.com/crx/packmgr`.
Tryck på **Enter** för att läsa in pakethanterarmiljön

![AEMCS](./images/aemcssetup22.png){zoomable="yes"}

Klicka sedan på **Överför paket**.

![AEMCS](./images/aemcssetup21.png){zoomable="yes"}

Klicka på **Bläddra** för att hitta det paket som ska överföras.

Paketet som ska överföras kallas **citisign-assets.zip** och kan hämtas här: [https://tech-insiders.s3.us-west-2.amazonaws.com/one-adobe/citisignal-assets.zip](https://tech-insiders.s3.us-west-2.amazonaws.com/one-adobe/citisignal-assets.zip){target="_blank"}.

![AEMCS](./images/aemcssetup23.png){zoomable="yes"}

Markera paketet och klicka på **Öppna**.

![AEMCS](./images/aemcssetup24.png){zoomable="yes"}

Klicka sedan på **OK**.

![AEMCS](./images/aemcssetup25.png){zoomable="yes"}

Paketet kommer sedan att överföras.

![AEMCS](./images/aemcssetup26.png){zoomable="yes"}

Klicka sedan på **Installera** på det paket som du just överförde.

![AEMCS](./images/aemcssetup27.png){zoomable="yes"}

Klicka på **Installera**.

![AEMCS](./images/aemcssetup28.png){zoomable="yes"}

Efter några minuter installeras ditt paket.

![AEMCS](./images/aemcssetup29.png){zoomable="yes"}

Du kan nu stänga det här fönstret.


## 1.1.3.4 Publicera CitiSignal-resurser

Gå till [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. Klicka på ditt **program** för att öppna det.

![AEMCS](./images/aemcs6.png){zoomable="yes"}

Klicka sedan på URL:en till din författarmiljö.

![AEMCS](./images/aemcssetup18.png){zoomable="yes"}

Klicka på **Logga in med Adobe**.

![AEMCS](./images/aemcssetup19.png){zoomable="yes"}

Därefter visas din författarmiljö. Klicka på **Assets**.

![AEMCS](./images/aemcsassets1.png){zoomable="yes"}

Klicka på **Filer**.

![AEMCS](./images/aemcsassets2.png){zoomable="yes"}

Klicka för att markera mappen **CitiSignal** och klicka sedan på **Hantera publikation**.

![AEMCS](./images/aemcsassets3.png){zoomable="yes"}

Klicka på **Nästa**.

![AEMCS](./images/aemcsassets4.png){zoomable="yes"}

Klicka på **Publicera**.

![AEMCS](./images/aemcsassets5.png){zoomable="yes"}

Dina resurser har nu publicerats.

## 1.1.3.5 Skapa CitiSignal-webbplats

Gå till [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. Klicka på ditt **program** för att öppna det.

![AEMCS](./images/aemcs6.png){zoomable="yes"}

Klicka sedan på URL:en till din författarmiljö.

![AEMCS](./images/aemcssetup18.png){zoomable="yes"}

Klicka på **Logga in med Adobe**.

![AEMCS](./images/aemcssetup19.png){zoomable="yes"}

Därefter visas din författarmiljö. Klicka på **Webbplatser**.

![AEMCS](./images/aemcssetup30.png){zoomable="yes"}

Klicka på **Skapa** och sedan på **Plats från mall**.

![AEMCS](./images/aemcssetup31.png){zoomable="yes"}

Klicka på **Importera**.

![AEMCS](./images/aemcssetup32.png){zoomable="yes"}

Nu måste du importera en förkonfigurerad mall för platsen. Du kan hämta mallen [här](./../../../assets/aem/citisignal-edge-delivery-services-template-0.0.4.zip){target="_blank"}. Spara filen på skrivbordet.

Markera sedan filen `citisignal-edge-delivery-services-template-0.0.4.zip` och klicka på **Öppna**.

![AEMCS](./images/aemcssetup33.png){zoomable="yes"}

Då ser du det här. Klicka för att välja mallen som du just överförde och klicka sedan på **Nästa**.

![AEMCS](./images/aemcssetup34.png){zoomable="yes"}

Nu måste du fylla i några detaljer.

- Platstitel: använd **CitiSignal**
- Platsnamn: använd **citisign-one**
- GitHub-URL: kopiera URL:en för GitHub-repo som du använde tidigare

![AEMCS](./images/aemcssetup35.png){zoomable="yes"}

Du får den här då. Klicka på **Skapa**.

![AEMCS](./images/aemcssetup36.png){zoomable="yes"}

Webbplatsen håller på att skapas. Det här kan ta några minuter. Klicka på **OK**.

![AEMCS](./images/aemcssetup37.png){zoomable="yes"}

Uppdatera skärmen efter några minuter så ser du din nya CitiSignal-webbplats.

![AEMCS](./images/aemcssetup38.png){zoomable="yes"}

## 1.1.3.6 Publicera CitiSignal-webbplats

Klicka sedan på kryssrutan framför **CitiSignal**. Klicka sedan på **Hantera publikation**.

![AEMCS](./images/aemcssetup39.png){zoomable="yes"}

Klicka på **Nästa**.

![AEMCS](./images/aemcssetup40.png){zoomable="yes"}

Klicka på **Inkludera underordnade inställningar**.

![AEMCS](./images/aemcssetup41.png){zoomable="yes"}

Klicka för att markera kryssrutan **Inkludera underordnade** och klicka sedan för att avmarkera de andra kryssrutorna. Klicka på **OK**.

![AEMCS](./images/aemcssetup42.png){zoomable="yes"}

Klicka på **Publicera**.

![AEMCS](./images/aemcssetup43.png){zoomable="yes"}

Du kommer då att skickas tillbaka hit. Navigera till **CitiSignal** > **us** > **en**. Klicka i kryssrutan framför **index** och klicka sedan på **Redigera**.

![AEMCS](./images/aemcssetup44.png){zoomable="yes"}

Din webbplats öppnas sedan i **Universal Editor**.

![AEMCS](./images/aemcssetup45.png){zoomable="yes"}

Du kan nu komma åt din webbplats genom att gå till `main--citisignal--XXX.aem.page/us/en/` och/eller `main--citisignal--XXX.aem.live/us/en/` efter att du ersatt XXX med ditt GitHub-användarkonto, som i det här exemplet är `woutervangeluwe`.

I det här exemplet blir den fullständiga URL:en följande:
`https://main--citisignal--woutervangeluwe.aem.page/us/en/` och/eller `https://main--citisignal--woutervangeluwe.aem.live/us/en/`.

Det kan ta en stund innan alla resurser visas korrekt, eftersom de måste publiceras först.

Då ser du det här:

![AEMCS](./images/aemcssetup46.png){zoomable="yes"}

Efter några minuter läses alla resurser in korrekt.

![AEMCS](./images/aemcssetup47.png){zoomable="yes"}

## 1.1.3.7 Testa sidprestanda

Gå till [https://pagespeed.web.dev/](https://pagespeed.web.dev/){target="_blank"}. Ange din URL och klicka på **Analysera**.

![AEMCS](./images/aemcssetup48.png){zoomable="yes"}

Då ser du att er webbplats, både i mobilvisualisering och i datorvisualisering, får högsta poäng:

**Mobil**:

![AEMCS](./images/aemcssetup49.png){zoomable="yes"}

**Skrivbord**:

![AEMCS](./images/aemcssetup50.png){zoomable="yes"}

Nästa steg: [1.1.4 Konfigurera ett anpassat block](./ex4.md){target="_blank"}

Gå tillbaka till [Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./aemcs.md){target="_blank"}

[Gå tillbaka till alla moduler](./../../../overview.md){target="_blank"}
