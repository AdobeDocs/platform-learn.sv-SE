---
title: Bootläger - Customer Journey Analytics - Dataförberedelse i Analysis Workspace - Brasilien
description: Bootläger - Customer Journey Analytics - Dataförberedelse i Analysis Workspace - Brasilien
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Workspace Basics, Calculated Metrics
exl-id: d56128af-dd1e-47ea-922f-85418e9da687
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '808'
ht-degree: 0%

---

# 4.4 Preparação de dados em Customer Journey Analytics

## Objetivos

- Entenda a UO do Analysis Workspace no CJA
- Entenda os conceitos de preparação de dados no Analysis Workspace
- Aprenda a fazer cálculos de dados

## 4.4.1 Gränssnittet gör Analysis Workspace inget CJA

O Analysis Workspace remove todas as limitações típicas de um único relório do Analytics. Ele fornece uma tela robusta e flexível para criar projetos de analytics personalizados. Arablone solte qualquer número de tabelas de dados, visualizações e components (dimensões, métricas, segmentos e granularidades de tempo) para um projeto. Criação instantânea de avarias e segmentos, criação de cortes para análise, criação de alertas, Comparação de segmentos, análise de fluxo e de falhas e relatórios de curadoria e dagamento para compartilhar com qualquer pessoa em seu negócio.

O Customer Journey Analytics traz essa solução além dos dados da plataforma. É altamente recomendável assistir a este vídeo de visão geral de quatro minutes:

>[!VIDEO](https://video.tv.adobe.com/v/35109?quality=12&learn=on)

Se você nunca usou o Analysis Workspace antes, recomendamos este vídeo:

>[!VIDEO](https://video.tv.adobe.com/v/26266?quality=12&learn=on)

### Crie Seu Projeto

Agora é hora de criar seu primeiro projeto do CJA. Vá para a aba de projetos dentro do CJA. Klicka på **Skapa ny**.

![demo](./images/prmenu.png)

Em seguida, você verá a tela abaixo. Välj **Tomt projekt** então clique em **Create**.

![demo](./images/prmenu1.png)

Você verá um projeto vazio.

![demo](./images/premptyprojects.png)

Primeiro, certifique-se de selecionar a Visualização de dados correta no canto superior direito da tela. Neste exemplo, a Visualização de dados a ser selecionada é `vangeluwe - Omnichannel Data View`.

![demo](./images/prdv.png)

Em seguida, você irá salvar seu projeto e dar um nome a ele. Você pode usar o seguinte comando para salvar:

| OS | Kort klipp |
| ----------------- |-------------| 
| Windows | Ctrl+S |
| Mac | Kommando + S |

Popup-fönstret Você verá este:

![demo](./images/prsave.png)

Använd este modelo de nomenklatura:

| Namn | Beskrivning |
| ----------------- |-------------| 
| `yourLastName - Omnichannel Analysis` | `yourLastName - Omnichannel Analysis` |

Em seguida, clique em **Save**.

![demo](./images/prsave2.png)

## 4.4.2 Métricas calculadas

Embora tenhamos organizado todos os Componentes na Visualização de dados, você ainda deve adaptar algun stjärtar que os usuários de negócios estejam prtos para iniciar suas análises. Além disso, durante qualquer processo de analytics, você pode criar métricas calculadas para aprogrundläggande ar a descoberta de insights.

Como exemplo, criaremos uma Taxa de conversão calculada usando a métrica/even to Compras que definimos na Visualização de dados.

## Taxa de conversão

Vamos começar a abrir o construtor de métricas calculadas. Clique em **+** para criar sua primeira Métrica calculada on Analysis Workspace.

![demo](./images/pradd.png)

O **Calculated Metric Builder** irá aparecer:

![demo](./images/prbuilder.png)

Encontre **Purchases** na lista de métricas no menu do lado esquerdo. Em **Metrics** clique em **Show all**

![demo](./images/calcbuildercr1.png)

Agora arablone solte a métrica **Purchases** na definção da métrica calculada.

![demo](./images/calcbuildercr2.png)

Normalmente, taxa de conversão signifika **Conversions / Sessions**. Então, vamos fazer o mesmo cálculo na tela de definção de métrica calculada. Encontre a métrica **Sessions** e arablone solte-a no criador de definção, no even to **Purchases**.

![demo](./images/calcbuildercr3.png)

Observera que o operador de divisão é selecionado automcamente.

![demo](./images/calcbuildercr4.png)

En taxa de conversão é comumente representada em porcentagem. Então, vamos mudar o formo para porcentagem e selecionar 2 casas decimais.

![demo](./images/calcbuildercr5.png)

Äntligen ändrar du namnet och beskrivningen för det beräknade måttet:

| Titel | Beskrivning |
| ----------------- |-------------| 
| Konverteringsgrad | Konverteringsgrad |

Por fim, alterne o nome e a descrição da métrica calculada:

![demo](./images/calcbuildercr6.png)

Não se esqueça de **Salvar** a Métrica calculada.

![demo](./images/pr9.png)

## 4.4.3 Dimensões calculadas: Filtros (segmentação) e intervalos de data

### Filtros: Dimensões calculadas

Os cálculos não devem ser apenas para métricas. Antes de iniciar qualquer análise, também é interessante criar algumas **Beräknade Dimensioner**. Isso signifika, essencialmente, **segments** no Adobe Analytics. Ingen Customer Journey Analytics, använder segment são chamados de **Filters**.

![demo](./images/prfilters.png)

A criação de filtros ajudará os usuários de negócios a iniciar o analytics com algumas dimensões calculadas valiosas. Isso irá automzar algumas tarefas, além de ajudar na parte de adoção. Abaixo estão algun:

1. Mídia Própria, Mídia Paga
2. Visitas novas x recorrentes
3. Clientes com carrinho

Esses filtros podem ser criados antes ou durante a parte de análise (o que você fará no próximo övício).

### Intervalos de data: Dimensões de tempo calculadas

As dimensões de tempo são outro tipo de dimensões calculadas. Algun já foram criados, mas você também pode criar suas próprias Dimensões de tempo personalizadas na fase de preparação de dados.

Essas Dimensões de tempo calculado ajudarão analistas e usuários de negócios a lembrar data as importantes e usá-las para filtrar e alterar o tempo de relório. Perguntas e dúvidas típicas quando fazemos análises:

- Quando foi a Black Friday do ano passado? Entre os dias 21 e 29?
- Quando veiculamos aquela campanha de TV em dezembro?
- De quando a quando fizemos as vendas de verão de 2018? Quero Comparar com 2019. En propósito, você sabe os dias exatos em 2019?

![demo](./images/timedimensions.png)

Agora você final o övício de preparação de dados usando o Analysis Workspace do CJA.

Próxima etapa: [4.5 Visualização usando Customer Journey Analytics](./ex5.md)

[Retornar para Fluxo de Usuário 4](./uc4.md)

[Retornar para Todos os Módulos](./../../overview.md)
