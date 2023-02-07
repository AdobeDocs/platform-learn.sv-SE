---
title: Bootcamp - Real-time Customer Profile - Visualize your own Real-time Customer Profile - UI - Brazil
description: Bootcamp - Real-time Customer Profile - Visualize your own Real-time Customer Profile - UI - Brazil
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
source-git-commit: 5d824244766135cd4998feab48be7f6a69c42a70
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 1%

---

# 1.2 Visualize seu próprio perfil de cliente em tempo real - UI

Neste övício, você irá fazer login na Adobe Experience Platform e visualizar seu próprio Perfil de cliente em tempo real na UI.

## História

Ingen Perfil do cliente em tempo real, todos os dados do perfil são exibidos juntamente com os dados do even to, além das associações de segmentos existentes. Os dados mostrados podem vir de qualquer lugar, de aplicativos da Adobe e soluções externas. Essa é a exibição mais poderosa da Adobe Experience Platform, o verdadeiro local do sistema de upplevelência.

## 1.2.1 Använda en visualização do perfil do cliente na Adobe Experience Platform

Åtkomst [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer inloggning, você irá acessar a página inicial da Adobe Experience Platform.

![Datainmatning](./images/home.png)

Antes de continuar, você preca selecionar um **sandlåda**. O nome do sandbox a ser selecionado é Bootcamp. É beível fazer isso clicando no texto **[!UICONTROL Produktionsprodukt]** na linha azul na parte superior da tela. Depois de selecionar o sandbox apropriado, você verá a tela mudando e agora você está em seu [!UICONTROL sandlåda] dedikat.

![Datainmatning](./images/sb1.png)

Ingen meny à esquerda, acesse **Profiler** e **Bläddra**.

![Kundprofil](./images/homemenu.png)

Inga smärtor Visualizador de perfil no seu site, você pode encontrar a visão geral da identidade. Cada identidade está vinculada a um namespace.

![Kundprofil](./images/identities.png)

Inga smärtor Visualizador de perfil, agora você pode ver uma identidade semelhante a seguinte:

| Namnutrymme | Identitet |
|:-------------:| :---------------:|
| Experience Cloud ID (ECID) | 19428085896177382402834560825640259081 |

Coma Adobe Experience Platform, todos os IDs são igualmente viktiga. Anteriormente, o ECID era o ID mais importante no contexto da Adobe e todos os outros IDs estavam vinculados ao ECID em uma relação hierárquica. Com a Adobe Experience Platform, isso mudou e cada ID pode ser Consiado um identificador primário.

Normalmente, o identificador primário depende do contexto. Se você perguntar ao seu Call Center: **Qual é o ID mais importante?** Eles provavelmente responderão: **o número de fax!** Mas se você perguntar à sua equipe de CRM, eles responderão: **o endereço de e-mail!** A Adobe Experience Platform entende essa komplexidade e gerencia isso para você. Cada aplicativo, seja um aplicativo da Adobe ou não, se comunicará com a Adobe Experience Platform referenindo-se ao ID que Consiam Principal. E Simplesmente funciona.

Para eller campo **Namnutrymme för identitet**, selecione **ECID** e para o campo **Identitetsvärde** insira o ECID que você pode encontrar no smärtel Visualizador de perfil do site do Bootcamp. Clique em **Visa**. Você verá seu perfil na lista. Klick nej **Profil-ID** para abrir seu perfil.

![Kundprofil](./images/popupecid.png)

Agora você tem uma visão geral de algun **Atributos de perfil** Importantes do seu perfil de cliente.

![Kundprofil](./images/profile.png)

Åtkomst **Händelser**, ond você pode ver as entradas de cada even to de experience ência vinculado ao seu Perfil.

![Kundprofil](./images/profileee.png)

Por fim, acesse a opção de menu **Segmentmedlemskap**. Agora você verá todos os segmentos que se Qualificam para este perfil.

![Kundprofil](./images/profileseg.png)

Agora vamos criar um novo segmento que permitirá que você personalize a experience ência do cliente para um cliente anônimo ou conhecido.

Próxima etapa: [1.3 Krim um segmento - UI](./ex3.md)

[Retornar para Fluxo de Usuário 1](./uc1.md)

[Retornar para Todos os Módulos](../../overview.md)
