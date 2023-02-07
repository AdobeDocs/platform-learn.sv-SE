---
title: Bootcamp - kundprofil i realtid - Skapa ett segment - UI - Brasilien
description: Bootcamp - kundprofil i realtid - Skapa ett segment - UI - Brasilien
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
source-git-commit: 5d824244766135cd4998feab48be7f6a69c42a70
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 2%

---

# 1.3 Krim um segmento - UI

Neste övício, você irá criar um segmento usando o Construtor de Segmentos da Adobe Experience Platform.

## História

Åtkomst [Adobe Experience Platform](https://experience.adobe.com/platform). Depois de fazer inloggning, você irá acessar a página inicial da Adobe Experience Platform.

![Datainmatning](./images/home.png)

Antes de continuar, você preca selecionar um **sandlåda**. O nome do sandbox a ser seleconado é ``Bootcamp``. É beível fazer isso clicando no texto **[!UICONTROL Produktionsprodukt]** na linha azul na parte superior da tela. Depois de selecionar o sandbox apropriado, você verá a tela mudando e agora você está em seu [!UICONTROL sandlåda] dedikat.

![Datainmatning](./images/sb1.png)

Ingen meny à esquerda, acesse **Segment**. Nesta página, você tem uma visão geral de todos os segmentos exist. Clique no botão + Criar segmento para começar a criar um novo segmento.

![Segmentering](./images/menuseg.png)

Quando estiver no novo construtor de segmentos, você irá perceber imediatamente a opção de menu **Attribut** e a referência do **Individuell XDM-profil**.

![Segmentering](./images/segmentationui.png)

Como o XDM é a linguagem que alimenta o setor de experience ência, o XDM também é a base para o construtor de segmentos. Todos os dados ingeridos na plataforma devem ser mapeados em relação ao XDM e, portanto, todos os dados se tornam parte do mesmo modelo de dados, independent entemente da origem desses dados. Isso oferece uma grande vantagem ao criar segmentos, pois a part dessa interface do usuário do construtor de segmento, é posiível combinar dados de qualquer origem no mesmo fluxo de trabalho. Os segmentos criados no Construtor de segmentos podem ser enviados para soluções como Adobe Target, Adobe Campaign e Adobe Audience Manager para ativação.

Agora você preca criar um segmento de todos os clientes que visualizaram o produto **Real-Time CDP**.

Para construir este segmento, você preca adicionar um Evento de experience ência. Você pode encontrar todos os Eventos de Experience ência clicando no ícone **Händelser** na barra de menu **Fält**.

![Segmentering](./images/findee.png)

Em seguida, você verá o nó **XDM ExperienceEvents** do nível superior. Clique em **XDM ExperienceEvent**.

![Segmentering](./images/see.png)

Åtkomst **Produktlisteobjekt**.

![Segmentering](./images/plitems.png)

Markering **Namn** e arablonsolte o objeto **Namn** do menu à esquerda na tela do construtor de segmentos na seção **Händelser**. Em seguida, o seguinte será exibido:

![Segmentering](./images/eewebpdtlname.png)

O parâmetro de Comparação deve ser **är lika med** e, no campo de entrada, insira **CDP i realtid**.

![Segmentering](./images/pv.png)

Sempre que adicionar um elemento ao construtor de segmentos, você pode clicar no botão **Uppdatera offert** para obter uma nova estimativa da população em seu segmento.

![Segmentering](./images/refreshest.png)

Para **Utvärderingsmetod**, selecione **Edge**.

![Segmentering](./images/evedge.png)

Por fim, vamos dar um nome ao seu segmento e salvá-lo.

Como modelo de nomenklatura, använd:

- `seuSobrenome - Interest in Real-Time CDP`

Em seguida, clique no botão **Spara och stäng** para salvar seu segmento.

![Segmentering](./images/segmentname.png)

Agora você irá retornar à página de visão geral do segmento, onde verá uma visualização de amostra dos perfis de clientes que se Qualificam para o seu segmento.

![Segmentering](./images/savedsegment.png)

Agora você pode continuar no próximo övício e usar seu segmento com o Adobe Target.

Próxima etapa: [1.4 Ação: envie seu segmento para o Adobe Target](./ex4.md)

[Retornar para Fluxo de Usuário 1](./uc1.md)

[Retornar para Todos os Módulos](../../overview.md)
