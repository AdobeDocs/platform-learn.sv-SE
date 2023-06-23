---
title: Bootcamp - Customer Journey Analytics - Customer Journey Analytics 101 - Brasilien
description: Bootcamp - Customer Journey Analytics - Customer Journey Analytics 101 - Brasilien
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 63933d9e-b774-483f-b547-188c77440595
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 0%

---

# 4.1 Customer Journey Analytics 101

## Objetivos

- Entenda o que é o CJA
- Entenda qual é o papel do CJA
- Entenda o workflow do CJA: da conexão de dados aos aos insights

## 4.1.1 O que é o Customer Journey Analytics?

O Customer Journey Analytics (CJA) fornece uma interface em que os times de Analytics, Negócios e Tecnologia conseguem unir todos os dados da companhia e analisar a jornada cross channel (online e offline) do cliente de ponta a ponta. O CJA é capaz de fornecer contexto e clareza para essa journnada, trazendo uma visão acionável em cima das dificuldades no processo de conversão e possibilitando o planejamento de upplevelências relevantes e personalizadas nos pontos mais relevantes.

O CJA traz o Analysis Workspace conectado à Adobe Experience Platform. A Adobe Experience Platform é o cérebro da comunicação e da orquestração e, com o CJA, as marcas agora podem contextualizar e visualizar todos esses dados, para que as equipes de negócios e insights possam aprender com eles, analisando toda a jnada on-line para off-line do cliente.

När equipes de negócios e insights podem conversar com o CJA, fazer perguntas e obter respostas em tempo real com a interface do usuário de arrastar e soltar, apontar e clicar e fácil de usar do Analysis Workspace.

![demo](./images/cja-adv-analysis1.png)

## 4.1.2 Principiella fördelar

Os três Principais benefits ícios para os clientes são:

- A Capidade de disonibilizar insights para todos (ou seja, demokratiatizar o acesso aos dados).
- A Capidade de ver o cliente em uma journnada contextual (ou seja, os dados podem ser visualizados sequencialmente, abrangendo múltiplos canais on-line e off-line).
- A Capidade de aproveitar o poder dos dados sem que haja a necessidade (ou seja, allow ite que indivíduos usem dados para desbloquear insights e análises profundamentas para ativação de marketing).

## 4.1.3 ## 4.1.3 Kort escolher i Customer Journey Analytics?

O CJA não se destina a substituir um aplicativo de BI atual, como Power BI, Microstrategy, Locker ou Tableau. O objectivo desses aplicativos de BI é visualizar dados para criar smärtéis corporativos para que todos em uma organização possam ver métricas importantes rapidamente. O objectivo do CJA é trazer poder de análise para as equipes de Marketing e Negócios, tornando-o uma ferramenta de análise obrigatória para essas pessoas



Tradicionalmente, os aplicativos de BI têm sido incapazes de permitir a verdadeira intligência do cliente:

- Eles não podem fazer atribuição e não fazem análises de jnada do cliente.
- Os aplicativos de BI precam saber a pergunta com antecedência
- As consultas interativas são limitadas pela estrutura do banco de dados
- Habilidades de SQL são necessary árias.
- Os aplicativos de BI não tillståndsitem que você pergunte o motivo de um acontecimento.
- Os aplicativos de BI não têm conexão direta com os pontos de contato do cliente.

Portanto, usuários de negócios e analistas chegam a becos sem saída quase imediatamente, tornando a análise cara, lenta, inflexível e desconectada dos sistemas de ação.

Com o CJA você pode ter uma visão Completa da hunada do cliente, usando dados offline e online, com as ferramentas certas para reduzir o tempo de insight, tornando os usuários de negócios independentes para entender por que algo aconteceu e como responder a isso.

![demo](./images/cja-use-case.png)

## 4.1.4 Komprimering av fluxo de trabalho do Customer Journey Analytics

Antes de iniciar os próximos övícios, é essencial compreender quais etapas são necessary árias para trazer dados da Adobe Experience Platform para o CJA para visualizá-los e obter algun insights profundos. É o que chamamos de fluxo de trabalho do CJA. Vamos verificar:

![demo](./images/cja-work-flow.jpg)

Antes de iniciar as etapas acima, não se esqueça da etapa 0, que é compreender os dados que estão DESoníveis na Adobe Experience Platform.

**Skräp in, skräp ut.** Você deve ter uma ideia clara de quais dados estão DISoníveis e como os esquemas na Adobe Experience Platform são configurados. Compreender os dados que estão na Adobe Experience Platform förenkltará as coisas, não só na parte de conexão de dados, mas também na hora de construir visualizações e fazer análises.

## 4.1.5 Etapa 0: Compreender esquemas e datasets da Adobe Experience Platform

Faça loggar in som Adobe Experience Platform acessando a URL: [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Depois de fazer inloggning, você irá acessar a página inicial da Adobe Experience Platform.

![Datainmatning](../uc1/images/home.png)

Antes de continuar, você preca selecionar um **sandlåda**. O nome do sandbox a ser seleconado é ``Bootcamp``. Você pode fazer isso clicando no ícone **[!UICONTROL Prod]** ingen canto superior direito da tela. Depois de selecionar o sandbox apropriado, você verá a tela mudando e agora você está em seu sandbox dedikado.

![Datainmatning](../uc1/images/sb1.png)

Verifique affärsscheman e datasets na Adobe Experience Platform.

| Datauppsättning | Schema |
| ----------------- |-------------| 
| Demo System - händelsedatauppsättning för webbplats (Global v1.1) | Demonstrationssystem - händelseschema för webbplats (Global v1.1) |
| Demo System - händelsedatauppsättning för callcenter (Global v1.1) | Demo System - händelseschema för callcenter (Global v1.1) |
| Demonstrationssystem - händelsedatauppsättning för röstassistenter (Global v1.1) | Demonstrationssystem - händelseschema för röstassistenter (Global v1.1) |

Certifique-se de ter verificado ao menos:

- Identifierare: CRMID, phoneNumber, ECID, email. Quais identidades são os identificadores primários, quais são os identificadores secundários?

Você pode encontrar os identificadores abrindo um schema e observando o objeto `_experienceplatform.identification.core`. Verifierat till schema [Demonstrationssystem - händelseschema för webbplats (Global v1.1)](https://experience.adobe.com/platform/schema).

![demo](./images/identity.png)

- Upptäck o objeto de comércio dentro do schema [Demonstrationssystem - händelseschema för webbplats (Global v1.1)](https://experience.adobe.com/platform/schema).

![demo](./images/commerce.png)

- Visa uppgifter [datauppsättningar](https://experience.adobe.com/platform/dataset/browse?limit=50&amp;page=1&amp;sortDescending=1&amp;sortField=created) e verifique os dados

Agora você está pronto para começar a usar a interface do usuário do Customer Journey Analytics.

Próxima etapa: [4.2 Conecte datasets da Adobe Experience Platform no Customer Journey Analytics](./ex2.md)

[Retornar para Fluxo de Usuário 4](./uc4.md)

[Retornar para Todos os Módulos](../../overview.md)
