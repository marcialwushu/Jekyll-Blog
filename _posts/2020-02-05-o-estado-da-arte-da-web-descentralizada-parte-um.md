---
layout: post
title:  "O estado da arte da web descentralizada - Parte 1"
date:   2020-02-05 17:59:38 -0200
categories: jekyll update
---


## 1. Introdução

Sou desenvolvedor da Web de pilha completa com uma boa experiência em JavaScript e arquiteturas sem servidor na AWS (consulte [meus outros artigos](https://medium.com/@christophe.bougere), se você estiver interessado neste tópico). Tenho a sensação de que a descentralização pode ser a próxima grande novidade no desenvolvimento da web. A propósito, uma biblioteca ÐApp muito popular é chamada [web3.js](https://github.com/ethereum/web3.js/) , como sucessora do que conhecemos atualmente como [Web 2.0](https://en.wikipedia.org/wiki/Web_2.0) . De certa forma, a descentralização poderia permitir uma verdadeira Web sem servidores, onde cada cliente contribuiria para a Web (como uma rede ponto a ponto).


>Descentralizado é o novo Serverless


Nesta série, tentarei desmistificar todo esse novo ecossistema. Compartilharei com vocês minhas descobertas em um nível bastante alto. Não veja isso como um curso completo ou uma lista exaustiva de tecnologias, mas como uma boa introdução que o ajudará a entender por que e como essa arquitetura pode revolucionar a web que conhecemos atualmente.

## Artigos da série

- **Introdução**

Principais conceitos e riscos de uma arquitetura descentralizada. Quais são os maiores desafios que enfrentaremos?
- **Armazenamento de arquivos**

Como armazenar arquivos (código fonte, imagens,…) da maneira descentralizada. O armazenamento de dados parece ser a área mais madura a partir de agora e veremos várias soluções.
- **Blockchain e contratos inteligentes**

As palavras-chave mais populares no momento. Embora seu potencial seja inquestionável em alguns casos de uso, vamos aprender quando você deve ou não usar blockchain, dependendo de suas necessidades. Vamos nos concentrar no Ethereum e no EOS.
- **Bancos de dados**

Depois de ter armazenamento e processamento de arquivos, a próxima etapa para muitos aplicativos da web é configurar um banco de dados. Quais são as opções distribuídas e descentralizadas?



## O que significa descentralizado?

Para começar, vamos ter certeza de que estamos usando o mesmo vocabulário. Se você já conhece a diferença, sinta-se à vontade para pular para a próxima seção. Caso contrário, aqui estão três topologias de rede e como cada uma delas reagiria no caso de um nó específico enfrentar um ataque:


![](https://hackernoon.com/hn-images/0*Mxv6E7jAXi84ZQee.gif)

>As redes centralizadas estão indo muito mal, você não acha?

## Centralizado / Descentralizado

Se o sistema for **controlado por uma única entidade** , ele será **centralizado** . No caso de um aplicativo Web, os clientes (navegador da Web, aplicativo móvel) se comunicam com um servidor para renderizá-lo. Se o servidor for desligado, todos os clientes perderão o acesso ao aplicativo. Isso é o que chamamos de **ponto único de falha (SPOF). A escalabilidade do sistema também é muito limitada** : você pode aumentar os recursos desse nó adicionando mais RAM ou discos rígidos (escala vertical), mas não pode adicionar mais nós (escala horizontal). Por outro lado, esse tipo de sistema é fácil de configurar, manter e evoluir porque você só precisa implantar o sistema em um único nó.

Se o sistema for controlado por muitas entidades , ele será considerado descentralizado . É mais resistente : se um nó principal estiver desativado, apenas os nós clientes conectados a este nó principal pararão de funcionar. O sistema ainda está vulnerável a falhas e ataques , mas o impacto é proporcional ao número de nós principais afetados. Também é mais escalável, porque você pode escalar horizontalmente (adicionar mais nós) e verticalmente.

## Distribuído

Quando se trata de sistemas **distribuídos , todos os nós são iguais e têm o mesmo controle sobre o sistema** . Um exemplo famoso é o BitTorrent, um protocolo de compartilhamento de arquivos ponto a ponto. Em vez de se conectar a um servidor para recuperar dados, você os recupera dos seus pares e também fornece os dados que eles desejam, se os tiver. Um sistema distribuído é **altamente escalável e robusto** . Por outro lado, uma evolução do sistema pode ser complicada porque envolve muitas entidades.

Estou simplificando este artigo, mas o assunto pode ser detalhado muito mais. Por exemplo, Vitalik Buterin, cofundador da Ethereum, distingue três tipos de (des) centralização: arquitetônica, política e lógica:


### [O significado da descentralização](https://medium.com/@VitalikButerin/the-meaning-of-decentralization-a0c92b76a274)

>“Descentralização” é uma das palavras usadas com mais frequência no espaço criptográfico e geralmente é até…

[medium.com](https://medium.com/@VitalikButerin/the-meaning-of-decentralization-a0c92b76a274)


## Por que isso Importa?

## Transparência e governança descentralizada

Esta é, na minha opinião, a verdadeira razão pela qual os sistemas descentralizados estão na moda no momento. Com o big data, as organizações possuem uma quantidade incrível de dados sobre você e sua vida pessoal. Mesmo que, no caso do Google, Amazon ou Facebook, seja usado principalmente para fins publicitários (que já podem levantar questões éticas), isso poderá piorar rapidamente se eles acharem interesse em política ou se alguns terceiros tiverem acesso a essas informações. (veja o que aconteceu com o Cambridge Analytica). Também sabemos que essas empresas podem ser forçadas a instalar backdoors em seus aplicativos. Os dados são provavelmente a coisa mais valiosa no momento e os usuários estão perdendo a confiança nessas empresas e buscando transparência.

A Internet também já é censurada em muitos países, e a descentralização pode ser uma maneira de contornar a censura movendo o controle da Internet e dos dados dos usuários nas mãos dos próprios usuários e ignorando governos e empresas.

Por fim, a estrutura organizacional pode ser descentralizada. A Organização Autônoma Descentralizada (DAO) oferece uma solução transparente para governança. Obviamente, ele ainda requer humanos no circuito para alguns casos de uso. Para ir além, o seguinte artigo explica que tipo de organização pode/deve ser descentralizada:


### [Governança de Blockchain: Quão descentralizados precisamos ser?](https://hackernoon.com/blockchain-governance-how-decentralized-do-we-need-to-be-799a7988ce84)

>Embora a governança descentralizada não seja uma solução panacéia para todos os casos de uso, mais é necessária em um mundo que é…

[hackernoon.com](https://hackernoon.com/blockchain-governance-how-decentralized-do-we-need-to-be-799a7988ce84)


## Segurança

Embora as atuais infraestruturas da Internet sejam bastante robustas, elas são feitas de ponto único de falha (SPOF) por design. O provedor de DNS é um deles e, quando Dyn passou por um ataque de DDOS em 2016, foi uma grande parte da web que caiu:

![](https://hackernoon.com/hn-images/1*FnX_FdkrAnRHUCNGHe2kjw.png)

>[Serviços afetados por ataques Dyn](https://en.wikipedia.org/wiki/2016_Dyn_cyberattack#Affected_services)

Os sistemas descentralizados e distribuídos ainda precisam cuidar da segurança (e provavelmente ainda mais), mas se o sistema for construído de uma maneira forte e confiável, resistirá melhor a um ataque do que um sistema centralizado, porque não é suficiente assumir o controle de um nó, em muitos casos, você precisaria assumir o controle da maioria dos nós ( [saiba mais sobre o ataques de 51%](https://en.bitcoin.it/wiki/Majority_attack)).


## Escalabilidade

Por último, mas não menos importante, a escalabilidade é a chave agora. As empresas migraram para a nuvem para poder lidar com a cobrança em qualquer circunstância e estão começando a migrar para a arquitetura sem servidor para pagar apenas pelo que realmente estão usando. Arquiteturas descentralizadas e distribuídas já são capazes de fazer isso por design. Quanto mais usuários um sistema tiver, mais recursos de computação e capacidade de armazenamento serão descartados. A capacidade de expansão desses sistemas é natural.

## Alguns exemplos promissores

![](https://hackernoon.com/hn-images/1*UwEacpQmLFQzY4oWsurVBQ.png)

>[Textile Photos](http://textile.photos/)

O Textile Photos propõe uma substituição descentralizada para serviços de armazenamento e compartilhamento de fotos na nuvem, como Google Photo e Apple Photos. As imagens são armazenadas no IPFS, que será o tópico do próximo capítulo. O Textile Photos ainda está na versão beta, mas a empresa já planeja expandir para outros casos de uso (podemos imaginar uma substituição do Dropbox / Drive funcionando da mesma maneira).

![](https://hackernoon.com/hn-images/1*9FPq_5QsE8gx13dK5ZSZkA.jpeg)

>[Eva](https://eva.coop/)

Eva tem como objetivo interromper o Uber e outros aplicativos de compartilhamento de viagens (que interromperam o negócio de táxi há alguns anos), conectando diretamente motoristas e passageiros através do blockchain.

![](https://hackernoon.com/hn-images/1*QWiYx80io3yyc-palrwEPA.png)

>[OpenBazaar](https://openbazaar.org/)

>### Um mercado online gratuito. Sem taxas de plataforma. Sem restrições. Ganhe criptomoeda


Você entende, o OpenBazaar é uma plataforma de comércio eletrônico descentralizada, onde qualquer pessoa pode vender e comprar. O interessante é como eles garantem o dinheiro durante a transação e como resolvem conflitos:

>Os golpistas podem tentar tirar proveito dos compradores e vendedores on-line, mas o OpenBazaar oferece um recurso exclusivo do Bitcoin que ajuda a evitar fraudes: custódia de várias assinaturas. Nesse mercado de comércio eletrônico, compradores e vendedores podem optar por concordar com um usuário OpenBazaar de terceiros com confiança mútua antes de iniciar uma negociação e, em seguida, o comprador envia seu bitcoin para uma conta de garantia. Esses Bitcoin só podem ser liberados quando duas das três partes concordam para onde serão enviadas. Normalmente, o comprador e o vendedor são as duas partes do contrato, mas se houver uma disputa, a terceira parte resolverá a disputa. Esses terceiros que oferecem resolução de disputas são selecionados em um mercado aberto.
- [Site do OpenBazaar](https://openbazaar.org/features/)

![](https://hackernoon.com/hn-images/1*_wjdvZq2SdSJtrP3KohYjQ.png)

>[Everipedia](https://everipedia.org/)

>Everipedia é uma enciclopédia online baseada em wiki. […] A empresa usa a tecnologia blockchain EOS e um token de criptomoeda chamado IQ para incentivar a geração de informações. Um dos objetivos da empresa é impedir que certos países bloqueiem seu conteúdo com a integração do modelo blockchain. A Everipedia foi lançada no blockchain da EOS em 9 de agosto de 2018. - [Leia o artigo da Everipedia na Wikipedia](https://en.wikipedia.org/wiki/Everipedia) (certamente irei ao inferno por isso 😈)

Observe que apenas a governança é armazenada na cadeia, enquanto os artigos são armazenados no IPFS. O blockchain da EOS é um sério concorrente do Ethereum que afirma resolver os desafios que o último enfrenta (é mais rápido, já baseado em uma Prova de Participação e não requer gás para realizar transações). Ainda é muito mais jovem, mas muito bem financiado. Somente o tempo dirá qual criptomoeda vence a guerra dos contratos inteligentes.

![](https://hackernoon.com/hn-images/1*Z03LhbPyE9CMIso6tF4HtQ.jpeg)

>[State of the ÐApps](https://www.stateofthedapps.com/)

Finalmente, você deseja descobrir novos ÐApps (significa Aplicativo Descentralizado, mas com um D estranho) ou apenas verificar se sua ideia já existe, este site faz referência a 1800 deles.

## Desafios

## Simplifique para o usuário final

Como veremos, o uso da blockchain requer uma carteira cheia de várias criptomoedas e, muitas vezes, o pagamento de taxas de transação (também chamadas de gás). Dependendo do seu projeto e de seus usuários, ele pode ser visto como uma configuração inútil, enquanto algumas soluções centralizadas já existem e funcionam bem. Este é, na minha opinião, o maior desafio, porque, para as pessoas abraçarem esse novo paradigma, a experiência do usuário deve ser tão fácil quanto antes. [Tem que "apenas trabalhar"](https://medium.com/textileio/wip-textile-threads-whitepaper-just-kidding-6ce3a6624338#1705) .



### Empacote para celular

Esse jovem ecossistema está evoluindo rapidamente, mas, atualmente, muitas tecnologias são projetadas para funcionar em um desktop ou em um navegador (às vezes com algumas extensões), e integrá-las em aplicativos móveis pode ser complicado. O celular já representa uma grande parte do uso da web e é vital para que a descentralização aconteça.



### Torne-o rápido e confiável

As pessoas já usam o sistema ponto a ponto há um tempo porque ele estava respondendo a uma necessidade específica (compartilhar livremente arquivos grandes). No entanto, navegar em sites usando o Tor é muito mais lento do que navegar diretamente na web através do seu navegador favorito. Esse problema deve ser resolvido no design das tecnologias.


### Não há mais back-end

Este ponto pode ser minha utopia pessoal. Embora eu goste de muitas tecnologias de back-end, gostaria que elas funcionassem de maneira descentralizada nos dispositivos dos usuários. Isso pode não ser possível para tudo em um futuro próximo, mas acredito que esse seja o caminho a seguir sempre que possível. Em janeiro, a [nuvem da DADI](http://dadi.cloud/) levantou US $ 29 milhões para construir um sistema em nuvem descentralizado. Eles têm [um roteiro muito ambicioso](https://dadi.cloud/en/marketplace/) que permitiria se livrar dos provedores de nuvem para muitos casos de uso.


### Reduzir a pegada ambiental da blockchain

Sozinho, o sistema BitCoin Proof of Work (PoW) consome tanta energia quanto a Suíça . Obviamente, isso não é concebível nem desejável substituir a rede existente por essa solução. Embora muito crítico, esse desafio já está sendo enfrentado e veremos como no Capítulo 3.


### As empresas devem adotar a descentralização

Ser descentralizado é uma perda de controle sobre os dados e a lógica de um aplicativo. Embora o software de código aberto seja um ajuste perfeito para isso, fazer com que as empresas adotem esse novo paradigma pode ser complicado. Em alguns casos, um projeto simultâneo descentralizado pode forçar as empresas a seguir o mesmo caminho, mas esse será um longo caminho.

### Encontre o "modelo de negócios" certo

Hoje, a maioria das ferramentas da Web (provedores de nuvem, APIs de terceiros,…) está lucrando para pagar seus funcionários e servidores com assinaturas ou um modelo de "pagamento conforme o uso". Com a descentralização, vejo duas opções:

- Tudo poderia ser gratuito, e as pessoas contribuiriam com a Web armazenando dados e compartilhando sua capacidade de processamento em seus dispositivos. As fundações da web seriam de código aberto e as empresas contribuiriam para isso. Mais uma vez, isso pode ser uma utopia e as pessoas podem tentar reduzir sua contribuição para economizar recursos e largura de banda, para que não seja viável em larga escala.
- O uso de recursos pode ser pago por meio de uma criptomoeda. Os usuários ganham tokens quando compartilham seus recursos e os gastam para usar a web. Esse método incentivaria as pessoas a contribuir e garantir uma boa confiabilidade do sistema.


## Pronto para começar?

Bem, espero que você esteja pronto e tão animado quanto eu para descobrir este novo mundo!

![](https://hackernoon.com/hn-images/0*QU288ho_auSeSFmP.gif)

>[Ainda não assistiu as últimas temporadas do Vale do Silício? É tudo uma questão de descentralização!](https://www.wired.com/2017/06/pied-pipers-new-internet-isnt-just-possible-almost/)


Vamos então. [O Capítulo 2 está disponível aqui](https://medium.com/@christophe.bougere/a-state-of-the-art-of-decentralized-web-part-2-ea630917332a) e trata de armazenamento de arquivos.

Este artigo reflete minha compreensão do tópico que pode ser subjetivo, portanto as discussões são muito bem-vindas nos comentários. E dê alguns 👏👏👏 se você gostou 😉.

**PS**: Eu sei que tenho usado as palavras "descentralizado" e "descentralização" muitas vezes neste artigo (deixo que você as conte), espero que você me perdoe 😬.

--- 

Autor: [Christophe Bougère](https://hackernoon.com/@christophe.bougere)

[Artigo Original](https://hackernoon.com/a-state-of-the-art-of-decentralized-web-part-1-54f70fdb7355)


