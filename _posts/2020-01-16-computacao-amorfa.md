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


## Exemplo: Usando soluções PDE aproximadas para organizar sistemas amorfos ##

Deveríamos ser capazes de usar as soluções aproximadas da equação de Laplace para fornecer um processo de autoinicialização para organizar a geometria de um sistema de computação amorfo, mesmo que não tenhamos conhecimento a priori das posições ou orientações reais dos vizinhos que estão se comunicando, além da suposição de local. comunicação.

Em particular, podemos resolver a equação de Laplace em um patch para obter soluções que são funções de coordenadas ortogonais localmente, especificando condições de contorno apropriadas. Essas soluções podem ser usadas para atribuir coordenadas virtuais às partículas computacionais no patch. Essas coordenadas virtuais são automaticamente consistentes e, portanto, podem ser usadas como uma grade para outras operações matemáticas. Por exemplo, poderíamos usar essas soluções para construir aproximações precisas para operadores diferenciais, permitindo assim começar com uma grade aleatória e obter respostas precisas para os PDEs. Dados os sistemas de coordenadas em cada patch, podemos costurar os patches com patches sobrepostos e, assim, criar soluções globais.

Assim, podemos usar métodos brutos para resolver equações diferenciais parciais para estabelecer um sistema de coordenadas para partículas computacionais, e podemos iterar esse processo para obter um sistema de coordenadas tão bom quanto desejamos. Atualmente, estamos investigando (em simulação) como pode ser possível ajustar dinamicamente as posições simuladas (ou físicas!) Dos processadores para otimizar o erro acumulado no processo de solução.

Este exemplo destaca um ponto geral importante: Na computação amorfa, somos forçados a desenvolver técnicas computacionais que são apenas ligeiramente dependentes da disposição e interconexão do processador físico. Essa restrição serve como uma alavanca intelectual para o desenvolvimento de novos algoritmos para resolver problemas difíceis. Por exemplo, como somos forçados a estabelecer e refinar nossos sistemas de coordenadas com base nos resultados da computação, temos uma base natural para executar multigridding dinâmico, uma técnica que pode ser usada para atacar uma grande classe de problemas atualmente intratáveis em física e engenharia .


## Processos morfológicos e sistemas de reação-difusão ##

Turing sugeriu que os mecanismos de morfogênese podem ser explicados por equações de reação-difusão (ver [ 11 ]). Estes são sistemas de equações diferenciais parciais da forma

![](https://trello-attachments.s3.amazonaws.com/5d7e8031eaec3e42c24aade0/5e3616fbd6040f4afd09841d/881b7a74539fbe63a52d5d44271fa4c9/img11.gif)

onde o valor do vetor ![](https://trello-attachments.s3.amazonaws.com/5d7e8031eaec3e42c24aade0/5e3616fbd6040f4afd09841d/75f52dee95af6c6546950401e0730bae/img12.gif) em cada momento t descreve as alterações nas concentrações espaciais de um conjunto de substâncias químicas chamadas **morfogênios**. Os padrões de Turing resultantes para várias especificações de reação ![](https://trello-attachments.s3.amazonaws.com/5d7e8031eaec3e42c24aade0/5e3616fbd6040f4afd09841d/bce53b8915634ce34546846a6294199b/img13.gif) foram amplamente simulados e mostraram produzir padrões regulares que lembram listras de zebra e manchas de leopardo. Quer os mecanismos de difusão da reação sejam ou não os fenômenos reais em tais sistemas biológicos, a gif simulação de tais sistemas tende a gerar padrões regulares que aparecem como soluções de ondas estacionárias para as equações.

Curiosamente, os padrões de Turing resultantes são frequentemente independentes do estado inicial do sistema. Partir de uma configuração aleatória e evoluir a equação resulta em padrões regulares nas concentrações dos morfogênios. A Figura 2 mostra um desses conjuntos de padrões, obtidos a partir de uma distribuição inicial aleatória em um sistema que evolui de acordo com um sistema de equações de reação-difusão chamado modelo de Gray-Scott . Criamos um ambiente de simulação para explorar esses tipos de modelos de reação. A Figura 2 mostra um resultado de amostra.

>O modelo de Gray-Scott descreve a evolução das concentrações de dois morfógenos de acordo com o sistema de equações não lineares:
14 # 14

>Simulações deste sistema são descritas por Pearson [ 7 ]. Os resultados dessas simulações (realizados por R. Williams na Caltech) podem ser vistos na Internet em www.ccsf.caltech.edu/ismap/image.html . A simulação mostrada na figura 2 é semelhante a algumas feitas por Pearson e Williams, exceto pelo fato de começarmos com uma distribuição aleatória de 15 # 15 e 16 # 16, não impor condições de contorno periódicas e usar um empacotamento aleatório de partículas computacionais em vez de uma grade regular.



![](https://trello-attachments.s3.amazonaws.com/5d7e8031eaec3e42c24aade0/5e3616fbd6040f4afd09841d/a83c95a3eac1a4775937a5c61432ab5a/img33.gif)


**Figura 2**: Simulação do modelo de Gray-Scott iniciando a partir de uma configuração inicial aleatória (esquerda) e evoluindo para pontos regulares após 20.000 etapas de tempo (direita). Há 2500 partículas empacotadas aleatoriamente em um quadrado de tamanho 1, começando com valores de ![](https://trello-attachments.s3.amazonaws.com/5d7e8031eaec3e42c24aade0/5e3616fbd6040f4afd09841d/041f01cf3c42c0189b34d757157a91c7/img25.gif) e ![](https://trello-attachments.s3.amazonaws.com/5d7e8031eaec3e42c24aade0/5e3616fbd6040f4afd09841d/739bc84dadaef20b79924da4964e2176/img26.gif) morfogênios designados aleatoriamente entre 0 e 1. Os vizinhos de cada partícula são aqueles a uma distância de 0,05 dela. As constantes para o modelo *Gray-Scott* aqui estão ![](https://trello-attachments.s3.amazonaws.com/5d7e8031eaec3e42c24aade0/5e3616fbd6040f4afd09841d/983795f354f49027850f7fc8e3e51097/img27.gif), ![](https://trello-attachments.s3.amazonaws.com/5d7e8031eaec3e42c24aade0/5e3616fbd6040f4afd09841d/1be606d83e3bd1bc5fa2203be0c3ee45/img28.gif), ![](https://trello-attachments.s3.amazonaws.com/5d7e8031eaec3e42c24aade0/5e3616fbd6040f4afd09841d/abcd10cb5b3addd24c92a46f5af75373/img29.gif), ![](https://trello-attachments.s3.amazonaws.com/5d7e8031eaec3e42c24aade0/5e3616fbd6040f4afd09841d/25f84dd14da20cd007a37cc8b05fc56e/img30.gif) , e integração é realizada utilizando o método forward-Euler com ![](https://trello-attachments.s3.amazonaws.com/5d7e8031eaec3e42c24aade0/5e3616fbd6040f4afd09841d/ef6c40b9e654efbced9f6eb3db227cd4/img31.gif). As diferentes cores das partículas indicam valores diferentes de ![](https://trello-attachments.s3.amazonaws.com/5d7e8031eaec3e42c24aade0/5e3616fbd6040f4afd09841d/3107e69ede406f2d7b2f7a032f2b06a3/img32.gif).

Isso sugere a possibilidade intrigante de organizar sistemas de computação amorfos começando com as partículas em um estado aleatório e resolvendo um análogo discreto de um sistema de difusão de reação. As bolhas espaçadas regularmente resultantes de partículas poderiam então servir como centros organizadores para os estágios subseqüentes da computação.


## Introdução: Hardware ##

Há uma série de possíveis realizações físicas para as partículas de um mecanismo de computação amorfo. Uma possibilidade atraente é uma *partícula de processador sem pinos* (PPP), que não requer interconexão física, porque extrai energia de seu ambiente e se comunica com seus vizinhos sem conexões físicas. Construir uma PPP parece possível em princípio, mas na prática é difícil usar processos fáceis de obter.

Uma abordagem menos agressiva, que seria suficiente para experimentos de curto prazo, é produzir uma *partícula de processador explicitamente alimentada* (EPPP). Isso possui conexões explícitas à fonte de alimentação, mas nenhuma conexão de comunicação explícita. Esperamos que possamos fabricar um EPPP que dependa da tecnologia atualmente acessível em alguns milímetros quadrados de silício.

## Poder ##

O principal desafio da tecnologia sem pinos é como fornecer energia aos elementos computacionais. Examinamos várias abordagens alternativas, incluindo fotodiodos, transdutores acústicos, microondas, acoplamento magnético e métodos químicos. Cada uma delas gera dificuldades, mas as dificuldades parecem ser técnicas e não fundamentais.

Para obter tensão suficiente para acionar uma PPP com fotodiodos, precisamos colocar vários diodos em série. Nos processos CMOS em massa, isso cria transistores parasitas que reduzem a fonte de alimentação. Outro problema com os fotodiodos é que, mesmo sob a luz do sol, a potência máxima obtida é de 1 kW/m ou 1 mW/mm . Aplicativos exigentes computacionalmente, no entanto, exigem mais do que alguns miliwatts. Pode ser possível usar a luz como fonte de energia para uma PPP fabricada com processamento SOI (silício sobre isolador) ou com módulos multichip.

Com transdutores acústicos, como cristais piezoelétricos, há diferenças de impedância significativas tanto no ambiente mecânico (o material é muito rígido) quanto nos requisitos elétricos (a voltagem é muito alta). As microondas podem funcionar, mas isso exigiria um ambiente com altos níveis de radiação de microondas no ambiente. Malamy, Glasser e Selvidge [ 9 ] experimentaram a indução magnética como um método para energia sem fio e comunicação para chips. Eles demonstraram com sucesso como fornecer energia usando ímãs fortes e peças de pólos que estavam intimamente acopladas a chips individuais. Isso não parece viável para um sistema grande, no entanto.

Métodos químicos fornecem densidade de energia suficiente. Se o sistema precisar funcionar apenas por um curto período de tempo, seria possível acumular baterias nas partículas. Também é possível, mas além do estado atual da arte, construir sistemas semelhantes a células de combustível que combinam hidrogênio e oxigênio para formar água. Esse PPP teria uma vida útil prolongada.

Em resumo, esperamos que o desafio da distribuição de energia seja atendido por uma ou mais tecnologias emergentes. No entanto, como nossa pesquisa se concentra na organização da computação, achamos que atualmente é mais produtivo evitar esse problema e usar a distribuição explícita de energia.

## Comunicação ##

A comunicação é um problema mais fácil. Uma idéia que pode ser feita para funcionar é o acoplamento eletroquasistático, em que cada partícula tem um eletrodo de antena que é capacitivamente acoplado a eletrodos de antena semelhantes nas partículas vizinhas.

Fizemos um estudo preliminar de um sistema usando uma antena construída na camada metal-2 em um processo CMOS e descobrimos que isso não funciona bem. A antena foi protegida no metal-1 para diminuir o efeito da capacitância do eletrodo da antena para o substrato. O eletrodo de proteção foi acionado por um amplificador operacional CMOS. Fizemos um layout preliminar desse esquema e o simulamos com o SPICE. Também construímos um modelo em escala para facilitar a investigação dos campos marginais. Supondo que os elementos computacionais estivessem dispostos em uma superfície com espaçamento semelhante ao tamanho dos elementos, poderíamos obter acoplamentos capacitivos entre antenas adjacentes da ordem de alguns centésimos de um picofarad. O eletrodo de proteção tinha uma capacitância para o substrato de algumas centenas de picofarads. O amplificador operacional teve que carregar essa capacitância bastante grande.

Podemos obter um desempenho muito melhor se relaxarmos a restrição de que a antena é plana, construída no processo CMOS. Por exemplo, pode-se desdobrar a antena para fora do chip. Uma implementação semelhante, mas talvez mais fácil, é remover o substrato de silício sob a estrutura da antena para reduzir a capacitância parasitária. Ainda mais simples, pode-se ligar um fio de antena a cada partícula. Com esse tipo de acoplamento e com boas fontes de energia, podemos esperar atingir velocidades de comunicação entre partículas vizinhas na faixa de dezenas de megabaud.

Pode-se imaginar o uso de esquemas de comunicação por rádio que não dependem da capacitância de acoplamento entre as antenas de transmissão e recepção. No entanto, para que esse esquema funcione, precisamos executar em frequências muito mais altas. Além disso, os esquemas de comunicação baseados no rádio não são muito locais, levando a sérios problemas de interferência, a menos que esquemas complexos para compartilhamento de canais, como grandes antenas direcionais ou espectro espalhado, sejam usados (veja [ 10 ] para mais informações sobre essa idéia).

## O que podemos construir agora ##

Enquanto esses problemas técnicos estão se resolvendo, podemos obter agora experiência com computação amorfa construindo uma partícula de processador de potência explícita (EPPP) que se comunica com vizinhos próximos por meio de acoplamento capacitivo. Cada partícula teria alguns milímetros quadrados de silício com um fio de antena com cerca de um centímetro de comprimento.


![](https://trello-attachments.s3.amazonaws.com/5d7e8031eaec3e42c24aade0/5e3616fbd6040f4afd09841d/06992ef05f7774dca799e578d10e327c/img36.gif)

**Figura 3**: Duas idéias possíveis para o design de uma partícula de processador explicitamente acionada (EPPP) destinada a ser plantada em um elastômero de múltiplas camadas. As partículas podem se comunicar usando acoplamento capacitivo para vizinhos próximos através de uma curta antena ligada a um bloco. Como alternativa, poderíamos tentar um elastômero de cinco camadas com partículas se comunicando através da detecção de tensões e injeção de correntes em uma camada condutora. Em qualquer um dos casos, o final do EPPP com sensores se sobressai do elastômero. Embora esses diagramas não estejam em escala, esperamos que a montagem do EPPP seja da ordem de 1 cm de comprimento.

![](https://trello-attachments.s3.amazonaws.com/5d7e8031eaec3e42c24aade0/5e3616fbd6040f4afd09841d/08ac1df8d41efa8e87860435c22ed0a5/img37.gif)

**Figura 4**: Usando um elastômero de três camadas com duas camadas condutoras, é possível fazer um gramado de elementos de computação. A energia é fornecida às pastilhas dos EPPPs por contato com as camadas condutoras do elastômero. Se os tamanhos forem escolhidos adequadamente, a inserção dos EPPPs poderá ser feita com pouca precisão: talvez eles possam ser disparados no elastômero com uma pistola de ar repetida.

Poderíamos fabricar uma placa com as partículas do processador dispostas em um padrão predefinido. Uma abordagem mais amorfa seria distribuir energia com um elastômero de três camadas com camadas externas condutoras separadas por um isolador. Cada processador teria pinos de comprimentos adequados para fazer contato quando o dispositivo é plantado no elastômero. É até possível colocar as almofadas em locais apropriados em um chip longo e fino (veja a figura 3) para que os eletrodos entrem em contato com as camadas condutoras do elastômero, se o próprio chip for plantado no elastômero. (Nem sequer é necessário obter o alinhamento dos blocos de potência na polaridade correta do elastômero, porque nosso projeto preliminar mostra que é fácil fazer um conjunto de retificador de ponte que fornecerá a energia correta aos circuitos, independentemente da polaridade. das pastilhas.) Poderíamos providenciar para que existissem sensores na parte das partículas que se projetam do elastômero. A idéia mais fácil parece ser tentar fotodiodos ou sensores de temperatura. As partículas podem então ser plantadas juntas para formar um gramado de elementos de computação (veja a figura 4 ).

Para a memória, parece melhor usar a RAM estática, pois no CMOS isso requer menos energia que a DRAM, mesmo que as células sejam maiores. Podemos esperar obter cerca de 20K bits por milímetro quadrado, o que resultaria em algo como 32K bytes por partícula.

Essa pequena quantidade de memória por partícula sugere o uso de um conjunto de instruções com alta densidade de código ou a interpretação de um conjunto de instruções de alta densidade. Implementamos uma arquitetura de pilha e máquina projetada para atender a esses requisitos. Implementamos um simulador em nível de instrução para essa arquitetura e estamos usando-o para desenvolver componentes básicos do sistema, como protocolos de comunicação e aritmética de ponto flutuante.

Como o design do nosso protótipo não é limitado em termos de energia, podemos executá-lo a uma velocidade superior a 100 MHz. Devido a limitações de espaço, não planejamos incluir hardware de ponto flutuante, portanto, visualizamos um desempenho de ponto flutuante de 8 a 10 MFLOPS por partícula. É importante ressaltar que cada processador inclui um gerador de números aleatórios (não pseudo-aleatórios), pois a capacidade de escolher números diferentes para os diferentes processadores é fundamental para os algoritmos que imaginamos.

A comunicação entre partículas de baixa latência e baixa sobrecarga de software será fundamental para o desempenho do sistema. Pretendemos incorporar suporte especial de hardware e software para tornar essa comunicação eficiente e fácil de programar. Esse suporte incluirá mecanismos acionados por interrupção, acesso direto à memória do canal de comunicação, suporte para agendamento eficiente de tráfego e suporte de hardware para detecção e correção automáticas de erros. Para aplicações de baixo consumo de energia, o suporte eficiente das comunicações é ainda mais crítico, pois precisamos desligar os circuitos analógicos que necessitam de energia dos receptores quando eles não estão em uso. A comunicação eficiente pode exigir sincronização precisa das comunicações. Isso pode exigir boas bases de tempo ou técnicas de bloqueio de fase. [ 10 ]

Para permitir a comunicação com um host, planejamos fabricar uma almofada adicional em cada partícula, que será conectada apenas a algumas partículas da coleção.


## Demonstrações iniciais ##

A computação amorfa certamente precipitará aplicações surpreendentes em materiais distribuídos e ativos. A realização dessas aplicações também exigirá mais progresso na fabricação de microssensores e microativadores. Nosso plano atual, no entanto, é escolher aplicativos iniciais que se concentrem em questões computacionais e não dependam dos desenvolvimentos em andamento em sistemas elétrico-micromecânicos.

Uma área que planejamos explorar é resolver equações diferenciais parciais. Como descrito acima, grandes coleções de partículas de computação amorfas podem ser plataformas eficazes para técnicas de grade adaptativa. No mínimo, devemos ser capazes de lidar efetivamente com a equação de Laplace, que é interessante por si só, e fornece a base para explorar algumas das idéias mais especulativas descritas acima, como organizar sistemas resolvendo equações de reação-difusão.

Também é importante, no entanto, explorar uma aplicação na qual as partículas interagem diretamente com o mundo físico. Aqui esperamos escolher uma aplicação puramente sensível, para evitar a necessidade de lidar com atuadores de baixa potência. Uma aplicação plausível seria incluir um fotosensor em cada partícula e programar um gramado de partículas para reconhecer e interpretar as sombras que passam por ela.

## Implicações desta pesquisa ##

É claro que a integração de um grande número de elementos computacionais e de comunicação inexpenientes, sensores e atuadores pode revolucionar o design de sistemas físicos. O plano de pesquisa descrito aqui produzirá três classes de resultados essenciais para a realização desse potencial.

1. *Significa reunir e coordenar agentes de computação a preços comparáveis aos custos de matéria-prima*. Há muito que se reconhece que o fator limitante é o custo da interconexão e cooperação, e não a complexidade dos elementos individuais. A computação amorfa propõe eliminar completamente a necessidade de interconexão de precisão, em favor de uma nova abordagem para organizar programas e processos.
2. *Mecanismos para incorporar sensoriamento, computação e atuação em materiais de engenharia comuns*. Tintas inteligentes e peles inteligentes admitem uma grande classe de aplicativos que parecem acessíveis.
3. *Tecnologia de programação necessária para orquestrar as atividades de um grande número de entidades programáveis*. Destilaremos princípios organizadores que nos permitirão desenvolver software que direcione a construção de estruturas específicas. Para criar um sistema tridimensional compactado, por exemplo, teremos que ter um software que organize as peças em estruturas de distribuição de energia e remoção de calor, bem como em caminhos de comunicação. Como o programa de DNA para uma célula de folha de bordo constrói o padrão de veias? Podemos usar essa idéia para construir máquinas melhores?



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
