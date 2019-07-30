---
title: GRC--NFE
description: Customizing GRC-NFE
published: true
date: 2019-07-19T12:02:03.855Z
tags: 
---

# NFE

## Ativar Contingência 

Com a Configuração de contingência já realizada no PI, é necessário ativar contingência no GRC, ela é ativada somente qunado a sefaz ativa contingência.

na SPRO do GRC:

![nfe_contingencia_1.png](/grc/nfe_contingencia_1.png)

![nfe_contingencia_2.png](/grc/nfe_contingencia_2.png)

Após definir para o sistema de SVC ser consultado, executar o programa para atualizar o status do serviço:

> SE38: /XNFE/NFE_CHECK_SRV_STATUS
{.is-success}

![nfe_contingencia_3.png](/grc/nfe_contingencia_3.png)


Agora no ECCna SPRO:

![nfe_contingencia_4.png](/grc/nfe_contingencia_4.png)

![nfe_contingencia_5.png](/grc/nfe_contingencia_5.png)

> Escalonar o JOB para Executar o programa :  J_BNFECALLRFC 
{.is-warning}

![nfe_contingencia_6.png](/grc/nfe_contingencia_6.png)

![nfe_contingencia_7.png](/grc/nfe_contingencia_7.png)



