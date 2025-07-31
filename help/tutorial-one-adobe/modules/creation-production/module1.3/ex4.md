---
title: GenStudio for Performance Marketing Create Email Experience for AJO
description: GenStudio for Performance Marketing Create Email Experience for AJO
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 9837c076-e6ca-47a0-96b9-5fa5fdba3fd2
source-git-commit: 10f1f6a1f77c41e3c912b3d03b73da7b6c68670c
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 0%

---

# 1.3.4 Skapa e-postupplevelse för AJO

>[!IMPORTANT]
>
>För att kunna slutföra den här övningen måste du ha tillgång till en Adobe Journey Optimizer-miljö som är avsedd för integrering med GenStudio for Performance Marketing, som för närvarande är en betaversion.

>[!IMPORTANT]
>
>För att kunna utföra alla steg i den här övningen måste du ha tillgång till en befintlig Adobe Workfront-miljö, och i den miljön måste du ha skapat ett projekt och ett arbetsflöde för godkännande. Om du följer övningen [Arbetsflödeshantering med Adobe Workfront](./../../../modules/workflow-planning/module1.2/workfront.md){target="_blank"} har du tillgång till de nödvändiga inställningarna.

## 1.3.4.1 Skapa och godkänn e-postupplevelse

Gå till **Skapa** på den vänstra menyn. Välj **E-post**.

![SGPeM](./images/gsemail1.png)

Välj mallen **E-post** som du importerade tidigare, med namnet `--aepUserLdap---citisignal-email-template`. Klicka på **Använd**.

![SGPeM](./images/gsemail2.png)

Du borde se det här då. Ändra namnet på din annons till `--aepUserLdap-- - Email Online Gamers Fiber Max`.

![SGPeM](./images/gsemail3.png)

Välj följande alternativ under **Parametrar**:

- **Varumärke**: `--aepUserLdap-- - CitiSignal`
- **Språk**: `English (US)`
- **Persona**: `--aepUserLdap-- - Online Gamers`
- **Produkt**: `--aepUserLdap-- - CitiSignal Fiber Max`

Klicka på **Välj från innehåll**.

![SGPeM](./images/gsemail4.png)

Välj resursen `--aepUserLdap-- - neon rabbit.png`. Klicka på **Använd**.

![SGPeM](./images/gsemail5.png)

Skriv uppmaningen `convince online gamers to start playing online multiplayer games using CitiSignal internet` och klicka på **Generera**.

![SGPeM](./images/gsemail6.png)

Du bör då se något sådant, med 4 e-postvarianter genererade. I standardvyn visas vyn **mobile**. Du kan växla till skrivbordsvyn genom att klicka på ikonen **computer** .

![SGPeM](./images/gsemail7.png)

För varje e-postmeddelande beräknas ett poängtal automatiskt. Klicka på musikspåret för mer information.

![SGPeM](./images/gsemail8.png)

Klicka på **Visa och åtgärda problem**.

![SGPeM](./images/gsemail9.png)

Du kan sedan se mer ingående vad du kan göra för att optimera komplikationspoängen.

![SGPeM](./images/gsemail10.png)

Klicka sedan på **Begär godkännande** som ansluter till Adobe Workfront.

![SGPeM](./images/gsemail11.png)

Välj ditt Adobe Workfront-projekt, som ska få namnet `--aepUserLdap-- - CitiSignal Fiber Launch`. Ange din egen e-postadress under **Bjud in personer** och kontrollera att din roll är inställd på **Godkännare**.

![SGPeM](./images/gsemail12.png)

Du kan också använda ett befintligt arbetsflöde för godkännande i Adobe Workfront. Det gör du genom att klicka på **Använd mall** och välja mallen `--aepuserLdap-- - Approval Workflow`. Klicka på **Skicka**.

![SGPeM](./images/gsemail13.png)

Klicka på **Visa kommentarer i Workfront** så skickas du nu till Adobe Workfront korrekturrundgränssnitt.

![SGPeM](./images/gsemail14.png)

Klicka på **Fatta beslut** i Adobe Workfront Proof UI.

![SGPeM](./images/gsemail15.png)

Välj **Godkänd** och klicka på **Fatta beslut**.

![SGPeM](./images/gsemail16.png)

Klicka på **Publicera**.

![SGPeM](./images/gsemail17.png)

Välj din kampanj `--aepUserLdap-- - CitiSignal Fiber Launch Campaign` och klicka på **Publicera**.

![SGPeM](./images/gsemail18.png)

Klicka på **Öppna i innehåll**.

![SGPeM](./images/gsemail19.png)

De fyra e-postupplevelserna är nu tillgängliga under **Innehåll** > **Erfarenheter**.

![SGPeM](./images/gsemail20.png)

## 1.3.4.2 Skapa en kampanj i AJO

Logga in på Adobe Journey Optimizer på [Adobe Experience Cloud](https://experience.adobe.com). Klicka på **Journey Optimizer**.

![ACOP](./../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Du omdirigeras till vyn **Hem** i Journey Optimizer. Kontrollera först att du använder rätt sandlåda. Sandlådan som ska användas kallas `--aepSandboxName--`. Du kommer sedan att vara i vyn **Hem** i din sandlåda `--aepSandboxName--`.

![ACOP](./../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

Nu ska ni skapa en kampanj. Till skillnad från den händelsebaserade resan från föregående övning, som bygger på inkommande upplevelsehändelser, målgruppsposter eller utträde för att utlösa en resa för en viss kund, riktar kampanjer sig mot en hel målgrupp en gång med unikt innehåll som nyhetsbrev, engångskampanjer eller allmän information eller regelbundet med liknande innehåll som skickas regelbundet, till exempel födelsedagskampanjer och påminnelser.

Gå till **Kampanjer** på menyn och klicka på **Skapa kampanj**.

![Journey Optimizer](./images/gsemail21.png)

Välj **Schemalagd - marknadsföring** och klicka på **Skapa**.

![Journey Optimizer](./images/gsemail22.png)

Konfigurera följande när kampanjen skapas:

- **Namn**: `--aepUserLdap--  - Online Gamers CitiSignal Fiber Max`.
- **Beskrivning**: Fiberkampanj för onlinespel

Klicka på **Åtgärder**.

![Journey Optimizer](./images/gsemail23.png)

Klicka på **+ Lägg till åtgärd** och välj sedan **E-post**.

![Journey Optimizer](./images/gsemail24.png)

Välj sedan en befintlig **e-postkonfiguration** och klicka sedan på **Redigera innehåll**.

![Journey Optimizer](./images/gsemail25.png)

Då ser du det här. Använd följande för **Subject line**:

```
{{profile.person.name.firstName}}, say goodbye to delays!
```

Klicka sedan på **Redigera innehåll**.

![Journey Optimizer](./images/gsemail26.png)

Klicka på **Importera HTML**.

![Journey Optimizer](./images/gsemail27.png)

Klicka sedan på knappen för **Adobe GenStudio for Performance Marketing**.

![Journey Optimizer](./images/gsemail28.png)

Du bör då se ett popup-fönster som visar alla e-postupplevelser som publicerats i GenStudio for Performance Marketing. Välj en av de tillgängliga e-postupplevelserna och klicka på **Använd**.

![Journey Optimizer](./images/gsemail29.png)

Välj en egen AEM Assets CS-databas som ska ha namnet `--aepUserLdap-- - CitiSignal dev` och klicka på **Importera**.

![Journey Optimizer](./images/gsemail30.png)

Du borde se det här då. Markera knappen för saknad bild och klicka på **Välj en resurs**.

![Journey Optimizer](./images/gsemail31.png)

Gå till den mapp som ser ut så här, med början från **GenStudio.zip....** och markera bilden `--aepUserLdap-- - neon rabbit.png`. CLick **Select**

![Journey Optimizer](./images/gsemail32.png)

Du borde se det här då.

![Journey Optimizer](./images/gsemail33.png)

Bläddra nedåt till sidfoten, markera ordet **Avsluta prenumeration** och klicka på ikonen **länk** .

![Journey Optimizer](./images/gsemail38.png)

Ange **Type** till **External Opt-out/Unsubscription** och ange URL:en till `https://techinsiders.org/unsubscribe.html` (det är inte tillåtet att ha en tom URL för länken för att avbryta prenumerationen).

Klicka på **Spara** och sedan på **pilen** i skärmens övre vänstra hörn för att gå tillbaka till kampanjkonfigurationen.

![Journey Optimizer](./images/gsemail39.png)

Gå till **målgrupp**.

![Journey Optimizer](./images/gsemail34.png)

Klicka på **Välj målgrupp**.

![Journey Optimizer](./images/gsemail35.png)

Välj målgrupp för prenumerationslistan för onlinespel, som ska få namnet `--aepUserLdap--_SL_Interest_Online_Gaming`. Klicka på **Spara**.

![Journey Optimizer](./images/gsemail36.png)

Klicka på **Granska för att aktivera**.

![Journey Optimizer](./images/gsemail37.png)

Om kampanjkonfigurationen inte har några problem kan du klicka på **Aktivera**.

![Journey Optimizer](./images/gsemail40.png)

Din kampanj kommer sedan att aktiveras, vilket tar några minuter.

![Journey Optimizer](./images/gsemail41.png)

Efter några minuter är kampanjen aktiv och e-postmeddelandet skickas till den prenumerationslista du valt.

![Journey Optimizer](./images/gsemail42.png)

Du har nu avslutat den här övningen.

## Nästa steg

Gå till [Sammanfattning och förmåner](./summary.md){target="_blank"}

Gå tillbaka till [GenStudio for Performance Marketing](./genstudio.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../overview.md){target="_blank"}
