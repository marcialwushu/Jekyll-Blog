---
layout: post
title:  "O que é DNA Computing, como funciona e por que é tão importante"
date:   2019-12-14 17:59:38 -0200
categories: jekyll update
---

Os cientistas estão fazendo progressos constantes na computação em DNA, mas o que é computação em DNA e como ela funciona?

![](https://inteng-storage.s3.amazonaws.com/images/MARCH/sizes/DNAHelix_resize_md.jpg)


Na última década, os engenheiros enfrentaram a dura realidade da física na busca de computadores mais poderosos: os transistores, os interruptores que acionam o processador do computador, não podem ser menores do que atualmente. Olhando além do chip de silício, atualmente está sendo desenvolvida uma alternativa intuitiva usando o DNA para realizar os mesmos tipos de cálculos complexos que os transistores de silício fazem agora. Mas o que é computação em DNA, como funciona a computação em DNA e por que isso é tão importante?

## Além do transistor

![](https://inteng-storage.s3.amazonaws.com/images/MARCH/sizes/IC-Chip_resize_md.jpg)

O problema dos transistores é que eles agora existem na escala de alguns nanômetros de tamanho - apenas alguns átomos de silício de espessura. Eles praticamente não podem ser menores do que são agora.

Se eles ficarem menores, a corrente elétrica que flui através do transistor vaza facilmente para outros componentes próximos ou deforma o transistor devido ao calor, tornando-o inútil. Você precisa de um número mínimo de átomos para fazer o transistor funcionar e, funcionalmente, [atingimos esse limite](https://interestingengineering.com/no-more-transistors-the-end-of-moores-law) .

Os engenheiros descobriram algumas soluções alternativas para esse problema, usando sistemas multicore e multiprocessamento para aumentar a potência computacional sem precisar diminuir ainda mais os transistores, mas isso também traz vantagens em termos de desafios de programação e requisitos de energia; portanto, é necessária outra solução se esperamos ver computadores mais poderosos no futuro.


Embora a [computação quântica](https://interestingengineering.com/ibm-introduces-first-integrated-quantum-computing-system-for-commercial-use) esteja ganhando muita imprensa ultimamente, a computação de DNA pode ser tão ou mais poderosa do que a computação quântica e não se depara com quase tantas restrições de estabilidade que a computação quântica tem. Além disso, sabemos que funciona; nós mesmos somos exemplos vivos do armazenamento de dados e do poder computacional da computação em DNA.

O desafio para a computação de DNA é que, comparado à computação clássica, é dolorosamente lento. A evolução teve centenas de milhões de anos para desenvolver a complicada sequência de DNA que existe dentro de todas e cada uma de nossas células, para que o DNA esteja acostumado a trabalhar de acordo com as escalas de tempo geológicas, e não os múltiplos gigahertz dos modernos processadores clássicos.

Então, como funciona a computação em DNA e por que a estamos perseguindo se é tão lenta?

## O que é DNA Computing, como funciona e por que é tão importante?

![](https://inteng-storage.s3.amazonaws.com/images/MARCH/sizes/DNA_helix_resize_md.jpg)

Para entender o que é a computação em DNA, como ela funciona e por que a computação em DNA é tão importante, primeiro precisamos parar de pensar nela como uma espécie de substituto para o uso cotidiano de computadores clássicos; não jogaremos jogos em um computador de DNA tão cedo, se isso fosse possível. Os chips de silicone estarão conosco por muito tempo ainda.

A computação em DNA é o que usaríamos para resolver problemas além do escopo do que um computador clássico pode resolver, da mesma forma que a computação quântica pode interromper a criptografia RSA em momentos, enquanto um computador clássico pode levar milhares de anos para fazer o mesmo.

A computação em DNA foi descrita pela primeira vez em 1994 pelo cientista da computação Leonard Adleman, da Universidade do Sul da Califórnia. Depois de ler a estrutura do DNA, ele foi inspirado a escrever um artigo na revista Science mostrando como você poderia usar o DNA para um infame problema matemático e de ciência da computação conhecido como problema direcionado de Hamilton Path, comumente chamado de "vendedor ambulante" (embora o problema do Hamilton Path seja uma [versão ligeiramente diferente](https://stackoverflow.com/questions/7763432/what-is-the-difference-between-travelling-salesman-and-finding-shortest-path) do problema do vendedor ambulante, para nossos propósitos eles são essencialmente intercambiáveis).

## Qual é o problema do vendedor ambulante?

Como o problema do vendedor ambulante o define, uma empresa possui um vendedor que deve visitar n número de cidades que fazem ligações e só pode visitar cada cidade uma vez. Que sequência de cidades visitadas fornece o caminho mais curto e, portanto, o mais barato?

Quando n é igual a 5, o problema pode ser resolvido manualmente em um pedaço de papel e um computador clássico pode testar todos os caminhos possíveis com relativa rapidez. Mas e se n for igual a 20? Encontrar o caminho mais curto pelas 20 cidades se torna muito mais difícil computacionalmente e levaria um computador clássico exponencialmente mais tempo para encontrar a resposta.

Tente encontrar o caminho mais curto entre 500 cidades e levaria um computador clássico mais longo do que toda a vida útil do Universo para encontrar o caminho mais curto, pois a única maneira de verificar se encontramos o caminho mais curto é verificar todas as permutações de cidades. . Alguns algoritmos existem usando computação dinâmica que, teoricamente, pode reduzir o número de verificações necessárias (e o problema atual do Hamilton Path não exige a verificação de todos os nós em um gráfico), mas isso pode reduzir alguns milhões de anos; o problema ainda será praticamente computacionalmente impossível em um computador clássico.

## Como a DNA Computing resolve esse problema

![](https://inteng-storage.s3.amazonaws.com/images/MARCH/sizes/DNA-Helix_resize_md.jpg)

O que Adleman conseguiu demonstrar [[PDF]](http://152.2.128.56/~montek/teaching/Comp790-Fall11/Home/Home_files/Adleman-ScAm94.pdf) é que o DNA pode ser montado de maneira que um tubo de ensaio cheio de blocos de DNA possa se montar para codificar todos os caminhos possíveis no problema do vendedor ambulante ao mesmo tempo.

No DNA, a codificação genética é representada por quatro moléculas diferentes, chamadas A, T, C e G. Esses quatro "bits", quando encadeados, podem armazenar uma quantidade incrível de dados. Afinal, o genoma humano é codificado em algo que pode ser compactado em um único núcleo de uma célula.

Ao misturar essas quatro moléculas em um tubo de ensaio, as moléculas se reuniram naturalmente em filamentos de DNA. Se alguma combinação dessas moléculas representa uma cidade e uma trajetória de vôo, cada fileira de DNA pode representar uma trajetória diferente para o vendedor, todas calculadas de uma só vez na síntese das fileiras de DNA que se montam em paralelo.

Então, seria simplesmente uma questão de filtrar os caminhos mais longos até que você tenha apenas o caminho mais curto restante. Em seu artigo, ele mostrou como isso poderia ser feito com 7 cidades e a solução do problema seria codificada assim que as fitas de DNA fossem sintetizadas.

![](https://inteng-storage.s3.amazonaws.com/images/MARCH/sizes/DNA-Computing_resize_md.jpg)

A razão pela qual isso gerou entusiasmo foi que as estruturas de DNA são baratas, relativamente fáceis de produzir e escalonáveis. Não há limite para o poder que teoricamente a computação em DNA pode ter, pois esse poder aumenta quanto mais moléculas você adiciona à equação e, diferentemente dos transistores de silício que podem executar uma única operação lógica por vez, essas estruturas de DNA podem teoricamente realizar tantos cálculos em o tempo necessário para resolver um problema e fazer tudo de uma vez.

O problema, no entanto, é a velocidade. Mesmo que a solução de Adleman para o problema do vendedor ambulante tenha levado algum tempo para ser codificada em suas cadeias de DNA no tubo de ensaio, demorou dias filtrando soluções ruins para encontrar a solução ideal que ele estava procurando - após uma preparação meticulosa para esse cálculo único .

Ainda assim, o conceito era sólido e o potencial para ganhos incríveis na capacidade de armazenamento e velocidade computacional era óbvio. Isso deu início a duas décadas de pesquisa sobre como criar uma realidade prática na computação com DNA.

## Quais são as vantagens da DNA Computing?

Como demonstrado no artigo de Adleman, a principal vantagem da computação em DNA sobre a computação clássica - e até a [computação quântica](https://interestingengineering.com/what-will-quantum-computing-change-exactly) até certo ponto - é que ela pode realizar inúmeros cálculos em paralelo. Essa idéia de computação paralela não é nova e é imitada na computação clássica há décadas.

Quando você executa dois aplicativos em um computador ao mesmo tempo, eles não estão sendo executados simultaneamente; a qualquer momento, apenas uma instrução está sendo executada. Portanto, se você estiver ouvindo música e comprando on-line usando um navegador, o computador está realmente usando algo chamado [alternância de contexto](https://www.tutorialspoint.com/what-is-context-switching-in-operating-system) para dar a aparência de simultaneidade.

Ele executa uma instrução para um programa, salva o estado desse programa após a execução da instrução e remove o programa da memória ativa. Em seguida, ele carrega o estado salvo anteriormente do segundo programa, executa sua próxima instrução, salva seu novo estado e o descarrega da memória ativa. Em seguida, recarrega o primeiro programa para executar sua próxima instrução e assim por diante.

Fazendo milhões de etapas incrementais por segundo em diferentes programas, a aparência de simultaneidade é alcançada, mas nada é realmente executado paralelamente. A computação em DNA pode realmente realizar esses milhões de operações ao mesmo tempo.

Mais de 10 trilhões de moléculas de DNA [podem ser](https://computer.howstuffworks.com/dna-computer2.htm) espremidas em um único centímetro cúbico. Esse centímetro cúbico de material poderia teoricamente executar 10 trilhões de cálculos de uma vez e conter até 10 terabytes de dados. De muitas maneiras, muita da imprensa ofegante, mas imprecisa, que a computação quântica recebe é realmente possível com a computação de DNA.

A computação em DNA é então melhor pensada como um complemento da computação quântica, de modo que, quando combinados e conduzidos por um computador clássico agindo como um [gerente no estilo Singleton](https://www.dictionary.com/browse/singleton) , os tipos de aumentos dramáticos no poder computacional que as pessoas esperam ver no futuro realmente se torna realisticamente possível.

## Quanto tempo levará para os computadores de DNA chegarem

Percorremos um longo caminho desde 1994. Logo após Adleman publicou seu artigo, os pesquisadores conseguiram construir portas lógicas a partir do DNA - as partes de um circuito construído a partir de transistores individuais que podem construir complicadas equações lógicas verdadeiro-falso a partir da corrente elétrica .

Apenas neste mês, cientistas da computação da Universidade da Califórnia em Davis e Caltech [sintetizaram](https://www.nature.com/articles/s41586-019-1014-9) moléculas de DNA que podem se auto-montar em estruturas executando essencialmente seu próprio programa usando entradas de seis bits.

A Microsoft ainda possui uma [linguagem de programação](https://www.microsoft.com/en-us/research/project/programming-dna-circuits/) para a computação em DNA que pode ajudar a tornar a computação em DNA prática, uma vez que a tecnologia dos bioprocessadores progride a ponto de executar algoritmos mais sofisticados. De fato, a Microsoft planeja [introduzir](https://bigthink.com/philip-perry/microsoft-plans-to-have-a-dna-based-computer-by-2020) a computação de DNA em seus serviços de nuvem até 2020 e desenvolver ativamente um armazenamento de dados de DNA [para integrar](https://www.technologyreview.com/s/607880/microsoft-has-a-plan-to-add-dna-data-storage-to-its-cloud/) seus serviços de nuvem.

É provável que esses avanços sejam realizados muito mais rapidamente do que os avanços na computação quântica. [A computação quântica](https://interestingengineering.com/what-will-quantum-computing-change-exactly) exige máquinas sofisticadas, supercondutores e condições extremamente frias para manter os qubits estáveis o suficiente para realizar tarefas computacionais realmente úteis, e, a menos que desenvolvamos um material que possa atuar como [supercondutor](https://interestingengineering.com/superconductivity-what-is-it-and-why-it-matters-to-our-future) à temperatura ambiente, eles não entrarão em ação. nossos computadores em breve.

Enquanto isso, a computação em DNA usa o DNA que nos tornamos especialistas em manipular a ponto de substituir um único gene de uma cadeia de DNA pelo [CRISPR](https://interestingengineering.com/scientists-use-crispr-on-edit-resistant-corn-to-boost-yields) . Os materiais necessários para sintetizar moléculas de DNA são baratos e prontamente disponíveis e permanecem estáveis à temperatura ambiente e além. O que a DNA Computing é potencialmente capaz de alcançar, dada a resiliência do DNA e o paralelismo biológico, representa um passo essencial para o futuro da computação.


---

Autor: [John Loeffler](https://interestingengineering.com/author/john-loeffler)

[Artigo Original](https://interestingengineering.com/what-is-dna-computing-how-does-it-work-and-why-its-such-a-big-deal)
