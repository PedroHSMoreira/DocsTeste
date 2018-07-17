---
date: 2017-01-16
title: Manual Client Web
categories:
  - Client Web
description:  Manual STCP OFTP Client Web Versão 3.0.0
type: Document
---

# STCP OFTP Client Web Versão 3.0.0

### O que é o STCP OFTP Client Web e como funciona?

STCP OFTP Client Web é um cliente de transferência de arquivos OFTP (Odette File Transfer Protocol) para aplicações de e-business e troca de informações corporativas, compatível com a tecnologia Microsoft ActiveX.      
O STCP OFTP Client Web oferece os recursos de comunicação segura com criptografia, recuperação de transferência interrompida, registro de log local das transferências, garantia de entrega dos arquivos, comunicação TCP-IP e SSL3.   
O STCP OFTP Client Web funciona como um componente do sistema operacional extendendo as suas funcionalidades e utilizando os recursos de comunicação disponíveis no equipamento onde está instalado.

### Uso do STCP OFTP Client Web

O STCP OFTP Client Web deve ser utilizado integrado ao navegador de internet (browser) para as aplicações de e-business que requerem upload e download de arquivos com segurança.

### Vantagens do STCP OFTP Client Web
* Segurança com criptografia
* Recuperação de transferência interrompida
* Garantia de entrega dos dados
* Log de transferência

--------
## **Como instalar o STCP OFTP Client Web**

### Como distribuir o STCP OFTP Client Web?

STCP OFTP Client Web é distribuído em um arquivo pacote digitalmente assinado pela Riversoft (stcpweb.cab). Este pacote pode ser acessado diretamente do servidor web da Riversoft ou instalado no servidor web acessível pelos usuários.

O STCP OFTP Client Web está disponível para todos os servidores web (Apache, IIS, Personal Web etc.) em todas as plataformas.

> Nota: STCP OFTP Web Client é compatível com Microsoft Internet Explorer* versão 4 ou superior, na plataforma PC.

---------
## **Como utilizar o STCP OFTP Client Web** 

A utilização do STCP OFTP Client Web é realizada através da referência na página HTML do componente ActiveX através da seguinte sintaxe:

< object classid="Clsid:[Inserir Classid do Componente]" id="stcpweb"       
width="0" height="0" codebase="stcpweb.cab#version=3,0,0,2028">       
< /object>   

Os métodos abaixo relacionados estão disponíveis para utilização na página HTML por um script java ou VB:

Método | Descrição
:---   | :---
Long Run( void ) | Inicia o proceso de transferência.
Long explorer( int nShowArea ) | Mostra através do explorer os diretórios dos dados de entrada e de saída. /nShowArea = 0 Mostra o diretório de entrada /nShowArea = 1 Mostra o diretório de saída
Long viewlog( int nShowLog )| Mostra através do explorer o diretório log de transferência. /nShowLog = 0 Mostra o diretório de log

```ini
<!-- Inicio do JavaScript -->
<SCRIPT LANGUAGE="JavaScript">
function ativa_stcp()
{
stcpweb.Run();
}
function log_stcp()
{
stcpweb.viewlog( 0 );
}
function msg_stcp()
{
stcpweb.viewlog( 1 );
}
function entrada_stcp()
{
stcpweb.explorer( 0 );
}
function saida_stcp()
{
stcpweb.explorer( 1 );
}
</SCRIPT>
```

Ao ser acessado pela primeira vez, o controle STCP OFTP Client Web irá mostrar uma mensagem de autenticidade. Após a confirmação do usuário, as suas funcionalidades estarão disponíveis. 

![](/images/imagem3/imgCW255.png) 

Ao término da instalação, um novo diálogo será apresentado ao usuário, com a solicitação do nome do usuário cadastrado no servidor STCP OFTP Server Enterprise.

![](/images/imagem3/imgCW256.png) 

Este diálogo será apresentado sempre que o método Run for executado pela primeira vez na página carregada.

### Arquivo HTML: exemplo da utilização do STCP OFTP Client Web

```ini
<html>
<head>
<title>Teste do STCPWEB</title>
</head>
<body>
<h2 align="center">
<font color="#800080">Página de Teste</font>
</h2>
<h2 align="center">
<font color="#800080">STCPWeb 3.0.0</font>
</h2>
<p align="center">
<object classid="Clsid:35614A46-AD03-44a8-AE8C-8647E8A94666" id="stcpweb" width="0"
height="0"
codebase="stcpweb.cab#version=3,0,0,2027">
<param name="Profile" value="O000055RIVERSOFT">
<param name="HostName" value="stcp.riversoft.com.br">
<param name="HostPort" value="3305">
<param name="Security" value="4">
<param name="Compat" value="0">
</object>
</p>
<div align="center" id="stcpinfo" style="width: 870; height: 248">
<table border="0" width="65%" height="242">
<tr>
<td width="50%" valign="center" height="238">
<form name="teste" method="post" action="">
<div align="center">
<table border="0" height="1">
<tr>
<td height="1" colspan="2" align="center" valign="top">
<p align="left"><input type="button" value=" STCP Web Run " name="stcp"
OnClick="ativa_stcp()"></p></td>
</tr>
<tr>
<td height="27">
<input type="button" value=" STCP Web Log " name="stcp1" OnClick="log_stcp()">
</td>
<td height="27">
</td>
</tr>
<tr>
<td height="27">
<input type="button" value=" STCP Web Entrada " name="stcp2" OnClick="entrada_stcp()">
</td>
<td height="27">
<input type="button" value=" STCP Web Saida " name="stcp3" OnClick="saida_stcp()">
</td>
</tr>
<tr>
<td height="27" colspan="2">
<p align="left"></p></td>
</tr>
<tr>
<td height="1">
</td>
<td height="5">
</td>
</tr>
<tr>
<td height="1"></td>
<td height="31">
</td>
</tr>
<tr>
<td height="12" colspan="2">
<p align="left"></p></td>
</tr>
<tr>
<td height="1" colspan="2">
</td>
</tr>
</table>
</div>
</form>
<center>
<p>&nbsp;</p></center></td>
</tr>
</table>
<CENTER></CENTER>
</div>
<!-- Inicio do JavaScript -->
<SCRIPT LANGUAGE="JavaScript">
function ativa_stcp()
{
stcpweb.Run();
}
function log_stcp()
{
stcpweb.viewlog( 0 );
}
function msg_stcp()
{
stcpweb.viewlog( 1 );
}
function entrada_stcp()
{
stcpweb.explorer( 0 );
}
function saida_stcp()
{
stcpweb.explorer( 1 );
}
</SCRIPT>
</body>
</html>
```

### Diagrama de execução STCP OFTP Client Web

![](/images/imagem3/imgCW257.png) 

