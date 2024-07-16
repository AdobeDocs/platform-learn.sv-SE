---
title: Bootläger - Customer Journey Analytics - Visualisering med Customer Journey Analytics - Brasilien
description: Bootläger - Customer Journey Analytics - Visualisering med Customer Journey Analytics - Brasilien
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Visualizations
exl-id: eb5eac54-22d8-428b-acac-16570f75085e
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '1569'
ht-degree: 0%

---

# 4.5 Visualização usando o Customer Journey Analytics

## Objetivos

- Entenda a UI do Analysis Workspace
- Conheça algun recursos que tornam o Analysis Workspace tão diferente.
- Aprenda a analisar no CJA usando o Analysis Workspace

## Sammanhang

Neste övício, você usará o Analysis Workspace no CJA para analisar visualizações de produtos, funis de produtos, rotatividade osv.

Vamos usar o projeto que você criou em [4.4 Preparação de dados no Analysis Workspace](./ex4.md), então acesse [https://analytics.adobe.com](https://analytics.adobe.com).

![demo](./images/prohome.png)

Abra seu projeto `yourLastName - Omnichannel Analysis`.

Com seu projeto aberto e Visualização de dados `yourLastName - Omnichannel Analysis` selecionado, você está pronto para começar a construir suas primeiras visualizações.

![demo](./images/prodataView1.png)

## Quantas visualizações de produtos temos diariamente?

Em primeiro lugar, precamos selecionar as data as certas para analisar os dados. Gå till Menu suspenso do calendário no lado direito da tela. Clique nele e selecione o intervalo de data as aplicável.

>[!IMPORTANT]
>
>Selecione um intervalo de data como **This Week** ou **This Month**. Os dados DISoníveis mais recentes foram absorvidos em 19 de setembro de 2022.

![demo](./images/pro1.png)
Ingen meny do lado esquerdo (área de components), encontre as métricas calculadas **Product Views** . Selecione-as e arbela solte na tela, no canto superior direito da tabela de format livre.

![demo](./images/pro2.png)

Automaticamente a dimensão **Day** será adicionada para criar sua primeira tabela. Agora você pode ver sua pergunta respondida imediatamente.

![demo](./images/pro3.png)

Em seguida, clique com o botão direito do mouse no resumo da métrica.

![demo](./images/pro4.png)

Klicka på em **Visualisera** e selecione **Line** como visualização.

![demo](./images/pro5.png)

Você verá as suas visualizações de produto por dia.

![demo](./images/pro6.png)

Você pode alterar o escopo de tempo para o dia clicando em **Settings** na visualização.

![demo](./images/pro7.png)

Klicka på ingen ponto ao lado de **Line** e **Hantera Data Source**.

![demo](./images/pro7a.png)

Em seguida, clique em **Lock Selection** e selecione **Selected Items** para bloquear esta visualização para que ela sempre exiba uma linha do tempo de Visualizações de produtos.

![demo](./images/pro7b.png)

## 5 produtos mais vibest

Quais são os 5 products mais vibest?

Lembre-se de salvar o projeto de tempos em tempos.

| OS | Kort klipp |
| ----------------- |-------------| 
| Windows | Ctrl+S |
| Mac | Kommando + S |

Vamos começar a encontrar os 5 produtos mais vibest. Ingen meny do lado esquerdo, encontre o Nome do produto - Dimensão.

![demo](./images/pro8.png)

Agora arablone solte **Product Name** para substituir a dimensão **Day**:

Este será o resultatado.

![demo](./images/pro10a.png)

Em seguida, tente dividir um dos produtos por Nome da marca. Förklara **brandName** e arablonpara baixo do primeiro nome do produto.

![demo](./images/pro13.png)

Em seguida, faça um detaljhamento usando o Agente de usuário. **Användaragent** e arablono para baixo do nome da marca.

![demo](./images/pro15.png)

Em seguida, será exibida a tela abaixo:

![demo](./images/pro15a.png)

Por fim, você pode adicionar mais visualizações. Ingen lado esquerdo, em visualizações, pesquise `Donut`. Pegue `Donut`, arraysolte na tela sob a visualização **Line** 

![demo](./images/pro18.png)

I tabellen väljer du sedan de första 5 **användaragentraderna** från den uppdelning vi gjorde under **Google Pixel XL 32 GB Black Smartphone** > **Citi Signal** . Håll ned knappen **CTRL** (i Windows) eller knappen **Command** (i Mac) när du markerar de 5 raderna.

Em seguida, na Tabela, selecione as primeiras 5 linhas de **User Agent** do detail hamento que fizemos em **Google Pixel XL 32 GB Black Smartphone** > **Citi Signal**. En seleconar som 5 linhas, segure eller botão **CTRL** (no Windows) eller botão **Command** (no Mac).

![demo](./images/pro20.png)

Você verá o gráfico de donut alternado:

![demo](./images/pro21.png)

Você pode até adaptar o design para ser mais legível, tornando o gráfico de **Line** e o gráfico de **Donut** um pouco menor para que sejam exibidos lado a lado:

![demo](./images/pro22.png)

Klicka på ingen ponto ao lado de *Donut** para **Hantera Data Source**. Em seguida, clique em **Lock Selection** para bloquear essa visualização para que ela sempre exiba uma linha do tempo de Visualizações de produto.

![demo](./images/pro22b.png)

Saiba mais sobre visualizações usando o Analysis Workspace em:

- [https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/freeform-analysis-visualizations.html](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/freeform-analysis-visualizations.html)
- [https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/t-sync-visualization.html](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/t-sync-visualization.html)

## Funil de interação do produto, da visualização à compra

Befintliga multimediaformat de resolver esta questão. Uma dela é usar o Tipo de Interação de Produto e usá-lo em uma tabela de formato livre. Outra forma é usar uma **Fallout Visualization**. Vamos usar o último, pois queremos visualizar e analisar ao mesmo tempo.

Feche o smärtan atual clicando aqui:

![demo](./images/pro23.png)

Agora adicione um novo smärtel em branco clicando em **+ Lägg till tom panel**.

![demo](./images/pro24.png)

Clique na visualização de **Fallout**.

![demo](./images/pro25.png)

Selecione o mesmo intervalo de data do övício anterior.

![demo](./images/prodatef.png)

Em seguida, você verá:

![demo](./images/prodatefa.png)

Ange en dimensão **Event Type** nos-komponent utan lado esquerdo:

![demo](./images/pro26.png)

Clique na seta para abrir a dimensão:

![demo](./images/pro27.png)

Você verá todos os Tipos de eventos DISoníveis.

![demo](./images/pro28.png)

Markera ett av objekten **commerce.productViews** e arraysolte-o no campo **Add Touchpoint** dentro da **Fallout Visualization** .

![demo](./images/pro29.png)

Faça o mesmo com **commerce.productListAdds** och **commerce.purchase** e solte-os no campo **Add Touchpoint** dentro da **Fallout Visualization** . Sua visualização agora deve ser semelhante ao seguinte:

![demo](./images/props1.png)

Você pode fazer muitas coisas aqui. Algun-exempel: Comparar ao longo do tempo, Comparar cada passo por disposivo ou Comparar por fidelidade. No entanto, se quisermos analisar coisas interessantes como porque os clientes não compram depois de adicionar um item ao carrinho, podemos usar a melhor ferramenta do CJA: clicar com o botão direito.

Click com o botão direito do mouse no touchpoint **commerce.productListAdds**. Em seguida, clique em **Breakdown fallout at this touch point**.

![demo](./images/pro32.png)

Uma nova tabela de formato livre será criada para analisar o que as pessoas fizeram se não compraram.

![demo](./images/pro33.png)

Ändra till **Händelsetyp** av **Sidnamn**, na nova tabela de formato livre, para ver em quais páginas eles estão indo, em vez da Página de confirmção de compra.

![demo](./images/pro34.png)

## O que as pessoas fazem no site antes de acessar a página Cancelar serviço?

Novamente, há muitas formas de realizar essa análise. Vamos usar a análise de fluxo para iniciar parte da descoberta.

Feche o smärtan atual clicando aqui:

![demo](./images/pro0.png)

Agora adicione um novo smärtel em branco clicando em **+ Lägg till tom panel**.

![demo](./images/pro0a.png)

Clique na visualização **Flow**.

![demo](./images/pro35.png)

Em seguida, será exibido:

![demo](./images/pro351.png)

Selecione o mesmo intervalo de data do övício anterior.

![demo](./images/pro0b.png)

Ange en dimensão **Page Name** nos-komponent utan lado esquerdo:

![demo](./images/pro36.png)

Clique na seta para abrir a dimensão:

![demo](./images/pro37.png)

Você encontrará todas as páginas view. Encontre o nome da página: **Avbryt tjänst**.
Arrappe solte **Cancel Service** na Visualização de fluxo no campo do meio:

![demo](./images/pro38.png)

Em seguida, será exibido:

![demo](./images/pro40.png)

Vamos agora analisar se os clientes que visitaram a página C **Cancel Service** no site também ligaram para o call center e qual foi o resultado.

Nas dimensões, retorne e encontre Tipo de interação de chamada. Arrappe solte **Call Interaction Type** para substituir a primeira interação à direita em **Flow Visualization**.

![demo](./images/pro43.png)

Agora você visualiza o tickets de suporte dos clientes que ligaram para a central de atendimento depois de visitar a página **Cancel Service**.

![demo](./images/pro44.png)

Em seguida, nas dimensões, procure **Call Feeling**. Arablone solte para substituir a primeira interação à direita na visualização de fluxo.

![demo](./images/pro46.png)

Em seguida, será exibido:

![demo](./images/flow.png)

Como pode ver, exutamos uma análise omnichannel usando a visualização de fluxo. Graças a isso, descobrimos que algun clientes que estavam pensando em cancelar o serviço tiveram uma avaliação positiva depois de ligar para o call center. Talvez tenhamos mudado de ideia com uma promoção?

## Qual é o desempenho dos clientes com um contato de Call center Positivo em relação aos Principais KPIs?

Primeiramente, vamos segmentar os dados para obter apenas usuários com chamadas **positive**. Ingen CJA, os Segmentos são chamados de Filtros. Acesse para filtros na área de components (no lado esquerdo) e clique em **+**.

![demo](./images/pro58.png)

Dentro do Construtor de filtro, dê um nome ao filtro

| Namn | Beskrivning |
| ----------------- |-------------| 
| Samtalskunskap - positiv | Samtalskunskap - positiv |

![demo](./images/pro47.png)

Inga komponenter (dentro do Construtor de filtro), encontre **Call Feeling** e arablone solte na Definição do construtor de filtro.

![demo](./images/pro48.png)

Agora selecione **positive** como valor para o filtro.

![demo](./images/pro49.png)

Ändra o escopo para o nível **Person**.

![demo](./images/pro50.png)

Para finalizar, basta clicar em **Save**.

![demo](./images/pro51.png)

Então, você irá retornar para esta tela. Se ainda não retornou, feche o smärtel anterior.

![demo](./images/pro0c.png)

Agora adicione um novo smärtel em branco clicando em **+ Lägg till tom panel**.

![demo](./images/pro24c.png)

Selecione o mesmo intervalo de data do övício anterior.

![demo](./images/pro24d.png)

Klicka på em **Frihandstabell**.

![demo](./images/pro52.png)

Agora arablone solte o filtro que você acabou de criar.

![demo](./images/pro53.png)

Hora de adicionar algumas métricas. Comece com **Product Views**. Arrappe solte na tabela de forma livre. Você também pode excluir a métrica **Events**.

![demo](./images/pro54.png)

Faça o mesmo com **People**, **Add to Cart** e **Purchases**. Você vai acabar com uma tabela como a seguinte.

![demo](./images/pro55.png)

Graças à primeira análise de fluxo, uma nova pergunta surgiu. Então decidimos criar esta tabela e verificar algun KPIs em segmento para responder a essa pergunta. Como você pode ver, o tempo de insight é muito mais rápido que usar SQL ou usar outras soluções de BI.

## Rekapitulação do Analysis Workspace e do Customer Journey Analytics

O Analysis Workspace remove todas as limitações típicas de um relório do Analytics. Ele fornece uma tela robusta e flexível para criar projetos de analytics personalizados. Arablone solte qualquer número de tabelas de dados, visualizações e components (dimensões, métricas, segmentos e granularidades de tempo) para um projeto. Você pode criar de format instantânea filtros e analises, gráficos de coorte, alertas, segmentos, análises de fluxo e relórios de curadoria e dagamento para compartilhar com qualquer pessoa em seu negócio.

Próxima etapa: [4.6 De insights a ação](./ex6.md)

[Retornar para Fluxo de Usuário 4](./uc4.md)

[Retornar para Todos os Módulos](./../../overview.md)
