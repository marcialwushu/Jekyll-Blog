---
layout: post
title:  "O estado da arte da web descentralizada - Parte 3"
date:   2020-02-07 17:59:38 -0200
categories: jekyll update
---

3. Blockchain e contratos inteligentes

Este artigo é o terceiro capítulo de uma série sobre descentralização da web. Aqui vamos nos concentrar em uma das palavras mais populares do ano: a blockchain . Embora tenha potencial real e inquestionável, também possui limites significativos. Vamos dar uma olhada nas principais blockchains públicas (ou seja, disponíveis para todos) e ver quando pode ser uma escolha inteligente em um projeto.

![](https://miro.medium.com/max/1300/0*ehuZeDiSybCagw_N.jpg)

>[Bingo codificador, CommitStrip](http://www.commitstrip.com/en/2016/06/20/coder-bingo/)

## Artigos da série

1. Introdução
2. Armazenamento de arquivo
3. Blockchain e contratos inteligentes
4. Bases de dados

Antes de prosseguir, se você não tem idéia do que é blockchain, assista a este vídeo de 2 minutos para obter os principais princípios:

[![](https://i.ytimg.com/vi/WiRFuHXHBhk/hqdefault.jpg)](https://youtu.be/WiRFuHXHBhk)


## Uma breve história da blockchain

### 1995 - Os primeiros sinais

![](https://miro.medium.com/max/200/0*sTzmq3XzGpwzzIy-.jpg)

Para a anedota, o primeiro blockchain conhecido foi criado em 1995 e seu livro era ... um jornal. Stuart Haber e Scott Stornetta, dois pesquisadores em criptografia, decidiram usar a seção AVISOS & PERDIDOS E ENCONTRADOS do New York Times para registrar o registro de data e hora. Qual é o link com o blockchain sobre o qual todos estão falando hoje em dia? Bem, ele tem as mesmas características: as informações são criptografadas e armazenadas em um bloco com registro de data e hora (aqui uma edição do jornal e serão distribuídas para uma rede (leitores de jornais). Esse processo torna quase impossível falsificar os dados. imprima uma versão antiga do jornal e altere seu conteúdo, mas seria extremamente fácil verificar se uma versão é falsa ou não, observando muitos arquivos.

Para ser mais preciso, as informações armazenadas no jornal são apenas um hash que permite verificar a integridade dos dados armazenados "fora da cadeia". Caso contrário, eles precisariam de muito mais espaço no jornal! Você pode ler mais sobre o processo [aqui](http://surety.com/digital-copyright-protection/prove-ownership) .

### 2009 - E Deus criou o Bitcoin

Bitcoin é uma moeda digital descentralizada criada em 2009 por alguém com o nome Satoshi Nakamoto. Sua identidade real ainda é desconhecida e sujeita a tantos debates quanto o artista de rua Banksy. [Pesquise "Identidade Satoshi Nakamoto" no Google](https://www.google.com/search?q=Satoshi+Nakamoto+identity) para ler sobre as melhores teorias da conspiração. Mas, com certeza, ele provavelmente é extremamente rico agora, pois extraiu cerca de um milhão de blocos no início (a taxa de câmbio varia muito, mas o torna multibilionário).

O que torna o Bitcoin revolucionário é o fato de ser descentralizado: não é de propriedade de nenhum banco ou organização e qualquer pessoa pode fazer parte da rede. As transações são verificadas pelos nós da rede por meio de criptografia e registradas em um livro público distribuído chamado blockchain. Você pode se perguntar como podemos obter um consenso sem uma entidade confiável centralizada? Para conseguir isso, os mineradores (também conhecidos como nós completos, são recompensados ​​por escrever dados) precisam fornecer uma **Prova de Trabalho** (PoW) para anexar novos dados à blockchain. Um PoW é o resultado de um cálculo complexo (tempo e consumo de energia) que pode ser facilmente verificado. Para resumir, um único nó gastará recursos para anexar dados ao blockchain, cuja integridade pode ser verificada por qualquer nó. Bitcoin usa o [HashCash](https://en.wikipedia.org/wiki/Hashcash) PoW e adapte constantemente a dificuldade de cálculo.

As duas principais desvantagens do algoritmo de consenso de Prova de Trabalho são as seguintes:

- A mineração consome muita energia devido à complexidade do cálculo. Embora a moeda seja puramente virtual, consome mais energia do que 159 países (embora não combinados). Não é sustentável nem desejável e é ainda mais lamentável, pois os cálculos são totalmente inúteis (eles não estão ajudando a ciência, por exemplo).

![](https://miro.medium.com/max/2000/0*yipypn2fCBHU6lB_.png)

- Na realidade, os nós completos do Bitcoin não são muito descentralizados porque os grandes pools de mineração têm mais chances de receber seu trabalho recompensado por mineradores individuais. Aqui está a distribuição dos pools do último ano:

![](https://miro.medium.com/max/1136/1*VuXn0SNkkTIJ9NTXDwCXVw.png)


>[Distribuição de pools de mineração](https://btc.com/stats/pool?pool_mode=year) - No ano passado, 58% dos blocos foram extraídos por apenas 4 pools de mineração

- É vulnerável a 51% de ataques. Para simplificar, se um grupo conseguisse controlar a maioria dos nós de mineração, seria capaz de comprometer toda a integridade do sistema. É, obviamente, um ataque muito caro, mas, dada a distribuição atual, os hackers "simplesmente" teriam que assumir o controle de algumas organizações para tornar isso possível.

Não vou gastar muito tempo com Bitcoin, que é limitado principalmente a transações financeiras (mesmo que [tenha uma linguagem de script](https://en.bitcoin.it/wiki/Script) e [seja tecnicamente possível escrever contratos inteligentes](https://bitcoinmagazine.com/articles/yes-bitcoin-can-do-smart-contracts-and-particl-demonstrates-how/) ).

### 2015 - Ethereum amplia o potencial da blockchain

Vitalik Buterin, um programador interessado em Bitcoin, viu um potencial muito mais amplo para a tecnologia por trás dessa moeda criptográfica. Ele e sua equipe introduziram um novo blockchain com o objetivo de criar **aplicativos descentralizados** . Em vez de seguir um conjunto básico de operações, como na linguagem de script do Bitcoin, o Ethereum oferece uma linguagem completa de Turing. Para simplificar, isso significa que você pode resolver teoricamente qualquer problema computacional em um **contrato inteligente**, supondo que você tenha recursos de computação suficientes. Sejamos claros, você enfrentará limites computacionais muito mais rapidamente do que na maioria dos idiomas, porque a execução de código no Ethereum tem um custo (chamado de gás) e levará mais tempo. Portanto, cabe ao desenvolvedor manter uma baixa complexidade no programa (evite loops aninhados ou loops com um número alto de iterações).


Os contratos inteligentes podem ser escritos em vários idiomas, sendo o mais popular o [Solidity](https://solidity.readthedocs.io/) . Eles são compilados em um bytecode específico do Ethereum e executados na **Ethereum Virtual Machine** (EVM), da mesma forma que em Java. O conceito de contrato inteligente ainda pode ser abstrato em sua cabeça. Se você está curioso sobre como pode ser um contrato inteligente, [aqui estão alguns exemplos](https://github.com/pbrudny/learning-solidity-2018) .

Ao codificar contratos inteligentes, a segurança é uma questão primordial porque você está lidando com dinheiro e um pequeno vazamento pode ter enormes impactos. Uma boa prática é reutilizar bibliotecas que foram auditadas em vez de escrever tudo sozinho. Dê uma olhada no **OpenZeppelin** , provavelmente o mais popular:


[**OpenZeppelin**](https://openzeppelin.org/)

O OpenZeppelin é uma estrutura de código aberto para criar contratos inteligentes e seguros. Reduza o risco de vulnerabilidades no seu…

[openzeppelin.org](https://openzeppelin.org/)

Além disso, ao lidar com o Ethereum, o pipeline de desenvolvimento pode ser complicado. O **Truffle Suite** oferece algumas ferramentas que devem facilitar sua vida: um IDE, um pipeline de testes, uma maneira simples de atualizar seus contratos (com migrações) e uma ferramenta para criar um novo blockchain on-the-fly para seus testes. É o canivete suíço do desenvolvedor Ethereum.

[**Truffle Suite | Ferramentas doces para contratos inteligentes**](https://truffleframework.com/)

O conjunto de ferramentas Truffle torna o desenvolvimento dapp mais fácil e consistente.

[truffleframework.com](https://truffleframework.com/)

Então, o Ethereum parece incrível! Você pode codificar tudo o que torna teoricamente possível descentralizar qualquer aplicativo! Vamos agora dar uma olhada nas **principais limitações** :

- **Desastre ambiental** . Quanto ao Bitcoin, o Ethereum usa um algoritmo de consenso de Prova de Trabalho e tem o mesmo problema de impacto ambiental devido ao seu consumo de eletricidade. A boa notícia é que eles planejam mudar para uma Prova de Estaca (PoS) em 2019 (nome do projeto: Casper). O que é isso? Bem, em vez de resolver cálculos de tempo e consumo de energia, os mineradores (aqui chamados validadores) terão que depositar uma quantidade de tokens que serão mantidos enquanto estiverem minerando. Eles receberão alguns blocos para validar com base em dois fatores: o valor da aposta (quanto mais você perder, mais você será considerado confiável) e um grau de chance (caso contrário, apenas os mais ricos poderão validar blocos) )
- **Lentidão** . Uma transação leva cerca de 15 segundos para processar . Pode ser aceitável para alguns casos de uso específicos, mas não para descentralizar aplicativos existentes que já são imediatos. Mas o PoS deve resolver esse problema reduzindo o tempo para 1 segundo.
- **Escalabilidade** . Por enquanto, o Ethereum pode suportar até 15 transações por segundo (1,3 milhão de transações por dia). Isso é muito baixo comparado ao seu potencial de uso. Em comparação, o sistema VISA pode lidar com 24.000 transações por segundo (teoricamente). A boa notícia aqui é que a Ethereum pretende aumentar esse limite para 1 milhão de TPS combinando duas soluções tecnológicas: sharding e um projeto chamado Plasma . O primeiro consiste em dividir a rede em fragmentos que processariam apenas determinadas transações (em vez de processá-las todas), e o segundo visa realizar algumas transações em uma cadeia lateral que deve liberar a cadeia principal. Casper está planejado para chegar em 2019, enquanto teremos que esperar até 2020 ou 2021 para que o sharding apareça.
- **Custo** . Toda transação tem um preço, chamado gás , cujo valor depende da complexidade do contrato. Os usuários estão acostumados a uma Internet gratuita e ilimitada, portanto, ter que pagar por todas as transações em seu aplicativo da vida cotidiana pode ser um sério obstáculo. [O preço médio do gás é de quase US $ 0,01](https://ethgasstation.info/) . Em um aplicativo de bate-papo em que cada mensagem enviada seria uma transação, seria muito caro usar o Ethereum!

Embora o Ethereum tenha muito o que abordar para permitir sua visão, eles já têm um plano para quase tudo. Mas ter que esperar 1 ou 2 anos para resolver esses problemas, se tudo der certo, coloque-os em uma situação de risco.

## 2018 - EOSIO, Ethereum em esteróides?

O EOSIO (ou simplesmente o EOS) tem objetivos muito semelhantes ao Ethereum. Então, em vez de uma descrição completa, vou focar no que a torna diferente:

- Contratos inteligentes estão sendo executados na máquina virtual [**WebAssembly**](https://webassembly.org/) (abreviada Wasm). Em resumo, é um novo padrão da Web que permite que os sites executem código nativo no navegador dentro de uma sandbox. Wasm pode se tornar um concorrente do Javascript para o desenvolvimento de front-end. Em teoria, você deve conseguir escrever contratos inteligentes de EOS em qualquer uma [dessas linguagens](https://github.com/appcypher/awesome-wasm-langs/blob/master/README.md) (mas, por enquanto, C, C ++ e Rust parecem ser os mais suportados).
- O EOS usa a **Delegated Proof of Stake** (DPoS) como algoritmo de consenso. É muito semelhante ao PoS, exceto que existe um número limitado de produtores de blocos (21). Embora deixar todo o poder para 21 atores pareça muito arriscado, ele depende da comunidade que pode votar para demitir produtores não confiáveis. É um novo paradigma, porque o algoritmo de consenso é um híbrido entre democracia, onde as pessoas elegem delegados para representá-los e um algoritmo determinístico entre os 21 delegados (cujas identidades reais são conhecidas). Fato interessante: A EOS tem uma [constituição escrita pela comunidade](https://github.com/EOSIO/eos/blob/37ce45c0b60d2710569c2d1a9229945cc0e855a9/governance/constitution.md) (qualquer mudança pode ser aplicada com 15/21 eleitores).
- O último ponto permite que a EOS obtenha desempenhos muito melhores : até 6000 TPS, e uma transação leva apenas cerca de 1 segundo.
- A EOS propõe um modelo econômico sem taxa (sem gás para pagar para executar uma transação); os produtores de blocos serão recompensados com 1% da inflação anual.
- O EOS também traz alguns recursos de nível superior, como recuperação de conta / senha, nomes de usuário legíveis por humanos (em vez de alguns endereços hexadecimais longos) e uma solução de armazenamento de arquivos. Esses recursos geralmente eram oferecidos por serviços de terceiros, e integrá-los é um experimento interessante.

Uma das maiores críticas à EOS é que ela é centralizada demais . Eles definitivamente estão fazendo uma troca interessante aqui e é muito cedo para saber se essa escolha é viável ou não. Por outro lado, provavelmente tornará a evolução da EOS muito mais simples . Em muitas cadeias de blocos, algumas evoluções importantes exigem quebras de mudanças que resultem na divisão da comunidade em duas partes: aqueles que desejam continuar com o sistema antigo e aqueles que aceitam a evolução. Ter alguns delegados deve, idealmente, oferecer mais agilidade. Você pode ler mais sobre os diferentes tipos de forks [aqui](https://vitalik.ca/general/2017/03/14/forks_and_markets.html) .

[Block.one](https://block.one/) , a empresa por trás da EOS fechou um ICO de US $ 4 bilhões para desenvolver o ecossistema. A equipe por trás do projeto também é renomada (o CTO Daniel Larimer fundou a BitShares e a Steemit). O projeto deles é muito ambicioso, pois o principal concorrente já é a solução de fato para muitos projetos de blockchain. 2019 será definitivamente um ano interessante e as duas plataformas provavelmente terão que incentivar usuários e desenvolvedores a se juntarem a elas.

Existem muitos outros concorrentes como o [HyperLedger](https://www.hyperledger.org/) ou o [Lisk](https://lisk.io/) e talvez eu tenha esquecido alguns dos principais. Sinta-se livre para compartilhar seus pensamentos nos comentários.


## Quando você deve usar o blockchain?

Primeiro de tudo, mesmo se estivermos focando em **blockchains públicas (ou sem permissão)** porque elas pretendem descentralizar a lógica de um aplicativo, você deve saber que existe outro tipo: **blockchains permitidos (ou privados)** . Eles são úteis em um projeto em que ninguém deve contribuir. O limite entre esses dois tipos não é nítido e também existem blockchains com semi-comissionamento.

Para resumir, aqui estão os principais benefícios de uma blockchain:

- **Nenhuma autoridade central** : ao usar um sistema, você não precisa confiar em terceiros e tudo é verificável e transparente.
- **Imutabilidade dos dados** : uma vez gravados na cadeia, é teoricamente impossível alterá-los (exceto no caso de um ataque).
- **Fonte única de verdade** : devido à estrutura da blockchain, você pode saber de maneira confiável se um token pertence a um usuário ou outro.

Esses recursos tornam o blockchain particularmente interessante para criar sistemas de rastreabilidade (em uma cadeia de suprimentos, por exemplo). Mas você também pode usá-lo para criar a lógica de um aplicativo descentralizado: ajuda você a se livrar do código que normalmente é executado nos seus servidores.

Aqui está um cenário de aplicativos blockchain:

![](https://miro.medium.com/max/1204/0*WGkU27Rs8D5aO9uP)

Então, quando você deve usá-lo? Você encontrará muitas árvores de decisão ajudando a decidir se você deve ou não usar uma blockchain em um projeto. Acho este particularmente relevante:


![](https://miro.medium.com/max/2000/0*TgMQCvCfg0e4Efz0.png)


>[Mais detalhes](http://www3.weforum.org/docs/48423_Whether_Blockchain_WP.pdf)

No entanto, eu meio que discordo da 5ª pergunta:

>Você pretende armazenar grandes quantidades de dados não transacionais como parte de suas soluções?

Se você ler o [segundo capítulo sobre armazenamento de arquivos](https://medium.com/@christophe.bougere/a-state-of-the-art-of-decentralized-web-part-2-ea630917332a) , saberá que existem soluções para armazenar grandes quantidades de dados de maneira descentralizada. Em seguida, é possível armazenar as transações na blockchain e alguns arquivos criptografados fora da cadeia.

## Blockchain também traz muita complexidade

Embora o blockchain tenha um enorme potencial, não esqueça que ele complexificará seu aplicativo:

### A evolução será complicada

Atualizar seus contratos inteligentes não será muito fácil. É importante ter uma boa arquitetura e pensar em todos os recursos que você implementará desde o primeiro dia.


### Segurança como prioridade

Como vimos anteriormente, um simples erro pode custar muito e você não poderá corrigi-lo tão facilmente quanto em um servidor centralizado. É por isso que a segurança deve ser a prioridade número um, e você deve auditar seus contratos inteligentes antes de implantá-los!

### Arquitetura mais complexa

Para problemas de desempenho e custo, você não poderá lidar com toda a lógica do seu aplicativo dentro de seus contratos inteligentes. Você também precisará coletar dados da API de terceiros. Para conseguir esse tipo de coisa com a blockchain, você precisará usar o **Oracles** :

>Um oráculo, no mundo blockchain, é um agente digital unidirecional que encontra e verifica dados do mundo real e envia criptograficamente essas informações ao contrato inteligente de consulta. Um oráculo não é a fonte de dados em si, mas a camada que faz interface com as fontes de dados e a blockchain ; é um tradutor de informações fornecidas por uma API de terceiros que deve ser adicionada a uma blockchain. Com os oráculos, os contratos inteligentes têm um caminho para interagir com dados fora do ambiente imediato da blockchain.
>[- Blockchain Oracles: O que são e por que são necessários](https://medium.com/@jesus_notchrist/blockchain-oracles-af3b216bed6b)

## Um monte de projetos legais de blockchain

### Fizzy

[Fizzy](https://fizzy.axa/) é um **seguro de atraso de voo** . Se você assinar, ele coletará automaticamente os dados de voo das companhias aéreas e o compensará imediatamente caso o seu avião esteja atrasado. Eu gosto deste porque traz transparência nos contratos de seguro que geralmente são extremamente complicados de decodificar. Se você estiver interessado na implementação técnica, confira este artigo .


[![](https://i.ytimg.com/vi/xJZulZ_-CMI/hqdefault.jpg)](https://youtu.be/xJZulZ_-CMI)

### FOAM

A [FOAM](http://foam.space/) está introduzindo uma solução de **mapeamento criptográfico** baseada em uma **prova de localização** . Já temos GPS, qual é o objetivo? Bem, o GPS é uma maneira de um dispositivo saber sua própria localização, mas não há como outro ator verificar se as coordenadas fornecidas por um dispositivo são reais ou não (isso pode facilmente falsificá-las). O FOAM conta com uma rede de beacons que ganharão tokens ao validar a localização dos dispositivos. Isso pode ser particularmente interessante quando usado com IOT.

[![](https://i.ytimg.com/vi/EJeMVh4tm1w/hqdefault.jpg)](https://youtu.be/EJeMVh4tm1w)


### EXERGIA

[EXERGY](https://exergy.energy/) é uma **rede de energia ponto a ponto** . Permite comprar e vender energia de maneira segura e transparente de seus vizinhos dentro de uma micro-rede. O interessante é que a descentralização também pode ser aplicada a outras redes que não a Internet.

[![](https://i.ytimg.com/vi/LxlMmFKOSUY/hqdefault.jpg)](https://youtu.be/LxlMmFKOSUY)

---

Autor: [Christophe Bougère](https://medium.com/@christophe.bougere)

[Artigo Original](https://medium.com/hackernoon/a-state-of-the-art-of-decentralized-web-part-3-7d901e09d06f)


