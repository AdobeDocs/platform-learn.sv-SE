---
title: Datainsamling - FAC - Skapa en federerad komposition
description: Foundation - FAC - Skapa en federerad komposition
kt: 5342
doc-type: tutorial
exl-id: 6c1773d1-ca2e-43e5-bfa7-6e5e0fbcf859
source-git-commit: 2beb052927f88e13f42b2af940a637cbc3caa19d
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---

# 1.3.3 Skapa en federerad komposition

Nu kan ni konfigurera er sammanslagna målgruppskomposition i AEP.

Logga in på Adobe Experience Platform via följande URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

När du har loggat in loggar du in på Adobe Experience Platform hemsida.

![Datainmatning](./../dc1.2/images/home.png)

Innan du fortsätter måste du välja en **sandlåda**. Sandlådan som ska markeras har namnet `--aepSandboxName--`. När du har valt rätt sandlåda ser du skärmändringen och nu befinner du dig i din dedikerade sandlåda.

![Datainmatning](./../dc1.2/images/sb1.png)

## 1.3.3.1 Skapa din publik

Gå till **Publiker** på den vänstra menyn och gå sedan till **Federerade kompositioner**. Klicka på **Skapa komposition**.

![FAC](./images/fedcomp1.png)

Använd följande för etiketten: `--aepUserLdap-- - CitiSignal Fiber`. Markera datamodellen som du skapade i föregående övning, som har namnet `--aepUserLdap-- - CitiSignal Snowflake Data Model`. Klicka på **Skapa**.

![FAC](./images/fedcomp2.png)

Då ser du det här.

![FAC](./images/fedcomp3.png)

Klicka på ikonen **+** och klicka på **Skapa målgrupp**.

![FAC](./images/fedcomp4.png)

Då ser du det här. Välj **Skapa målgrupp**. Klicka på ikonen **sök** för att välja ett schema.

![FAC](./images/fedcomp5.png)

Välj schemat **`--aepUserLdap--_HOUSEHOLDS`**. Klicka på **Bekräfta**.

![FAC](./images/fedcomp6.png)

Klicka sedan på **Fortsätt**.

![FAC](./images/fedcomp7.png)

Nu kan du börja skapa frågan som ska skickas till Snowflake. Klicka på ikonen **+** och sedan på **Anpassat villkor**.

![FAC](./images/fedcomp8.png)

Markera attributet **ISELIGIBLEFORFIBER** och klicka på **Bekräfta**.

![FAC](./images/fedcomp9.png)

Då ser du det här. Ange fältet **Värde** som **Sant**. Klicka på **Beräkna** om du vill skicka frågan till Snowflake och få en uppskattning av de profiler som nu är kvalificerade.

![FAC](./images/fedcomp10.png)

Klicka sedan på ikonen **+** igen och klicka på **Anpassat villkor** igen för att lägga till ett annat villkor.

![FAC](./images/fedcomp11.png)

Det andra villkoret som ska läggas till är: `Is the user an existing CitiSignal Mobile subscriber?`. Du kan besvara den frågan genom att använda relationen mellan hushållet och den primära kunden i hushållet, som definieras i en annan tabell, **`--aepUserLdap--_PERSONS`**. Du kan detaljgranska på attributmenyn med länken **house2person** .

![FAC](./images/fedcomp12.png)

Markera attributet **ISMOBILESUB** och klicka på **Bekräfta**.

![FAC](./images/fedcomp13.png)

Ställ in fältet **Värde** till **Sant** Klicka på **Beräkna** igen för att uppdatera antalet profiler som ska användas. Klicka på **Bekräfta**.

![FAC](./images/fedcomp14.png)

Klicka på ikonen **+** och sedan på **Spara publik**.

![FAC](./images/fedcomp15.png)

Ställ in **publiketiketten** på `--aepUserLdap-- - CitiSignal Eligible for Fiber`.

Klicka på **+ Lägg till målgruppsmappning**.

![FAC](./images/fedcomp16.png)

Välj **HOUSEHOLD_ID** och klicka på **Bekräfta**.

![FAC](./images/fedcomp17.png)

Klicka på **+ Lägg till målgruppsmappning**.

![FAC](./images/fedcomp18.png)

Detaljgranska genom att klicka på **Måldimension**.

![FAC](./images/fedcomp18a.png)

Granska genom att klicka på länken **house2person**.

![FAC](./images/fedcomp18b.png)

Markera fältet **NAME**. Klicka på **Bekräfta**.

![FAC](./images/fedcomp18c.png)

Klicka på **+ Lägg till målgruppsmappning**.

![FAC](./images/fedcomp20.png)

Detaljgranska genom att klicka på **Måldimension**.

![FAC](./images/fedcomp20a.png)

Granska genom att klicka på länken **house2person**.

![FAC](./images/fedcomp20b.png)

Markera fältet **EMAIL**. Klicka på **Bekräfta**.

![FAC](./images/fedcomp20c.png)

Då ser du det här. Du måste nu ange fältet **Primär identitet** och ställa in det på **Household2person_EMAIL**. Ange **Identity Namespace** till **Email**.

Klicka på **Spara**.

![FAC](./images/fedcomp21.png)

Din komposition är nu färdig. Klicka på **Start** för att köra den.

![FAC](./images/fedcomp21a.png)

Frågan kommer nu att laddas ned till Snowflake, som kommer att fråga källdata där. Resultatet överförs tillbaka till AEP, men källdata finns kvar i Snowflake.

Publiken är nu befolkad och målgruppen kan målgruppsanpassas inifrån AEP ekosystem.

![FAC](./images/fedcomp22.png)

## Nästa steg

Gå till [Sammanfattning och förmåner](./summary.md){target="_blank"}

Gå tillbaka till [Sammansatt målgrupp](./fac.md){target="_blank"}

Gå tillbaka till [Alla moduler](./../../../../overview.md){target="_blank"}
