---
title: Inställningar
description: Konfigurera din Adobe Experience Platform-instans
doc-type: multipage-overview
hide: false
exl-id: 1150c5ec-3fba-4506-8f17-c34872f9b3ea
source-git-commit: 1526661a80b4d551627dfca42a7e97c9498dd1f2
workflow-type: tm+mt
source-wordcount: '1048'
ht-degree: 0%

---

# Konfigurera din Adobe Experience Platform-instans

>[!IMPORTANT]
>
>Den här sidan är endast avsedd för systemadministratörsroller. Du behöver behörighet som systemadministratör för den specifika instansen för att kunna följa stegen nedan. Om du inte är systemadministratör i din Adobe Experience Cloud-organisation kontaktar du systemadministratören och ber om deras godkännande och hjälp innan du fortsätter med något av nedanstående steg.

## Översikt

För att kunna genomföra alla dessa självstudiekurser på ett praktiskt sätt måste följande Adobe Experience Cloud-program finnas med i din IMS-organisation:

- Adobe CDP i realtid
- Adobe Experience Platform Data Collection
- Adobe Journey Optimizer
- Customer Journey Analytics
- Data Distiller
- Federerad målgruppssammansättning

Om en specifik programtjänst inte har etablerats för din IMS-organisation kan du inte utföra den specifika övningen på ett praktiskt sätt.

## Skapa en sandlåda

Om du vill gå igenom självstudiekursen i din egen Adobe Experience Platform-instans bör du först skapa en ny utvecklingssandlåda. Om du vill skapa en ny sandlåda går du till [https://experience.adobe.com/platform](https://experience.adobe.com/platform), går till Sandlådor och sedan till **Bläddra**. Klicka på **Skapa sandlåda**.

![Skapa sandlåda](./assets/images/sandbox1.png)

Skapa din sandlåda så här:

- Typ: **Utveckling**
- Namn: **aep-tutorial**
- Titel: **Adobe Experience Platform självstudiekurs**

Klicka på **Skapa**.

![Skapa sandlåda](./assets/images/sandbox2.png)

Din sandlåda kommer nu att skapas. Efter några minuter kommer du att se det här.

![Skapa sandlåda](./assets/images/sandbox3.png)

## Konfigurera behörigheter

Gå till **Behörigheter** och gå sedan till **Roller**.

Klicka för att öppna den specifika **roll** som ska användas av de studerande som ska gå igenom kursen. Klicka på **Skapa roll**.

![Skapa sandlåda](./assets/images/perm1.png)

Ge din roll ett namn som **Adobe Experience Platform Tutorial**, klicka på **Bekräfta**.

![Skapa sandlåda](./assets/images/perm2.png)

I listrutan **Sandlådor** markerar du den sandlåda som du just har skapat och ser till att du tar bort alla andra sandlådor (ta även bort **Prod**).

![Skapa sandlåda](./assets/images/perm3.png)

Lägg till de olika resurserna och ange behörigheter. Se till att du inte lägger till några behörigheter för **Sandlådeadministration**.

![Skapa sandlåda](./assets/images/perm4.png)

Lägg till fler resurser enligt vad som anges och ange behörigheter.

![Skapa sandlåda](./assets/images/perm5.png)

Lägg till fler resurser enligt vad som anges och ange behörigheter. Klicka på **Spara**. Klicka sedan på **Stäng**.

![Skapa sandlåda](./assets/images/perm6.png)

## Konfigurera Adobe I/O

Gå till
[https://developer.adobe.com/console/integrations](https://developer.adobe.com/console/integrations). Kontrollera att du är i rätt instans. Klicka på **Skapa nytt projekt**.

![Skapa sandlåda](./assets/images/io1.png)

Klicka på **Lägg till i projekt** och sedan på **API**.

![Skapa sandlåda](./assets/images/io2.png)

Klicka på **Adobe Experience Platform** och aktivera sedan **Experience Platform API**. Klicka på **Nästa**.

![Skapa sandlåda](./assets/images/io3.png)

Använd **DSN AEP-självstudiekurs** för **inloggningsnamnet**. Klicka på **Nästa**.

![Skapa sandlåda](./assets/images/io4.png)

Välj en av de tillgängliga produktprofilerna. Den här produktprofilen avgör inte behörigheter för det här Adobe I/O-projektet - det görs i ett nästa steg. Klicka på **Spara konfigurerat API**.

![Skapa sandlåda](./assets/images/io5.png)

Klicka på **Lägg till i projekt** och sedan på **API** igen.

![Skapa sandlåda](./assets/images/io6.png)

Klicka på **Adobe Experience Platform** och aktivera sedan **Experience Platform Launch API**. Klicka på **Nästa**.

![Skapa sandlåda](./assets/images/io7.png)

Klicka på **Nästa**.

![Skapa sandlåda](./assets/images/io8.png)

Välj en produktprofil som gör det möjligt att skapa och hantera egenskaper för datainsamling. Klicka på **Spara konfigurerat API**.

![Skapa sandlåda](./assets/images/io9.png)

Då ser du det här. Klicka på det aktuella **Project XXX**-namnet.

![Skapa sandlåda](./assets/images/io10.png)

Klicka på **Redigera projekt**.

![Skapa sandlåda](./assets/images/io11.png)

Ange en ny **projekttitel**, till exempel **DSN Adobe Experience Platform-självstudiekurs**. Klicka på **Spara**.

![Skapa sandlåda](./assets/images/io12.png)

Ditt Adobe I/O-projekt är nu klart.

## Länka Adobe I/O-projekt till roll

Gå till **Behörigheter**, till **Roller** och klicka sedan på den nya rollen som du skapade tidigare.

![Skapa sandlåda](./assets/images/role1.png)

Gå till **API-autentiseringsuppgifter**. Klicka på **+ Lägg till API-autentiseringsuppgifter**.

![Skapa sandlåda](./assets/images/role2.png)

Du ser sedan de Adobe I/O-autentiseringsuppgifter som du skapade i föregående steg. Markera den och klicka på **Spara**.

![Skapa sandlåda](./assets/images/role3.png)

Ditt Adobe I/O-projekt har nu konfigurerats med de behörigheter som krävs för att komma åt Adobe Experience Platform API:er.

![Skapa sandlåda](./assets/images/role4.png)

>[!IMPORTANT]
>
>Du måste vänta i minst 10 minuter innan du fortsätter med nästa steg i Demo System Next.

## Konfigurera din miljö i Demo System Next

Gå till [https://dsn.adobe.com/tools/org-admin](https://dsn.adobe.com/tools/org-admin). Klicka på **+ Lägg till organisation**.

![Skapa sandlåda](./assets/images/dsnorg1.png)

Fyll i obligatoriska fält:

- IMS-organisations-ID
- Namn
- Klient-ID (ta inte med **understreck**)
- Län

Systemadministratören bör kunna hjälpa dig med värdena för dessa fält.

Klicka på **Spara**.

![Skapa sandlåda](./assets/images/dsnorg2.png)

Din miljö kommer nu att ingå i listan. Leta reda på den i listan och klicka på ikonen **link** .

![Skapa sandlåda](./assets/images/dsnorg3.png)

Du måste nu ange de värden som du skapade som en del av Adobe I/O-projektets autentiseringsuppgifter. **Klient-ID**, **Klienthemlighet** och **Omfång** finns här:

![Skapa sandlåda](./assets/images/dsnorg4.png)

**ID för tekniskt konto**:

![Skapa sandlåda](./assets/images/dsnorg5.png)

Kopiera och klistra in dem här, klicka på **Spara**.

![Skapa sandlåda](./assets/images/dsnorg6.png)

DSN-miljön är nu korrekt konfigurerad.

## Konfigurera din åtkomst till DSN-miljön

Gå till [https://dsn.adobe.com/tools/environment-admin](https://dsn.adobe.com/tools/environment-admin). Markera den IMS-organisation som du nyss skapade, markera användaren och klicka sedan på **+ Tilldela** under **Sandlådor**.

![Skapa sandlåda](./assets/images/dsnorg7.png)

Ange **namnet på sandlådan** som du definierade i det första steget ovan. Det borde se ut så här:

- Namn: **aep-tutorial**

Klicka på **Bekräfta**.

![Skapa sandlåda](./assets/images/dsnorg8.png)

Din sandlåda är nu tillgänglig för den användare du har valt.

![Skapa sandlåda](./assets/images/dsnorg9.png)

## DSN Quick Setup

Gå till [https://dsn.adobe.com/quick-setup](https://dsn.adobe.com/quick-setup). Öppna listrutan **Miljö** och välj din IMS-organisation/sandlåda.

![Skapa sandlåda](./assets/images/dsnorg10.png)

För **Konfiguration** väljer du **Global v2.0**.

![Skapa sandlåda](./assets/images/dsnorg11.png)

Bläddra ned till **Bransch - Telco** och välj **Citi Signal - Avancerat**.

![Skapa sandlåda](./assets/images/dsnorg12.png)

Bläddra uppåt och klicka på **Start**.

![Skapa sandlåda](./assets/images/dsnorg13.png)

Ange en **titel** och klicka på **Start**.

![Skapa sandlåda](./assets/images/dsnorg14.png)

>[!NOTE]
>
>Det kan uppstå fel om ingen standardkopplingsprofil har skapats i sandlådan. Om så är fallet kan du antingen vänta lite till så att sammanfogningsprincipen skapas automatiskt, eller manuellt gå till Adobe Experience Platform, Profiler > Sammanfogningsprinciper och skapa en ny standardsammanfogningsprincip.

Du kommer då att se förloppet för den pågående installationen, som kommer att ta några minuter.

![Skapa sandlåda](./assets/images/dsnorg15.png)

När allt är klart är din Adobe Experience Platform-instans konfigurerad och klar att användas av eleverna.

>[!NOTE]
>
>Steget för dataimport används inte av självstudiekursen, så om det steget misslyckas behöver du inte bekymra dig. Fortsätt sedan.

![Skapa sandlåda](./assets/images/dsnorg16.png)

Gå till [https://experience.adobe.com/platform](https://experience.adobe.com/platform), till **Datauppsättningar**. Nu bör du se en liknande lista med datauppsättningar, som alla skapades av snabbinstallationsprogrammet för DSN.

![Skapa sandlåda](./assets/images/dsnorg17.png)

>[!NOTE]
>
>Tack för att du lägger ned din tid på att lära dig allt om Adobe Experience Platform och dess program. Om du har frågor kan du dela allmän feedback om dina förslag på framtida innehåll. Kontakta Tech Insiders direkt genom att skicka ett e-postmeddelande till **techinsiders@adobe.com**.

[Gå tillbaka till Alla moduler](./overview.md)
