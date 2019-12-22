---
layout: post
title:  "Computação Neuromórfica"
date:   2019-12-13 17:59:38 -0200
categories: jekyll update
---

![](https://www.intel.com.br/content/dam/www/public/us/en/images/research/16x9/labs-article-neuromorphic-marquee-16x9.jpg.rendition.intel.web.480.270.jpg)

>Além da IA de hoje

>Novas abordagens algorítmicas simulam as interações do cérebro humano com o mundo.

## O que é computação neuromórfica

A primeira geração de IA foi baseada em regras e emulada lógica clássica para tirar conclusões fundamentadas dentro de um domínio de problema específico e definido de maneira restrita. Era adequado para monitorar processos e melhorar a eficiência, por exemplo. A segunda geração atual preocupa-se principalmente com a detecção e a percepção, como o uso de redes de aprendizado profundo para analisar o conteúdo de um quadro de vídeo.

A próxima geração estenderá a IA para áreas que correspondem à cognição humana, como interpretação e adaptação autônoma. Isso é fundamental para superar a chamada "fragilidade" das soluções de IA com base no treinamento e inferência de redes neurais, que dependem de visões determinísticas e literais de eventos que carecem de compreensão do contexto e do senso comum. A IA da próxima geração deve ser capaz de lidar com novas situações e abstrações para automatizar atividades humanas comuns.

O Intel Labs está conduzindo pesquisas em ciência da computação que contribuem para esta terceira geração de IA. As principais áreas de foco incluem a computação neuromórfica, que se preocupa em emular a estrutura neural e a operação do cérebro humano, bem como a computação probabilística, que cria abordagens algorítmicas para lidar com a incerteza, ambiguidade e contradição no mundo natural.

## Foco na pesquisa em computação neuromórfica

Os principais desafios da pesquisa neuromórfica estão combinando a flexibilidade de um ser humano e a capacidade de aprender com estímulos não estruturados com a eficiência energética do cérebro humano. Os blocos de construção computacionais nos sistemas de computação neuromórficos são logicamente análogos aos neurônios. As redes neurais de spiking (SNNs) são um novo modelo para organizar esses elementos para emular redes neurais naturais que existem nos cérebros biológicos.

Cada "neurônio" no SNN pode disparar independentemente dos outros e, ao fazê-lo, envia sinais pulsados ​​para outros neurônios da rede que alteram diretamente os estados elétricos desses neurônios. Ao codificar informações dentro dos próprios sinais e seu tempo, os SNNs simulam processos naturais de aprendizado, remapeando dinamicamente as sinapses entre neurônios artificiais em resposta a estímulos.

## Produzindo uma base de silício para computação inspirada no cérebro

Para fornecer sistemas funcionais para os pesquisadores implementarem SNNs, a Intel Labs projetou o Loihi, seu chip de teste de pesquisa neuromórfica de quinta geração e autoaprendizagem, que foi lançado em novembro de 2017. Esse design de 128 núcleos é baseado em uma arquitetura especializada que é otimizada para algoritmos SNN e fabricada na tecnologia de processo de 14nm. Loihi apoia a operação de SNNs que não precisam ser treinados da maneira convencional de uma rede neural convolucional, por exemplo. Essas redes também se tornam mais capazes (“mais inteligentes”) ao longo do tempo.

O chip Loihi inclui um total de cerca de 130.000 neurônios, cada um dos quais pode se comunicar com milhares de outros. Os desenvolvedores podem acessar e manipular recursos no chip programaticamente por meio de um mecanismo de aprendizado incorporado em cada um dos 128 núcleos. Como o hardware é otimizado especificamente para SNNs, ele suporta aprendizado dramaticamente acelerado em ambientes não estruturados para sistemas que exigem operação autônoma e aprendizado contínuo, com consumo de energia extremamente baixo, além de alto desempenho e capacidade.

O Intel Labs está comprometido em permitir à comunidade de pesquisa em geral o acesso a sistemas de teste baseados em Loihi. Como a tecnologia ainda está em fase de pesquisa (em oposição à produção), existe apenas um número limitado de sistemas de teste baseados em Loihi; Para expandir o acesso, o Intel Labs desenvolveu uma plataforma baseada em nuvem para o acesso da comunidade de pesquisa à infraestrutura escalável baseada em Loihi.


![](https://www.intel.com.br/content/dam/www/public/us/en/images/research/16x9/neuromorphic-chip-loihi-2-16x9.png.rendition.intel.web.1648.927.png)

>O chip de pesquisa neuromórfica de auto-aprendizagem da Intel Corporation, codinome "Loihi". (Crédito: Intel Corporation)

## Avançando na computação neuromórfica como um desafio

interdisciplinar A computação neuromórfica se desenvolve no cruzamento de diversas disciplinas de pesquisa, incluindo neurociência computacional, aprendizado de máquina, microeletrônica e arquitetura de computadores, entre outros. O Intel Labs estabeleceu a Comunidade de pesquisa neuromórfica da Intel , um esforço de pesquisa colaborativo que reúne entidades acadêmicas, governamentais e do setor para trabalhar em arquiteturas, ferramentas e abordagens complementares que permitem a computação neuromórfica como um todo.

A comunidade trabalha para abstrair os princípios da neurociência e adaptá-los à tecnologia computacional prática. Por exemplo, a produção de algoritmos SNN mais avançados é uma área de foco principal, incluindo o desenvolvimento de modelos e ferramentas de programação. Em particular, ele conduz a experimentação e desenvolvimento com o chip de pesquisa Loihi, incluindo aplicativos para resolver problemas e mecanismos do mundo real para fazer a interface de sistemas baseados em SNNs com dados externos e sistemas de computação.

Os membros da comunidade concordam com uma abordagem aberta e colaborativa, na qual compartilharão os resultados de suas pesquisas. O Intel Labs facilita alguns esforços de pesquisa na comunidade por meio de financiamento e acesso aos sistemas de desenvolvimento Loihi.

## Foco de pesquisa em computação probabilística

A incerteza e o ruído fundamentais que são modulados em dados naturais são um desafio fundamental para o avanço da IA. Os algoritmos devem tornar-se hábeis em tarefas baseadas em dados naturais, que os humanos gerenciam intuitivamente, mas os sistemas de computadores têm dificuldade.

Ter a capacidade de entender e calcular com incertezas permitirá aplicativos inteligentes em diversos domínios da IA. Por exemplo, em imagens médicas, com base nas medidas de incerteza, é possível priorizar quais imagens um radiologista precisa olhar e mostrar nas regiões de imagem destacadas com baixa incerteza. No caso de assistente inteligente em casa, um agente pode interagir com o usuário fazendo perguntas esclarecedoras para entender melhor uma solicitação quando houver uma alta incerteza no reconhecimento de intenção.
No domínio de veículos autônomos, os sistemas que pilotam carros autônomos têm muitas tarefas que são adequadas à computação convencional, como navegar por uma rota GPS e controlar a velocidade. O estado atual da IA permite que os sistemas reconheçam e respondam às suas vizinhanças, como evitar colisões com pedestres inesperados.

Para avançar esses recursos no campo da direção totalmente autônoma, os algoritmos devem incorporar o tipo de conhecimento que os humanos desenvolvem como condutores experientes. Os sensores, como GPS, câmeras, etc. exibem incerteza em suas estimativas de posição. Além disso, a bola com a qual as crianças brincam em um quintal próximo pode rolar para a rua e uma das crianças pode decidir persegui-la. É prudente ter cuidado com um motorista agressivo na próxima pista. Nesses ciclos de percepção e resposta, tanto as entradas quanto as saídas carregam um grau de incerteza. A tomada de decisão em tais cenários depende da percepção e compreensão do ambiente para prever eventos futuros, a fim de decidir sobre o curso de ação correto. As tarefas de percepção e compreensão precisam estar cientes da incerteza inerente a essas tarefas.

## Gerenciamento e modelagem da incerteza A

computação probabilística geralmente aborda problemas de lidar com a incerteza, que é inerentemente incorporada aos dados naturais. Existem duas maneiras principais pelas quais a incerteza desempenha um papel nos sistemas de IA:

- Incerteza na percepção e reconhecimento de dados naturais. As fontes contribuintes incluem incerteza de entrada resultante de sensores e ambiente de hardware, bem como a incerteza do modelo de reconhecimento devido à disparidade nos dados de treinamento e nos dados que estão sendo reconhecidos.
- Incerteza ao subestimar e prever eventos dinâmicos. O movimento humano e a previsão de intenção são um exemplo em que essa incerteza é exibida. Qualquer agente que tente prever tais eventos dinâmicos precisa modelar a intenção humana e entender as incertezas no modelo. As observações podem ser usadas para reduzir continuamente as incertezas para uma previsão eficiente de intenção e objetivo.

Os principais problemas nessa área giram em torno da caracterização e quantificação eficientes da incerteza, incorporando essa incerteza em cálculos e resultados e armazenando um modelo das incertezas que interagem com os dados correspondentes.

Uma implicação do fato de que os resultados são expressos como probabilidades, em vez de valores determinísticos, é que todas as conclusões são experimentais e associadas a graus específicos de confiança. Para estender o exemplo de direção autônoma acima, a bola das crianças desaparecendo de vista ou um comportamento cada vez mais irregular do motorista agressivo pode aumentar a confiança de que esse risco potencial exigirá uma resposta.

Além de permitir a intuição e a previsão na IA, métodos probabilísticos também podem ser usados ​​para conferir um certo grau de transparência aos sistemas de reconhecimento de IA existentes que tendem a operar como uma caixa preta. Por exemplo, os mecanismos atuais de Deep Learning produzem um resultado sem uma certa incerteza. Os métodos probabilísticos podem aumentar esses mecanismos para gerar uma estimativa de incerteza baseada em princípios juntamente com o resultado, possibilitando que um aplicativo decida a confiabilidade da previsão. Tornar a incerteza visível ajuda a estabelecer confiança na confiança do sistema de IA na tomada de decisões.

Enquanto os processos determinísticos têm resultados previsíveis e repetíveis, os probabilísticos não, devido a influências aleatórias que não podem ser conhecidas ou medidas. Esse processo de incorporação de ruídos, incertezas e contradições de dados naturais é um aspecto vital da construção de computadores capazes de níveis humanos (ou super-humanos) de entendimento, previsão e tomada de decisão. Este trabalho baseia-se em aplicações anteriores de aleatoriedade na análise de dados, como o uso bem estabelecido de algoritmos de Monte Carlo para modelar probabilidade.


## Habilitando um ecossistema probabilístico de computação

Além de seu principal objetivo - lidar com dados incompletos e incertos - a computação probabilística depende do seu sucesso em ser integrada de forma colaborativa e holística ao universo mais amplo da tecnologia de computação. O Intel Labs está ajudando a construir as pontes necessárias entre entidades da academia e da indústria por meio da Aliança de pesquisa estratégica da Intel para computação probabilística.

Esta iniciativa de pesquisa é dedicada ao avanço da computação probabilística do laboratório para a realidade, integrando probabilidade e aleatoriedade em componentes fundamentais de hardware e software. Reunindo e possibilitando a pesquisa nessas áreas, a Aliança trabalha para projetar as capacidades de percepção e julgamento para permitir a próxima geração de IA.

# PESQUISA 

>Loihi: Um processador Manyom Neuromorphic com aprendizado no chip

>O chip Loihi integra uma ampla gama de novos recursos para o campo - incluindo regras de aprendizado sináptico programáveis.

[Leia o paper](https://ieeexplore.ieee.org/document/8259423)

---

[Original](https://www.intel.com.br/content/www/br/pt/research/neuromorphic-computing.html)
