---
title: Bootcamp - Mixing physical and digital - Test your travel - Brazil
description: Bootcamp - Mixing physical and digital - Test your travel - Brazil
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Events
exl-id: 04e2877f-8672-4584-8204-4489a7025c63
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---

# 3.4 Testa sua janda

Para testar sua jnada, você deve usar o eventID criado no övício 3.2, que deve ser semelhante ao seguinte.

![ACOP](./images/payloadeventID.png)

O eventID é o que precise a ser enviado à Adobe Experience Platform para acionar a jnada. Neste exemplo, o eventID é:
`e76c0bf0c77c3517e5b6f4c457a0754ebaf5f1f6b9357d74e0d8e13ae517c3d5`.

Abra o aplicativo móvel e vá para a página inicial. Clique no ícone de **Configuração**.

![DSN](./images/appsett.png)

Cole seu eventID no campo **Beacon EventID** e clique em **Save**.

![DSN](./images/beacon1.png)

Antes de continuar, abra esta página da Web em seu compador: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html)

Em seguida, será exibida a tela:

![DSN](./images/screen1.png)

Retorne para a página inicial. Klicka på no ícone do **beacon**.

![DSN](./images/app23.png)

Primeiro, selecione **Bootcamp Screen Beacon** e clique no botão de **entrada** button. Isso permitirá que você simule uma entrada do beacon.

![DSN](./images/app21.png)

Agora confira a tela da loja. Você verá o último produto visualizado aparecer nessa tela em 5 segundos.

![DSN](./images/beacon3.png)

Você também terá recebido sua notificação push.

![DSN](./images/beacon2.png)

Você terminou este övício.

[Retornar para Fluxo de Usuário 3](./uc3.md)

[Retornar para Todos os Módulos](../../overview.md)
