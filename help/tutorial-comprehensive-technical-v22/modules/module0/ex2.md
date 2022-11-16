---
title: Komma igång - Använd demonstrationssystemet bredvid för att konfigurera Launch-egenskapen
description: Komma igång - Använd demonstrationssystemet bredvid för att konfigurera Launch-egenskapen
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 9c0eddf5-bfd7-4e7a-a8e2-ccd55ccd966d
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# 0.2 Använd Demo System bredvid för att konfigurera klientegenskapen för Adobe Experience Platform Data Collection

När du har registrerat dig för den omfattande tekniska självstudiekursen för Adobe Experience Platform finns det en automatiserad process som ger dig tillgång till Demo System, så att du kan komma åt och köra konfigurationen nedan.

När du har tillgång till Demo System fortsätter du med stegen nedan.

Gå till [https://dashboard.adobedemo.com/](https://dashboard.adobedemo.com/). Markera din sandlåda och klicka på **Snabbinställningar**.

![DSN](./images/dsnh1.png)

Du kommer att se det här:

![DSN](./images/dsnhome.png)

Under **Allmänt** - **Miljö** markerar du din Adobe Experience Platform-instans och din sandlåda, i det här fallet:

- **Experience Platform International**
- **aepenablementfy22**
- Konfiguration: välj **Global v2.0**

![DSN](./images/dsn1.png)

Välj sedan förinställningen **Aktivera användare** och klicka **Starta**.

![DSN](./images/dsn2.png)

Ange ett namn för datainsamlingsegenskapen på popup-menyn. Använd den här namnkonventionen: **Demonstrationssystem (DD/MM/ÅÅÅÅ)**. Obs! LDAP läggs till automatiskt, du behöver inte lägga till den själv.

Klicka **Starta**.

![DSN](./images/dsn3.png)

Du kommer då att se den här popup-rutan, som visar hur arbetet fortskrider när du skapar projekt för webbplatser och mobilappar samt egenskaper för datainsamling.

![DSN](./images/dsn4.png)

När snabbinstallationsprocessen är klar får du:

- 1 Web Retail-projekt, som gör det möjligt att använda en demowebbplats med varumärket Luma demo
- 1 Mobilt detaljhandelsprojekt, som gör det möjligt att använda en demomobilapp med varumärket Luma demo
- 1 CX App Retail-projekt, vilket gör det möjligt att använda ett callcenter och en kundapp med varumärket Luma demo
- 1 Datainsamlingsegenskap för webben, som du använder för att samla in data från webbplatsen
- 1 Datainsamlingsegenskap för mobilen, som du använder för att samla in data från mobilappen

![DSN](./images/dsn5.png)

Håll den här skärmen öppen som du vill i nästa steg.

Nästa steg: [0.3 Skapa ditt datastream](./ex3.md)

[Gå tillbaka till modul 0](./getting-started.md)

[Gå tillbaka till Alla moduler](./../../overview.md)
