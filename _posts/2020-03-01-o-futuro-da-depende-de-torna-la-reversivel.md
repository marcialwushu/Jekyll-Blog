---
layout: post
title:  "O futuro da computação depende de torná-la reversível"
date:   2020-03-01 17:59:38 -0200
categories: jekyll update
---

>## É hora de adotar a computação reversível, que pode oferecer melhorias drásticas na eficiência energética

![](https://spectrum.ieee.org/image/Mjk0NDk4Mw.jpeg)

>Ilustração: Chad Hagen


Por mais de 50 anos, os computadores fizeram melhorias constantes e dramáticas, tudo graças à Lei de Moore - o aumento exponencial ao longo do tempo no número de transistores que podem ser fabricados em um circuito integrado de um determinado tamanho. A Lei de Moore deveu seu sucesso ao fato de que, à medida que os transistores foram diminuindo, eles se tornaram simultaneamente mais baratos, mais rápidos e mais eficientes em termos de energia. A recompensa desse cenário ganha-ganha-ganha possibilitou o reinvestimento na tecnologia de fabricação de semicondutores que poderia produzir transistores ainda menores e mais densamente compactados. E assim esse círculo virtuoso continuou, década após década.

Agora, porém, especialistas em laboratórios da indústria, da academia e do governo antecipam que a miniaturização de semicondutores não continuará por muito mais tempo - [talvez 5 ou 10 anos](https://spectrum.ieee.org/semiconductors/devices/transistors-could-stop-shrinking-in-2021). Diminuir os transistores não gera mais as melhorias que costumava ser. As características físicas de pequenos transistores fizeram com que a velocidade do relógio estagnasse mais de uma década atrás, o que levou a indústria a começar a construir chips com [múltiplos núcleos](https://spectrum.ieee.org/computing/software/the-trouble-with-multicore) . Mas mesmo as arquiteturas multicore devem lidar com quantidades crescentes de "silício escuro", áreas do chip que devem ser desligadas para evitar superaquecimento.

Estão sendo feitos esforços heróicos na indústria de semicondutores para tentar manter a miniaturização em andamento. Mas nenhuma quantidade de investimento pode mudar as leis da física. Em algum momento - agora não muito distante - um novo computador que simplesmente possui transistores menores não será mais mais barato, mais rápido ou mais eficiente em termos de energia que seus antecessores. Nesse ponto, o progresso da tecnologia convencional de semicondutores irá parar.

E a tecnologia de semicondutores não convencional , como [transistores de nanotubos de carbono](https://spectrum.ieee.org/nanoclast/semiconductors/materials/carbon-nanotube-transistors-finally-outperform-silicon) , [transistores de tunelamento](https://spectrum.ieee.org/semiconductors/devices/the-tunneling-transistor) ou [dispositivos spintrônicos?](https://spectrum.ieee.org/semiconductors/processors/the-quest-for-the-spin-transistor) Infelizmente, muitas das mesmas barreiras físicas fundamentais que impedem a atual tecnologia complementar de metal-óxido-semicondutor (CMOS) de avançar muito mais ainda serão aplicadas, de forma modificada, a esses dispositivos. Poderemos conseguir mais alguns anos de progresso, mas se quisermos continuar avançando décadas adiante, novos dispositivos não serão suficientes: também teremos que repensar nossas noções mais fundamentais de computação.

Deixe-me explicar. Durante toda a história da computação, nossas máquinas de calcular operaram de maneira a causar a perda intencional de algumas informações (sobrescritas destrutivamente) no processo de realização dos cálculos. Porém, há várias décadas, sabemos que é possível, em princípio, realizar qualquer cálculo desejado sem perder informações - isto é, de tal maneira que o cálculo sempre pode ser revertido para recuperar seu estado anterior. Essa idéia de [computação reversível](https://en.wikipedia.org/wiki/Reversible_computing) vai ao cerne da termodinâmica e da teoria da informação e, de fato, é a única maneira possível dentro das leis da física de podermos continuar melhorando o custo e a eficiência energética da computação de uso geral até o fim. futuro.

No passado, a computação reversível nunca recebeu muita atenção. Isso ocorre porque é muito difícil de implementar e havia poucas razões para enfrentar esse grande desafio, desde que a tecnologia convencional continuasse avançando. Mas, com o fim agora à vista, é hora das melhores mentes de física e engenharia do mundo iniciarem um esforço total para levar a computação reversível à fruição prática.

**A história da computação reversível** começa com o físico Rolf Landauer, da IBM, que publicou um artigo em 1961 intitulado ["Irreversibilidade e geração de calor no processo de computação "](http://ieeexplore.ieee.org/document/5392446/). Nele, Landauer argumentou que o caráter logicamente irreversível das operações computacionais convencionais tem implicações diretas no comportamento termodinâmico de um dispositivo que está realizando essas operações.

O raciocínio de Landauer pode ser entendido observando-se que as leis mais fundamentais da física são reversíveis, o que significa que, se você tivesse conhecimento completo do estado de um sistema fechado em algum momento, sempre poderia - pelo menos em princípio - executar as leis da física. reverter e determinar o estado exato do sistema a qualquer momento anterior.

Para ver melhor, considere um jogo de bilhar - ideal, sem atrito. Se você fizesse um filme das bolas ricocheteando umas nas outras e nos pára-choques, o filme pareceria normal, se você o rodasse para trás ou para a frente: a física da colisão seria a mesma e você poderia descobrir a configuração futura das bolas da configuração anterior ou vice-versa com a mesma facilidade.

A mesma reversibilidade fundamental vale para a física da escala quântica. Como conseqüência, você não pode ter uma situação em que dois estados detalhados diferentes de qualquer sistema físico evoluam para o mesmo estado em algum momento posterior, porque isso tornaria impossível determinar o estado anterior a partir do último. Em outras palavras, no nível mais baixo da física, as informações não podem ser destruídas.

A reversibilidade da física significa que nunca podemos realmente apagar informações em um computador. Sempre que sobrescrevemos um pouco de informação com um novo valor, as informações anteriores podem ser perdidas para todos os fins práticos, mas não foram realmente destruídas fisicamente. Em vez disso, foi empurrado para o ambiente térmico da máquina, onde se torna entropia - em essência, informações aleatórias - e se manifesta como calor.

Voltando ao nosso exemplo de jogo de bilhar, suponha que as bolas, os pára-choques e o feltro não tenham atrito. Então, com certeza, duas configurações iniciais diferentes podem terminar no mesmo estado - digamos, com as bolas descansando em um lado. A perda de informações por atrito geraria calor, embora uma quantidade minúscula.

Os computadores de hoje dependem de apagar informações o tempo todo - tanto que cada porta lógica ativa nos projetos convencionais substitui destrutivamente sua saída anterior em cada ciclo do relógio, desperdiçando a energia associada. Um computador convencional é, essencialmente, um aquecedor elétrico caro que, por acaso, executa uma pequena quantidade de computação como efeito colateral.

---

## De volta para o Futuro

A computação reversível é baseada na física reversível, onde nenhuma energia é perdida por atrito

![](https://spectrum.ieee.org/image/Mjk0NDkzOA.jpeg)

>Ilustração: James Provost

DUAS BOLAS IDEAIS, perfeitamente elásticas e livres de atrito interno, caem de diferentes alturas. Eles retornarão repetidamente às suas alturas originais. A qualquer momento, a velocidade e a posição futura ou passada de uma bola podem ser calculadas com base em sua velocidade e posição atual [esquerda]. Mas se houver atrito interno, a situação não será mais reversível: as duas bolas acabam no chão e você não pode determinar as velocidades e posições do passado em relação às atuais [direita]. Aqui, a energia é desperdiçada através da geração friccional de calor

![](https://spectrum.ieee.org/image/Mjk0NDk0MA.jpeg)

>Ilustração: James Provost


Uma PORTA LÓGICA poderia, em princípio, ser construída a partir de bolas e barreiras idealizadas. Esse portão E de bola de bilhar possui duas entradas e três saídas. Se um "verdadeiro" for aplicado apenas à entrada "A" (uma bola entrando do topo), um "verdadeiro" aparecerá na saída "A" (bola saindo do fundo) [esquerda]. Se "true" for aplicado apenas à entrada "B" (uma bola entrando pela esquerda), então "true" aparecerá apenas na saída "(NOT-A) AND B" (bola saindo à direita) [ meio]. Se "true" for aplicado às duas entradas, um "true" aparecerá nas saídas "A" e "A AND B" [direita].

---


Quanto calor é produzido? A conclusão de Landauer, que desde então foi [confirmada experimentalmente](https://www.nature.com/nature/journal/v483/n7388/full/nature10872.html) , foi que cada apagamento de bit deve dissipar pelo menos 17 milésimos de um elétron-volt à temperatura ambiente. Essa é uma quantidade muito pequena de energia, mas, considerando todas as operações que ocorrem em um computador, acrescenta-se. Atualmente, a tecnologia CMOS realmente é muito pior do que Landauer calculou, dissipando algo em torno de 5.000 elétron-volts por bit apagado. Os projetos CMOS padrão podem ser aprimorados nesse sentido, mas eles nunca serão capazes de obter muito abaixo de cerca de 500 eV de energia perdida por bit apagado, ainda longe do limite inferior do Landauer.

Podemos fazer melhor? Landauer começou a considerar essa questão em seu artigo de 1961, onde deu exemplos de operações logicamente reversíveis, ou seja, aquelas que transformam estados computacionais de tal maneira que cada estado inicial possível produz um estado final único. Tais operações poderiam, em princípio, ser realizadas de uma maneira termodinamicamente reversível, caso em que qualquer energia associada aos sinais de informação no sistema não precisaria necessariamente ser dissipada como calor, mas poderia potencialmente ser reutilizada para operações subseqüentes.

Para provar que essa abordagem ainda poderia fazer tudo o que um computador convencional poderia fazer, Landauer também observou que qualquer operação computacional logicamente irreversível desejada poderia ser incorporada em uma reversível, simplesmente deixando de lado qualquer informação que não era mais necessária, em vez de apagá-la. Mas Landauer originalmente pensava que fazer isso atrasava apenas o inevitável, porque as informações ainda precisariam ser apagadas eventualmente, quando a memória disponível fosse preenchida.

Foi deixado para o colega mais novo de Landauer, Charles Bennett , mostrar em 1973 que é possível construir computadores totalmente reversíveis, capazes de executar qualquer cálculo sem encher rapidamente a memória com dados temporários. O truque é desfazer as operações que produziram os resultados intermediários. Isso permitiria que qualquer memória temporária fosse reutilizada para cálculos subsequentes sem precisar apagá-la ou substituí-la. Dessa maneira, cálculos reversíveis, se implementados no hardware correto, poderiam, em princípio, contornar o limite de Landauer.

Infelizmente, a idéia de Bennett de usar a computação reversível para tornar a computação muito mais eficiente em termos energéticos permaneceu nos remansos acadêmicos por muitos anos. O problema era que é realmente difícil projetar um sistema que faça algo interessante em termos de computação, sem incorrer inadvertidamente em uma quantidade significativa de aumento de entropia a cada operação. Mas a tecnologia melhorou e a necessidade de minimizar o uso de energia agora é aguda. Portanto, alguns pesquisadores estão mais uma vez procurando a computação reversível para economizar energia.

**Como seria um computador reversível** ? As primeiras tentativas detalhadas para descrever um mecanismo físico eficiente para a computação reversível foram realizadas no final dos anos 70 e início dos anos 80 por Edward Fredkin e seu colega Tommaso Toffoli em seu [grupo de pesquisa em Mecânica da Informação](http://www.ai.mit.edu/projects/im/) no MIT.

Como prova de conceito, Fredkin e Toffoli propuseram que operações reversíveis poderiam, em princípio, ser realizadas por circuitos eletrônicos idealizados que usavam indutores para transportar pacotes de carga entre capacitores. Sem resistores que amorteciam o fluxo de energia, esses circuitos eram teoricamente sem perdas. No domínio mecânico, Fredkin e Toffoli imaginaram [esferas rígidas saltando umas das outras](https://en.wikipedia.org/wiki/Billiard-ball_computer) e fixando barreiras em trajetórias restritas, não muito diferentes do jogo de bilhar sem atrito que descrevi anteriormente.

Infelizmente, esses sistemas idealizados não puderam ser construídos na prática. Mas essas investigações levaram ao desenvolvimento de duas primitivas computacionais abstratas, agora conhecidas como o [portão de Fredkin](https://en.wikipedia.org/wiki/Fredkin_gate) e o [portão de Toffoli](https://en.wikipedia.org/wiki/Toffoli_gate) , que se tornaram a base de grande parte do trabalho teórico subsequente em computação reversível. Qualquer cálculo pode ser realizado usando esses portões, que operam em três bits de entrada, transformando-os em configurações finais exclusivas de três bits de saída.

Enquanto isso, outros pesquisadores em locais como Caltech , Rutgers , Universidade do Sul da Califórnia e Xerox PARC continuaram a explorar possíveis implementações eletrônicas. Eles chamaram seus circuitos de "adiabáticos" após o regime termodinâmico idealizado no qual a energia é impedida de deixar o sistema como calor.

Mais tarde, essas idéias encontraram terreno fértil no MIT, onde, em 1993, um estudante de pós-graduação chamado Saed Younis, no grupo de Tom Knight, mostrou pela primeira vez que circuitos adiabáticos poderiam ser usados para implementar lógica totalmente reversível. Os alunos posteriores do grupo, incluindo Carlin Vieri e eu, construímos sobre essa base para projetar e [construir processadores totalmente reversíveis](http://www.nytimes.com/1999/06/15/science/a-radical-computer-learns-to-think-in-reverse.html) de vários tipos no CMOS como simples provas de conceito. Este trabalho estabeleceu que não havia barreiras fundamentais que impedissem que toda a disciplina da arquitetura de computadores fosse traduzida para o domínio reversível.

Enquanto isso, outros pesquisadores estavam explorando abordagens alternativas para implementar a computação reversível, que não eram baseadas na eletrônica de semicondutores. No início dos anos 90, o visionário da nanotecnologia K. Eric Drexler produziu projetos detalhados para dispositivos lógicos nanomecânicos reversíveis feitos de materiais semelhantes a diamantes. Ao longo das décadas, pesquisadores russos e japoneses desenvolveram dispositivos eletrônicos supercondutores reversíveis, como o quantron paramétrico de nome semelhante (mas distinto) e o parametron de fluxo quântico . E um grupo da Universidade de Notre Dame estava estudando como usar elétrons únicos interagindo em matrizes de pontos quânticos. Para aqueles de nós que trabalhavam em computação reversível nos anos 90, parecia que, com base na ampla gama de possíveis hardwares que já haviam sido propostos, algum tipo de tecnologia prática de computação reversível pode não estar muito distante.

Infelizmente, a idéia ainda estava à frente de seu tempo. A tecnologia convencional de semicondutores melhorou rapidamente entre os anos 90 e o início dos anos 2000 e, portanto, o campo da computação reversível definhava. No entanto, foram feitos alguns progressos. Por exemplo, em 2004, Krishna Natarajan (uma estudante que eu estava orientando na Universidade da Flórida) e mostrei em simulações detalhadas que uma nova e simplificada família de circuitos para computação reversível chamada lógica adiabática de dois níveis, ou 2LAL, poderia se dissipar tão pouco como 1 eV de energia por transistor por ciclo - cerca de 0,001% da energia normalmente usada pelos sinais lógicos nessa geração de CMOS. Ainda assim, um computador reversível prático ainda precisa ser construído usando essa ou outras abordagens.

Não resta muito tempo para desenvolver máquinas reversíveis, porque o progresso na tecnologia convencional de semicondutores pode parar em breve. E se isso acontecer, o setor poderá estagnar, tornando o progresso muito mais difícil. Portanto, chegou a hora de buscar essa tecnologia, pois provavelmente levará pelo menos uma década para que os computadores reversíveis se tornem práticos.

A necessidade mais crucial é de novas tecnologias de dispositivos reversíveis. Os transistores CMOS convencionais - especialmente os menores e mais modernos - vazam muita corrente para produzir circuitos adiabáticos muito eficientes. Transistores maiores baseados em tecnologia de fabricação mais antiga vazam menos, mas teriam que ser operados muito lentamente, o que significa que muitos dispositivos precisariam ser usados ​​para acelerar a computação por meio de operação paralela. Empilhá-los em camadas pode gerar circuitos adiabáticos compactos e com baixo consumo de energia, mas, no momento, essa fabricação 3D ainda é bastante cara. E o CMOS pode ser um beco sem saída em qualquer caso.


Felizmente, existem algumas alternativas promissoras. Uma é usar eletrônicos supercondutores rápidos para construir circuitos reversíveis, que já demonstraram dissipar menos energia por dispositivo do que o limite de Landauer quando operados reversivelmente. Os avanços nesse domínio foram feitos por pesquisadores da Universidade Nacional de Yokohama , da Stony Brook University e da Northrop Grumman. Enquanto isso, uma equipe liderada por Ralph Merkle no Institute for Molecular Manufacturingem Palo Alto, Califórnia, projetou máquinas moleculares reversíveis em escala nanométrica, que, em teoria, poderiam consumir cem bilhões de biliões da energia da tecnologia de computação atual, enquanto ainda alternavam as escalas de tempo em nanossegundos. O problema é que a tecnologia para fabricar esses dispositivos atomicamente precisos ainda precisa ser inventada.

Independentemente de essas abordagens serem bem-sucedidas, os físicos que estão trabalhando no desenvolvimento de novos conceitos de dispositivos precisam manter em mente o objetivo da operação reversível. Afinal, essa é a única maneira que qualquer novo substrato de computação pode superar os recursos práticos da tecnologia CMOS de fim de linha em muitas ordens de magnitude, em oposição a apenas algumas no máximo.

---

## Computando com pequena lógica de link

![](https://spectrum.ieee.org/image/Mjk0NDgyNw.jpeg)

>Ilustração: James Provost

**Ralph Merkle** e seus colegas imaginam fazer cálculos usando a "lógica de link" nanomecânica, um componente básico para o qual é mostrado aqui. Esse dispositivo contém duas barras móveis [cinza escuro], conectadas de forma que apenas uma barra de cada vez possa ser deslocada de sua posição central. Essas barras mediam algumas centenas de átomos de diâmetro e seus pontos de articulação seriam quase sem atrito. Assim, um grande número deles conectados da maneira correta poderia realizar cálculos, assim como os transistores fazem hoje. A diferença é que um pequeno sistema de lógica de link seria reversível.

---

**Para ser claro**, a computação reversível não é nada fácil. De fato, os obstáculos de engenharia são enormes. A obtenção de computação reversível eficiente com qualquer tipo de tecnologia provavelmente exigirá uma revisão completa de toda a nossa infraestrutura de design de chips. Também teremos que treinar grande parte da força de trabalho de engenharia digital para usar as novas metodologias de design. Eu acho que o custo total de todos os novos investimentos em educação, pesquisa e desenvolvimento que serão necessários nas próximas décadas provavelmente vai chegar a bilhões de dólares. É um tiro na lua da computação do futuro.

Mas, na minha opinião, a dificuldade desses desafios seria uma desculpa muito ruim para não enfrentá-los. Nesse momento, chegamos a um momento histórico na evolução da tecnologia de computação e precisamos escolher um caminho em breve.

Se continuarmos em nosso curso atual, isso significaria desistir do futuro da computação e aceitar que a eficiência energética de nosso hardware em breve chegará ao platô. Mesmo conceitos não convencionais, como a computação neural analógica ou baseada em picos , chegarão a um limite se eles não forem projetados para serem reversíveis. E mesmo um avanço na computação quântica ajudaria a acelerar significativamente algumas classes de computação altamente especializadas, e não a computação em geral.

Mas se decidirmos abrir caminho para essa nova trilha da computação reversível, podemos continuar a encontrar maneiras de continuar melhorando a computação no futuro. A física não conhece um limite superior para a quantidade de computação reversível que pode ser realizada usando uma quantidade fixa de energia. Até onde sabemos, um futuro ilimitado para a computação nos espera, se tivermos coragem suficiente para aproveitá-lo.

Este artigo aparece na edição impressa de setembro de 2017 como "Jogando a computação para trás".

---

Autor: [Michael P. Frank](https://cfwebprod.sandia.gov/cfdocs/CompResearch/templates/insert/profile.cfm?mpfrank)

[Artigo Original](https://spectrum.ieee.org/computing/hardware/the-future-of-computing-depends-on-making-it-reversible)




