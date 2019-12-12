---
layout: post
title:  "Micro Frontends no BuzzFeed"
date:   2019-12-12 17:59:38 -0200
categories: jekyll update
---

A definição do que constitui um "micro Frontend" talvez ainda não tenha chegado a um consenso. O [smart folks at DAZN](https://medium.com/dazn-tech/orchestrating-micro-frontends-a5d2674cbf33) considera uma série de páginas completas gerenciadas por um orquestrador do lado do cliente. Outras abordagens, como o OpenComponents , compõem páginas únicas de vários micro frontends.


O caso de uso do BuzzFeed se encaixa em algum lugar entre os dois. Eu não diria que temos uma arquitetura de micro frontend; no entanto, nós os alavancamos em algumas partes da página. Consideramos algo como um micro front-end se a API retornar html totalmente renderizado (e ativos), mas não um elemento ```<html>``` ou ```<body>```.

Temos três micro frontends: o componente do cabeçalho, o conteúdo da postagem e nossas incorporações interativas. Cada um deles adotou a abordagem de micro front-end porque apresentava problemas de negócios reais e distintos.

## Micro Frontend ```#``` 1: O cabeçalho

Por quê? Distribuição de componentes

![](https://miro.medium.com/max/1600/0*dOnfRQsyxQq4SkX0)

Este é o cabeçalho do buzzfeed.com. Ele possui uma leve camada de configuração e uma quantidade razoável de código por trás dele: certamente o suficiente para merecer uma abstração em vez de duplicá-la em todos os nossos serviços.


Originalmente, fizemos essa abstração e a extraímos em um pacote npm, cujos serviços importaram como parte de seu processo de criação. Isso nos permitiu remover a duplicação e fazer com que o serviço agrupasse o cabeçalho como parte de seu próprio processo de compilação (o que significa que poderíamos deduplicar facilmente códigos e bibliotecas comuns).


Com apenas dois ou três serviços, essa técnica funciona muito bem, mas temos mais de dez serviços de renderização no buzzfeed.com. Isso significava que toda vez que desejávamos fazer uma alteração no cabeçalho, tínhamos que fazer as seguintes alterações mais de 10 vezes:



1. Atualize o código no cabeçalho
2. Fazer uma solicitação pull
3. Mesclar e publicar para npm
4. Atualize o serviço package.json
5. Fazer uma solicitação pull
6. Mesclar e implantar o serviço


Isso tornou-se extremamente demorado e levou as equipes a evitar alterações no cabeçalho por causa disso. Claro, existem maneiras pelas quais poderíamos ter aprimorado esse fluxo de trabalho (por exemplo, usando sempre solto e apenas reconstruindo o serviço, automatizando a atualização e a criação de PRs de serviço), mas ainda assim parecia a abordagem errada. Ao mudar para um padrão de micro front-end, agora podemos distribuir o cabeçalho instantaneamente para todos os serviços e o fluxo de trabalho para atualizá-lo em todo o site buzzfeed.com agora:

1. Atualize o código no cabeçalho
2. Fazer uma solicitação pull
3. Implantar o cabeçalho




