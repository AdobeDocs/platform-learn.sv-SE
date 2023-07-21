---
title: Bootcamp - Real-time CDP - Build a segment and take action - Send your segment to DV360 - Brazil
description: Bootcamp - Real-time CDP - Build a segment and take action - Send your segment to DV360 - Brazil
jira: KT-5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
feature: Destinations
exl-id: acb32859-6f82-44e0-8948-a045a9fe2afe
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 1%

---

# 1.5 Ação: envie seu segmento para o Facebook

Åtkomst [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer inloggning, você irá acessar a página inicial da Adobe Experience Platform.

![Datainmatning](./images/home.png)

Antes de continuar, você preca selecionar um **sandlåda**. O nome do sandbox a ser selecionado é Bootcamp. É beível fazer isso clicando no texto **[!UICONTROL Produktionsprodukt]** na linha azul na parte superior da tela. Depois de selecionar o sandbox apropriado, você verá a tela mudando e agora você está em seu [!UICONTROL sandlåda] dedikat.

![Datainmatning](./images/sb1.png)

Ingen meny à esquerda, vá para **Destinationer** e, em seguida, vá para **Katalog**. Você verá o **Målkatalog**. FM **Destinationer**, clique em **Aktivera segment** no cartão **Facebook Custom Audience**.

![RTCDP](./images/rtcdpgoogleseg.png)

Markera **bootcamp-facebook** e clique em **Nästa**.

![RTCDP](./images/rtcdpcreatedest2.png)

Na lista de segmentos display oníveis, selecione o segmento que você criou no övício anterior. Clique em **Nästa**.

![RTCDP](./images/rtcdpcreatedest3.png)

Na página **Mappning**, verifique se a caixa de seleção **Använd omformning** está marcada. Clique em **Nästa**.

![RTCDP](./images/rtcdpcreatedest4a.png)

Na página **Segmentschema**, välj en **Målgruppens ursprung** e defina como **Direkt från kunderna**. Clique em **Nästa**.

![RTCDP](./images/rtcdpcreatedest4.png)

Por fim, na página **Granska**, clique em **Slutför**.

![RTCDP](./images/rtcdpcreatedest5.png)

Seu segmento agora está vinculado aos Públicos Personalizados do Facebook. Sempre que um cliente se Qualificar para esse segmento, um sinal será enviado ao lado do servidor (server-side) do Facebook para includes esse cliente no Público Personalizado no lado do Facebook.

No Facebook, você encontrará seu segmento da Adobe Experience Platform em Públicos Personalizados:

![RTCDP](./images/rtcdpcreatedest5b.png)

Agora você pode ver seu público personalizado aparecer no Facebook:

![RTCDP](./images/rtcdpcreatedest5a.png)

[Retornar para Fluxo de Usuário 1](./uc1.md)

[Retornar para Todos os Módulos](../../overview.md)
