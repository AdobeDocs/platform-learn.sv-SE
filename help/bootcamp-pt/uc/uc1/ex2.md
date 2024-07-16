---
title: Bootcamp - Real-time Customer Profile - Visualize your own Real-time Customer Profile - UI - Brazil
description: Bootcamp - Real-time Customer Profile - Visualize your own Real-time Customer Profile - UI - Brazil
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Profiles
exl-id: 4eebb080-77fd-4162-aa64-d599f1274c93
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 0%

---

# 1.2 Visualize seu próprio perfil de cliente em tempo real - UI

Neste övício, você irá fazer login na Adobe Experience Platform e visualizar seu próprio Perfil de cliente em tempo real na UI.

## História

Ingen Perfil do cliente em tempo real, todos os dados do perfil são exibidos juntamente com os dados do even to, além das associações de segmentos existentes. Os dados mostrados podem vir de qualquer lugar, de aplicativos da Adobe e soluções externas. Essa é a exibição mais poderosa da Adobe Experience Platform, o verdadeiro local do sistema de upplevelência.

## 1.2.1 Använda en visualização do perfil do cliente na Adobe Experience Platform

Öppna [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer inloggning, você irá acessar a página inicial da Adobe Experience Platform.

![Datainmatning](./images/home.png)

Antes de continuar, você preca selecionar um **sandbox**. O nome do sandbox a ser selecionado é Bootcamp. É kapível fazer isso clicando no texto **[!UICONTROL Production Prod]** na linha azul na parte superior da tela. Depois de selecionar o sandbox apropriado, você verá a tela mudando e agora você está em seu [!UICONTROL sandbox] dedikado.

![Datainmatning](./images/sb1.png)

Ingen meny à esquerda, öppna **profiler** e **Bläddra**.

![Kundprofil](./images/homemenu.png)

Inga smärtor Visualizador de perfil no seu site, você pode encontrar a visão geral da identidade. Cada identidade está vinculada a um namespace.

![Kundprofil](./images/identities.png)

Inga smärtor Visualizador de perfil, agora você pode ver uma identidade semelhante a seguinte:

| Namnutrymme | Identitet |
|:-------------:| :---------------:|
| Experience Cloud ID (ECID) | 19428085896177382402834560825640259081 |

Coma Adobe Experience Platform, todos os IDs são igualmente viktiga. Anteriormente, o ECID era o ID mais importante no contexto da Adobe e todos os outros IDs estavam vinculados ao ECID em uma relação hierárquica. Com a Adobe Experience Platform, isso mudou e cada ID pode ser Consiado um identificador primário.

Normalmente, o identificador primário depende do context. Se você perguntar ao seu Call Center: **Qual é o ID mais importante?** Eles provavelmente responderão: **o número de fax!** Mas se você perguntar à sua equipe de CRM, eles responderão: **o endereço de e-mail!** En Adobe Experience Platform entende essa komplexidade e gerencia isso para você. Cada aplicativo, seja um aplicativo da Adobe ou não, se comunicará com a Adobe Experience Platform referenindo-se ao ID que Consiam Principal. E Simplesmente funciona.

Para eller campo **Identity namespace**, selecione **ECID** e para o campo **Identity Value** insira o ECID que você pode encontrar no smärtel Visualizador de perfil do site do Bootcamp. Klicka på dem **Visa**. Você verá seu perfil na lista. Klicka på **Profil-ID** para abrir seu perfil.

![Kundprofil](./images/popupecid.png)

Agora você tem uma visão geral de algun **Atributos de perfil** importantes do seu perfil de cliente.

![Kundprofil](./images/profile.png)

Öppna **Händelser**, din vokê pode ver som entradas de cada even to de experience ência vinculado ao seu Perfil.

![Kundprofil](./images/profileee.png)

Por fim, accesse a opção de menu **Segment membership**. Agora você verá todos os segmentos que se Qualificam para este perfil.

![Kundprofil](./images/profileseg.png)

Agora vamos criar um novo segmento que permitirá que você personalize a experience ência do cliente para um cliente anônimo ou conhecido.

Próxima etapa: [1.3 Crie um segmento - UI](./ex3.md)

[Retornar para Fluxo de Usuário 1](./uc1.md)

[Retornar para Todos os Módulos](../../overview.md)
