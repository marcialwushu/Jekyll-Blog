---
layout: post
title:  "Micro Frontends no BuzzFeed"
date:   2019-12-12 17:59:38 -0200
categories: jekyll update
---

A definição do que constitui um "micro Frontend" talvez ainda não tenha chegado a um consenso. O pessoal inteligente da DAZN considera uma série de páginas completas gerenciadas por um orquestrador do lado do cliente. Outras abordagens, como o OpenComponents , compõem páginas únicas de vários micro frontends.


O caso de uso do BuzzFeed se encaixa em algum lugar entre os dois. Eu não diria que temos uma arquitetura de micro frontend; no entanto, nós os alavancamos em algumas partes da página. Consideramos algo como um micro front-end se a API retornar html totalmente renderizado (e ativos), mas não um elemento <html> ou <body>.

