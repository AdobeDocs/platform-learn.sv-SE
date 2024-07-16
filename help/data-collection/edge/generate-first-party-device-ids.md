---
title: Generera enhets-ID:n från första part
description: Lär dig hur du skapar enhets-ID:n från första part
feature: Web SDK
level: Experienced
jira: KT-9728
thumbnail: KT-9728.jpeg
exl-id: 2e3c1f71-e224-4631-b680-a05ecd4c01e7
source-git-commit: ac07d62cf4bfb6a9a8b383bbfae093304d008b5f
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 1%

---

# Generera enhets-ID:n från första part

Adobe Experience Cloud-program har traditionellt genererat cookies för att lagra enhets-ID med olika tekniker, bland annat:

1. cookies från tredje part
1. cookies från första part som anges av en Adobe-server med hjälp av domännamnets CNAME-konfiguration
1. cookies från första part som anges av JavaScript

De senaste ändringarna i webbläsaren begränsar varaktigheten för dessa typer av cookies. Första parts-cookies är mest effektiva när de ställs in med en kundägd server som använder en DNS A/AAA-post i motsats till en DNS CNAME. Med funktionen för FPID (First-party device ID) kan kunder som implementerar Adobe Experience Platform Web SDK använda enhets-ID i cookies från servrar med DNS A/AAAA-poster. Dessa ID:n kan sedan skickas till Adobe och användas som frön för att generera Experience Cloud ID:n (ECID), som förblir den primära identifieraren i Adobe Experience Cloud-program.

Här är ett kort exempel på hur funktionen fungerar:

![Första parts enhets-ID (FPID) och Experience Cloud-ID (ECID)](../assets/kt-9728.png)

1. En slutanvändares webbläsare begär en webbsida från en kunds webbserver eller CDN.
1. Kunden genererar ett enhets-ID (FPID) på sin webbserver eller CDN (webbservern ska vara knuten till domännamnets DNS A/AAAA-post).
1. Kunden ställer in en cookie för första part för att lagra FPID i slutanvändarens webbläsare.
1. Kundens implementering av Adobe Experience Platform Web SDK gör en begäran till Platform Edge Network, inklusive FPID i identitetskartan.
1. Experience Platform Edge Network tar emot FPID och använder det för att generera ett Experience Cloud ID (ECID).
1. SDK-svaret för plattformen skickar ECID tillbaka till slutanvändarens webbläsare.
1. Om `idMigrationEnabled=true` används JavaScript för att lagra ECID som `AMCV_`-cookie i slutanvändarens webbläsare.
1. Om cookien `AMCV_` går ut upprepas processen. Så länge samma enhets-ID finns tillgängligt skapas en ny `AMCV_`-cookie med samma ECID-värde som tidigare.

>[!NOTE]
>
>`idMigrationEnabled` behöver inte anges till `true` för att använda FPID. Med `idMigrationEnabled=false` kanske du inte ser någon `AMCV_`-cookie och måste leta efter ECID-värdet i nätverkssvaret.


I den här självstudiekursen används ett specifikt exempel med skriptspråket PHP för att visa hur du:

* Generera en UUIDv4
* Skriv UUIDv4-värde till en cookie
* Inkludera cookie-värdet i identitetskartan
* Validera ECID-genereringen

Ytterligare dokumentation om enhets-ID:n från första part finns i produktdokumentationen.

## Generera en UUIDv4

PHP har inget systemspecifikt bibliotek för UUID-generering, så dessa kodexempel är mer omfattande än vad som troligtvis skulle behövas om ett annat programmeringsspråk användes. PHP valdes för det här exemplet eftersom det är ett språk på serversidan som har brett stöd.


När följande funktion anropas genereras ett slumpmässigt UUID version-4:

```
<?php
    
    function guidv4($data)
    {
        $data = $data ?? random_bytes(16);

        $data[6] = chr(ord($data[6]) & 0x0f | 0x40); // set version to 0100
        $data[8] = chr(ord($data[8]) & 0x3f | 0x80); // set bits 6-7 to 10

        return vsprintf('%s%s-%s-%s-%s-%s%s%s', str_split(bin2hex($data), 4));
    }

?>
```

## Skriv UUIDv4-värde till en cookie

Följande kod skickar en begäran till funktionen ovan om att generera ett UUID. Sedan anges de cookie-flaggor som din organisation har bestämt. Om en cookie redan har genererats förlängs giltigheten.

```
<?php

    if(!isset($_COOKIE['FPID'])) {
        $cookie_value = guidv4(openssl_random_pseudo_bytes(16));        
        $arr_cookie_options = array (
        'expires' => time() + 60*60*24*30*13,
        'path' => '/',
        'domain' => 'mysiteurl.com',
        'secure' => true,
        'httponly' => true,
        'samesite' => 'lax'
        );
        setcookie($cookie_name, $cookie_value, $arr_cookie_options);
        $_COOKIE[$cookie_name] = $cookie_value;
    }
    else {
        $cookie_value = $_COOKIE[$cookie_name];
        $arr_cookie_options = array (
        'expires' => time() + 60*60*24*30*13,
        'path' => '/',
        'domain' => 'mysiteurl.com',
        'secure' => true,
        'httponly' => true,
        'samesite' => 'lax'
        );
        setcookie($cookie_name, $cookie_value, $arr_cookie_options);
    }

?>
```

>[!NOTE]
>
>Den cookie som innehåller det första enhets-ID:t kan ha vilket namn som helst.

## Inkludera cookie-värdet i identitetskartan

Det sista steget är att använda PHP för att eko cookie-värdet till identitetskartan.


```
{
    "identityMap": {
        "FPID": [
                    {
                        "id": "<? echo $_COOKIE[$cookie_name] ?>",
                        "authenticatedState": "ambiguous",
                        "primary": true
                    }
                ]
        }
}
```

>[!IMPORTANT]
>
>Identitetsnamnutrymmessymbolen som används i identitetskartan måste kallas `FPID`.
>
> `FPID` är ett reserverat ID-namnutrymme som inte visas i gränssnittslistorna med identitetsnamnutrymmen.


## Validera ECID-generering

Validera implementeringen genom att bekräfta att samma ECID genereras från ditt första enhets-ID:

1. Skapa en FPID-cookie.
1. Skicka en begäran till Platform Edge Network via Platform Web SDK.
1. En cookie med formatet `AMCV_<IMSORGID@AdobeOrg>` genereras. Denna cookie innehåller ECID.
1. Anteckna cookie-värdet som genereras och ta sedan bort alla cookies för din webbplats utom `FPID`-cookien.
1. Skicka ytterligare en begäran till Platform Edge Network.
1. Bekräfta att värdet i cookien `AMCV_<IMSORGID@AdobeOrg>` har samma `ECID`-värde som i cookien `AMCV_` som togs bort. Om cookie-värdet är samma för en viss FPID har sederingsprocessen för ECID slutförts.

Mer information om den här funktionen finns i [dokumentationen](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/first-party-device-ids.html).
