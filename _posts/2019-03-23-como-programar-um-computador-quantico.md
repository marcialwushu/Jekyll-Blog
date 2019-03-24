---
layout: post
title:  "Como programar um computador quântico"
date:   2019-03-23 00:43:31 -0200
categories: jekyll update
---

>Como fazer Battleships de quantum NOT gates

![](https://cdn-images-1.medium.com/max/800/1*lVVOJh13uhwPjZPE0o-Vvg.jpeg)

Os computadores quânticos são um novo tipo estranho de computador. Eles criam números impensáveis de universos paralelos para executar programas mais rapidamente e usam princípios que confundem até mesmo Einstein. Eles são as mágicas caixas de milagres que vão deixar suas estúpidas caixas de transistores na poeira.

Isso é o que os artigos científicos populares provavelmente dirão a você, de qualquer maneira. Eles sem dúvida conseguem fazer com que essa nova tecnologia pareça excitante. Mas eles também podem fazer a computação quântica parecer uma arte arcana, confiada apenas aos cientistas mais inteligentes. Certamente não é algo para o público de programação mais amplo para se preocupar com!

Eu não acho que isso seja verdade. E com empresas como a IBM e o Google, na verdade, fabricando dispositivos quânticos, a hora de começar a brincar com a programação quântica é agora.

Você não precisa fazer nada extravagante no começo. Você pode começar sua jornada na programação quântica no mesmo lugar em que muitos de nós começam nossa jornada na programação normal: fazendo jogos.

Não se preocupe, não será necessário ter seu próprio computador quântico. Programas quânticos simples podem ser facilmente simulados em um computador normal. Também podemos emprestar algum tempo em um dispositivo quântico real, graças ao IBM Q Experience .

Este é o primeiro de uma série de artigos nos quais descrevo alguns programas simples feitos usando o quantum SDK da IBM. Cada um será uma versão independente dos Battleships, com processos quânticos simples usados ​​para implementar a mecânica básica do jogo.

Estes estão entre os primeiros jogos feitos para um computador quântico. Mostrarei os detalhes sangrentos do código por trás do jogo, para que você possa começar a experimentar também a programação quântica.

## O que é um computador quântico?

Antes de começarmos o programa, precisamos de algumas informações básicas. Não vou contar tudo sobre computação quântica. Nós vamos conseguir o suficiente para entender o que acontece no nosso jogo.

Um computador normal é baseado em bits: variáveis que possuem apenas dois valores possíveis. Muitas vezes os chamamos 0 e 1, embora no contexto da álgebra booleana, podemos chamá-los Truee False. Não importa o que nós chamamos. O ponto importante é que existem apenas dois estados.

Com bits podemos fazer operações booleanas simples, como NOT, AND e OR. Estes são os blocos de construção básicos da computação. Com estes podemos fazer qualquer coisa. Qualquer variável mais complexa que um bit (como um int ou float) é apenas uma coleção de muitos bits. Qualquer operação mais complexa que um AND ou NOT é, na verdade, apenas muitas delas juntas. Em seu nível mais básico, isso é o que um computador normal é.

Os computadores quânticos são baseados em bits quânticos ou qubits. Estes também têm dois valores possíveis que podemos chamar 0e 1. Mas as leis da mecânica quântica também permitem outras possibilidades, que chamamos de estados de superposição.

Em certo sentido, os estados de superposição são valores que existem a meio caminho entre os extremos de 0e 1. Podemos imaginar um qubit como uma esfera, com 0e 1sentando em postes opostos. Os estados de superposição são todos os outros pontos possíveis na superfície.

