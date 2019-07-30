---
title: INBOUND NFE
description: Documentação PI Inbound NFe
published: true
date: 2019-07-22T11:56:58.246Z
tags: 
---

# INBOUND NFE

Links de acesso ao GRC:

[GRC PRODUÇÃO::](https://pmsrvsapnfp.gbj.corp:44300/nwbc/)
[GRC QUALIDADE::](https://pmsrvsapnfq.gbj.corp:44300/nwbc/)
[GRC DESENVOLVIMENTO::](https://pmsrvsapnfd.gbj.corp:44300/nwbc/)

O Inbound NFe-SAP consiste na etapa de entrada de NFes, a Recepção das Notas é realizada seguindo a funcionalidade da Receita de listagem e download das NFes emitidas contra o CNPJ da empresa.
Sendo assim o processo consiste em:

Consultar NFes emitidas contra o CNPJ, listando a partir do úl!timo NSU notas ainda não manifestadas(mais informações na seção de operação Manifesto NFe).

GRC então utilizando das interfaces do  PI consome o webservice de distribuição de documentos eletrônicos (DFe)
Notas pendentes então são listadas na solução NFE Inbound SAP, para continuar o processo.

Para o correto funcionamento os CNPJS que deseja consulta junto a SEFAZ nacional, precisam estar configuradas no PI, cada novo CNPJ precisa ser incluído na condição de determinação de sua empresa, segue configuração do Serviço de distribuição de documentos eletrônicos:

> Links de Acesso PI:
> 
> [PID - Process Integration](http://pmsrvsappid.gbj.corp:50000/dir/start/index.jsp)
> [PIQ - Process Integration](http://pmsrvsappiq.gbj.corp:50000/dir/start/index.jsp)
> [PIP - Process Integration](http://pmsrvsappip.gbj.corp:50000/dir/start/index.jsp)
{.is-info}

![manifesto_1.png](/desenvolvimento/imagens_pi/manifesto_pi/manifesto_1.png)


Como é recuperado as NFes por CNPJ, é necessário criar um canal de comunicação por CNPJ, sendo assim, foi criado uma Party **NFE_AN** , o serviço de distribuição de documentos fiscais, é realizado pela [sefaz Nacional](http://www.nfe.fazenda.gov.br/portal/webServices.aspx?tipoConteudo=Wak0FwB7dKs=#AN)

![sefaz_an.png](/desenvolvimento/imagens_pi/manifesto_pi/sefaz_an.png)

Foi Então criado um **Bussines Component** para Cada CNPJ, visto que a comunicação precisa ser realizada com o certificado digital:

![manifesto_4.png](/desenvolvimento/imagens_pi/manifesto_pi/manifesto_4.png)
![manifesto_5.png](/desenvolvimento/imagens_pi/manifesto_pi/manifesto_5.png)



É Criado então um canal de comunicação com a sefaz AN, após o primeiro canal de comunicação criado, basta replicar alterando a informação, de certificado digital da empresa correspondente.

> Os Certificados são instalados na camada JAVA do PI: 
{.is-danger}

[PIP - SAP NetWeaver Administrator](http://pmsrvsappip.gbj.corp:50000/webdynpro/resources/sap.com/tc~lm~itsam~ui~mainframe~wd/FloorPlanApp?home=true#)

![certificado_pi_1.png](/desenvolvimento/imagens_pi/manifesto_pi/certificado_pi_1.png)

![certificado_pi_2.png](/desenvolvimento/imagens_pi/manifesto_pi/certificado_pi_2.png)

Entrada Criada e mantida com os certificados para uso na Manifestação:

---

Então criado o cenário de comunicação, baseado na interface de distribuição de documentos
![manifesto_2.png](/desenvolvimento/imagens_pi/manifesto_pi/manifesto_2.png)

Criar então um Receiver determinnation:

![manifesto_receiver1.png](/desenvolvimento/imagens_pi/manifesto_pi/manifesto_receiver1.png)

Cada condição contem os CNPJS da empresa, apontando para o componente de comunicação correspondente.

---

Após Criar o Receiver criar o sender agreement:

![sender_agreement.png](/desenvolvimento/imagens_pi/manifesto_pi/sender_agreement.png)

O sender é ligado ao Communication Channel criado em :

![communication_channel_aex.png](/desenvolvimento/imagens_pi/manifesto_pi/communication_channel_aex.png)

Este HTTP destination (from NWA) ::  é criado na camada JAVA do PI na parte dos destination.

Cria-se então o Interface Determination:

![interface_determination.png](/desenvolvimento/imagens_pi/manifesto_pi/interface_determination.png)


Proximo Passo Criar o Receiver Agremment, é neste passo que indicamos qual Webservice será consumido, passo criado no inicio.

> Em receiver Communication Channel, indicamos o canal de comunicação relevante para comunicação
{.is-info}
![receiver_agremment.png](/desenvolvimento/imagens_pi/manifesto_pi/receiver_agremment.png)

Informado o Canal de Comunicação, a interce já preenche corretamente:

![canal_comunicação_1.png](/desenvolvimento/imagens_pi/manifesto_pi/canal_comunicação_1.png)

![canal_comunicação_2.png](/desenvolvimento/imagens_pi/manifesto_pi/canal_comunicação_2.png)

---

Sendo Assim está é a configuração necessária para ser possivel recuperar as NFes apartir da sefaz, a configuração precisa ser então replicada para cada empresa, e incluido então cada CNPJ em sua empresa relacionada.












## Incluir CNPJ para recepção de documentos:

Identificar a qual Condição este CNPJ pertence, e adicionar o CNPJ.

![incluir_cnpj_1.png](/desenvolvimento/imagens_pi/manifesto_pi/incluir_cnpj_1.png)

![incluir_cnpj_2.png](/desenvolvimento/imagens_pi/manifesto_pi/incluir_cnpj_2.png)

![incluir_cnpj_3.png](/desenvolvimento/imagens_pi/manifesto_pi/incluir_cnpj_3.png)

![incluir_cnpj_4.png](/desenvolvimento/imagens_pi/manifesto_pi/incluir_cnpj_4.png)

![incluir_cnpj_5.png](/desenvolvimento/imagens_pi/manifesto_pi/incluir_cnpj_5.png)

> **Salvar e Ativar**
{.is-success}

> Já no **GRC:** Escalonar o Programa:  /XNFE/COLLECT_DOCUMENTS
{.is-info}

> Customizing do GRC presente na documentação sobre GRC.




















