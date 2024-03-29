---
title: Bootcamp - Personalization in the call center - Brazil
description: Bootcamp - Personalization in the call center - Brazil
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
feature: Profiles
exl-id: 7acf778b-042f-4deb-9406-ddcf63daacda
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 0%

---

# 2.6 Personalização no call center

Conforme discutido várias vezes durante o bootcamp, personalizar a experience ência do cliente é algo que deve acontecer de maneira omnichannel. UM call center geralmente é bastante desconectado do restante da jnada do cliente e isso pode, com frekvência, levar a upplevelências frustrantes do cliente, mas não preca ser assim. Vamos moSER um exemplo de como o o call center pode ser facilmente conectado à Adobe Experience Platform, em tempo real.

## Fluxo da husnada do cliente

Ingen övício anterior, usando o aplicativo móvel, você comprou um produto clicando no botão **Köp**.

![DSN](./images/app20.png)

Vamos supor que você tenha uma pergunta sobre o status do seu pedido, o que você faria? Normalmente, você ligaria para o call center.

Antes de ligar para o call center, você just a saber seu **Förmåns-ID**. Você pode encontrar seu ID de fidelidade no Visualizador de Perfil do site.

![DSN](./images/cc1.png)

Nesse caso, o **Förmåns-ID** é **5863105**. Como parte de nossa implação personalizada do recurso de call center no ambiente de demonstração, você deve adicionar um prefixo ao seu **Förmåns-ID**. O prefixo é **11373**, portanto, o ID de fidelidade a ser usado neste exemplo é **11373 5863105**.

Vamos fazer isso agora. Använd seu fax e ligue para o número **+1 (323) 745-1670**.

![DSN](./images/cc2.png)

Será soLawado que você insira seu ID de fidelidade, seguido de **#**. Digite seu ID de fidelidade.

![DSN](./images/cc3.png)

Você ouvirá **Hej, sön nome**. Esse nome é pensiondo Perfil do Cliente em tempo real na Adobe Experience Platform. Você tem 3 escolhas. Pressione o número **1**, **Orderstatus**.

![DSN](./images/cc4.png)

Depois de ouvir o status do seu pedido, você terá a opção de pressionar **1** para voltar ao menu main ou pressionar 2. Pressione **2**.

![DSN](./images/cc5.png)

Em seguida, será soadvokado que você avalie sua experience ência de call center, selecionando um número entre 1 e 5, sendo 1 baixo e 5 alto. Faça a a sua escolha.

![DSN](./images/cc6.png)

Sua chamada para o call center será encerrada.

Åtkomst [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer inloggning, você irá acessar a página inicial da Adobe Experience Platform.

![Datainmatning](./images/home.png)

Antes de continuar, você preca selecionar um **sandlåda**. O nome do sandbox a ser seleconado é ``Bootcamp``. É beível fazer isso clicando no texto **[!UICONTROL Produktionsprodukt]** na linha azul na parte superior da tela. Depois de selecionar o [!UICONTROL sandlåda] apropriado, você verá a tela mudando e agora você está em seu [!UICONTROL sandlåda] dedikat.

![Datainmatning](./images/sb1.png)

Ingen meny à esquerda, acesse **Profiler** e **Bläddra**.

![Kundprofil](./images/homemenu.png)

Markera **Namnutrymme för identitet** **E-post** e insira o endereço de e-mail do seu perfil de cliente. Clique em **Visa**. Clique para abrir seu perfil.

![DSN](./images/cc7.png)

Você verá seu perfil de cliente novamente. Åtkomst **Händelser**.

![DSN](./images/cc8.png)

Em eventos, você verá 2 eventos com um eventType de **callCenter**. O primeiro even to é o resultatado da sua resposta à pergunta **Betygsätt hur nöjd du är med ditt samtal** (avalie seu chamada).

![DSN](./images/cc9.png)

Role um pouco para baixo e você verá o evento que foi registrado quando você selecionou a opção de verificar o **Orderstatus**.

![DSN](./images/cc10.png)

Åtkomst **Segmentmedlemskap**. Agora você verá que 2 segment se Qualificam em seu perfil, em tempo real, com base nas interações que você teve meio do call center. Essas associações de segmento podem e devem ser usadas para impactar qual comunicação e personalização acontece em qualquer outro canal.

![DSN](./images/cc11.png)

Você terminou este övício.

[Retornar para Fluxo de Usuário 2](./uc2.md)

[Retornar para Todos os Módulos](../../overview.md)
