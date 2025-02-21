---
title: Automatisering med kopplingar
description: Automatisering med kopplingar
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
source-git-commit: 6ef4ce94dbbcd65ab30bcfad24f4ddd746c26b82
workflow-type: tm+mt
source-wordcount: '1721'
ht-degree: 0%

---

# 1.2.4 Automatisering med kontakter

Du kommer nu att börja använda de färdiga anslutningarna i Workfront Fusion för Photoshop och du kopplar ihop Firefly Text-2-Image-begäran och Photoshop-förfrågningarna till ett enda scenario.

## 1.2.4.1 Duplicera och förbered ditt scenario

Gå till **Scenarier** på den vänstra menyn och markera mappen `--aepUserLdap--`. Du bör sedan se scenariot som du skapade tidigare, med namnet `--aepUSerLdap-- - Adobe I/O Authentication`.

![WF Fusion](./images/wffc1.png)

Klicka på pilen för att öppna listrutan och välj **Klona**.

![WF Fusion](./images/wffc2.png)

Ange **namnet** för det klonade scenariot till `--aepUserLdap-- - Firefly + Photoshop` och välj lämpligt **målteam**. Klicka på **Lägg till** om du vill lägga till en ny webkrok.

![WF Fusion](./images/wffc3.png)

Ange **Webkrok-namnet** till `--aepUserLdap-- - Firefly + Photoshop Webhook`. Klicka på **Spara**.

![WF Fusion](./images/wffc4.png)

Du borde se det här då. Klicka på **Spara**.

![WF Fusion](./images/wffc5.png)

Du borde se det här då. Klicka på noden **Webkrok**.

![WF Fusion](./images/wffc6.png)

Klicka på **Kopiera adress till Urklipp** och klicka sedan på **Kontrollera datastrukturen igen**.

![WF Fusion](./images/wffc7.png)

Öppna Postman. Lägg till en ny begäran i samma mapp som du använde tidigare.

![WF Fusion](./images/wffc9.png)

Kontrollera att följande inställningar används:

- Namn på begäran: `POST - Send Request to Workfront Fusion Webhook Firefly + Photoshop`
- Typ av begäran: `POST`
- Begär URL: klistra in den URL du kopierade från webkroken i ditt Workfront Fusion Scenario.

Gå till **Body** och ställ in **Body Type** på **raw** - **JSON**. Klistra in följande nyttolast i **Body**.

```json
{
    "psdTemplate": "citisignal-fiber.psd",
    "xlsFile": "placeholder",
    "prompt":"misty meadows",
    "cta": "Buy this now!",
    "button": "Click here to buy!"
}
```

Denna nya nyttolast säkerställer att all variabelinformation tillhandahålls utanför scenariot i stället för att den hårdkodas i scenariot. I ett företagsscenario måste ett scenario definieras på ett återanvändbart sätt, vilket innebär att ett antal variabler måste anges som indatavariabler i stället för att de ska vara hårdkodade i scenariot.

Du borde ha den här då. Klicka på **Skicka**.

![WF Fusion](./images/wffc10.png)

Workfront Fusion-webbkroken väntar fortfarande på indata.

![WF Fusion](./images/wffc11.png)

När du har klickat på **Skicka** bör meddelandet ändra tp **har identifierats**. Klicka på **OK**.

![WF Fusion](./images/wffc12.png)

## 1.2.4.2 Uppdatera Firefly T2I-nod

Klicka på noden **Firefly T2I**. Du borde se det här då. Frågepanelen i den här begäran har tidigare hårdkodats för **hästar i ett fält**. Du kommer nu att ta bort den hårdkodade texten och ersätta den med ett fält som kommer från webbkroken.

![WF Fusion](./images/wffcfft2i1.png)

Ta bort texten **hästar i ett fält** och ersätt den med variabeln **prompt** som finns under **Webkroks** -variablerna. Klicka på **OK** om du vill spara ändringarna.

![WF Fusion](./images/wffcfft2i2.png)

## 1.2.4.2 Ändra bakgrund för PSD-filen

Du kommer nu att uppdatera ditt scenario så att det blir smartare med färdiga anslutningar. Du kommer också att ansluta utdata från Firefly till Photoshop så att bakgrundsbilden av PSD-filen ändras dynamiskt med hjälp av utdata från Firefly Generate Image-åtgärden.

I föregående övning hade du inaktiverat **Firefly T2I**-vägen. Du borde nu ångra det. Klicka på ikonen **stop** för att aktivera vägen igen.

![WF Fusion](./images/wffc13.png)

Du kommer då att se att ikonen **stop** försvinner. Klicka sedan på ikonen **skiftnyckel** på den andra vägen mot konfigurationen för föregående övning och välj **Inaktivera flöde**.

![WF Fusion](./images/wffc14.png)

Du borde se det här då. Håll sedan markören över **Firefly T2I**-noden och klicka på ikonen **+** .

![WF Fusion](./images/wffc15.png)

Ange `Photoshop` på sökmenyn och klicka sedan på åtgärden **Adobe Photoshop** .

![WF Fusion](./images/wffc16.png)

Välj **Använd PSD-redigeringar**.

![WF Fusion](./images/wffc17.png)

Du borde se det här då. Klicka på **Lägg till** för att lägga till en ny anslutning till Adobe Photoshop.

![WF Fusion](./images/wffc18.png)

Konfigurera anslutningen enligt följande:

- Anslutningstyp: välj **Adobe Photoshop (Server-till-server)**
- Anslutningsnamn: ange `--aepUserLdap-- - Adobe IO`
- Klient-ID: klistra in klient-ID
- Klienthemlighet: klistra in din klienthemlighet

Klicka på **Fortsätt**.

![WF Fusion](./images/wffc19.png)

Om du vill hitta ditt **klient-ID** och **klienthemlighet** går du till [https://developer.adobe.com/console/home](https://developer.adobe.com/console/home){target="_blank"} och öppnar ditt Adobe I/O-projekt, som har namnet `--aepUserLdap-- One Adobe tutorial`. Gå till **OAuth Server-to-Server** för att hitta ditt klient-ID och din klienthemlighet. Kopiera dessa värden och klistra in dem i anslutningsinställningarna i Workfront Fusion.

![WF Fusion](./images/wffc20.png)

När du har klickat på **Fortsätt** visas ett popup-fönster under tiden som dina autentiseringsuppgifter verifieras. När du är klar, borde du se det här.

![WF Fusion](./images/wffc21.png)

Nu måste du ange filplatsen för den PSD-fil som du vill att Fusion ska arbeta med. För **Lagring** väljer du **Azure** och för **Filplats** anger du `{{1.AZURE_STORAGE_URL}}/{{1.AZURE_STORAGE_CONTAINER}}/{{1.AZURE_STORAGE_SAS_READ}}`. Placera markören bredvid den andra `/`. Titta sedan på de tillgängliga variablerna och bläddra nedåt för att hitta variabeln **psdTemplate**. Klicka på variabeln **psdTemplate** för att markera den.

![WF Fusion](./images/wffc22.png)

Du borde se det här då.

![WF Fusion](./images/wffc23.png)

Bläddra ända ned till **Lager**. Klicka på **Lägg till objekt**.

![WF Fusion](./images/wffc24.png)

Du borde se det här då. Nu måste du ange namnet på det lager i Photoshop PSD-mallen som används för filens bakgrund.

![WF Fusion](./images/wffc25.png)

I filen **citisign-fiber.psd** hittar du det lager som användes för bakgrunden. I det här exemplet heter det lagret **2048x2048-background**.

![WF Fusion](./images/wffc26.png)

Klistra in namnet **2048x2048-background** i dialogrutan Workfront Fusion.

![WF Fusion](./images/wffc27.png)

Bläddra nedåt tills du ser **indata**. Nu måste du definiera vad som ska infogas i bakgrundslagret. I det här fallet måste du välja utdata för Firefly T2I-objektet, som innehåller den dynamiskt genererade bilden.

För **Lagring** väljer du **Extern**. Sök efter och hitta variabeln `data.outputs[].image.url` från utdata för **Firefly T2I** -begäran för **filplatsen**.

![WF Fusion](./images/wffc28.png)

Bläddra sedan nedåt tills du ser **Redigera**. Ange **Redigera** till **Ja** och ange **Typ** till **Lager**. Klicka på **Lägg till**.

![WF Fusion](./images/wffc29.png)

Du borde se det här då. Därefter måste du definiera åtgärdens utdata. Klicka på **Lägg till objekt** under **utdata**.

![WF Fusion](./images/wffc30.png)

Välj **Azure** för **Lagring**, klistra in `{{1.AZURE_STORAGE_URL}}/{{1.AZURE_STORAGE_CONTAINER}}/citisignal-fiber-replacedbg.psd{{1.AZURE_STORAGE_SAS_WRITE}}` under **Filplats** och välj **vnd.adobe.photoshop** under **Typ**. Klicka för att aktivera **Visa avancerade inställningar**.

![WF Fusion](./images/wffc31.png)

Under **Avancerade inställningar** väljer du **Ja** om du vill skriva över filer med samma namn.
Klicka på **Lägg till**.

![WF Fusion](./images/wffc32.png)

Du borde ha den här då. Klicka på **OK**.

![WF Fusion](./images/wffc33.png)

## 1.2.4.3 Ändra textlager i PSD-filen

### Text för uppmaning

Håll sedan pekaren över noden **Adobe Photoshop - Tillämpa PSD-redigeringar** och klicka på ikonen **+** .

![WF Fusion](./images/wffc34.png)

Välj **Adobe Photoshop**.

![WF Fusion](./images/wffc35.png)

Välj **Redigera textlager**.

![WF Fusion](./images/wffc36.png)

Du borde se det här då. Välj först din tidigare konfigurerade Adobe Photoshop-anslutning, som ska heta `--aepUserLdap-- Adobe IO`.

Du måste nu definiera platsen för **indatafilen**, som är utdata från föregående steg och under **Lager**, måste du ange **namnet** för textlagret som du vill ändra.

![WF Fusion](./images/wffc37.png)

För **indatafilen** väljer du **Azure** för **indatafilens lagringsutrymme** och ser till att du väljer utdata från den tidigare begäran, **Adobe Photoshop - Tillämpa PSD-redigeringar**, som du kan hämta här: `data[]._links.renditions[].href`

![WF Fusion](./images/wffc37a.png)

Öppna filen **citisign-fiber.psd**. I filen kommer du att märka att lagret som innehåller anropet till åtgärd har namnet **2048x2048-cta**.

![WF Fusion](./images/wffc38.png)

Ange namnet **2048x2048-cta** under **Namn** i dialogrutan.

![WF Fusion](./images/wffc39.png)

Bläddra nedåt tills du ser **Text** > **Innehåll**. Välj variabeln **cta** från Webkroks nyttolast.

![WF Fusion](./images/wffc40.png)

Bläddra nedåt tills du ser **Utdata**. För **Lagring** väljer du **Azure**. Ange platsen nedan för **filplatsen**. Observera att variabeln `{{timestamp}}` har lagts till i filnamnet, som används för att säkerställa att alla filer som genereras har ett unikt namn. Ange även **Type** som **vnd.adobe.photoshop**. Klicka på **OK**.

`{{1.AZURE_STORAGE_URL}}/{{1.AZURE_STORAGE_CONTAINER}}/citisignal-fiber-changed-text-{{timestamp}}.psd{{1.AZURE_STORAGE_SAS_WRITE}}`

![WF Fusion](./images/wffc41.png)

### Knapptext

Högerklicka på noden som du just skapade och välj **Klona**. Detta skapar ett andra liknande objekt.

![WF Fusion](./images/wffc42.png)

Du borde se det här då. Välj först din tidigare konfigurerade Adobe Photoshop-anslutning, som ska heta `--aepUserLdap-- Adobe IO`.

Du måste nu definiera platsen för **indatafilen**, som är utdata från föregående steg och under **Lager**, måste du ange **namnet** för textlagret som du vill ändra.

![WF Fusion](./images/wffc43.png)

För **indatafilen** väljer du **Azure** för **indatafilens lagringsutrymme** och ser till att du väljer utdata från den tidigare begäran, **Adobe Photoshop - Redigera textlager**, som du kan ta här: `data[]._links.renditions[].href`

Öppna filen **citisign-fiber.psd**. I filen kommer du att märka att lagret som innehåller anropet till åtgärd har namnet **2048x2048-button-text**.

![WF Fusion](./images/wffc44.png)

Ange namnet **2048x2048-cta** under **Namn** i dialogrutan.

![WF Fusion](./images/wffc43.png)

Bläddra nedåt tills du ser **Text** > **Innehåll**. Välj variabeln **cta** från Webkroks nyttolast.

![WF Fusion](./images/wffc45.png)

Bläddra nedåt tills du ser **Utdata**. För **Lagring** väljer du **Azure**. Ange platsen nedan för **filplatsen**. Observera att variabeln `{{timestamp}}` har lagts till i filnamnet, som används för att säkerställa att alla filer som genereras har ett unikt namn. Ange även **Type** som **vnd.adobe.photoshop**. Klicka på **OK**.

`{{1.AZURE_STORAGE_URL}}/{{1.AZURE_STORAGE_CONTAINER}}/citisignal-fiber-changed-text-{{timestamp}}.psd{{1.AZURE_STORAGE_SAS_WRITE}}`

![WF Fusion](./images/wffc46.png)

Klicka på **Spara** för att spara ändringarna.

![WF Fusion](./images/wffc47.png)

## 1.2.4.4 Webkrok-svar

När du har tillämpat dessa ändringar i din Photoshop-fil måste du nu konfigurera ett **Webkrok-svar** som skickas tillbaka till det program som aktiverat det här scenariot.

Håll pekaren över noden **Adobe Photoshop - Redigera textlager** och klicka på ikonen **+** .

![WF Fusion](./images/wffc48.png)

Sök efter **webkrok** och välj **Webkrok**.

![WF Fusion](./images/wffc49.png)

Välj **Webkrok-svar**.

![WF Fusion](./images/wffc50.png)

Du borde se det här då. Klistra in nyttolasten nedan i **Body**.

```json
{
    "newPsdTemplate": ""
}
```

![WF Fusion](./images/wffc51.png)

Välj sökvägen `data[]._links.renditions[].href` från utdata från föregående begäran. Aktivera kryssrutan för **Visa avancerade inställningar** och klicka sedan på **Lägg till objekt**.

![WF Fusion](./images/wffc52.png)

Ange `Content-Type` i fältet **Nyckel**. Ange `application/json` i fältet **Värde**. Klicka på **Spara**.

![WF Fusion](./images/wffc52a.png)

Du borde ha den här då. Klicka på **OK**.

![WF Fusion](./images/wffc53.png)

Klicka på **Autojustera**.

![WF Fusion](./images/wffc54.png)

Du borde se det här då. Klicka på **Kör en gång**.

![WF Fusion](./images/wffc55.png)

Gå tillbaka till Postman och klicka på **Skicka**. Uppmaningen som används här är **mister-metadata**.

![WF Fusion](./images/wffc56.png)

Scenariot aktiveras sedan och efter en stund visas ett svar i Postman som innehåller URL:en för den nyligen skapade PSD-filen.

![WF Fusion](./images/wffc58.png)

Som en påminnelse: när scenariot har körts i Workfront Fusion kan du visa information om varje nod genom att klicka på bubblan ovanför varje nod.

![WF Fusion](./images/wffc59.png)

Med Azure Storage Explorer kan du sedan hitta och öppna den nya PSD-filen genom att dubbelklicka på den i Azure Storage Explorer.

![WF Fusion](./images/wffc60.png)

Filen bör sedan se ut så här, med bakgrunden som ersätts av en bakgrund med **mister-metadata**.

![WF Fusion](./images/wffc61.png)

Om du kör ditt scenario en gång till och sedan skickar en ny begäran från Postman via en annan uppmaning, kommer du att se hur enkelt och återanvändbart ditt scenario har blivit. I det här exemplet används den nya uppmaningen **solöde**.

![WF Fusion](./images/wffc62.png)

Några minuter senare har en ny PSD-fil skapats med en ny bakgrund.

![WF Fusion](./images/wffc63.png)

## Nästa steg

Gå till [Sammanfattning och fördelar med Firefly Services Automation](./summary.md){target="_blank"}

Gå tillbaka till [Automatisera Adobe Firefly-tjänster](./automation.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../overview.md){target="_blank"}
