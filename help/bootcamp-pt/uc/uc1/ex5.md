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
source-wordcount: '290'
ht-degree: 0%

---

# 1.5 Ação: envie seu segmento para o Facebook

Öppna [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer inloggning, você irá acessar a página inicial da Adobe Experience Platform.

![Datainmatning](./images/home.png)

Antes de continuar, você preca selecionar um **sandbox**. O nome do sandbox a ser selecionado é Bootcamp. É kapível fazer isso clicando no texto **[!UICONTROL Production Prod]** na linha azul na parte superior da tela. Depois de selecionar o sandbox apropriado, você verá a tela mudando e agora você está em seu [!UICONTROL sandbox] dedikado.

![Datainmatning](./images/sb1.png)

Ingen meny à esquerda, vá para **Destinations** e, em seguida, vá para **Catalog**. Você verá o **Målkatalog**. Fm **Destinations**, clique em **Activate Segments** no cartão **Facebook Custom Audience**.

![RTCDP](./images/rtcdpgoogleseg.png)

Välj **bootcamp-facebook** e clique em **Next**.

![RTCDP](./images/rtcdpcreatedest2.png)

Na lista de segmentos display oníveis, selecione o segmento que você criou no övício anterior. Klicka på **Nästa**.

![RTCDP](./images/rtcdpcreatedest3.png)

Na página **Mapping**, verifique se a caixa de seleção **Apply Transformation** está marcada. Klicka på **Nästa**.

![RTCDP](./images/rtcdpcreatedest4a.png)

Na página **Segmentschema**, välj en **publikens ursprung** e defina como **direkt från kunderna**. Klicka på **Nästa**.

![RTCDP](./images/rtcdpcreatedest4.png)

Por fim, na página **Review**, clique em **Finish**.

![RTCDP](./images/rtcdpcreatedest5.png)

Seu segmento agora está vinculado aos Públicos Personalizados do Facebook. Sempre que um cliente se Qualificar para esse segmento, um sinal será enviado ao lado do servidor (server-side) do Facebook para includes esse cliente no Público Personalizado no lado do Facebook.

No Facebook, você encontrará seu segmento da Adobe Experience Platform em Públicos Personalizados:

![RTCDP](./images/rtcdpcreatedest5b.png)

Agora você pode ver seu público personalizado aparecer no Facebook:

![RTCDP](./images/rtcdpcreatedest5a.png)

[Retornar para Fluxo de Usuário 1](./uc1.md)

[Retornar para Todos os Módulos](../../overview.md)
