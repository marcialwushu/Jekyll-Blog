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

Em certo sentido, os estados de superposição são valores que existem a meio caminho entre os extremos de 0 e 1. Podemos imaginar um qubit como uma esfera, com 0 e 1sentando em postes opostos. Os estados de superposição são todos os outros pontos possíveis na superfície.

![](https://cdn-images-1.medium.com/max/800/1*2CmzGqe_tVECBj2QjhUoLg.png)

Além de 0 e 1, essa imagem também sinaliza alguns estados de superposição importantes. Um é chamado ```u3(0.5*pi,0,0) |0⟩```. É certo que não é um nome muito cativante, mas vamos ver o que realmente significa durante este artigo.

Esse modo de pensar sobre qubits faz com que pareçam um pouco com variáveis contínuas. Podemos representar qualquer ponto na superfície de uma esfera (como o ponto ```ψ``` na imagem) usando coordenadas polares com apenas alguns ângulos ```(θ e φ)```. Então você seria perdoado por pensar que um qubit é apenas um par de carros alegóricos. De certa forma, eles são. Mas em outro sentido mais preciso, eles não são.

Uma diferença importante é que nunca podemos extrair mais do que uma informação binária de um qubit. As próprias leis da física nos impedem de descobrir exatamente o que estão fazendo. Não podemos pedir um qubit para os detalhes exatos do estado de superposição. Nós só podemos forçá-lo a escolher entre dois pontos opostos na esfera (como 0 e 1). Se for algo diferente desses dois estados, terá que decidir aleatoriamente um ou outro.

Portanto, um qubit tem algumas propriedades de uma variável contínua e algumas propriedades de uma variável discreta. Na verdade, não é nenhum dos dois. É uma variável quântica.

## O que faremos com os qubits?

O jogo Battleships que estamos fazendo hoje é baseado em uma variante japonesa. Nisso, todos os navios ocupam apenas um único quadrado, mas alguns demoram mais para afundar do que outros. Teremos um navio que pode ser afundado por uma única bomba, um que precisa de dois e um que precise de três.

Para simular isso em um computador quântico, podemos usar um qubit para cada nave. O estado 0 pode ser identificado com um navio totalmente intacto e 1 com um que tenha sido destruído. Os estados de superposição corresponderão então à jornada de um navio rumo à destruição.

Um navio destruído por um único ataque será muito fácil de simular. Podemos inicializá-lo no estado 0 e, em seguida, aplicar um NOT quando for atingido. Quando o encontrarmos em estado 1, saberemos que foi destruído.

Vamos ver como implementar apenas esse processo simples em um computador quântico. Não nos preocuparemos com quaisquer outros navios, ou entradas e saídas no momento.

Para fazer isso, usaremos o SDK quântico QISKit para configurar um programa quântico. Aqui está um script que inicializa uma nave, a bombardeia e depois analisa se ela ainda está flutuando.

```
q = QuantumRegister(1) # inicializa um registrador com um único qubit 
c = ClassicalRegister(1) # inicializa um registrador com um bit normal 
qc = QuantumCircuit(q, c) # cria e esvazia o programa quântico
qc.u3(math.pi,0,0, q[0]) # aplica um NOT ao qubit
qc.measure( q[0], c[0] ) # mede o qubit

```






