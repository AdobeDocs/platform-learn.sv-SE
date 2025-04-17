---
title: Bildruta I/O till Workfront Fusion till AEM Assets
description: Bildruta I/O till Workfront Fusion till AEM Assets
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: f02ecbe4-f1d7-4907-9bbc-04e037546091
source-git-commit: 297fba1810934e6ce4d9b8dfaea0e1250e761ab5
workflow-type: tm+mt
source-wordcount: '1878'
ht-degree: 0%

---

# 1.2.6 Bildruta I/O till Workfront Fusion till AEM Assets

>[!IMPORTANT]
>
>För att slutföra den här övningen måste du ha tillgång till en fungerande AEM Assets CS-redigeringsmiljö. Om du följer övning [Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./../../../modules/asset-mgmt/module2.1/aemcs.md){target="_blank"} har du tillgång till en sådan miljö.

>[!IMPORTANT]
>
>Om du tidigare har konfigurerat ett AEM Assets CS-program med en redigeringsmiljö kan det bero på att din AEM CS-sandlåda har tagits i viloläge. Eftersom det tar 10-15 minuter att dölja en sådan sandlåda, är det en bra idé att börja denavigeringsprocessen nu så att du inte fastnar vid ett senare tillfälle.

I föregående övning konfigurerade du ett scenario som automatiskt genererar varianter av en Adobe Photoshop PSD-fil med Adobe Firefly, Photoshop API:er och Workfront Fusion. Resultatet av det scenariot var en ny Photoshop PSD-fil.

Affärsteamen behöver dock inte ha någon PSD-fil, de behöver en PNG-fil eller en JPG-fil. I den här övningen ska du konfigurera en ny automatisering som resulterar i att en PNG-fil genereras när resursen i bildruta-I/O har godkänts och att PNG-filen lagras i AEM Assets automatiskt.

## 1.2.6.1 Skapa ett nytt scenario

Gå till [https://experience.adobe.com/](https://experience.adobe.com/). Öppna **Workfront Fusion**.

![WF Fusion](./images/wffusion1.png)

Gå till **Scenarier** på den vänstra menyn och markera mappen `--aepUserLdap--`. Klicka på **Skapa ett nytt scenario**.

![Bildruta-I/O](./images/aemf1.png)

Använd namnet `--aepUserLdap-- - Asset Approved PNG AEM Assets`. Klicka sedan på **?**, ange söktermen `webhook` och klicka sedan på **Webbhooks**.

![Bildruta-I/O](./images/aemf2.png)

Klicka på **Anpassad webkrok**.

![Bildruta-I/O](./images/aemf3.png)

Klicka på **Lägg till** om du vill skapa en ny webkrok.

![Bildruta-I/O](./images/aemf4.png)

Använd namnet `--aepUserLdap-- - Frame.io Webhook`. Klicka på **Spara**.

![Bildruta-I/O](./images/aemf5.png)

Du borde se det här då. Klicka på **Kopiera adress till Urklipp**.

![Bildruta-I/O](./images/aemf6.png)

## 1.2.6.2 Konfigurera webkrok i Frame.io

Gå till [https://developer.frame.io/](https://developer.frame.io/). Klicka på **UTVECKLINGSVERKTYG** och välj sedan **Anpassade åtgärder**.

![Bildruta-I/O](./images/aemf7.png)

Klicka på **Skapa en webkrok**.

![Bildruta-I/O](./images/aemf8.png)

Ange följande värden:

- **NAME**: använd `--aepUserLdap-- - Asset Labels Updated`
- **URL**: Ange URL:en för den webkrok som du nyss skapade i Workfront Fusion
- **TEAM**: välj lämpligt Frame.io-team, i det här fallet **One Adobe Tutorial**.

![Bildruta-I/O](./images/aemf9.png)

Bläddra nedåt och aktivera kryssrutan intill **Resursetiketter - uppdaterad**. Klicka på **Skicka**.

![Bildruta-I/O](./images/aemf10.png)

Du borde se det här då.

![Bildruta-I/O](./images/aemf11.png)

Gå till [https://app.frame.io/projects](https://app.frame.io/projects) och gå till mappen som du skapade tidigare, som bör ha namnet `--aepUserLdap--`. Dubbelklicka för att öppna den resurs som skapades i föregående övning.

![Bildruta-I/O](./images/aemf11a.png)

Då borde du se något sådant här. Klicka på fältet **Ingen status** och ändra statusen till **Pågår**.

![Bildruta-I/O](./images/aemf12.png)

Byt tillbaka till Workfront Fusion. Du bör nu se att anslutningen **har identifierats**.

![Bildruta-I/O](./images/aemf13.png)

Klicka på **Spara** för att spara ändringarna och klicka sedan på **Kör en gång** för att göra ett snabbtest.

![Bildruta-I/O](./images/aemf14.png)

Växla tillbaka till Frame.io och klicka på fältet **Pågår** och ändra statusen till **Behöver granskas**.

![Bildruta-I/O](./images/aemf15.png)

Växla tillbaka till Workfront Fusion och klicka på bubblan i modulen **Anpassad webkrok** .

Detaljerad vy av bubblan visar data som tagits emot från Frame.io. Du bör se olika ID:n. Fältet **resource.id** visar till exempel det unika ID:t i Frame.io för resursen **citisign-fiber.psd**.

![Bildruta-I/O](./images/aemf16.png)

## 1.2.6.3 Hämta resursinformation från Frame.io

Nu när kommunikationen mellan Frame.io och Workfront Fusion har upprättats via en anpassad webkrok bör du få mer information om resursen som statusetiketten uppdaterades för. För att göra detta använder du återigen kontakten Frame.io i Workfront Fusion, som i föregående övning.

Klicka på **?** och ange söktermen `frame`. Klicka på **Frame.io**.

![Bildruta-I/O](./images/aemf18.png)

Klicka på **Frame.io (äldre)**.

![Bildruta-I/O](./images/aemf19.png)

Klicka på **Hämta en resurs**.

![Bildruta-I/O](./images/aemf20.png)

Kontrollera att anslutningen är inställd på samma anslutning som du skapade i den tidigare övningen, som bör ha namnet `--aepUserLdap-- - Frame.io Token`.

![Bildruta-I/O](./images/aemf21.png)

Därefter måste du ange **resurs-ID**. **Resurs-ID:t** delas av Frame.io till Workfront Fusion som en del av den inledande **anpassade webkrockkommunikationen** och finns under fältet **resource.id**. Välj **resource.id** och klicka på **OK**.

![Bildruta-I/O](./images/aemf22.png)

Klicka på **Spara** för att spara ändringarna och klicka sedan på **Kör en gång** för att testa konfigurationen.

![Bildruta-I/O](./images/aemf23.png)

Växla tillbaka till Frame.io och klicka på fältet **Behöver granskas** och ändra statusen till **Pågår**.

![Bildruta-I/O](./images/aemf24.png)

Gå tillbaka till Workfront Fusion och klicka på bubblan i modulen **Frame.io - Hämta en resurs**. Du bör då se en liknande översikt.

![Bildruta-I/O](./images/aemf25.png)

I resursinformationen som tillhandahålls av Frame.io hittar du ett fält med namnet **Label** som är inställt på **in_progress**. Du måste använda det fältet i ett senare skede för att konfigurera ett filter.

![Bildruta-I/O](./images/aemf26.png)

## 1.2.6.4 Konvertera till PNG

Håll pekaren över modulen **Frame.io - Hämta en resurs** och klicka på ikonen **+** .

![Bildruta-I/O](./images/aemf27.png)

Ange söktermen `photoshop` och klicka sedan på **Adobe Photoshop**.

![Bildruta-I/O](./images/aemf28.png)

Klicka på **Konvertera bildformat**.

![Bildruta-I/O](./images/aemf29.png)

Kontrollera att fältet **Connection** använder din tidigare skapade anslutning, som har namnet `--aepUserLdap-- - Adobe IO`.

Under **Indata** ställer du in fältet **Lagring** till **Extern** och ställer in **Filplats** till att använda variabeln **Original** som returneras av modulen **Frame.io - Hämta en resurs**.

Klicka sedan på **Lägg till objekt** under **Utdata**.

![Bildruta-I/O](./images/aemf30.png)

För konfigurationen **Utdata** anger du **Lagring** till **Fusion internal storage** och **Type** till **image/png**. Klicka på **Spara**.

![Bildruta-I/O](./images/aemf31.png)

Klicka på **OK**.

![Bildruta-I/O](./images/aemf33.png)

Klicka på **Spara** för att spara ändringarna.

![Bildruta-I/O](./images/aemf32.png)

Därefter bör du konfigurera ett filter så att bara en PNG-fil återges för resurser som har statusen **Godkänd**. Det gör du genom att klicka på ikonen **Rench** mellan modulerna **Frame.io - Hämta en resurs** och **Adobe Photoshop - Konvertera bildformat** och sedan välja **Konfigurera ett filter**.

![Bildruta-I/O](./images/aemf34.png)

Konfigurera följande fält:

- **Etikett**: använd `Is Asset Approved`.
- **Villkor**: markera fältet **Etikett** i svaret från modulen **Frame.io - Hämta en resurs**.
- **Grundläggande operatorer**: välj **Lika med**.
- **Värde**: `approved`.

Klicka på **OK**.

![Bildruta-I/O](./images/aemf35.png)

Klicka på **Spara** för att spara ändringarna och klicka sedan på **Kör en gång** för att testa konfigurationen.

![Bildruta-I/O](./images/aemf36.png)

Växla tillbaka till Frame.io och klicka på fältet **Pågår** och ändra statusen till **Godkänd**.

![Bildruta-I/O](./images/aemf37.png)

Gå tillbaka till Workfront Fusion. Nu bör du se att alla moduler i ditt scenario har körts korrekt. Klicka på bubblan i modulen **Adobe Photoshop - Konvertera bildformat** .

![Bildruta-I/O](./images/aemf38.png)

I informationen om körningen av modulen **Adobe Photoshop - Konvertera bildformat** kan du se att en PNG-fil nu har genererats. Nästa steg är att sedan lagra filen i AEM Assets CS.

![Bildruta-I/O](./images/aemf39.png)

## 1.2.6.5 Lagra PNG i AEM Assets CS

Håll pekaren över modulen **Adobe Photoshop - Konvertera bildformat** och klicka på ikonen **+** .

![Bildruta-I/O](./images/aemf40.png)

Ange söktermen `aem` och välj **AEM Assets**.

![Bildruta-I/O](./images/aemf41.png)

Klicka på **Överför en resurs**.

![Bildruta-I/O](./images/aemf42.png)

Nu måste du konfigurera anslutningen till AEM Assets CS. Klicka på **Lägg till**.

![Bildruta-I/O](./images/aemf43.png)

Använd följande inställningar:

- **Anslutningstyp**: **AEM Assets as a Cloud Service**.
- **Anslutningsnamn**: `--aepUserLdap-- AEM Assets CS`.
- **Instans-URL**: kopiera instans-URL:en för AEM Assets CS-redigeringsmiljön, som ska se ut så här: `https://author-pXXXXX-eXXXXXXX.adobeaemcloud.com`.
- **Fyllningsalternativ för åtkomstinformation**: välj **Tillhandahåll JSON**.

Du måste nu ange autentiseringsuppgifterna för **det tekniska kontot i JSON-format**. För att göra detta finns det ett antal steg som du måste utföra när du använder AEM Cloud Manager. Låt skärmen vara öppen medan du gör det.

![Bildruta-I/O](./images/aemf44.png)

Gå till [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. Organisationen som du bör välja är `--aepImsOrgName--`. Då ser du något sådant här. Klicka för att öppna programmet, som bör ha namnet `--aepUserLdap-- - Citi Signal`.

![Bildruta-I/O](./images/aemf45.png)

Klicka på de tre punkterna **..** och välj **Developer Console**.

![Bildruta-I/O](./images/aemf46.png)

Klicka på **Logga in med Adobe**.

![Bildruta-I/O](./images/aemf47.png)

Du dirigeras sedan till **Developer Console**. Klicka på **Skapa nytt tekniskt konto**.

![Bildruta-I/O](./images/aemf48.png)

Då borde du se något sådant här. Kopiera den fullständiga JSON-nyttolasten till Urklipp.

![Bildruta-I/O](./images/aemf50.png)

Gå tillbaka till Workfront Fusion och klistra in den fullständiga JSON-nyttolasten i fältet **för det tekniska kontot i JSON-format**. Klicka på **Fortsätt**.

![Bildruta-I/O](./images/aemf49.png)

Anslutningen valideras sedan och när den lyckas väljs anslutningen automatiskt i AEM Assets-modulen. Nästa steg är att konfigurera en mapp. Som en del av övningen bör du skapa en ny dedikerad mapp.

![Bildruta-I/O](./images/aemf51.png)

Om du vill skapa en ny dedikerad mapp går du till [https://experience.adobe.com](https://experience.adobe.com/). Kontrollera att rätt Experience Cloud-instans är markerad, som ska vara `--aepImsOrgName--`. Klicka sedan på **Experience Manager Assets**.

![Bildruta-I/O](./images/aemf52.png)

Klicka på **Markera** i din AEM Assets CS-miljö, som bör ha namnet `--aepUserLdap-- - Citi Signal dev`.

![Bildruta-I/O](./images/aemf53.png)

Gå till **Resurser** och klicka på **Skapa mapp**.

![Bildruta-I/O](./images/aemf54.png)

Ange namnet `--aepUserLdap-- - Frame.io PNG` och klicka på **Skapa**.

![Bildruta-I/O](./images/aemf55.png)

Mappen skapas sedan.

![Bildruta-I/O](./images/aemf56.png)

Gå tillbaka till Workfront Fusion, klicka **Klicka här för att välja mapp** och välj sedan mappen `--aepUserLdap-- - Frame.io PNG`.

![Bildruta-I/O](./images/aemf57.png)

Kontrollera att målet är inställt på `--aepUserLdap-- - Frame.io PNG`. Välj sedan **Karta** under **Source-fil**.

Välj variabeln `{{3.filenames[]}}` under **Filnamn**.

Välj variabeln `{{3.files[]}}` under **Data**.

>[!NOTE]
>
>Variabler i Workfront Fusion kan anges manuellt med följande syntax: `{{3.filenames[]}}`. Talet i variabeln refererar till modulen i scenariot. I det här exemplet ser du att den tredje modulen i scenariot heter **Adobe Photoshop - Konvertera bildformat** och har sekvensnumret **3**. Det innebär att variabeln `{{3.filenames[]}}` kommer åt fältet **filnamn[]** från modulen med sekvensnummer 3. Sekvensnummer kan ibland vara olika, så var uppmärksam när du kopierar/klistrar in sådana variabler och kontrollera alltid att det sekvensnummer som används är det rätta.

Klicka på **OK**.

![Bildruta-I/O](./images/aemf58.png)

Klicka på **Spara** för att spara ändringarna.

![Bildruta-I/O](./images/aemf59.png)

Därefter måste du ange specifika behörigheter för det tekniska konto som du nyss skapade. När kontot skapades i **Developer Console** i **Cloud Manager** fick det **läsbehörighet**, men i det här fallet krävs **skrivbehörighet**. Det gör du genom att gå till AEM CS Author.

Gå till [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. Organisationen som du bör välja är `--aepImsOrgName--`. Klicka för att öppna programmet, som bör ha namnet `--aepUserLdap-- - Citi Signal`. Då ser du något sådant här. Klicka på författarens URL.

![Bildruta-I/O](./images/aemf60.png)

Klicka på **Logga in med Adobe**.

![Bildruta-I/O](./images/aemf61.png)

Gå till **Inställningar** > **Säkerhet** > **Användare**.

![Bildruta-I/O](./images/aemf62.png)

Klicka för att öppna användarkontot för det tekniska kontot.

![Bildruta-I/O](./images/aemf63.png)

Gå till **Grupper** och lägg till den här tekniska kontoanvändaren i gruppen **DAM-Users**.

![Bildruta-I/O](./images/aemf64.png)

Klicka på **Spara och stäng**.

![Bildruta-I/O](./images/aemf65.png)

Gå tillbaka till Workfront Fusion. Klicka på **Kör en gång** för att testa ditt scenario.

![Bildruta-I/O](./images/aemf66.png)

Växla tillbaka till Frame.io och se till att resursens status ändras till **Godkänd** igen.

>[!NOTE]
>
>Du kan behöva ändra den först till **Pågår** eller **Behöver granskas** för att sedan ändra tillbaka den till **Godkänd**.

![Bildruta-I/O](./images/aemf15.png)

Ditt Workfront Fusion-scenario aktiveras sedan och slutförs. Genom att visa informationen i bubblan i modulen **AEM Assets** kan du redan se att PNG-filen sparades korrekt i AEM Assets CS.

![Bildruta-I/O](./images/aemf67.png)

Gå tillbaka till AEM Assets CS och öppna mappen `--aepUserLdap-- - Frame.io PNG`. Nu bör du se PNG-filen som skapades som en del av Workfront Fusion-scenariot. Dubbelklicka på filen för att öppna den.

![Bildruta-I/O](./images/aemf68.png)

Nu kan du se mer information om metadata för PNG-filen som genererades.

![Bildruta-I/O](./images/aemf69.png)

Du har nu slutfört den här övningen.

## Nästa steg

Gå till [Sammanfattning och fördelar med Creative Workflow Automation med Workfront Fusion](./summary.md){target="_blank"}

Gå tillbaka till [Creative Workflow Automation med Workfront Fusion](./automation.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../overview.md){target="_blank"}
