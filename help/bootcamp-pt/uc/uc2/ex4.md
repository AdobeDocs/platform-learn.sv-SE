---
title: Bootcamp - Journey Optimizer Create your travel - Brazil
description: Bootcamp - Journey Optimizer Create your travel - Brazil
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Journeys
exl-id: 674a9baa-5900-405e-b744-ea211f60a16d
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# 2.4 Testa sua janda

## Fluxo da husnada do cliente

Abra uma nova janela e anônima do navegador e vá para [https://bootcamp.aepdemo.net](https://bootcamp.aepdemo.net). Clique em **Tillåt alla**. Com base no seu comportamento de navegação no fluxo de usuário anterior, você verá a personalização acontecer na página inicial do site.

![DSN](./images/web8a.png)

Clique no ícone **Profil** ingen canto superior direito da tela.

![Demo](./images/web8b.png)

Clique em **Skapa ett konto**.

![Demo](./images/pv5.png)

Preencha todos os campos do formário. Använd um valor real para endereço de e-mail e número de fax, pois será usado em övícios posteriores para envio de e-mail e SMS.

![Demo](./images/pv7a.png)

Role para baixo. Agora você deve inserir o eventID do seu even to personalizado que você criou no övício 2.2. Você pode encontrá-lo aqui:

![ACOP](./images/payloadeventID.png)

O eventID é o que preca ser enviado à Adobe Experience Platform para acionar a jnada que você construiu. Este é o eventID neste example:
`19cab7852cdef99d25b6d5f1b6503da39d1f486b1d585743f97ed2d1e6b6c74f`

Preencha o eventID no campo **Händelse-ID för att skapa ditt konto** e clique em **Registrera**.

![Demo](./images/pv8a.png)

Em seguida, a tela abaixo será exibida:

![Demo](./images/pv9.png)

Você também receberá este e-mail, que é o e-mail que você mesmo criou como parte deste övício.

![Demo](./images/pv10a.png)

Você terminou este övício.

Próxima etapa: [2.5 Instale e use of aplicativo móvel](./ex5.md)

[Retornar para Fluxo de Usuário 2](./uc2.md)

[Retornar para Todos os Módulos](../../overview.md)
