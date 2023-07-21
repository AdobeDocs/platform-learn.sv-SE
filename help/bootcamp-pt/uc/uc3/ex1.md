---
title: Bootcamp - Blending physical and digital - Use the mobile app and trigger a beacon entry - Brazil
description: Bootcamp - Blending physical and digital - Use the mobile app and trigger a beacon entry - Brazil
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Mobile SDK
exl-id: 14bfbebe-6df3-4a0e-875c-b4c0d016f8da
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 0%

---

# 3.1 Användning av aplicativo móvel e acione um beacon

## Instale of aplicativo móvel

Antes de installar o aplicativo, é necessary ário habilitar o **Rastreamento** ingen disposivo iOS. Para isso, acesse **Configurações** > **Privacidade e segurança** > **Rastreamento** e verifique a opção **Permitir que os aplicativos solicitem o rastreamento**.

![DSN](./../uc3/images/app4.png)

Öppna ett App Store da Apple e pesquise `aepmobile-bootcamp`. Clique em **Instalar** Du **Hämta**.

![DSN](./../uc3/images/app1.png)

Depois que o aplicativo estiver installado, clique em **Abrir**.

![DSN](./../uc3/images/app2.png)

Clique em **OK**.

![DSN](./../uc3/images/app9.png)

Clique em **Permitir**.

![DSN](./../uc3/images/app3.png)

Klicka **Jag håller med**.

![DSN](./../uc3/images/app7.png)

Clique em **Permitir enquanto usa o aplicativo**.

![DSN](./../uc3/images/app8.png)

Clique em **Permitir**.

![DSN](./../uc3/images/app5.png)

Agora você está no aplicativo, na página inicial, pronto(a) para verificar toda a tjandnada do cliente.

![DSN](./../uc3/images/app12.png)

## Fluxo da husnada do cliente

Primeiramente, é required ário fazer to login. Clique em **Inloggning**.

![DSN](./images/app13.png)

Depois de criar sua conta nos övícios anteriores, isso é exibido no site. Agora é necessary ário reutilizar o endereço de e-mail da conta que você criou no aplicativo para fazer o login.

![Demo](./images/pv1.png)

Digite o endereço de e-mail que você usou no site e clique em **Inloggning**.

![DSN](./images/app14.png)

Você receberá uma bekräftmação de que está conectado e receberá uma notificação push.

![DSN](./images/app15.png)

Retorne para a página inicial do aplicativo e os recursos adicionais irão aparecer.

![DSN](./images/app17.png)

Primeiro, acesse **Produkter**. Clique em qualquer produto, neste example: **Kaffe att gå**.

![DSN](./images/app19.png)

Você verá a página do produto **Kaffe att gå** ingen aplicativo.

![DSN](./images/app20.png)

Agora você irá simular um even to de entrada de sinalização (beacon) em uma loja offline. O object tivo da simulação é personalizar a experience ência do cliente nas telas da loja. Para visualizar a experience ência na loja, foi criada uma página que mostrará de forma dinâmica as informações relevantes para o cliente ao entrar na loja.

Antes de continuar, abra esta página da Web em seu compador: [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html)

Em seguida, a tela abaixo será exibida:

![DSN](./images/screen1.png)

Em seguida, retorne para a página inicial. Clique no ícone do **beacon**.

![DSN](./images/app23.png)

Após essa etapa, o seguinte será exibido. Primeiro, selecione **Bootcamp Screen Beacon** e clique no botão de **entrada**. Isso permitirá que você simule uma entrada de sinalização com beacon.

![DSN](./images/app21.png)

Agora confira a tela da loja. Você verá o último produto visualizado aparecer nessa tela em 5 segundos.

![DSN](./images/screen2.png)

Em seguida, retorne para **Produkter**. Clique em qualquer produto, neste example: **Strandfilt Tan**.

![DSN](./images/app22.png)

Em seguida, retorne para a página inicial. Clique no ícone do **beacon**.

![DSN](./images/app23.png)

Fyrkant, selecone **Bootcamp Screen Beacon** e clique no botão de **Entrada** novamente. Isso permitirá que você simule uma entrada de sinalização (beacon).

![DSN](./images/app21.png)

Agora, confira a tela da loja novamente. Você verá o último produto visualizado aparecer nessa tela em 5 segundos.

![DSN](./images/screen3.png)

Agora, vamos verificar também o seu Visualizador de Perfil no site. Você verá muitos eventos que foram adicionados, para moedereller que qualquer interação com um cliente é coletada e armazenada na Adobe Experience Platform.

![DSN](./images/screen4.png)

Nr. próximos övícios, você irá configurar e testar sua própria husnada de entrada do beacon.

Próxima etapa: [3.2 Kriminalvårdsöar till och med](./ex2.md)

[Retornar para Fluxo de Usuário 3](./uc3.md)

[Retornar para Todos os Módulos](../../overview.md)
