---
date: 2017-01-16
title: Informativo Server
categories:
  - Server
description:  STCP OFTP SERVER – Arquivos de Log 
type: Document
---

# STCP OFTP SERVER – Arquivos de Log

Os logs do STCP OFTP estão divididos em duas categorias:

## **Logs do Sistema**

Disponíveis na pasta _Log_ do diretório de instalação do _STCP OFTP Server_ (Ex. C:\STCPODT\Log) e são criados
diariamente. Registram as informações referentes aos eventos do SISTEMA.

* Início/Fim do STCP OFTP;  
* Início/Fim de Execução de Comando Externo;  
* Início e Término da Agenda;  
* Erros do Sistema em geral.  

A nomenclatura dos arquivos de log, segue o padrão abaixo:

**YYYYMMDD.log.txt**  
**YYYYMMDD.msg.txt**  

----
## **Logs da Comunicação**

Disponíveis na pasta _Log_ do usuário registrado na aplicação (Ex. C:\STCPODT\NOME-USUARIO\LOG), também são criados diariamente . Registram as informações referentes aos eventos do processo de transferências de um determinado usuário. Cada usuário, registrado no sistema (guia _Usuários_), possui uma pasta _Log_ correspondente.

* Os eventos listados nestes arquivos podem ser: 
* Início/Fim de Conexão Entrante ou Sainte;  
* Início/Fim de Sessão;  
* Início/Fim de Transmissão ou Recepção de arquivos;  
* Erros no processo de transferência.  

A nomenclatura dos arquivos de log, segue o padrão abaixo:

**YYYYMMDD.NOME-USUARIO.msg.txt**

Em caso de dúvidas ou maiores informações sobre este procedimento, entre em contato com a equipe de suporte da Riversoft Integração e Inovação através de nossos contatos.

RIVERSOFT INTEGRAÇÃO E DESENVOLVIMENTO DE SOFTWARE LTDA  
Rua Marechal Deodoro, 480, 1º andar, Pouso Alegre – MG – CEP 37553-405  
Telefone 35 3421-2221  
E-mail: suporte@riversoft.com.br  
Web: (http://www.riversoft.com.br)  
