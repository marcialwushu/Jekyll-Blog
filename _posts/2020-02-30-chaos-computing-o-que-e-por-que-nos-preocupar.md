---
layout: post
title:  "Chaos Computing: O que é e por que devemos nos preocupar com isso?"
date:   2020-02-30 17:59:38 -0200
categories: jekyll update
---

A operação de qualquer máquina de computação é necessariamente um processo físico, e isso determina crucialmente as possibilidades e limitações do dispositivo de computação. Nos últimos 20 anos, a taxa de transferência de computadores digitais aumentou a uma taxa exponencial. Alimentado por melhorias na tecnologia de circuitos integrados, o crescimento exponencial previsto pela lei de Moore se manteve verdadeiro. Mas a Lei de Moore chegará ao fim quando os fabricantes de chips atingirem uma parede quando se trata de diminuir o tamanho dos transistores. Como a tecnologia convencional de fabricação de chips atinge limites físicos na densidade de circuitos e velocidade do sinal, que estabelece limites para o escalonamento de comutadores lógicos binários, estão surgindo alternativas aos computadores digitais binários baseados em semicondutores. Além do VLSI analógico, eles incluem bio-chips, que são baseados em materiais encontrados em seres vivos,

![](https://miro.medium.com/max/700/1*by2Cekav1qkSbwj5Y8ZdXQ.png)

>Teoria do caos

Existe também outro paradigma de computação emergente, que explora a riqueza e a complexidade inerentes à dinâmica não linear, chamada computação do caos. A computação em caos é a idéia de usar sistemas caóticos para computação. Em particular, sistemas caóticos podem ser criados para produzir todos os tipos de portas lógicas e permitir que eles se transformem um no outro. Este artigo analisa mais profundamente essa tecnologia e explora suas possíveis aplicações na tecnologia de computação convencional.

## O que é um sistema caótico?

Dinâmica é o estudo de como as coisas mudam com o tempo. Em seus termos mais simples, a dinâmica pode ser caracterizada por dois comportamentos: regular e irregular. Comportamentos regulares incluem relógios, estações do ano, metrônomos e assim por diante. Comportamentos irregulares incluem clima, bolsas de valores, jogos de cassino e assim por diante. No entanto, enquanto o comportamento regular repete um único padrão ou vários padrões de maneira previsível e imutável, comportamentos irregulares (geralmente atribuíveis a efeitos não lineares, portanto, o nome dinâmica não linear) são muito mais variados e incluem dois extremos: dinâmica aleatória e dinâmica caótica.

Dinâmica regular (ou periódica) As mudanças no comportamento dependem do estado anterior, o movimento se repete de maneira rigidamente previsível. Exemplos: estações, relógios, eletrônica linear, órbita da Terra,…

Dinâmica Irregular (ou Aperiódica)

Aleatório: a próxima mudança no comportamento ou dinâmica não depende do estado atual da dinâmica. As mudanças são completamente imprevisíveis. Exemplos: sequência de sorteio, roleta,…

Caótico: a próxima mudança na dinâmica tem uma dependência determinística do estado atual da dinâmica. As alterações, embora irregulares, se movem regularmente e irregularmente entre muitos padrões. Exemplos: torneiras de água pingando, padrões climáticos, populações de predadores-presas, eletrônicos não lineares, órbita de Plutão,…
Agora, concentrando-nos em sistemas caóticos, podemos essencialmente resumir-se a duas características essenciais:

Geração de padrões : Os sistemas caóticos geram um grande número de padrões de comportamento e são irregulares porque alternam entre esses padrões.

Sensibilidade às condições iniciais : Os sistemas caóticos exibem "sensibilidade às condições iniciais", o que, na prática, significa que os sistemas caóticos podem alternar entre padrões extremamente rápido.

## Portas lógicas

Todos os computadores digitais modernos realizam cálculos baseados em operações lógicas digitais implementadas no nível mais baixo como portas lógicas, o que significa essencialmente que todos os cálculos podem ser realizados por sequências de uns e zeros. Todos os cálculos em computadores digitais, tão simples quanto adicionar dois números e tão complicado quanto reformatar um documento de processamento de texto, são realizados em hardware com combinações desses portões que executam funções lógicas. Existem essencialmente sete funções lógicas básicas implementadas como portas lógicas: AND, OR, NOT, NAND, NOR, XOR e XNOR, conforme mostrado abaixo, com ícones de circuitos associados que representam o circuito que implementa a função lógica.

## Princípio das portas lógicas caóticas que se transformam

As portas lógicas, baseadas no padrão elétrico de entrada de uns e zeros, produzem um padrão elétrico de saída de uns ou zeros que corresponde à sua respectiva operação lógica (ou tabela de verdade). Cada porta lógica convencional consiste em um circuito dedicado que produz a saída lógica adequada. Uma porta lógica de transformação caótica, a partir de agora ChaoGate, consiste principalmente em um circuito não-linear genérico que exibe dinâmica caótica. Essa dinâmica caótica é capaz de gerar muitos padrões diferentes. Exploramos esse recurso e selecionamos, através de um mecanismo de controle, padrões que correspondem a todos os portões lógicos. Exploramos ainda mais a sensibilidade às condições iniciais para alternar entre diferentes padrões de maneira extremamente rápida (bem abaixo de um ciclo de clock do computador). Na prática, para criar um candidato ChaoGate, construímos um ambiente otimizado (potência, tamanho, velocidade, estabilidade) circuito eletrônico caótico com circuitos de controle interno associados que podem selecionar qualquer porta lógica e alternar entre quaisquer portas lógicas exponencialmente rápidas. Assim, com um único ChaoGate, podemos reproduzir rapidamente qualquer porta lógica desejada no hardware a cada ciclo do relógio.





