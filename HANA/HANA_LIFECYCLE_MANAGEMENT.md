---
title: SAP HANA LIFECYCLE MANAGEMENT
description: SAP HANA LIFECYCLE MANAGEMENT
published: true
date: 2019-07-17T20:13:24.639Z
tags: 
---

# Transporte de Objetos entre ambientes HANA

Configuração necessário para transporte de objetos criado no HANA, entre os ambientes existentes:

Na Camada Hana de cada ambiente, é necessário a definição de um **content vendor** 

Está configuração foi realizada pelo Eclipse, evitando ter que alterar diretamente no servidor do hana, altera-se então os parametros diretamente do HANA:

![content_vendor.png](/desenvolvimento/content_vendor.png)

> Criar Sistema em Lifecycle Management:
{.is-success}

[SAP HANA Lifecycle Management](https://srvsaphanad:4300/sap/hana/xs/lm/index.html?page=HomeTab)

![life_hana.png](/desenvolvimento/life_hana.png)

> Foi Criado as Rotas de transporte para HDB>>BHQ>>HBP
{.is-success}



---
# Unidade de Entrega
> Criação da Unidade de Entrega:
{.is-success}

![unidade_eclipse.png](/desenvolvimento/hana/unidade_eclipse.png)

![unidade_entrega.png](/desenvolvimento/unidade_entrega.png)
![unidade_entrega_1_entrega.png](/desenvolvimento/unidade_entrega_1_entrega.png)


A definição das unidades de entrega segue o conceito utilizado do HANA de packages, sendo assim as unidades de entrega devem seguir um padrão de aplicação/necessidade.

---

# Realizando Transport

A rota de transporte é Criada baseado na unidade de entrega, seguindo o conceito do  HANA de trabalhar com pacotes, ou entrega de produtos. sua entrega seria feita por releases, subindo o pacote a qual funcionalidade pertence. 

[SAP HANA TRANSPORT](https://srvsaphanaq:4300/sap/hana/xs/lm/index.html?page=TransportTab)

![transp_1.png](/desenvolvimento/transp_1.png)

![transp_2.png](/desenvolvimento/transp_2.png)

![transp_3.png](/desenvolvimento/transp_3.png)

Uma Vez Criada a Rota de transprote, como ela é baseada em uma unidade de entrega não é mais necessário criar novamente a rota, basta somente clicar no botão **Start Transport** que será executado o transporte para o ambiente selecionado dos pacotes pertencentes a unidade de entrega.






