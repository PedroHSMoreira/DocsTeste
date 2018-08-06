---
date: 2017-01-16
title: Procedimento Server
categories:
  - Server
description:  Procedimentos STCP OFTP Server
type: Document
---

# Procedimentos STCP OFTP Server 

## **Configuração suíte STCP OFTP para uso de certificado digital emitido por uma autoridade certificadora (CA)**

### 1. Objetivo

Este documento tem como objetivo descrever os procedimentos necessários para configuração do Riversoft STCP OFTP Server e Riversoft STCP OFTP Client, utilizando certificado emitido por uma Autoridade Certificadora.

### 2. Geração da CSR

A CSR, cuja sigla significa Certificate Signing Request, é um arquivo de texto, gerado pelo servidor web, contendo as informações para a solicitação do seu certificado junto à entidade certificadora escolhida e usada para gerar um certificado assinado digitalmente.

A CSR conterá informações importantes da companhia e deve ser preenchida conforme instruções da encaminhadas pela entidade certificadora contratada.

A geração da CSR é divida em duas etapas: geração do par de chaves (que deve ser gerada no tamanho de 2048 bits) e geração da CSR.

![](/images/imagem1/img84.png) 

O procedimento de geração de CSR, por ser realizado por outro software de servidor (IIS, IBM Webshepere, iPlanet, Keytool, entre outros), conforme a infraestrutura utilizada.

**2.1 Geração do Par de Chaves**

Acesse a pasta “Program” do diretório de instalação do Riversoft STCP OFTP Server (Ex. C:\STCPODT\Program) e em seguida, para gerar o par de chaves, digite a linha de comando:

openssl genrsa -des3 > C:\STCPODT\Keys\chaveprivada.key 2048

Após digitar a linha de comando, o sistema solicitará que informe uma senha para proteger o par de chaves que será criado no diretório C:\STCPODT\Keys.

![](/images/imagem1/img85.png) 

**2.2 Geração da CSR (Certificate Signing Request)**

Em seguida, para gerar a requisição (CSR), utilize a linha de comando e digite as informações solicitadas.

openssl req -new -key C:\STCPODT\Keys\chaveprivada.key > C:\STCPODT\Keys\solicitacao.csr -config C:\STCPODT\Program\openssl.cnf

![](/images/imagem1/img86.png)  

### 3. Solicitação do certificado SSL
A CSR, gerada no passo anterior, deverá ser encaminhada para a entidade certificadora conforme procedimentos fornecidos por essa. Para maiores dúvidas referente ao envio da CSR entre em contato com seu agente de contas junto à entidade certificadora.

Faça uma cópia de segurança de sua chave privada e do CSR em CD, e guarde-as em local seguro.
Nenhuma cópia de sua chave privada deverá ser distribuída e/ou solicitada por terceiros.

### 4. Instalação e Configuração do certificado SSL
Uma vez Aprovado e Emitido, o contato técnico responsável do processo de certificação digital, receberá da entidade certificadora todas as informações pertinentes à instalação e configuração do certificado.

Para maiores dúvidas referente ao processo de instalação e configuração entre em contato com o seu agente de suporte (CA) e/ou com a sua equipe de segurança.

![](/images/imagem1/img87.png) 

### 5. Configuração do certificado SSL no STCP OFTP Server
Para que seja possível configurar o STCP OFTP Server Enterprise/Lite, a fim de utilizar o certificado digital emitido por uma Autoridade Certificadora, será necessário possuir às chaves pública e privada e realizar os procedimentos descritos abaixo.

**5.1 Chave pública**

Faça uma cópia da chave pública do certificado (arquivo .cer), encaminhado pela entidade certificadora, para a pasta Certs do diretório de instalação do STCP OFTP Server Enterprise/Lite (Ex. C:\STCPODT\Certs).

> NOTA: Em alguns casos o administrador precisa realizar a exportação da chave pública (*.cer) do Certificado.   Para isso, é possível utilizar o snap-in Certificados do Console de Gerenciamento Microsoft (MMC).  
Para mais detalhes consulte: (https://technet.microsoft.com/pt-br/library/cc730988.aspx)

**5.2 Chave Privativa**

A chave privativa (arquivo .key ou .pem) do certificado deverá ser copiada para a pasta Keys do diretório de instalação do STCP OFTP Server Enterprise/Lite (Ex. C:\STCPODT\Key).

> NOTA: Em alguns casos, onde o arquivo do certificado está no formato PFX, o processo de conversão para o formato PEM será necessário. É possível realizar a conversão usando o OpenSSL, disponível na pasta Program, do diretório de instalação do STCP OFTP Server/Lite (Ex. C:\STCPODT\Program).  
Para mais detalhes consulte: (https://www.openssl.org/docs/apps/pkcs12.html)

openssl pkcs12 -in C:\TEMP\empresateste.com.br.pfx -out C:\TEMP\private-key.pem -nodes

![](/images/imagem1/img88.png)

**5.3 Configuração da Rede**

1. No menu, Iniciar > Todos os programas > Riversoft STCP OFTP Server, acesse o STCP OFTP Server Config.
2. Na guia Redes selecione a rede desejada e clique no botão Propriedades.

![](/images/imagem1/img89.png) 

3. Na janela Propriedades da rede, selecione a guia SSL3 (Openssl) e no grupo Chave privativa, informe os parâmetros Chave e Certificado.

> NOTA: Caso o certificado tenha sido instalado em um servidor Microsoft IIS, previamente será necessária a exportação do certificado para um arquivo PFX e a conversão desse arquivo para o formato PEM através
do utilitário OpenSSL¹.

![](/images/imagem1/img90.png) 

PARAMÊTROS | DESCRIÇÃO
:---       | :---
Chave      | Preencha este campo com o nome do arquivo (caminho completo) onde se encontra instalada a chave privativa.
Certificado| Preencha este campo com o nome do arquivo (caminho completo) onde se encontra o certificado digital (X509) associado à chave privativa.

4. Pressione o botão OK para salvar e sair do STCP OFTP Server Config.  
5. Reinicie o serviço do Riversoft STCP OFTP Server para que as alterações sejam aplicadas.

-------
¹ (https://www.openssl.org/docs/apps/pkcs12.html)

### 6. Geração do hash do certificado para uso no STCP OFTP Client

Anterior ao processo de configuração do certificado no STCP OFTP Client, será necessária obter uma cópia da cadeia de certificados, a partir do certificado assinado e enviado pela entidade certificadora e o realizar o renomeio de cada certificado dessa hierarquia para o seu hash correspondente.

> NOTA: Caso você já possua os certificado raíz e intermediário vá para o passo 10.

1. Faça uma cópia do certificado, encaminhado pela certificadora, para um diretório temporário do servidor onde o STCP OFTP Server está instalado (Ex. C:\TEMP)  

2. Acesso o diretório temporário e clique com o botão direito do mouse no certificado (Ex. empresateste_certificate.cer) e selecione Abrir  

3. Na guia Caminho de Certificação selecione o certificado raíz (Ex. VeriSign Trial Secure Server Root CA – G2) e clique no botão Exibir Certificado.  

![](/images/imagem1/img91.png)

4. Uma nova janela será exibida, contendo as informações do certificado selecionado (neste exemplo serão exibidas as informações do certificado raiz _VeriSign Trial Secure Server Root CA – G2)_ 

5. Selecione a guia Detalhes e clique no botão Copiar para Arquivo para iniciar o Assistente para Exportação de Certificados

![](/images/imagem1/img92.png) 

6. Para continuar, clique em Avançar

7. No formato do arquivo de exportação selecione X.509 codificado na base 64 (*.cer) e clique no botão Avançar

![](/images/imagem1/img93.png) 

8. Informe o caminho e nome do arquivo a ser exportado (Ex. C:\TEMP\root_certificate.cer)

9. Para finalizar, clique no botão Concluir

![](/images/imagem1/img94.png) 

10. Repita os passos de 3 a 9 para os exportar os demais certificados existentes na hierarquia de certificados, o certificado raiz (G2) e o intermediário (G3).

![](/images/imagem1/img95.png) 

> NOTA: Neste exemplo serão gerados mais dois arquivos no diretório temporário (Ex. root_certificate.cer e intermediate_certificate.cer). 

11. Acesse a pasta “Program” do diretório de instalação do Riversoft STCP OFTP Server (Ex. C:\STCPODT\Program) e em seguida, para gerar o _hash_, digite a linha de comando:

openssl x509 –noout –hash -in C:\TEMP\root_certificate.cer

![](/images/imagem1/img96.png) 

12. Uma vez obtido o _hash_ do arquivo indicado, renomeie esse arquivo para o seu _hash_ correspondente e mais a extensão .**0** (Ex. _root_certificate.cer para F877295a.0_)

![](/images/imagem1/img97.png) 

13. Repita os passos 11 e 12 para realizar o renomeio dos demais arquivos exportados
(Ex. _root_certificate.cer e intermediate_certificate.cer_)

![](/images/imagem1/img98.png) 

14. Copie os arquivos renomeados para a pasta Certs do diretório de instalação do STCP OFTP Client (Ex. C:\STCPCLT\Certs)

### 7. Configuração do certificado SSL no STCP OFTP Client

1. No menu, Iniciar > Todos os programas > Riversoft STCP OFTP Client, acesse o STCP OFTP Client Config.

2. Na guia Perfis selecione o perfil desejado e clique no botão Propriedades

![](/images/imagem1/img99.png) 

3. Na janela Propriedades do perfil, na guia Geral, clique no botão Configurar e selecione a guia SSL3 (Openssl)

4. No grupo Certificados CA (Autoridades) informe o parâmetro Diretório.

![](/images/imagem1/img100.png) 

PARAMÊTROS | DESCRIÇÃO
:---       | :---
Diretório  | Preencha este campo com o nome do diretório (caminho completo) onde se encontram instalados os certificados digitais (X509) contendo a chave pública que assina o certificado apresentado pelo servidor.

5. Pressione o botão OK para salvar e sair do STCP OFTP Client Config

6. Realize os testes de conexão ao STCP OFTP Server através do STCP OFTP Client

Em caso de dúvidas ou maiores informações sobre este procedimento, entre em contato com a equipe de suporte da Riversoft Integração e Inovação atarvés de nossos contatos.

RIVERSOFT INTEGRAÇÃO E DESENVOLVIMENTO DE SOFTWARE LTDA  
Rua Marechal Deodoro, 480, 1º andar – Santa Lúcia – Pouso Alegre – MG – CEP 37550-000  
Telefone 35 3421-2221    
E-mail: suporte@riversoft.com.br   
Web: (http://www.riversoft.com.br)    

----------
## **STCP OFTP - Notificação por E-mail através de Scripts VBS**

### 1. Introdução

O STCP OFTP Server Lite/Enterprise e STCP OFTP Client nos permite a execução de processos por eventos (início e/ou fim de conexão, transmissão e/ou recepção de arquivos com sucesso, ocorrência de erros, etc.) através de linha de comandos.

Por exemplo, podemos executar um script VBS - previamente configurado - para enviar e-mails para uma determinada área sempre que um arquivo for enviado e/ou recebido com sucesso. Neste mesmo cenário, outro script poderá ser executado sempre que ocorrer alguma falha de conexão ou na transferência dos arquivos. Tais scripts também podem ser utilizados para gerar Traps para um servidor SNMP ou gerar evidências no Event Viewer do sistema operacional.

Este documento tem como finalidade, demonstrar os procedimentos necessários para a configuração e execução dos scripts VBS, responsáveis pelo envio de notificações por e-mail, no STCP. Por se tratar de um script que utiliza uma linguagem universal (Visual Basic Scripting) e distribuída gratuitamente pela Microsoft, podemos customizá-lo para atender as mais diversas necessidades da área de monitoração, assim como filtrar as notificações e erros desejados.

### 2. Configuração de notificações de erro por e-mail

Conforme mencionado no item 1, é possível configurar o STCP para enviar uma notificação por e-mail sempre que houver algum erro no processo de conexão e/ou transferência de arquivos. 

Tal procedimento pode ser realizado através do script “STCPEMAILEVT.VBS”, existente na pasta “Program”, do diretório de instalação (Diretório de Controle) da aplicação (Ex C:\STCPODT\Program).

2.1 Edite o arquivo “STCPEMAILEVT.VBS” e preencha as informações conforme a imagem.

![](/images/imagem1/img101.png) 

2.2 Além das configurações “_strMailFrom_”, “_strMailTo_” também deverão ser configurados os
parâmetros referentes ao servidor SMTP.

![](/images/imagem1/img102.png)

2.3 Salve o arquivo. 

2.4 Para realizar a validação do funcionamento do script e do servidor SMTP, acesse o "Prompt de
Comando" e digite o comando abaixo. Caso nenhuma mensagem de erro seja apresentada,
verifique se os e-mails foram recebidos nas contas indicadas.

_cscript C:\STCPODT\Program\STCPEMAILEVT.VBS NOME-SERVIDOR MSG1 MSG2_

![](/images/imagem1/img103.png) 

Após a configuração e testes do script VBS, uma alteração nas Propriedades de Log do STCP (vide imagem abaixo) será necessária, habilitando a execução de um comando externo sempre ocorrer eventos que contenham algum erro (Nível de log = 1) e informando a linha de comando abaixo no parâmetro “Comando externo”.

_cscript //B C:\STCPODT\Program\STCPEMAILEVT.VBS NOME-SERVIDOR “_

Nota: Observe que logo após o nome do servidor será necessário inserir uma aspas duplas (abre aspas).

![](/images/imagem1/img104.png) 

Após a execução destes procedimentos, clique no botão OK para salvar as alterações e reinicie o serviço do Riversoft STCP OFTP Server para que as estas sejam ativadas.

Uma vez realizadas as configurações com êxito, um e-mail será encaminhado para os destinatários informados no script sempre que um erro ocorrer no processo de transferência de arquivos.

### 3. Configuração de notificações de envio/recebimento de arquivos

Dentre várias outras possibilidades, além das notificações de erro apresentadas no item 2 deste procedimento, também é possível gerar notificações para alertar o envio e/ou recebimento (com sucesso) de arquivos.

Tal procedimento pode ser realizado através do script “stcpemail.vbs”, existente na pasta “Program”, do diretório de instalação (Diretório de Controle) da aplicação (Ex C:\STCPODT\Program).

3.1 Edite o arquivo “stcpemail.vbs” e preencha os parâmetros referentes ao servidor SMTP

![](/images/imagem1/img105.png) 

3.2 Salve o arquivo.  

3.3 Para realizar a validação do funcionamento do script e do servidor SMTP, acesse o "Prompt de Comando" e digite o comando abaixo. Caso nenhuma mensagem de erro seja apresentada, verifique se os e-mails foram recebidos nas contas indicadas.

_cscript //B C:\STCPODT\Program\ stcpemail.vbs “de@dominio.com.br”_  

_“para@dominio.com.br” “” “nome-arquivo-teste”_

![](/images/imagem1/img106.png) 

3.4 Acesse o STCP OFTP Server Config (Iniciar – Todos os programas – Riversoft STCP OFTP Server – Riversoft STCP OFTP Server Config) e na guia “Usuários”, selecione o usuário desejado e clique no botão “Propriedades”.

3.5 Na janela de propriedades do usuário selecionado, na guia “Tipos de arquivos” selecione o tipo “default” ou o tipo de arquivo desejado e clique no botão “Propriedades”.

3.6 Na janela de propriedades do tipo de arquivo desejado, no grupo “Características da transmissão”, preencha o parâmetro “Executar comando externo” com a linha de comando abaixo:

_cscript //B C:\STCPODT\Program\stcpemail.vbs “de@dominio.com.br”_  

_“para@dominio.com.br” “” $LFNAME_

Nota: Na linha de comando utilizamos a variável interna do STCP, **$LFNAME**, que nos contém o nome completo do arquivo local. A relação completa das variáveis internas do STCP OFTP Server pode ser obtida no item “Definição das variáveis internas do STCP OFTP Server”, página 103, da documentação do produto  
(http://www.riversoft.com.br/downloads/manuais/STCPSrv_4_0-PTB.pdf).

![](/images/imagem1/img107.png) 

3.7 Clique no botão OK para salvar as alterações.

Uma vez realizadas as configurações com êxito, um e-mail será encaminhado para o destinatário informado, sempre que um arquivo for transmitido com sucesso. O mesmo procedimento poderá ser utilizado para implantar notificações também na recepção de arquivos.

Em caso de dúvidas entre em contato com o suporte técnico.

-------------
## **STCP OFTP Server Enterprise/Lite**

### Geração da chave privativa e certificado de autenticação SSL3

Os seguintes procedimentos devem ser executados para a geração da chave privativa e certificado digital para utilização na comunicação SSL3.

No prompt de comando execute a aplicação **openssl.exe** (Ex.: C:\STCPODT\Program\openssl.exe) para iniciar o processo de geração do par de chaves assimétricas (privada/pública).

![](/images/imagem1/img108.png) 

Utilize o comando abaixo para gerar a chave privativa que será utilizada para criptografia da conexão.

**genrsa -out [unidade_disco [diretório_instalação_stcp]\keys\[nome_da_chave].key 1024**

Exemplo:  
genrsa -out c:\stcpodt\keys\stcp_riversoft.key 1024

![](/images/imagem1/img109.png) 

O próximo passo é gerar o Certificado Digital associado à chave gerada anteriormente, para isto utilize o comando abaixo.

req -new -x509 -key [unidade_disco][diretório_instalação_stcp]\keys\[nome_da_chave].key -out [unidade_disco][diretório_instalação_stcp]\certs\[nome_do_certificado].cer -days 1825 – config ./openssl.cnf

Exemplo:  
req -new -x509 –key c:\stcpodt\keys\stcp_riversoft.key -out c:\stcpodt\certs\stcp_riversoft.cer -days 1825 -config ./openssl.cnf

Obs.: O parâmetro ‘-days’ equivale a quantos dias o certificado terá validade, podendo ser inserido o valor que mais se adequar às políticas da empresa.

Preencha as informações solicitadas para concluir o processo de geração do Certificado Digital.

![](/images/imagem1/img110.png) 

### Configuração da interface de transferência do STCP OFTP Server Enterprise/Lite para comunicação SSL3

Para acesssar o configurador do STCP OFTP Server Enterprise/Lite, clique em **Iniciar** e depois clique em **Riversoft STCP OFTP Server Config.**

Acesse a guia de Redes para adicionar as interfaces que ficarão disponíveis para o serviço de transferência e então adicione uma interface do serviço de transferência.

![](/images/imagem1/img111.png) 

Clique na guia **TCP/IP** e configura os parâmetros conforme apresentados.

![](/images/imagem1/img112.png) 

Clique na guia **SSL3 (Openssl)** e configure os parâmetros conforme apresentado abaixo e pressione o botão Ok para finalizar.

![](/images/imagem1/img113.png) 

---------------
## **Habilitando o Debug no STCP OFTP Server**

Em alguns casos, para se obter uma análise mais detalhada de problemas relacionados ao intercâmbio de
arquivos, torna-se necessária a depuração dos processos de conexão e transferência, realizadas pelo STCP OFTP Server.

Através da configuração do parâmetro “Nível de debug” é possível gerar um arquivo de depuração na pasta **DEBUG** (Ex. C:\STCPODT\Debug) do diretório de instalação do STCP.

Acesse o STCP OFTP Server Config (Iniciar – Todos os programas – Riversoft STCP OFTP Server). Selecione o usuário desejado na guia Usuários e clique no botão Propriedades Na janela Propriedades do usuário, na guia do protocolo utilizado (Odette, SFTP, FTP, HTTP) altere o valor do campo "Nível de debug" para 63 (outros valores podem ser utilizados – vide Tabela 2). Após a alteração, disponibilize um arquivo de teste na pasta SAIDA do usuário, que apresenta o erro, e inicie uma nova conexão. O arquivo de debug será gerado no diretório **DEBUG** (Ex. C:\STCPODT\Debug).

> NOTA: Uma vez gerado o erro, você pode voltar o nível de debug para o seu valor padrão (0).

![](/images/imagem1/img114.png) 

Para cada tentativa de conexão será criado um novo arquivo de depuração no diretório **DEBUG** com a seguinte sintaxe:  
ODTDEB.< Protocolo>.< Usuario>.YYYYMMDDhhmmssnnn

Protocolo| TCPIP, X25, SERIAL ou PAD
:---:    | :---:
Usuário  | Nome do perfil utilizado
YYYY     | Ano
MM       | Mês
DD       | Dia
hh       | Hora
mm       | Minuto
ss       | Segundos
nnn      | Milésimos de segundos
Tabela 1 |


A tabela a seguir contém a relação entre o nível de detalhamento e as informações que serão geradas.

Nível | Descrição
:---  | :---
0     | Não grava o arquivo de depuração.
1     | Grava as informações de entrada e saída das sub-rotinas.
2     | Grava as informações de mudanças do estado do protocolo.
4     | Grava as informações dos pacotes recebidos e enviados, formatado por campo.
8     | Grava as informações dos pacotes recebidos e enviados, formatado em hexadecimal.
16    | Grava as informações dos eventos ocorridos (Somente se ocorrer algum erro).
32    | Grava as informações dos sub-registros.
63    | Grava as informações completas (Debug completo).
Tabela 2 |


Em caso de dúvidas ou mais informações sobre este procedimento, entre em contato com a equipe de suporte da Riversoft Integração e Inovação atarvés de nossos contatos.


RIVERSOFT INTEGRAÇÃO E DESENVOLVIMENTO DE SOFTWARE LTDA  
Rua Marechal Deodoro, 480, 1º andar – Santa Lúcia – Pouso Alegre – MG – CEP 37550-000  
Telefone 35 3421-2221  
E-mail: suporte@riversoft.com.br  
Web: (http://www.riversoft.com.br)  
