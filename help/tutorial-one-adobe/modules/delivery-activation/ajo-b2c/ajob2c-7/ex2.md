---
title: Offer Decisioning - Konfigurera erbjudanden och beslut-ID
description: Offer Decisioning - Konfigurera erbjudanden och beslut-ID
kt: 5342
doc-type: tutorial
source-git-commit: 13d790855601fa6f36c1afa0f2d5faad5fc07eb0
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 10%

---

# 3.7.2 Konfigurera erbjudanden och beslut

## 3.7.2.1 Skapa anpassade erbjudanden

I den här övningen skapar du fyra **Personaliserade erbjudanden**. Här följer de uppgifter som ska beaktas när erbjudandena skapas:

| Namn | Datumintervall | Bildlänk för e-post | Bildlänk för webben | Text | Prioritet | Kvalificering | Språk | Begränsningsfrekvens | Bildnamn |
|-----|------------|----------------------|--------------------|------|:--------:|--------------|:-------:|:-------:|:-------:|
| `--aepUserLdap-- - AirPods Max` | idag - 1 månad senare | https://bit.ly/4a9RJ5d | Välj från Assets Library | `{{ profile.person.name.firstName }}, 10% discount on AirPods Max` | 25 | alla - kvinnliga kunder | Engelska (USA) | 3 | Apple AirPods Max- Female.jpg |
| `--aepUserLdap-- - Galaxy S24` | idag - 1 månad senare | https://bit.ly/3W8yuDv | Välj från Assets Library | `{{ profile.person.name.firstName }}, 5% discount on Galaxy S24` | 15 | alla - kvinnliga kunder | Engelska (USA) | 3 | Galaxy S24 - Female.jpg |
| `--aepUserLdap-- - Apple Watch` | idag - 1 månad senare | https://bit.ly/4fGwfxX | https://bit.ly/4fGwfxX | `{{ profile.person.name.firstName }}, 10% discount on Apple Watch` | 25 | alla - Manliga kunder | Engelska (USA) | 3 | Apple Watch - Male.jpg |
| `--aepUserLdap-- - Galaxy Watch 7` | idag - 1 månad senare | https://bit.ly/4gTrkeo | Välj från Assets Library | `{{ profile.person.name.firstName }}, 5% discount on Galaxy Watch 7` | 15 | alla - Manliga kunder | Engelska (USA) | 3 | Galaxy Watch7 - Male.jpg |

{style="table-layout:auto"}

Logga in på Adobe Journey Optimizer på [Adobe Experience Cloud](https://experience.adobe.com). Klicka på **Journey Optimizer**.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Du omdirigeras till vyn **Hem** i Journey Optimizer. Kontrollera först att du använder rätt sandlåda. Sandlådan som ska användas kallas `--aepSandboxName--`. Du kommer sedan att vara i vyn **Hem** i din sandlåda `--aepSandboxName--`.

![ACOP](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

## Nästa steg

Gå till [3.7.3 Web SDK-konfiguration för Experience Decisioning](./ex3.md){target="_blank"}

Gå tillbaka till [Experience Decision](ajo-decisioning.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../../overview.md){target="_blank"}
