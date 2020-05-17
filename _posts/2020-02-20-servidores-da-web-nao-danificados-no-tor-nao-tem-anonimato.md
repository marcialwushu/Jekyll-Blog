---
layout: post
title:  "Servidores da Web não danificados no Tor não têm anonimato"
date:   2020-02-20 17:59:38 -0200
categories: jekyll update
---

![](https://osintcurio.files.wordpress.com/2019/03/2019-03-04_10-00-16.png)


Olá. Este é o Micah / WebBreacher e estou invadindo aplicativos da Web há muitos anos. Algumas das sugestões mais comuns que dei / dei aos clientes foram fortalecer seus sistemas antes de colocá-los online. Proteger significa desativar recursos não utilizados, restringir o acesso sempre que possível e garantir que o servidor da Web, seja qual for o sabor que esteja usando, seja protegido usando as orientações de algumas das listas de verificação disponíveis on-line ou impressas ( <https://www.owasp.org /index.php/Secure_Configuration_Guide#2._Web_servers_misconfiguration> ).

## Divulgação de Informações do Apache mod_status

Em 2001, o scanner de vulnerabilidades Nessus da Tenable começou a procurar destinos para a vulnerabilidade de divulgação de informações do [Apache mod_status](https://httpd.apache.org/docs/2.4/mod/mod_status.html) ( <https://www.tenable.com/plugins/nessus/10677> ). Encontrar este problema foi trivial. Usando um navegador da web, você faria uma solicitação para um servidor da web Apache com http (s): //example.com / server-status / . Essa parte / status do servidor / levou o navegador a uma página que divulgava informações sobre o servidor Apache. Alguns dos dados mostrados incluem:

