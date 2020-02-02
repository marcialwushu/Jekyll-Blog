---
layout: post
title:  "Computação amorfa"
date:   2020-01-16 17:59:38 -0200
categories: jekyll update
---

>Harold Abelson, Thomas F. Knight, Gerald Jay Sussman e amigos 

>Este white paper foi escrito com contribuições substanciais e ajuda séria dos seguintes membros do nosso grupo: Stephen Adams, Natalya Cohen, Daniel Coore, Sola Grantham, Chris Hanson, Kevin Lin, Nick Papadakis, Sofya Raskhodnikova, Thanos Siapas e Jack Wisdom.


Uma colônia de células coopera para formar um organismo multicelular sob a direção de um programa genético compartilhado pelos membros da colônia. Um enxame de abelhas coopera para construir uma colméia. Os seres humanos se agrupam para construir vilas, cidades e nações. Estes exemplos levantam questões fundamentais para a organização de sistemas de computação:

- Como obtemos um comportamento coerente com a cooperação de um grande número de partes não confiáveis ​​que são interconectadas de maneiras desconhecidas, irregulares e que variam no tempo?
- Quais são os métodos para instruir uma miríade de entidades programáveis ​​a cooperar para alcançar objetivos específicos?

Essas questões foram reconhecidas como fundamentais por gerações. Mas este artigo argumenta que agora é um momento oportuno para enfrentar a engenharia de ordem emergente: identificar os princípios e linguagens de engenharia que podem ser usados ​​para observar, controlar, organizar e explorar o comportamento de multidões programáveis.

Chamamos esse esforço de estudo da *computação amorfa* .

O objetivo desta pesquisa é criar as bases arquitetônicas, algorítmicas e tecnológicas do sistema para explorar materiais programáveis. Estes são materiais que incorporam um grande número de elementos programáveis ​​que reagem entre si e com o ambiente. Esses materiais podem ser fabricados economicamente, desde que os elementos de computação sejam acumulados a granel sem providenciar interconexão e teste de precisão. Para explorar materiais programáveis, precisamos identificar os princípios de engenharia para organizar e instruir inúmeras entidades programáveis ​​a cooperar para alcançar objetivos pré-estabelecidos, mesmo que as entidades individuais não sejam confiáveis ​​e estejam interconectadas de maneiras desconhecidas, irregulares e que variam no tempo. Chamamos esse esforço de estudo da *computação amorfa* .

A computação amorfa é inspirada nos recentes desenvolvimentos surpreendentes na biologia molecular e na microfabricação. Cada uma delas é a base de uma tecnologia de kernel que torna possível construir ou aumentar um grande número de unidades de processamento de informações quase idênticas, com atuadores e sensores integrais (por exemplo, MEMS), quase sem nenhum custo. Os componentes microeletrônicos são tão baratos que podemos imaginar misturá-los em materiais produzidos a granel, como tintas, géis e concreto. Esses materiais inteligentes '' serão usados ​​em elementos estruturais e em revestimentos de superfície, como peles ou tintas.

Os engenheiros usarão materiais inteligentes para reduzir a necessidade de força e precisão em aparelhos mecânicos e elétricos, através da aplicação de computação. Será possível revestir um edifício ou uma ponte com tinta inteligente que relate cargas de tráfego e cargas de vento, que monitore a integridade da estrutura, que resista à flambagem ou até cure pequenas rachaduras, deslocando o material. Será possível criar uma sala limpa com pele ativa, forrada com cílios, que pode empurrar sujeira e poeira para um canto para remoção. Será possível construir uma parede que possa detectar vibrações (e se mover levemente por conta própria) para monitorar invasões ou cancelar ativamente o ruído.

Como a computação amorfa fornecerá meios para acumular e controlar agentes de computação a preços comparáveis ​​aos custos de matéria-prima, esperamos inventar maneiras de usar sistemas amorfos para atacar problemas de simulação anteriormente impossíveis. Como a computação amorfa nos oferece os meios para coordenar informações de um grande número de sensores distribuídos e usá-las para controlar um número igualmente vasto de efetores distribuídos, podemos usar a computação amorfa para criar sistemas que tenham uma resposta sem precedentes ao seu ambiente.

Explorar o potencial dessas tecnologias exigirá novos insights sobre a programação e organização de sistemas que possuem tantas partes que nem podem ser nomeadas. Existem princípios da física, matemática e biologia que podemos aplicar. Por exemplo, para relatar uma rachadura em uma ponte, um revestimento de tinta inteligente deve nomear locais na ponte. Podemos gerar soluções de equações diferenciais para construir amostras de coordenadas e combiná-las para criar uma descrição da geometria global da ponte. Esse processo de inicialização determina a geometria da tinta inteligente, embora tenhamos começado sem conhecimento a priori das posições ou orientações reais dos vizinhos que se comunicam além da suposição da comunicação local.


- [Porque agora?]()
- [O que é necessário]()
- [Introdução: Programação]()
    - [Exemplo: definição de região]()
    - [Exemplo: Equações diferenciais parciais]()
    - [Exemplo: Usando soluções PDE aproximadas para organizar sistemas amorfos]()
    - [Processos morfológicos e sistemas de reação-difusão]()
- [Introdução: Hardware]()
    - [Poder]()
    - [Comunicação]()
    - [O que podemos construir agora]()
- [Demonstrações iniciais]()
- [Implicações desta pesquisa]()
- [Referências]()
- [Sobre este documento ...]()


## Porque agora? ##


O novo impulso para a computação amorfa é inspirado nos recentes desenvolvimentos surpreendentes na biologia fundamental e na microfabricação. Cada uma delas é a base de uma tecnologia de kernel que torna possível construir ou aumentar um grande número de unidades de processamento de informações quase idênticas (com atuadores e sensores) quase sem nenhum custo. No entanto, explorar o potencial dessas tecnologias exigirá novas idéias sobre programação e organização do sistema.

Os componentes microeletrônicos são tão baratos que podemos imaginar misturá-los em materiais produzidos a granel, como tintas, géis e concreto. Os engenheiros podem explorar os materiais inteligentes resultantes para reduzir a necessidade de força e precisão em aparelhos mecânicos e elétricos, através da aplicação de inteligência computacional. Por exemplo, podemos imaginar revestir um edifício ou uma ponte com tinta inteligente, que relata cargas de tráfego e ventos e monitora a integridade da estrutura, ou até cura pequenas rachaduras, deslocando o material. Uma sala limpa com peles ativas  forradas com cílios pode empurrar sujeira e poeira para um canto para remoção. Uma parede que pudesse detectar vibrações (e se mover levemente por conta própria) poderia monitorar as instalações quanto a invasões ou cancelar ativamente o ruído.

Existem tecnologias existentes (como circuitos impressos flexíveis) que permitem organizar os microcomponentes em padrões pré-especificados. No entanto, para explorar totalmente o potencial de materiais inteligentes, será essencial obter o comportamento desejado sem a necessidade de fabricar com precisão a interconexão dos componentes microeletrônicos e sem a expectativa de que todos os componentes estejam operacionais ou que estejam organizados conforme o planejado. .

Organismos biológicos, é claro, realizam exatamente o tipo de comportamento organizado de sistemas amorfos que desejamos criar. Mas é apenas agora que os biólogos estão aprendendo a estrutura precisa de organismos completos: a edição de julho de 1995 da Science imprimiu o genoma completo de uma bactéria, e centenas de outros organismos completos serão sequenciados nos próximos anos. gif Assim, estaremos na posição de conhecer o microcódigo  completo para os organismos, o efeito da maioria dos genes, e teremos ainda em mãos a tecnologia para montar esses programas. No entanto, não temos paradigmas e metodologias de programação que nos ajudem a explorar mecanismos biológicos como uma tecnologia de engenharia para fabricar materiais inteligentes.

Podemos esperar encontrar algumas pistas na biologia do desenvolvimento. Avanços recentes na compreensão do processo de desenvolvimento em sistemas biológicos complexos, principalmente Drosophila (ver, por exemplo, [ 4 ]), estão descobrindo os princípios organizadores usados ​​para diferenciar e organizar órgãos e grupos de órgãos dentro de tais sistemas. Podemos aprender muito com a capacidade dos seres vivos de organizar dinamicamente matrizes de células inicialmente idênticas em matrizes altamente ordenadas de órgãos diferenciados e de interconectar esses sistemas de maneira organizada.

Existem ainda visões de longo prazo, como as nanotecnologias descritas por Drexler e outras [ 2 ]. Isso envolve o uso de novas químicas e materiais exóticos, e podemos esperar que a invenção da nanotecnologia seja iniciada pela aplicação de ferramentas biológicas e computacionais avançadas.

Todas essas visões de materiais inteligentes apresentam o mesmo desafio fundamental:

>Obter o comportamento desejado e coerente a partir de um grande número de partes não confiáveis interconectadas de maneiras desconhecidas, irregulares e que variam no tempo, orquestrando deliberadamente seu comportamento individual e sua cooperação.

Além de suas aplicações imediatas em materiais programáveis, o estudo da computação amorfa tem implicações fundamentais para o design de software em geral. Nossa capacidade de programar sistemas de software complexos não atende ao nosso desejo de resolver problemas complexos. Também não acompanhou o crescimento de recursos computacionais disponíveis para ajudar na solução. Em muitos casos, fizemos barganhas faustianas no design de sistemas de software - atingindo a eficiência reduzindo o número de operações de computação necessárias, mas com o sacrifício da simplicidade e da compreensão. Certa vez, fazia sentido tentar obter o desempenho dos computadores por qualquer técnica que pudesse reduzir a contagem de operações. À medida que os sistemas se tornam mais capazes, no entanto, os custos dominantes não são medidos em termos de contagem de operações, mas em termos da simplicidade conceitual do código e da comunicação necessária entre tarefas simultâneas. Um efeito do estudo da computação amorfa é que ela nos obriga a reavaliar o custo, agora talvez pouco justificado, de tornar os algoritmos não locais e inerentemente complexos para reduzir a contagem de operações.


## O que é necessário ##

Para progredir, precisamos inventar novas metodologias de software. Devemos entender que tipos de linguagens são apropriadas para descrever processos computacionais amorfos. Devemos isolar mecanismos computacionais primitivos apropriados e desenvolver meios poderosos para combiná-los e abstraí-los.

Trabalhos anteriores em sistemas de computação massivamente paralelos podem fornecer algumas orientações nessas investigações. Por exemplo, assistentes de autômatos celulares e processadores paralelos de granulação fina criaram algoritmos notáveis ​​que organizam recursos imensos de maneira eficaz. Eles também desenvolveram um suporte linguístico significativo para descrever esses algoritmos. gif A computação amorfa apresenta um desafio maior, porque seus mecanismos devem ser independentes da configuração detalhada e da confiabilidade dos elementos. Por exemplo, a tinta inteligente deve poder determinar as propriedades geométricas da superfície que ela reveste sem o conhecimento inicial das posições dos elementos computacionais da tinta.

Outra fonte de idéias pode ser a pesquisa de sistemas auto-organizados, que exibiu como alguns comportamentos coerentes de sistemas de grande escala podem emergir de interações puramente locais de elementos individuais. gif A computação amorfa pode explorar fenômenos semelhantes, mas não é nosso objetivo estudar os princípios da auto-organização em si . Como engenheiros, queremos construir sistemas para que eles acabem organizados para se comportarem como pretendemos a priori, não apenas para a evolução.

Embora a metodologia de programação para computação amorfa possa ser parcialmente explorada em simulação, materiais inteligentes reais devem ser desenvolvidos e demonstrados. Isso é tecnicamente desafiador, porque as tecnologias disponíveis de distribuição de energia e comunicação exigem que a interconexão de precisão seja robusta.

A computação amorfa precisa ser demonstrada em algumas aplicações convincentes. Por exemplo, podemos construir uma sala sensível pintando as paredes com tinta que incorpora computação, sensores de luz e sensores de vibração.

## Introdução: Programação ##

A maneira de começar a desenvolver técnicas de programação para computação amorfa é se concentrar em alguns problemas de paradigma. Já desenvolvemos simuladores que nos permitem experimentar idéias com um pequeno número de elementos computacionais, mas muitos dos fenômenos mais interessantes surgem apenas ao lidar com um grande número de elementos.

## Exemplo: definição de região ##

Suponha que pintemos uma superfície com tinta inteligente: queremos que a tinta divida a superfície em algumas regiões rotuladas, identifique os limites entre as regiões e gere uma estrutura de dados global que reflita a topologia de como as regiões estão conectadas. Esse problema de definição de região pode ser a primeira etapa de um programa que monitora a integridade da estrutura que a tinta cobre ou executa um controle distribuído com base na observação das variáveis ​​dinâmicas locais.

Em nossa pintura imaginada, existem elementos computacionais suficientes que podemos considerá-los como partículas que são aleatoriamente e uniformemente distribuídas por toda a pintura. Cada partícula pode se comunicar com dez ou vinte vizinhos próximos, por exemplo, através de comunicações eletrostáticas ou de rádio de muito curto alcance, mas uma partícula não sabe as direções ou distâncias para seus vizinhos. (Essa é uma suposição conservadora. Alguns substratos de hardware podem fornecer mais informações geométricas que isso.) Cada partícula também possui um gerador de números aleatórios de hardware (não pseudo-aleatório) que pode ser usado para escolher um identificador quase único (o ID) . Não assumimos que exista sincronização a priori entre partículas.

Para realizar a definição da região, suponha que já estamos no ponto em que cada partícula identificou um conjunto de vizinhos com os quais pode se comunicar. (A identificação dos vizinhos já é uma parte complicada do processo de inicialização, mas não falaremos sobre isso aqui.)

O primeiro passo é fazer um cluster local em pequena escala . Cada partícula inicializa uma variável de estado (seu LOWNUM) para ser o ID dessa partícula. A partícula compara seu LOWNUM com o de seus vizinhos e adota o menor valor como seu novo LOWNUM. Esse processo continua por algumas iterações. No final desta etapa, temos algumas regiões (partículas que possuem o mesmo LOWNUM). Cada região possui um raio aproximadamente igual ao número de iterações, mas as regiões têm um formato irregular e podem ter orifícios e limites mal definidos.

O próximo passo é regularizar as regiões: alise as bordas e preencha os orifícios. Isso pode ser feito com um algoritmo de pressão dos colegas . Cada partícula calcula uma tabela de frequência dos LOWNUMs de si e de seus vizinhos, encontra o LOWNUM que é afirmado com mais frequência e o adota como seu novo LOWNUM. Esse processo continua até que as coisas se estabilizem. Observe que o LOWNUM para uma região é de fato o ID da partícula de uma partícula específica nessa região. Podemos escolher essa partícula para atuar como representante da região. (A Figura 1 mostra um exemplo do algoritmo em andamento.)


![](https://trello-attachments.s3.amazonaws.com/5d7e8031eaec3e42c24aade0/5e3616fbd6040f4afd09841d/522be3df14efa6eaf6fc4dcefcfede33/img9.gif)

**Figura 1**: Progresso do algoritmo de crescimento da região, a partir de uma configuração inicial de 1000 partículas colocadas aleatoriamente em um quadrado de extremidade 1. Os vizinhos de cada partícula são todas as partículas a uma distância de 0,1 a partir dela. A figura à esquerda mostra as regiões formadas após o agrupamento local, mas antes da regularização. A figura à direita mostra o efeito da regularização. Antes da regularização, existem muitas regiões e as várias regiões são misturadas. Observe como as regiões se tornam compactas e bem definidas quando regularizadas.

Nesse ponto, as partículas sabem se estão dentro de uma região ou nos limites entre as regiões: Cada partícula observa todos os LOWNUMs declarados em sua vizinhança. Uma partícula que vê mais de um LOWNUM está perto de uma aresta. Partículas que vêem exatamente dois LOWNUMs são interiores até a borda. Mais de dois LOWNUMs sinalizam um vértice.

Agora usamos o mesmo algoritmo de propagação LOWNUM, mas restrito a arestas, para que cada aresta adote um ID representativo (e partícula associada). Cada aresta se propaga apenas para as arestas que têm as mesmas duas regiões que elas vinculadas. Assim, as arestas disjuntas que vinculam as mesmas duas regiões receberão identificadores diferentes.

Agora, fazemos o mesmo processo para os vértices, as partículas em cada vértice selecionam um ID para o vértice (e uma partícula representativa correspondente).

Finalmente, combinamos todas essas informações por acumulação de transmissão . Cada partícula transmite o que sabe: os IDs das regiões, arestas e vértices, quais arestas separam quais regiões e quais arestas se encontram em cada vértice. Inicialmente, uma partícula conhece apenas as estruturas das quais faz parte. Mas, como uma partícula recebe mais informações, passa adiante. Para impedir a saturação da comunicação, uma partícula passa informações apenas quando aprende algo novo. Eventualmente, todas as partículas conhecerão todas as informações.

Este exemplo é instrutivo de várias maneiras:

- Ele expõe alguns padrões comuns e úteis, como pressão dos colegas e propagação de comparação.
- A capacidade de cada região escolher um representante, embora não seja usada acima, é útil no estabelecimento de árvores e protocolos de comunicação.
- Os algoritmos tendem a depender implicitamente da geometria. Por exemplo, a técnica de regularização baseia-se em suposições sobre a distribuição espacial uniforme e áspera das partículas e no fato de que a pressão dos pares corroerá os buracos preenchendo concavidades. As idéias aqui são remanescentes dos algoritmos de visão computacional, e algumas das técnicas da visão computacional podem ser relevantes. 

>Por exemplo, o método de dilatação e erosão usado no processamento de imagens morfológicas está realizando o mesmo tipo de processamento, embora isso geralmente seja feito no contexto de uma grade subjacente ou outro arranjo espacial regular dos elementos. (Veja, por exemplo, [ 5 ].)


- Estamos organizando abstrações computacionais que serão úteis no controle do comportamento da tinta. Por exemplo, agora podemos considerar as regiões, arestas e vértices como objetos computacionais que possuem identidades bem definidas e propriedades conhecidas.


## Exemplo: Equações diferenciais parciais ##

Muitos processos físicos, como o fluxo de ar sobre uma asa ou a vibração de uma membrana, são descritos em termos de campos restringidos por equações diferenciais parciais (PDEs). Os mecanismos que dependem do controle de tais sistemas podem ter que resolver essas equações, pelo menos aproximadamente, em tempo real. Atualmente, esse tipo de computação é muito caro e requer grandes recursos computacionais, que, por exemplo, não são facilmente integrados à asa de um avião. Um computador amorfo que incorpore os sensores e atuadores, integrados ao sistema a ser medido e controlado, pode ser exatamente o que é necessário para esta atividade computacionalmente exigente, mas altamente local.

Podemos começar a investigar esse tipo de computação examinando algumas equações diferenciais parciais autônomas elementares para ver o que é necessário para calcular suas soluções por um material inteligente. Suponha que usamos cada partícula computacional para representar uma região do espaço (ou espaço-tempo). Se as partículas computacionais realmente conhecerem suas posições com precisão, bons métodos estarão disponíveis para aproximar os operadores diferenciais à ordem superior, mesmo que os vizinhos não sejam relacionados por uma grade regular. Mas, a menos que sejam as fontes de medições físicas ou os controles dos atuadores físicos, não é realmente necessário que as posições assumidas das partículas sejam suas posições reais. De fato,

Mostraremos na próxima seção como é possível organizar partículas para escolher posições consistentes apropriadas para cálculos de alta precisão. No entanto, mesmo que as partículas não tenham informações sobre suas posições, ainda é possível calcular uma solução de baixa precisão para alguns PDEs, usando um processo amorfo que aproxima a localidade espacial da formulação do PDE com a comunicação local disponível para o PDE. partículas.

Um desses PDE é a equação de Laplace ![](https://trello-attachments.s3.amazonaws.com/5d7e8031eaec3e42c24aade0/5e3616fbd6040f4afd09841d/1175e74a17d5d14fb0beccdf62ef9057/img10.gif), cujas soluções são as funções harmônicas. Para qualquer solução da equação de Laplace, cada ponto interior é a média dos pontos ao seu redor. Em uma grade regular, produz um bom método de aproximação que pode ser relaxado para obter soluções precisas. No entanto, mesmo em uma grade aleatória, onde não há informações sobre a distância ou a direção de cada vizinho, nossas análises e simulações preliminares mostram que o processo de substituir o valor de cada ponto pela média dos vizinhos que se comunicam converge para uma aproximação a uma solução da equação de Laplace. Precisamos apenas configurar condições de contorno apropriadas para aproximar uma função harmônica designada.






## References ##

1. paper on sequencing of E-coli???
2. K. Eric Drexler, Chris Peterson, and Gayle Pergamit. 1991. Unbounding the future: the nanotechnology revolution. New York: Morrow.
3. Robert Fleischmann, et.al. 1995. Whole-Genome Random Sequencing and Assembly of Haemophilus influenzae Rd. Science, vol. 269 (July 28, 1995), pp. 496--512.
4. G. Halder, P. Callaerts, and W.J. Gehring. 1995. Induction of ectopic eyes by targeted expression of the eyeless gene in Drosophila. Science, vol. 267 (March 24, 1995), pp. 1788--92.
5. Robert Haralick and Linda Shapiro. 1992. Computer and Robot Vision. Reading, MA: Addison-Wesley.
6. S. Kondo and R. Asai. 1995. A reaction-diffusion wave on the skin of the marine angelfish Pomacanthus. Nature, vol. 376, (August 31, 1995), pp. 765--768.
7. John Pearson. 1993. Complex Patterns in a Simple System. Science, vol. 261, no. 189, (July 9, 1993), pp. 189--192.
8. Ilya Prigogine and Isabelle Stengers. 1984. Order out of chaos: man's new dialogue with nature. New York, NY: Bantam Books.
9. Charles Selvidge, Adam Malamy, and Lance Glasser. 1987. Power and communication techniques for physically isolated integrated circuits. Proceedings of the Stanford Conference on Advanced Research in VLSI, (May 1987), pp. 231--247.
10. Timothy Shepard. 1995. MIT Ph.D. thesis: Decentralized Channel Management in Scalable Multihop Spread-Spectrum Packet Radio Networks.
11. A.M. Turing. 1952. The Chemical Basis of Morphogenesis. Phil. Trans. Royal Society, vol. B237, pp. 37--72.







---

[Artigo Original](http://groups.csail.mit.edu/mac/projects/amorphous/white-paper/amorph-new/amorph-new.html)
