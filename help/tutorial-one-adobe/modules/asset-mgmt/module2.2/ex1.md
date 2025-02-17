---
title: Komma igång med Workfront
description: Komma igång med Workfront
kt: 5342
doc-type: tutorial
exl-id: 7ed76d37-5d3e-49c7-b3d3-ebcfe971896d
source-git-commit: dd075b0296c6ba06d72b229145635060c2c6abb1
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 0%

---

# 1.2.1 Komma igång med Workfront

Logga in på Adobe Workfront på [https://experienceplatform.my.workfront.com/](https://experienceplatform.my.workfront.com/){target="_blank"}.

Då ser du det här.

![WF](./images/wfb1.png)

## 1.2.1.1 Konfigurera din AEM Assets-integrering

Klicka på ikonen **hamburger** med nio punkter och välj sedan **Konfigurera**.

![WF](./images/wfb2.png)

Bläddra nedåt till **Dokument** på den vänstra menyn och klicka sedan på **Experience Manager Assets**.

![WF](./images/wfb3.png)

Klicka på **+ Lägg till Experience Manager-integrering**.

![WF](./images/wfb4.png)

Använd `--aepUserLdap-- - Citi Signal AEM` för integreringens namn.

Öppna listrutan **Experience Manager-databas** och välj din AEM CS-instans, som bör ha namnet `--aepUserLdap-- - Citi Signal`.

![WF](./images/wfb5.png)

Konfigurera följande mappning under **Metadata**:

| Workfront Field | Experience Manager Assets |
| --------------- | ------------------------------ | 
| **Dokument** > **Namn** | **wm:documentName** |
| **Projekt** > **Beskrivning** | **wm:projectDescription** |
| **Aktivitet** > **Namn** | **wm:taskName** |
| **Aktivitet** > **Beskrivning** | **wm:taskDescription** |

Aktivera växeln för **Synkronisera objektmetadata**.

Klicka på **Spara**.

![WF](./images/wfb6.png)

Din integrering från Workfront till AEM Assets CS är nu konfigurerad.

![WF](./images/wfb7.png)

## 1.2.1.2 Konfigurera metadataintegrering med AEM Assets

Därefter måste du konfigurera AEM Assets så att metadatafälten från resursen i Workfront delas med AEM.

Gå till [https://experience.adobe.com/](https://experience.adobe.com/) om du vill göra det. Klicka på **Experience Manager Assets**.

![WF](./images/wfbaem1.png)

Klicka för att välja din AEM Assets-miljö, som ska få namnet `--aepUserLdap-- - Citi Signal dev`.

![WF](./images/wfbaem2.png)

Du borde se det här då. Gå till **Assets** på den vänstra menyn och klicka på **Skapa mapp**.

![WF](./images/wfbaem3.png)

Namnge mappen `--aepUserLdap-- - Workfront Assets` och klicka på **Skapa**.

![WF](./images/wfbaem4.png)

Gå sedan till **Metadata Forms** i den vänstra menyn och klicka på **Skapa**.

![WF](./images/wfbaem5.png)

Använd namnet `--aepUserLdap-- - Metadata Form` och klicka på **Skapa**.

![WF](./images/wfbaem6.png)

Lägg till tre nya **enkelradiga textfält** i formuläret och markera det första fältet. Klicka sedan på ikonen **Schema** bredvid fältet **Metadata-egenskap** .

![WF](./images/wfbaem7.png)

Ange `wm:project` i sökfältet och markera sedan fältet **Projektbeskrivning**. Klicka på **Markera**.

![WF](./images/wfbaem8.png)

Ändra fältets etikett till **Projektbeskrivning**.

![WF](./images/wfbaem9.png)

Markera sedan det andra **enkelradiga textfältet** och klicka på ikonen **Schema** bredvid fältet **Metadata-egenskap** igen.

![WF](./images/wfbaem10b.png)

Du kommer då att se den här popup-rutan igen. Ange `wm:project` i sökfältet och markera sedan fältet **Projekt-ID**. Klicka på **Markera**.

![WF](./images/wfbaem10.png)

Ändra fältets etikett till **projekt-ID**.

![WF](./images/wfbaem10a.png)

Markera det tredje fältet **Enkelradig text** och klicka på ikonen **Schema** bredvid fältet **Metadataegenskap** igen.

![WF](./images/wfbaem11a.png)

Du kommer då att se den här popup-rutan igen. Ange `wm:project` i sökfältet och markera sedan fältet **Projektnamn**. Klicka på **Markera**.

![WF](./images/wfbaem11.png)

Ändra etiketten för fältet till **Projektnamn**. Klicka på **Spara**.

![WF](./images/wfbaem12.png)

Ändra **fliknamnet** i formuläret till `--aepUserLdap-- - Workfront Metadata`. Klicka på **Spara** och **Stäng**.

![WF](./images/wfbaem13.png)

**Metadataformuläret** har konfigurerats.

![WF](./images/wfbaem14.png)

Därefter måste du tilldela metadataformuläret till mappen som du skapade tidigare. Markera kryssrutan för ditt metadataformulär och klicka på **Tilldela till mapp(ar)**.

![WF](./images/wfbaem15.png)

Välj din mapp som ska ha namnet `--aepUserLdap-- - Workfront Assets`. Klicka på **Tilldela**.

![WF](./images/wfbaem16.png)

Metadataformuläret har nu tilldelats mappen.

![WF](./images/wfbaem17.png)

## 1.2.1.2 Konfigurera din AEM Sites-integrering

>[!NOTE]
>
>Det här plugin-programmet är för närvarande i läget **Tidig åtkomst** och är inte allmänt tillgängligt än.
>
>Detta plugin-program kan redan vara installerat i den Workfront-instans som du använder. Om den redan är installerad kan du läsa instruktionerna nedan, men du behöver inte ändra något i konfigurationen då.

Gå till [https://experience.adobe.com/#/@experienceplatform/aem/extension-manager/universal-editor](https://experience.adobe.com/#/@experienceplatform/aem/extension-manager/universal-editor){target="_blank"}.

Kontrollera att **toggle** för det här plugin-programmet är inställt på **Enabled**. Klicka sedan på ikonen **kugghjulet** .

![WF](./images/wfb8.png)

En popup-meny för **tilläggskonfiguration** visas. Konfigurera följande fält för att använda det här plugin-programmet.

| Nyckel | Värde |
| --------------- | ------------------------------ | 
| **`IMS_ENV`** | **PROD** |
| **`WORKFRONT_INSTANCE_URL`** | **https://experienceplatform.my.workfront.com** |
| **`SHOW_CUSTOM_FORMS`** | **&#39;{&quot;previewUrl&quot;: true, &quot;publishUrl&quot;: true}&#39;** |

Klicka på **Spara**.

![WF](./images/wfb8.png)

Gå tillbaka till ditt Workfront-gränssnitt och klicka på ikonen **hamburger** med nio punkter. Välj **Konfigurera**.

![WF](./images/wfb9.png)

Gå till **Anpassad Forms** på den vänstra menyn och välj **Formulär**. Klicka på **+ Nytt anpassat formulär**.

![WF](./images/wfb10.png)

Välj **Aktivitet** och klicka på **Fortsätt**.

![WF](./images/wfb11.png)

Då visas ett tomt anpassat formulär. Ange formulärnamnet `Content Fragment & Integration ID`.

![WF](./images/wfb12.png)

Dra och släpp ett nytt **enkelradigt textfält** på arbetsytan.

![WF](./images/wfb13.png)

Konfigurera det nya fältet så här:

- **Etikett**: **Innehållsfragment**
- **Namn**: **`aem_workfront_integration_content_fragment`**

![WF](./images/wfb14.png)

Lägg till ett nytt **enradigt textfält** på arbetsytan och konfigurera det nya fältet så här:

- **Etikett**: **Integrerings-ID**
- **Namn**: **`aem_workfront_integration_id`**

Klicka på **Använd**.

![WF](./images/wfb15.png)

Nu måste du konfigurera ett andra anpassat formulär. Klicka på **+ Nytt anpassat formulär**.

![WF](./images/wfb10.png)

Välj **Aktivitet** och klicka på **Fortsätt**.

![WF](./images/wfb11.png)

Då visas ett tomt anpassat formulär. Ange formulärnamnet `Preview & Publish URL`.

![WF](./images/wfb16.png)

Dra och släpp ett nytt **enkelradigt textfält** på arbetsytan.

![WF](./images/wfb17.png)

Konfigurera det nya fältet så här:

- **Etikett**: **URL för förhandsgranskning**
- **Namn**: **`aem_workfront_integration_preview_url`**

![WF](./images/wfb18.png)

Lägg till ett nytt **enradigt textfält** på arbetsytan och konfigurera det nya fältet så här:

- **Etikett**: **Publicera URL**
- **Namn**: **`aem_workfront_integration_publish_url`**

Klicka på **Använd**.

![WF](./images/wfb19.png)

Du bör sedan ha 2 anpassade formulär tillgängliga.

![WF](./images/wfb20.png)

Nästa steg: [1.2.2 Korrektur med Workfront](./ex2.md){target="_blank"}

Gå tillbaka till [Arbetsflödeshantering med Adobe Workfront](./workfront.md){target="_blank"}

[Gå tillbaka till alla moduler](./../../../overview.md){target="_blank"}
