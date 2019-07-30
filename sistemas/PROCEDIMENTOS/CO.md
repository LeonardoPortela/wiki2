---
title: SAP-CO
description: Procedimentos Relativos a CO
published: true
date: 2019-07-22T20:36:51.593Z
tags: 
---

# Estorno confirmação CO13

Ao estornar confirmações na CO13, o sistema marca todos os itens como eliminado, porém um único lote fica sem movimentação de estorno.

Para sanar o problema, movimentamos o material do estoque QM para livre, então movimentamos via MB31 com movimento 102 o material estornando o consumo e finalmente via MB1A com movimento 262 aumentamos o estoque do 300000.

Transações utilizadas para analise: CO03, ZMM015, MB51.

![co15_1.jpg](/co15_1.jpg)

![co15_2.jpg](/co15_2.jpg)

![co15_3.jpg](/co15_3.jpg)