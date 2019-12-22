---
layout: post
title:  "Práticas recomendadas para conformidade com DO-178C"
date:   2019-12-12 17:59:38 -0200
categories: jekyll update
---

![](https://www.perforce.com/sites/default/files/image/2018-07/image-blog-do-178c-compliance.jpg)

Todo mundo que embarca em um avião assume que ele permanecerá no ar durante toda a jornada. O motivo? Os veículos aéreos - seja uma companhia aérea comercial ou um jato militar - precisam cumprir os padrões funcionais de segurança.

É por isso que a conformidade com DO-178C para cada nível de segurança do software é tão crítica. Ele protege os passageiros e a tripulação a bordo - assim como os desenvolvedores do hardware e software da aeronave.

Mas alcançar a conformidade pode ser um desafio.

## O que é o DO-178C?

O Considerações sobre o software DO-178C na certificação de sistemas e equipamentos transportados por via aérea é um padrão usado nas indústrias aeroespacial e militar / de defesa. É uma atualização para o DO-178B.

A conformidade com este padrão é necessária para receber a certificação de dignidade de voo. Sem ele, você (literalmente) não vai tirar o avião do chão.


## Níveis de segurança de software

O DO-178C classifica a segurança em cinco níveis. Cada nível corresponde à conseqüência se o software falhar.

- Nível A: Catastrófico
- Nível B: Perigoso
- Nível C: Maior
- Nível D: Menor
- Nível E: sem efeito de segurança

Esses níveis de segurança do software são designados com base no risco. E quanto maior o risco, mais objetivos de segurança precisam ser alcançados. (E mais difícil será provar a conformidade.)

Os níveis A a C são os mais graves. As falhas de software do nível A podem resultar em fatalidades devido a um acidente de avião. Falhas no software do nível B podem resultar em ferimentos nos passageiros. Falhas no software de nível C podem causar desconforto ao passageiro.

Os níveis D e E são muito mais pequenos. As falhas no software do nível D causam transtornos aos passageiros, como atrasos nos voos. E as falhas de software de nível E não têm impacto na segurança.

## Como obter conformidade com DO-178C no desenvolvimento

É importante alcançar a conformidade com o DO-178C. E isso precisa ser feito em todos os aspectos do  desenvolvimento.

#### Planejamento

O planejamento é crítico. Você precisa planejar o que vai entregar ao mercado e quando - e como será compatível com seus processos.

Isso significa que você precisa reunir requisitos. E você precisa garantir que esses requisitos sejam responsáveis ​​pelo padrão.

Você pode gerenciar esses requisitos de várias maneiras. O documento de requisitos pode estar no Microsoft Word. Ou pode estar em uma sofisticada ferramenta de gerenciamento de requisitos .

Seu plano também deve incluir garantia de qualidade. Como você garantirá que seu código seja compatível? E como você provará que testou e verificou que esses requisitos foram atendidos?

Se você estiver usando um processo do Agile ALM , provavelmente definirá requisitos com casos de teste em mente. Isso facilita a garantia de qualidade.

#### Desenvolvimento

O DO-178C deve ser lembrado durante os processos de desenvolvimento.

Isso significa:

- Os requisitos devem ser claramente definidos.
- Os casos de teste devem ser desenvolvidos a partir dos requisitos.
- O código deve ser escrito para atender a esses requisitos.
- Os testes devem satisfazer os casos de teste e mostrar que os requisitos foram atendidos.
- A rastreabilidade deve vincular todos os itens.

#### Verificação

Os processos de verificação o ajudarão a provar que você atendeu aos requisitos de conformidade.

Há três coisas importantes que você precisará verificar:

- Exigências
- Código
- Testes

Portanto, você precisa confirmar se o código atende aos seus requisitos - conformidade ou não. Isso pode ser alcançado através da criação de uma matriz de rastreabilidade. Em seguida, você poderá mostrar os links entre requisitos, código e testes - e provar que os requisitos foram atendidos.

 

[Conteúdo relacionado: Como criar uma matriz de rastreabilidade](https://www.perforce.com/blog/alm/how-create-traceability-matrix)
 

Você também precisa garantir que o código esteja em conformidade com um padrão de codificação . Isso pode ser alcançado através de análises de código ou usando uma ferramenta de análise estática .

 

[Conteúdo relacionado: Introdução aos padrões de codificação]
 

E você precisa verificar seus testes e sua cobertura. Uma maneira de fazer isso é criando testes a partir de um caso de teste. Dessa forma, você confirmará que testou as coisas certas - especialmente o requisito para o qual o caso de teste foi escrito.

Considerações sobre a qualificação da ferramenta de software DO-330
A qualificação da ferramenta faz parte de muitos padrões de conformidade. Para o DO-178C, existe um padrão suplementar que faz isso - o DO-330.

O DO-330 é um padrão de requisitos de qualificação de ferramenta. Foi criado para o DO-178C, mas pode ser usado fora das indústrias aéreas.

Portanto, o DO-330 é um componente importante da conformidade. E o uso de ferramentas já qualificadas facilita esse processo.

O que procurar nas ferramentas de desenvolvimento do DO-178C
O desenvolvimento de software e hardware nas indústrias aeroespacial e militar / de defesa é complexo. E o DO-178C o torna mais complexo.

Os custos podem se acumular quando você está demonstrando conformidade. Mas escolher as ferramentas certas pode ajudá-lo a alcançar a conformidade com o DO-178C - e reduzir o custo de conformidade.

Aqui está o que procurar.

Cobertura de teste completa
Se você deseja estar em conformidade com o DO-178C, precisa de uma cobertura de teste completa.

Com o Helix ALM, você pode criar casos de teste a partir de requisitos. E você pode executar testes a partir de casos de teste. Isso ajuda a garantir 100% de cobertura do teste.

Rastreabilidade no desenvolvimento
A rastreabilidade é sempre importante para conformidade. E isso aumentará significativamente sua capacidade de conformidade.

Com o Helix ALM , você pode estabelecer links entre tudo. Requisitos. Código. Testes. Insetos.

Qualidade garantida
Qualidade é importante. E para as organizações aeroespaciais e militares / de defesa, a qualidade é crítica.

Com o Helix QAC , você pode melhorar a qualidade do código. E você pode cumprir seu padrão de codificação C ou C ++. E com o Helix ALM , você terá certeza de que os requisitos são atendidos. Com essas ferramentas combinadas, você garante qualidade e entrega no prazo.

A conformidade com DO-178C é fácil com o Perforce
O Perforce oferece uma variedade de ferramentas que podem ajudá-lo a entrar em conformidade durante todo o ciclo de vida do desenvolvimento.

O Helix ALM reúne seus requisitos, testes e bugs em um único local. Você poderá demonstrar a cobertura do teste para seus requisitos. E você poderá criar uma matriz de rastreabilidade com facilidade. 

CRIAR UMA MATRIZ DE RASTREABILIDADE COM HELIX ALM 

 

O Helix QAC verifica se seu código-fonte está em conformidade com os padrões de codificação. Este analisador de código estático vem com um pacote de qualificação DO-330 para documentar automaticamente a qualificação da sua ferramenta.

VERIFIQUE O CÓDIGO FONTE COM O HELIX QAC

