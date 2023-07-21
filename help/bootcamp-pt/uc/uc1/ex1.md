---
title: Bootcamp - Real-time Customer Profile - From unknown to known on the website - Brazil
description: Bootcamp - Real-time Customer Profile - From unknown to known on the website - Brazil
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Profiles
exl-id: 853a69d2-5dac-413d-bb40-ef29604a26ae
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# 1.1 Do desconhecido ao conhecido em nosso site

## Sammanhang

En Adobe Experience Platform desempenha um papel importante nessa jnada. A plataforma é o cérebro da comunicação, o **upplevelsesystem**.

Plataforma é um ambiente em que a palavra cliente engloba mais do que clientes conhecidos. UM visitante desconhecido no site também é um cliente do ponto de vista da Plataforma e, como tal, todo o comportamento de um visitante desconhecido também é enviado à Plataforma. Graças a essa abordagem, quando esse visitante se torna um cliente conhecido, uma marca também pode visualizar o que aconteceu antes daquele momento. Isso ajuda a part de uma perspectiva de otimização de atribuição e experience ência.

## Fluxo da husnada do cliente

Åtkomst [https://bootcamp.aepdemo.net](https://bootcamp.aepdemo.net). Clique em **Tillåt alla**.

![DSN](./images/web8.png)

Clique no ícone do logotipo da Adobe no canto superior esquerdo da tela para abrir o Visualizador de perfil.

![Demo](./images/pv1.png)

Verifique o smärtel do Visualizador de perfil e no Perfil do cliente em tempo real com o **Experience Cloud ID** como o identificador primário para este cliente que ainda é desconhecido.

![Demo](./images/pv2.png)

Você também pode ver todos os Eventos de Experiência coletados com base no comportamento do cliente. En lista está vazia no momento, mas isso mudará em breve.

![Demo](./images/pv3.png)

Öppna en opção de menu **Programtjänster** e clique no produto **Real-Time CDP**.

![Demo](./images/pv4.png)

Você verá a página de details do produto. UM Evento de experience ência do tipo **Produktvy** agora foi enviado para a Adobe Experience Platform usando a implação do Web SDK que você reviou no Módulo 1. Abra o smärtel Visualizador de perfil e verifique seus **Experience Events**.

![Demo](./images/pv5.png)

Öppna en opção de menu **Programtjänster** e clique no produto **Adobe Journey Optimizer**. Mais um Evento de experience ência foi enviado para a Adobe Experience Platform.

![Demo](./images/pv7.png)

Abra o smärtel Visualizador de perfil. Agora você verá 2 Eventos de Experience ência do tipo **Produktvy**. Embora o comportamento seja anônimo, cada clique é rastreado e armazenado na Adobe Experience Platform. Depois que o cliente anônimo se tornar conhecido, poderemos mesclar todo o comportamento anônimo automcamente ao perfil conhecido.

![Demo](./images/pv8.png)

Agora vamos analisar seu perfil de cliente e usar seu comportamento para personalizar sua experience ência do cliente no site.

Próxima etapa: [1.2 Visualize seu próprio perfil de cliente em tempo real - UI](./ex2.md)

[Retornar para Fluxo de Usuário 1](./uc1.md)

[Retornar para Todos os Módulos](../../overview.md)
