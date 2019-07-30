---
title: GRC
description: Procedimentos Relativos ao GRC
published: true
date: 2019-07-22T14:40:12.329Z
tags: 
---


Links de acesso ao GRC:

[GRC PRODUÇÃO::](https://pmsrvsapnfp.gbj.corp:44300/nwbc/)
[GRC QUALIDADE::](https://pmsrvsapnfq.gbj.corp:44300/nwbc/)
[GRC DESENVOLVIMENTO::](https://pmsrvsapnfd.gbj.corp:44300/nwbc/)

# NFE

## Rejeição 204: Duplicidade de NF-e [nRec:999999999999999]

Quando Status de NFe estivar com codigo 204, significa que já está aprovada na sefaz, ocorrendo mensagem de duplicidade, procedimento padrão no GRC, solicitar Verificação de Status:


![nfe_204.png](/grc/nfe_204.png)

![nfe_204_verificação_de_status.png](/grc/nfe_204_verificação_de_status.png)

O GRC então dispara uma solicitação ao PI para consultar e retornar numero de protocolo de autorização da NFe, ajustando seu status e retornando ao ECC.

---
Caso a NFe já se encontre autorizada na SEFAZ, porém sem retorno, estando em amarelo, é necessário retornar para estado de erro e assim Habilitar obotão de verificação de status, realizando o procedimento anterior.
![204_editar_solicitar_status.png](/grc/204_editar_solicitar_status.png)

> Os campos em destaque deve-se alterar para **02**
{.is-danger}

Repetindo o procedimento.
Caso Relizar a solicitação de status não resolva ou fique travado na solicitação de status necessário realizar o sequinte procedimento:
Consultar a Chave de acesso da NFe em no [Portal Nacional](http://www.nfe.fazenda.gov.br/portal/consultaRecaptcha.aspx?tipoConsulta=completa&tipoConteudo=XbSeqxE8pl8=)

Verificar o Protocolo:

![nfe_protocolo.png](/grc/nfe_protocolo.png)

Editando da Seguinte forma:

> SE16: /XNFE/OUTNFEHD
{.is-success}

![se16_editar.png](/grc/se16_editar.png)

**Ficando da seguinte forma no GRC:**
![grc_editado.png](/grc/grc_editado.png)

> Com o GUID da nota executar o seguinte modulo de função(SE37)
> /XNFE/PROCSTEP_NFOUPDFS
{.is-warning}

![nfe_modulo_funcao.png](/grc/nfe_modulo_funcao.png)):

> Antes de executar a função de atualização do ECC, certificar que está tudo correto, visto que executar pela segunda vez não costuma funcionar
{.is-danger}

Caso tenha ocorrido erro na atualização do ECC, ficando da seguinte forma:

![ecc_erro_nfe.png](/grc/ecc_erro_nfe.png)

Neste Casos é necessário editar diretamente no ECC:
> SE16N: J_1BNFE_ACTIVE
{.is-info}


## CC-e Travado

Evento de carta de correção de NFe Travado.


![cce_travado.png](/grc/cce_travado.png)

Consultar a Chave de acesso da NFE no portal nacional: [Portal Nacional](http://www.nfe.fazenda.gov.br/portal/consultaRecaptcha.aspx?tipoConsulta=completa&tipoConteudo=XbSeqxE8pl8=)

![protocolo_cce.png](/grc/protocolo_cce.png)

Editar conforme a imagem com as informações pertinentes a cada NFe.

![se16_events.png](/grc/se16_events.png)

Com o GUID da NFe deixar da Seguinte forma:

![event_stat.png](/grc/event_stat.png)

No GRC em Eventos:

![grc_evento.png](/grc/grc_evento.png)


![repetir_evento.png](/grc/repetir_evento.png)

O Processo demonstrado deve então atualizar o ECC.




# NFE INBOUND


# CTE

## Desacordo de Serviço:

O Evento de desacordo de serviço, acontece quando o documento recebido pela solução de CT-e Inbound não corresponde a um determinado serviço contratado, sendo assim no monitor do inbound de Cte é feito o envio do evento de Desacordo.
na situação abaixo o evento ficou com erro, não sendo enviado para a SEFAZ, sendo assim caso se consulta-se o CTe no [Portal Nacional CTe](http://www.cte.fazenda.gov.br/portal/consultaRecaptcha.aspx?tipoConsulta=completa&tipoConteudo=mCK/KoCqru0=) na aba de eventos o evento não constaria.


> [Configuração do GRC/PI se encontra em documentaçaõ de desenvolvimento](/sistemas/desenvolvimento)
{.is-success}

>  [Documentação operacional de envio do Evento em Documentação de Processos do GRC.](/PROCESSOS/GRC)
{.is-success}

![desacordo_erro.png](/grc/desacordo/desacordo_erro.png)

Envio do Evento com erro, neste caso com o Evento já configurado em GRC/PI, bastaria continuar processo, ou solicitar verificação de status.

Nenhuma das alternativas tendo sucesso realizar intervenção como o [ajuste de carta de correção.](/SISTEMAS/PROCEDIMENTOS/GRC#rejei%C3%A7%C3%A3o-204-duplicidade-de-nf-e-nrec999999999999999)

Não tendo sucesso Verificar aba Mensagens:

![desacordo_erro_mensagem.png](/grc/desacordo/desacordo_erro_mensagem.png)

Neste caso significa que o evento foi gerado pelo GRC,porém ao ser enviado ao PI ocorreu uma exceção, onde o PI não conseguiu entrar a mensagem a SEFAZ.

> [Verificar Configuração do PIP para evento](/SISTEMAS/DESENVOLVIMENTO/PI)
{.is-info}


# CTE INBOUND


# MDFE





