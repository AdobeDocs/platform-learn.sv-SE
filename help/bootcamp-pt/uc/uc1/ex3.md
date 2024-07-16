---
title: Bootcamp - kundprofil i realtid - Skapa ett segment - UI - Brasilien
description: Bootcamp - kundprofil i realtid - Skapa ett segment - UI - Brasilien
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Segments
exl-id: 9b8d93b5-5bed-4600-8602-b438a0893612
source-git-commit: ee5c0af17c12f1d90774a3a4150c9788e2368e39
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 2%

---

# 1.3 Krim um segmento - UI

Neste övício, você irá criar um segmento usando o Construtor de Segmentos da Adobe Experience Platform.

## História

Öppna [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer inloggning, você irá acessar a página inicial da Adobe Experience Platform.

![Datainmatning](./images/home.png)

Antes de continuar, você preca selecionar um **sandbox**. O nome do sandbox a ser selecionado é ``Bootcamp``. É kapível fazer isso clicando no texto **[!UICONTROL Production Prod]** na linha azul na parte superior da tela. Depois de selecionar o sandbox apropriado, você verá a tela mudando e agora você está em seu [!UICONTROL sandbox] dedikado.

![Datainmatning](./images/sb1.png)

Ingen meny à esquerda, åtkomst till **segment**. Nesta página, você tem uma visão geral de todos os segmentos exist. Clique no botão + Criar segmento para começar a criar um novo segmento.

![Segmentering](./images/menuseg.png)

Quando estiver no novo construtor de segmentos, você irá perceber imediatamente a opção de menu **Attributes** e a referenência do **XDM Individual Profile**.

![Segmentering](./images/segmentationui.png)

Como o XDM é a linguagem que alimenta o setor de experience ência, o XDM também é a base para o construtor de segmentos. Todos os dados ingeridos na plataforma devem ser mapeados em relação ao XDM e, portanto, todos os dados se tornam parte do mesmo modelo de dados, independent entemente da origem desses dados. Isso oferece uma grande vantagem ao criar segmentos, pois a part dessa interface do usuário do construtor de segmento, é posiível combinar dados de qualquer origem no mesmo fluxo de trabalho. Os segmentos criados no Construtor de segmentos podem ser enviados para soluções como Adobe Target, Adobe Campaign e Adobe Audience Manager para ativação.

Agora você preca criar um segmento de todos os clientes que visualizaram o produto **Real-Time CDP**.

Para construir este segmento, você preca adicionar um Evento de experience ência. Você pode encontrar todos os Eventos de experience ência clicando no ícone **Events** na barra de menu **Fields**.

![Segmentering](./images/findee.png)

Em seguida, você verá o nó **XDM ExperienceEvents** do nível superior. Klicka på **XDM ExperienceEvent**.

![Segmentering](./images/see.png)

Öppna **produktlisteobjekt**.

![Segmentering](./images/plitems.png)

Välj **Namn** e arraysole o objeto **Namn** do menu à esquerda na tela do construtor de segmentos na seção **Events**. Em seguida, o seguinte será exibido:

![Segmentering](./images/eewebpdtlname.png)

O parâmetro de comparação deve ser **equals** e, no campo de entrada, insira **Real-time CDP**.

![Segmentering](./images/pv.png)

Sempre que adicionar um elemento ao construtor de segmentos, você pode clicar no botão **Refresh Estimat** para obter uma nova estimativa da população em seu segmento.

![Segmentering](./images/refreshest.png)

Para **Utvärderingsmetod**, välj **Edge**.

![Segmentering](./images/evedge.png)

Por fim, vamos dar um nome ao seu segmento e salvá-lo.

Como modelo de nomenklatura, använd:

- `seuSobrenome - Interest in Real-Time CDP`

Em seguida, clique no botão **Save and Close** para salvar seu segmento.

![Segmentering](./images/segmentname.png)

Agora você irá retornar à página de visão geral do segmento, onde verá uma visualização de amostra dos perfis de clientes que se Qualificam para o seu segmento.

![Segmentering](./images/savedsegment.png)

Agora você pode continuar no próximo övício e usar seu segmento com o Adobe Target.

Próxima etapa: [1.4 Ação: envie seu segmento para o Adobe Target](./ex4.md)

[Retornar para Fluxo de Usuário 1](./uc1.md)

[Retornar para Todos os Módulos](../../overview.md)
