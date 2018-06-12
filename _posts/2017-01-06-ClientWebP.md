---
date: 2017-01-16
title: Procedimento Client Web
categories:
  - Client Web
description:  Procedimento padrão para geração de componente ActiveX e site do STCP Client Web
type: Document
---

# Procedimento padrão para geração de componente ActiveX e site do STCP Client Web

## **1. Objetivo**

Este documento tem por objetivo descrever os passos necessários para a geração, customização e configuração do componente ActiveX e do site padrão para o STCP OFTP Client Web.

STCP OFTP Client Web é distribuído em um arquivo pacote digitalmente assinado pela Riversoft (stcpweb.cab). Este pacote pode ser acessado diretamente do servidor web da Riversoft ou instalado no servidor web acessível pelos usuários.

O STCP OFTP Client Web está disponível para todos os servidores web (Apache, IIS, Personal Web etc.) em todas as plataformas.

Para maiores detalhes consulte a documentação do produto através do link:   
(http://www.riversoft.com.br/downloads/manuais/STCPCliweb_3_0-PTB.pdf)

----
## **2. STCP OFTP Client Web (ActiveX)**

O componente STCP Client Web (ActiveX) será preparado pela Riversoft mediante o envio, para o e-mail (suporte@riversoft.com.br), dos dados abaixo:

a. Logotipo do cliente (.jpg ou .png);   
b. Endereço IP ou FQDN do servidor STCP OFTP Server;  
c. Porta de comunicação TCP/IP;  
d. Certificado de segurança (.cer ou .pem) do servidor STCP OFTP Server.   
e. Será utilizada a opção “Nome longo para arquivos”?  

----
## **3. STCP OFTP Client Web (Site – Template padrão)**

A Riversoft disponibiliza um template padrão do site para acesso e utilização do componente STCP OFTP Client Web. Trata-se de um site HTML, sendo necessário somente criar uma imagem de fundo customizada para o cliente, copiá-la para o diretório “**/img**” e configurar a chamada desta imagem no arquivo CSS, disponível no diretório “**/css**”.

Uma imagem padrão para servir de modelo no design do site pode ser encontrada no diretório "**/modelos**".

![](/images/imagem2/imgCW251.png) 

O nome da imagem deverá ser alterado na classe “**#box-stcp**“.  
A dimensão da imagem deve ser de **909 x 1300px**.

![](/images/imagem2/imgCW252.png) 

----
## **4. STCP OFTP Client Web (Site – Pacotes.cab)**

Após a liberação do componente ActiveX, pela Riversoft, o arquivo “stcpctrl_nomecliente.cab”, conforme o idioma, deverá ser copiado para o seu respectivo diretório da pasta “/cab”, do diretório de instalação do site.

![](/images/imagem2/imgCW253.png) 

----
## **5. STCP OFTP Client Web (Site – Arquivos de configuração)**

Para configurar o acesso do site STCP OFTP Client Web ao componente ActiveX, será necessário editar os arquivos de configuração “**stcpweb_ptb.js**”, “**stcpweb_esp.js**” e “**stcpweb_enu.js**”. Tais arquivos encontram-se na pasta “**/js**” do diretório do site.

Os parâmetros que deverão ser configurados são:

![](/images/imagem2/imgCW254.png) 

***Os exemplos de links abaixo redirecionam para aplicação STCP OFTP Change Password, onde o usuário poderá realizar a alteração da senha do seu usuário de acesso.

**Exemplo 1:**

Após clicar na opção "**Alterar senha a sua senha**", o usuário é encaminhado para o site do STCP OFTP Change Password, com opção de download do manual e de pacote de instalador (**disableDownload=yes**). Após o processo de alteração da senha ser realizado com sucesso, o usuário é redirecionado novamente para o site informado no parâmetro "(urlRet=stcp.exemplo2.com.br)", na versão portugûes (lang=ptb)

(http://stcp.exemplo1.com.br/?disableDownload=yes&urlRet=http://stcp.exemplo2.com.br&lang=ptb)

**Exemplo 2:**

Após clicar na opção "**Alterar senha a sua senha**", o usuário é encaminhado para o site do STCP OFTP Change Password, sem opção de download do manual e de pacote de instalador (**disableDownload=no**). Após o processo de alteração da senha ser realizado com sucesso, o usuário é redirecionado novamente para o site informado no parâmetro "(urlRet=stcp.exemplo2.com.br)", na versão espanhol (**lang=esp**)

(http://stcp.exemplo1.com.br/?disableDownload=no&urlRet=http://stcp.exemplo2.com.br&lang=esp)

