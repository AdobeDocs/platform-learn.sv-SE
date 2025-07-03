---
title: Experience Decision - Experience Decision 101
description: Experience Decision - Experience Decision 101
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
source-git-commit: 13d790855601fa6f36c1afa0f2d5faad5fc07eb0
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---

# 3.7.1 Experience Decision 101

## 3.7.1.1 Terminologi

För att få en bättre förståelse för Experience Decision rekommenderar vi att du läser [översikten](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=en) om hur Offer Decisioning Application Service fungerar med Adobe Experience Platform.

När du arbetar med Offer Decisioning måste du förstå följande koncept:

| Villkor | Förklaring |
| ------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Erbjudande** | Ett erbjudande är ett marknadsföringsmeddelande som kan ha kopplade regler som anger vem som kan se erbjudandet. Ett erbjudande har status: utkast, godkänt eller arkiverat. |
| **Placement** | Den kombination av plats (eller kanaltyp) och kontext (eller innehållstyp) i vilken ett erbjudande visas för en slutanvändare. Det är en kombination av kanalerna Text, HTML, Image, JSON för mobiler, webben, sociala medier, snabbmeddelanden och icke-digitala. |
| **Regel** | Den logik som definierar och styr slutanvändarnas rätt till ett erbjudande. |
| **Personaliserat erbjudande** | Ett anpassningsbart marknadsföringsmeddelande baserat på regler och begränsningar för behörighet. |
| **Reserverbjudande** | Det standarderbjudande som visas när en slutanvändare inte är berättigad till något av erbjudandena i den mängd som används. |
| **Hämtning** | Används i en offertdefinition för att definiera hur många gånger ett erbjudande kan presenteras totalt och för en viss användare. |
| **Prioritet** | Nivå för att fastställa prioritetsrangordningen utifrån en resultatmängd med erbjudanden. |
| **Samling** | Används för att filtrera bort en delmängd av erbjudanden från listan över personaliserade erbjudanden för att snabba upp beslutsprocessen för erbjudanden. |
| **Beslut** | En kombination av en uppsättning erbjudanden, placering och profil marknadsföraren vill att beslutsmotorn ska erbjuda det bästa erbjudandet. |
| **AEM Assets Essentials** | En universell och centraliserad upplevelse för lagring, sökning och val av mediefiler i Adobe Experience Cloud Solutions och Adobe Experience Platform. |

{style="table-layout:auto"}

## 3.7.1.2 Experience Decision

Logga in på Adobe Journey Optimizer på [Adobe Experience Cloud](https://experience.adobe.com). Klicka på **Journey Optimizer**.

![ExD](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Du omdirigeras till vyn **Hem** i Journey Optimizer. Kontrollera först att du använder rätt sandlåda. Sandlådan som ska användas kallas `--aepSandboxName--`. Du kommer sedan att vara i vyn **Hem** i din sandlåda `--aepSandboxName--`.

![ExD](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

I nästa övning kommer ni att konfigurera era egna erbjudanden och beslut.

## Nästa steg

Gå till [3.7.2 Konfigurera erbjudanden och beslut](./ex2.md){target="_blank"}

Gå tillbaka till [Experience Decision](ajo-decisioning.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../../overview.md){target="_blank"}
