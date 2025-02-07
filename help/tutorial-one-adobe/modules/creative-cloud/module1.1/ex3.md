---
title: Arbeta med Photoshop API:er
description: Lär dig hur du arbetar med Photoshop API:er och Firefly Services
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 60eecc24-1713-4fec-9ffa-a3186db1a8ca
source-git-commit: e6a549441d425801f2a554da9af803dca646009e
workflow-type: tm+mt
source-wordcount: '952'
ht-degree: 0%

---

# 1.1.3 Arbeta med Photoshop API:er

Lär dig hur du arbetar med Photoshop API:er och Firefly Services.

## 1.1.3.1 Uppdatera integreringen med Adobe I/O

1. Gå till [https://developer.adobe.com/console/home](https://developer.adobe.com/console/home){target="_blank"}.

![Ny integrering för Adobe I/O](./images/iohome.png)

1. Gå till **Projekt** och välj det projekt du skapade i föregående övning, som kallas `--aepUserLdap-- Firefly`.

![Azure Storage](./images/ps1.png)

1. Välj **+ Lägg till i projekt** och välj sedan **API**.

![Azure Storage](./images/ps2.png)

1. Markera **Creative Cloud** och välj **Photoshop - Firefly-tjänster**. Välj **Nästa**.

![Azure Storage](./images/ps3.png)

1. Välj **Nästa**.

![Azure Storage](./images/ps4.png)

Därefter måste du välja en produktprofil som definierar vilka behörigheter som är tillgängliga för den här integreringen.

1. Välj **Standardkonfiguration för Firefly Services** och **Standardkonfiguration för Creative Cloud Automation Services**.

1. Välj **Spara konfigurerat API**.

![Azure Storage](./images/ps5.png)

Ditt Adobe I/O-projekt har nu uppdaterats för att fungera med API:er för Photoshop och Firefly Services.

![Azure Storage](./images/ps6.png)

## 1.1.3.2 Interagera med PSD

>[!IMPORTANT]
>
>Om du är anställd i Adobe följer du instruktionerna här för att använda [PostBuster](./../../../postbuster.md).

1. Hämta [citisign-fiber.psd](./../../../assets/ff/citisignal-fiber.psd){target="_blank"} till skrivbordet.

1. Öppna **citisign-fiber.psd** i Photoshop.

![Azure Storage](./images/ps7.png)

I rutan **Lager** har fildesignern gett varje lager ett unikt namn. Du kan se lagerinformationen genom att öppna PSD-filen i Photoshop, men du kan också göra det programmatiskt.

Låt oss skicka din första API-begäran till Photoshop API:er.

1. I Postman måste du autentisera till Adobe I/O innan du skickar API-begäranden till Photoshop. Öppna föregående begäran med namnet **POST - Hämta åtkomsttoken**.

1. Gå till **Parametrar** och kontrollera att parametern **Scope** är korrekt inställd. **Värdet** för **Scope** ska se ut så här:

`openid,session,AdobeID,read_organizations,additional_info.projectedProductContext, ff_apis, firefly_api`

1. Välj **Skicka**.

![Azure Storage](./images/ps8.png)

Nu har du en giltig åtkomsttoken för att interagera med Photoshop API:er.

![Azure Storage](./images/ps9.png)

### Photoshop API - Hello World

Sedan hälsar vi på Photoshop API:er för att testa om alla behörigheter och all åtkomst är korrekt inställda.

1. I samlingen **Photoshop** öppnar du begäran **Photoshop Hello (Test Auth.)**. Välj **Skicka**.

![Azure Storage](./images/ps10.png)

Du bör få svaret **Välkommen till Photoshop API!**.

![Azure Storage](./images/ps11.png)

För att programmässigt kunna interagera med PSD-filen **citisign-fiber.psd** måste du överföra den till ditt lagringskonto. Du kan göra det manuellt - genom att dra och släppa det i behållaren med Azure Storage Explorer - men den här gången bör du göra det via API:t.

### Överför PSD till Azure

1. Öppna begäran **Överför PSD till Azure Storage-kontot** i Postman. I föregående övning konfigurerade du dessa miljövariabler i Postman, som du nu kommer att använda:

- `AZURE_STORAGE_URL`
- `AZURE_STORAGE_CONTAINER`
- `AZURE_STORAGE_SAS_READ`
- `AZURE_STORAGE_SAS_WRITE`

Som du kan se i begäran **Överför PSD till Azure Storage-konto**, är URL:en konfigurerad att använda dessa variabler.

![Azure Storage](./images/ps12.png)

1. I **Body** markerar du filen **citisign-fiber.psd**.

![Azure Storage](./images/ps13.png)

1. Skärmen bör se ut så här. Välj **Skicka**.

![Azure Storage](./images/ps14.png)

Du bör få tillbaka det här tomma svaret från Azure, vilket innebär att din fil lagras i din behållare i ditt Azure Storage-konto.

![Azure Storage](./images/ps15.png)

Om du använder Azure Storage Explorer för att titta på din fil måste du uppdatera din mapp.

![Azure Storage](./images/ps16.png)

### Photoshop API - skaffa manifest

Därefter måste du hämta manifestfilen för din PSD-fil.

1. Öppna begäran **Photoshop - Hämta PSD-manifestet** i Postman. Gå till **Body**.

Kroppen ska se ut så här:

```json
{
  "inputs": [
    {
      "storage": "external",
      "href": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/citisignal-fiber.psd{{AZURE_STORAGE_SAS_READ}}"
    }
  ],
  "options": {
    "thumbnails": {
      "type": "image/jpeg"
    }
  }
}
```

1. Välj **Skicka**.

I svaret ser du nu en länk. När åtgärder i Photoshop ibland kan ta lite tid att slutföra, tillhandahåller Photoshop en statusfil som svar på de flesta inkommande begäranden. För att förstå vad som händer med din begäran måste du läsa statusfilen.

![Azure Storage](./images/ps17.png)

1. Om du vill läsa statusfilen öppnar du begäran **Photoshop - Hämta PS-status**. Du kan se att den här begäran använder en variabel som URL-adress, vilket är en variabel som anges av den tidigare begäran som du skickade, **Photoshop - Hämta PSD-manifest**. Variabler anges i **Skript** för varje begäran. Välj **Skicka**.

![Azure Storage](./images/ps18.png)

Skärmen bör se ut så här. För närvarande är statusen inställd på **väntande**, vilket innebär att processen inte har slutförts än.

![Azure Storage](./images/ps19.png)

1. Markera Skicka några gånger till på **Photoshop - Hämta PS-status** tills statusen ändras till **Slutförd**. Det här kan ta några minuter.

När svaret är tillgängligt kan du se json-filen som innehåller information om alla lager i PSD-filen. Detta är användbar information eftersom exempelvis lagernamn eller lager-ID kan identifieras.

![Azure Storage](./images/ps20.png)

Sök till exempel efter texten `2048x2048-cta`. Skärmen bör se ut så här:

![Azure Storage](./images/ps21.png)

### Photoshop API - Ändra text

Därefter måste du ändra texten för anropet till åtgärd med API:erna.

1. Öppna begäran **Photoshop - Ändra text** i Postman och gå till **Brödtext**.

Skärmen bör se ut så här:

- först anges en indatafil: `citisignal-fiber.psd`
- därefter anges det lager som ska ändras, med texten som ska ändras till
- För det tredje har en utdatafil angetts: `citisignal-fiber-changed-text.psd`

```json
{
  "inputs": [
    {
      "storage": "external",
      "href": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/citisignal-fiber.psd{{AZURE_STORAGE_SAS_READ}}"
    }
  ],
  "options": {
    "layers": [
      {
        "name": "2048x2048-cta",
        "text": {
          "content": "Get Fiber now!"
        }
      }
    ]
  },
  "outputs": [
    {
      "storage": "azure",
      "href": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/citisignal-fiber-changed-text.psd{{AZURE_STORAGE_SAS_WRITE}}",
      "type": "vnd.adobe.photoshop",
      "overwrite": true
    }
  ]
}
```

Utdatafilen har ett annat namn eftersom du inte vill åsidosätta den ursprungliga indatafilen.

1. Välj **Skicka**.

![Azure Storage](./images/ps23.png)

Precis som tidigare innehåller svaret en länk som pekar på statusfilen som håller reda på förloppet.

![Azure Storage](./images/ps22.png)

1. Om du vill läsa statusfilen öppnar du begäran **Photoshop - Hämta PS-status** och väljer **Skicka**. Om statusen inte är inställd på **success** omedelbart, vänta några sekunder och välj sedan **Skicka** igen.

1. Välj den URL som du vill hämta utdatafilen från.

![Azure Storage](./images/ps24.png)

1. Öppna **citisign-fiber-changed-text.psd** när du har hämtat filen till datorn. Platshållaren för anropet till åtgärd har ersatts av texten **Hämta nu!**.

![Azure Storage](./images/ps25.png)

Du kan även se den här filen i din behållare med Azure Storage Explorer.

![Azure Storage](./images/ps26.png)

## Nästa steg

Gå till [API för anpassade modeller för Firefly](./ex4.md){target="_blank"}

Gå tillbaka till [Översikt över Adobe Firefly Services](./firefly-services.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../overview.md){target="_blank"}