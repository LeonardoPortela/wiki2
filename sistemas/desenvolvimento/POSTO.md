---
title: Desenvolvimento Posto Transamérica
description: Documentação de Desenvolvimento Posto Transamérica
published: true
date: 2019-07-22T15:12:15.701Z
tags: 
---

# Relatório Notas Fiscais Posto

Desenvolvimento efetuado para trazer dentro do SAP, as notas fiscais de entrada e saida do posto.

Foi Realizado desenvolvimento em nodejs, realizando uma busca dentro do banco de dados Postgresql.

No servidor Node (172.17.1.113) na pasta **C:\node_posto**, contem os arquivos de desenvolvimento.
 
 ## Configuração:
 
 No SAP, criar um parametro na STVARV:
 
>  Transação : STVARV
{.is-warning}

>  Z_HOST_SRV_API_POSTO: HTTP://172.17.1.113:3010
{.is-success}

Apontando para o servidor onde o node está sendo executado.


> Na Transação: ZNFE002 se executa o relatório.
{.is-success}




