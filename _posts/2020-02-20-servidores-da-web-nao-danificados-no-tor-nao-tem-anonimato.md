---
layout: post
title:  "Falhas em Servidores Web no Tor não mantem anonimato"
date:   2020-02-20 17:59:38 -0200
categories: jekyll update
---

![](https://osintcurio.files.wordpress.com/2019/03/2019-03-04_10-00-16.png)


Olá. Este é o Micah / WebBreacher e estou invadindo aplicativos da Web há muitos anos. Algumas das sugestões mais comuns que dei / dei aos clientes foram fortalecer seus sistemas antes de colocá-los online. Proteger significa desativar recursos não utilizados, restringir o acesso sempre que possível e garantir que o servidor da Web, seja qual for o sabor que esteja usando, seja protegido usando as orientações de algumas das listas de verificação disponíveis on-line ou impressas ( <https://www.owasp.org/index.php/Secure_Configuration_Guide#2._Web_servers_misconfiguration> ).

## Divulgação de Informações do Apache mod_status

Em 2001, o scanner de vulnerabilidades Nessus da Tenable começou a procurar destinos para a vulnerabilidade de divulgação de informações do [Apache mod_status](https://httpd.apache.org/docs/2.4/mod/mod_status.html) ( <https://www.tenable.com/plugins/nessus/10677> ). Encontrar este problema foi trivial. Usando um navegador da web, você faria uma solicitação para um servidor da web Apache com http (s): //example.com / **server-status** / . Essa parte / **status do servidor** / levou o navegador a uma página que divulgava informações sobre o servidor Apache. Alguns dos dados mostrados incluem:

1. Os endereços IP estão se conectando ao servidor
2. Os parâmetros e valores foram passados ​​para o servidor nas solicitações GET (por exemplo: **http://example.com/login.php ? User = admin & password = letmein** )
3. Os hosts ou domínios virtuais estão localizados nesse servidor
4. Detalhes sobre a instalação do servidor, como 32 ou 64 bits, e qual sistema operacional está sendo usado

Aqui está a aparência dessa página da Web em um servidor ativo na Internet:

![](https://osintcurio.files.wordpress.com/2019/03/2019-03-04_11-16-47.png)


>Saída de uma página de status mod_status

Encontrar esta página da web é super simples. Como mencionado acima, o Nessus possui um plugin para ele. [O **nmap**](https://nmap.org/) do scanner de rede possui um plug-in [criado por Eric Gershman](https://twitter.com/EricGershman) ( <https://nmap.org/nsedoc/scripts/http-apache-server-status.html> ). O banco de dados do Exploit que hospeda o banco de dados de hackers do Google tem várias entradas para esse problema ( <https://www.exploit-db.com/ghdb/1355> ). Visitar o Google.com e colocar [intext:”Apache Server Status for”](https://www.google.com/search?q=intext%3A%22Apache+Server+Status+for%22) no campo de pesquisa ainda gera milhares de hosts mostrando essas informações.


![](https://osintcurio.files.wordpress.com/2019/03/2019-03-04_11-19-13.png)


>Consulta do Google para sistemas da Web de superfície habilitados para mod_status


Ver esta página em uma verificação de vulnerabilidade sempre foi uma bênção. Como pentester, eu sempre esperava que houvesse algum conteúdo sensível sendo passado nos parâmetros da URL. Isso tornaria a descoberta de alto risco e empolgante para explorar e escrever.

Mas, geralmente, não havia dados confidenciais e acabei escrevendo uma descoberta para o relatório, informando que o cliente precisava proteger seu sistema para evitar a vulnerabilidade de divulgação de informações de baixo risco. Além disso, como esse era um problema de baixo risco, a maioria dos lugares nunca conseguiu consertar esses tipos de descobertas.

## Into the Dark Web

Mudando nossa atenção da “web de superfície” para a “dark web”, a [**rede Tor Dark Web**](https://www.torproject.org/) concentra-se em manter seus usuários e [“serviços de cebola” (onion services)](https://www.torproject.org/docs/onion-services) (às vezes chamados de “serviços ocultos”) anônimos. Deve ser um desafio descobrir alguns serviços de cebola, como um servidor Web rodando no Tor, endereço IP e pesquisá-lo na Web de superfície. A camada Tor deve proteger contra isso.

Mas o que aconteceria com um serviço de cebola anônimo em execução na dark web se estivesse executando o software para servidor da web Apache e o módulo mod_status estivesse ativado? Vamos descobrir!

Pegue uma cópia do Navegador Tor ( <https://www.torproject.org/download/download-easy.html.en> ) ou use outro método de visitar sites no Tor e vá até o serviço de cebola Fresh Onions ( <http://vps7nsnlz3n4ckiie5evi5oz2znes7p57gmrvundbmgat22luzd4z2id.onion/path/server-status> )

![](https://osintcurio.files.wordpress.com/2019/03/2019-032-04_11-19-13.png)


>Serviço Fresh Onions Tor exibindo serviços com mod_status ativado

A URL do Fresh Onions acima o levará a um local em seu site que exibe serviços do Tor onion com o módulo mod_status ativado e onde você pode visitar o http: // ONIONADDRESS / server-status / e ver detalhes sobre o servidor executando o Tor serviço.

## Maior risco de encontrar

Quando procurávamos na superfície da Web sistemas que tivessem esse mod_status ativado, a visualização das informações sobre o endereço IP do servidor, domínios virtuais que ele hospedava e o conteúdo enviado apresentava principalmente um risco baixo, a descoberta de divulgação de informações. Aqui na dark web, as coisas são diferentes. Vamos dar uma olhada no porquê.

O site <http://eplckll7rbvdupln.onion/server-status> pode ser acessado pelo Tor usando esse nome de serviço de cebola, como você pode ver no “1” na imagem abaixo. Quando olhamos para o “2” na imagem, podemos ver vários outros domínios **DA WEB DE SUPERFÍCIE** que também estão sendo executados nesse sistema!

![](https://osintcurio.files.wordpress.com/2019/03/2019-03-04_13-31-58-1.png)

>Página de status do servidor mod_status do serviço Tor onion mostrando hosts da Web de superfície em execução no mesmo sistema que um serviço Tor onion

Observando os outros números (3, 4 e 5) na imagem acima, podemos ver outras informações importantes, como em qual sistema operacional o servidor está executando, quais endereços de cliente são (para as conexões da Web de superfície) e parâmetros que estão sendo passados para o servidor (respectivamente).

Essa é uma visão incrível de um serviço "oculto" de cebola! Temos pistas a seguir na Web de superfície, pois esses outros domínios estão sendo hospedados no mesmo computador.

Alguns dos sites que visualizamos mostraram outros serviços ocultos em execução no mesmo computador. O site <http://ey4oty36pfgmec2c.onion/server-status> faz isso (mostrado abaixo).


![](https://osintcurio.files.wordpress.com/2019/03/2019-03-04_13-59-25.png)

>Página de status do servidor mod_status do serviço Tor onion mostrando vários serviços em execução no mesmo sistema

## Mas espere ... tem mais! Apresentando o mod_info!


Acontece que existe outro módulo de servidor da web Apache que deve ser desligado durante o fortalecimento, mas às vezes é esquecido. Isso é mod_info e mostra quais módulos estão configurados no servidor da web e informações sobre o arquivo de configuração do servidor. E se ... e se este módulo também estivesse ativado em um servidor Tor? Seria devastador para o anonimato do servidor. Por que "devastador"? Veja isso.

O servidor <http://lchuditewd4ltjti.onion/server-status> (mostrado abaixo) tem o módulo mod_status ativado e podemos ver sua saída abaixo. Nada de novo aqui. Na verdade, não vemos nenhum outro serviço de cebola ou host de superfície em execução neste servidor.


![](https://osintcurio.files.wordpress.com/2019/03/2019-03-04_13-49-53.png)


>Página de status do servidor mod_status do serviço Tor onion


Junte isso [**à questão da divulgação mod_info**](https://www.tenable.com/plugins/nessus/10678) (http://ONIONADDRESS/server-info)  e podemos ver rapidamente por que isso é tão destrutivo para o anonimato do serviço Tor. Visitamos a página de informações em <http://lchuditewd4ltjti.onion/server-info> e vimos as informações abaixo: 1 - dados do sistema operacional; 2 - endereço de serviço do Tor; 3 - Caminho instalado no servidor.

![](https://osintcurio.files.wordpress.com/2019/03/2019-03-04_13-51-48.png)

>Página de informações do servidor mod_info do serviço de cebola Tor mostrando dados de configuração detalhados

ESTÁ BEM. Isso é interessante, mas ... e daí? Continue rolando esta página para baixo e você obtém o que está na imagem abaixo.

![](https://osintcurio.files.wordpress.com/2019/03/2019-03-04_13-52-49.png)


>Página de informações do servidor mod_info do serviço Tor onion mostrando vários serviços cebola configurados no sistema

O gráfico acima mostra que esse servidor, no qual vimos apenas um único serviço Tor onion em execução, está configurado para hospedar mais de 10 outros serviços ocultos! Agora, isso é útil para nossa investigação!

Abaixo está uma página de informações do servidor diferente do sistema <http://w56m67cjc6f3qyet.onion/server-info> . Este contém os dados do caminho do sistema operacional e uma entrada para quem é o "administrador do servidor" (desfocamos o endereço de email). Também existem outros endereços de e-mail mencionados neste arquivo.

![](https://osintcurio.files.wordpress.com/2019/03/2019-03-04_14-03-43.png)

>Página de informações do servidor mod_info do serviço Tor onion mostrando um endereço de email

## Embrulhando-o

Novamente, se configurado corretamente, os mod_status e mod_info módulos seria desativado ou restrito a um administrador. Como eles não são, podemos ler arquivos nos serviços de ocultação / cebola do Tor, que não devemos ler e consumir os dados que des-anonimamente os sistemas; vinculando-os a outros hosts da Web de superfície e e-mails, agora podemos pesquisar usando técnicas tradicionais da Web de superfície.

Quer ver isso em ação, mas não consegue chegar ao Tor? Confira nosso vídeo com dicas de 10 minutos: <https://www.youtube.com/watch?v=71dSepA-gqc>

---

Author: [WEBBREACHER](https://osintcurio.us/author/webbreacher/)

[Artigo Original](https://osintcurio.us/2019/03/05/apache-mod_status-in-tor-hidden-services-destroy-anonymity/)










