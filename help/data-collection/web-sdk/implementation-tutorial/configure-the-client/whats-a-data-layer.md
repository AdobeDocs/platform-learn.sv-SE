---
title: Vad är ett datalager?
description: Vad är ett datalager?
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
kt: 10447
hide: true
hidefromtoc: true
exl-id: 747f2e60-646e-4324-993c-88568415ea59
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---

# Vad är ett datalager?

När ni implementerar marknadsföringsteknologier på er webbplats är det troligt att ni har viktiga datadelar utspridda i hela användargränssnittet. En produkts namn kan till exempel vara i en rubrik på sidan och priset kan vara lägre på sidan nedanför produktbilden. Om du vill skicka dessa data till Adobe eller någon annan leverantör kan du säkert hitta elementen i HTML som innehåller data genom att söka efter särskilda taggar eller attribut för HTML, hämta data från dessa element och skicka dem. Men vad händer när konstruktörerna bestämmer sig för att flytta produktnamnet från huvudet till ett sidofält? Implementeringen avbryts. Din implementering kan inte längre hitta rubriken eller, ännu värre, hitta rubriken och skicka irrelevanta data till servern.

Ett viktigt mål med ett datalager är att lösa det här problemet. I det enklaste fallet är ett datalager ett JavaScript-objekt (eller, som vi kommer att se senare, en array) som innehåller data om produkten på sidan eller andra relevanta data som er marknadsföringsteknologi förlitar sig på för att uppnå era mål. Genom att inte förlita sig på elementen i användargränssnittet för att tillhandahålla dessa data blir implementeringen mer robust. Datalagret innehåller data och bör betraktas som ett kontrakt. Kontraktet är vanligtvis mellan konstruktörerna, som placerar data i datalagret, och marknadsföringsteamet, som hämtar data från datalagret.

Om en tekniker ska ändra dataskiktets struktur är det mycket mer troligt att de kommer att överväga att samarbeta med marknadsföringsteamet så att lämpliga ändringar kan göras i implementeringen av marknadsföringen. Detta kommunikation och samarbete _måste_ etableras i organisationen för att säkerställa en stabil implementering.

## Behållare kontra innehåll

I branschen kastas termen&quot;datalager&quot; lite löst och kan ofta leda till förvirring och missförstånd. Överväg en låda med marmor. Det finns två delar: behållaren (lådan) och innehållet (marmor). På samma sätt anses ett datalager ofta ha två delar: behållaren (JavaScript-objektet eller -arrayen) och innehållet (datadelar som `priceTotal`, `currencyCode`och `purchaseOrderNumber` ).

Eftersom den här självstudiekursen refererar till datalagret för klienten i Adobe, refererar den till behållaren och inte till innehållet. När det refererar till XDM avser det innehållet och inte behållaren. När det gäller datalagret för klienten i Adobe spelar det ingen roll om innehållet är XDM eller din egen datamodell. Adobe-klientdatalagret bryr sig inte. Det är bara en låda. Men det _är_ en låda med specialkrafter..

## Kommunicera ändringar

När du använder ett datalager kan du när som helst ändra innehållet. Det är en bra funktion eftersom data kan bli tillgängliga vid olika tillfällen. Du kan till exempel ha en del data om användaren tillgängliga omedelbart, men du kan behöva göra en asynkron begäran till en tredje part om ytterligare information. Detta kräver särskild hänsyn. Om ni behöver skicka dessa asynkrona data till Adobe Experience Platform vid något tillfälle, hur vet marknadsföringsteknologierna när vissa datadelar har lagts till i datalagret och är klara att skickas? Ni behöver ett smartare datalager - ett händelsestyrt datalager.

Ett händelsestyrt datalager kan förmedla att dess innehåll har ändrats så att marknadsföringsteknologierna kan reagera på förändringen. Om detta används på rätt sätt kan det hjälpa till att undvika timingproblem som ofta uppstår med datalager som inte har något sätt att kommunicera när ändringar sker.

Adobe Client Data Layer är ett händelsestyrt datalager.
