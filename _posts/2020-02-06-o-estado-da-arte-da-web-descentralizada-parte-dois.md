---
layout: post
title:  "O estado da arte da web descentralizada - Parte 2"
date:   2020-02-06 17:59:38 -0200
categories: jekyll update
---

## 2. Armazenamento de arquivos

Este artigo é o segundo capítulo de uma série sobre descentralização da web. Aqui vamos nos concentrar em como armazenar arquivos. Acredito que o armazenamento é o campo mais avançado quando se fala em descentralização, porque conta com tecnologias maduras e robustas: ponto a ponto e criptografia. Se você é desenvolvedor de aplicativos (web ou móvel), já pode substituir sua camada de armazenamento por uma descentralizada.

![](https://hackernoon.com/hn-images/1*l11VtUM3MJlc09H71J-wUQ.png)

>E onde quer que você armazene seus dados, sempre antecipe os piores cenários 😉


## Artigos da série

- Introdução
- Armazenamento de arquivo
- Blockchain e contratos inteligentes
- Bases de dados

## Por que descentralizar o armazenamento de arquivos?

Em arquiteturas típicas de nuvem, usaríamos serviços em nuvem como [Amazon S3](https://aws.amazon.com/s3/) , [Azure Files](https://azure.microsoft.com/en-us/services/storage/files/) ou [Google Cloud Storage](https://cloud.google.com/storage/) . No nível de segurança e confiabilidade, não se preocupe, essa é uma escolha muito boa: os arquivos podem ser criptografados no servidor (para que o provedor de nuvem não tenha acesso aos seus arquivos), você pode configurar backups e replicação entre regiões. Você também tem uma escalabilidade infinita e um bom conjunto de APIs para acessar seu arquivo a partir de qualquer programa.

No entanto, vejo dois problemas com esses serviços:

- Eles são centralizados, o que significa que, no caso de uma interrupção, todo o sistema é impactado. Às vezes, [um erro de digitação pode desligar a web por quatro horas](https://www.theverge.com/2017/3/2/14792442/amazon-s3-outage-cause-typo-internet-server) .
- Eles têm um preço significativo (geralmente em $ / GB / mês), o que dificulta a organização sem fins lucrativos propor um aplicativo usando um serviço de armazenamento em nuvem.

Por outro lado, o seu novo computador pode ter um disco rígido de 2 TB enquanto você estiver usando apenas um décimo. Então, por que não usar esse espaço livre para oferecer suporte a um sistema de armazenamento de arquivos colaborativo?

Vamos dar uma olhada nos principais candidatos que oferecem essa solução:


- InterPlanetary File System
- Swarm
- Storj
- DADI
- Dat Project
- Sia
- Blockstack

São muitas opções e, às vezes, oferecem recursos semelhantes, então vou me concentrar no que os torna únicos. Pronto?

## 1. Sistema de Arquivos InterPlanetário

### [IPFS é o protocolo da Web distribuído de](http://ipfs.io/)
>hipermídia ponto a ponto para tornar a web mais rápida, segura e mais aberta.

[ipfs.io](http://ipfs.io/)

Por trás desse [nome enigmático](https://discuss.ipfs.io/t/why-the-name-ipfs/307) está o sistema mais maduro a partir de agora, na minha opinião.


### Recursos:

- Um protocolo ponto a ponto e uma rede. É uma combinação de Kademlia, BitTorrent e Git.
- O IPFS pode ser usado de forma independente, portanto, você não precisa usar uma pilha específica para usar o IPFS.
- O IPFS fornece um sistema de nomes (IPNS), uma CDN e pode servir diretamente sites.
- Não fornece garantias sobre disponibilidade ou redundância de dados. [O FileCoin](https://filecoin.io/) , um dos projetos irmãos do IPFS, propõe resolver isso introduzindo um sistema de incentivo baseado em blockchain (usuários que armazenam dados ganharão tokens FileCoin). Podemos ver isso como uma "edição corporativa" do IPFS com um SLA em cadeia.
- [Código aberto](https://github.com/ipfs/ipfs) . Alguns módulos do IPFS já se tornaram projetos independentes ( [libp2p](https://libp2p.io/) , [IPLD](https://ipld.io/) ).


**Preços**: o IPFS é gratuito. Os usuários contribuem para a rede servindo arquivos para seus pares. O preço da FileCoin dependerá do mercado (quanto mais pessoas propuserem armazenamento em disco, mais barato será).

**Status**: embora ainda esteja na versão alfa desde 2015, o protocolo parece bastante estável e rápido. Cético? [Assista a essa compilação de gatos engraçados](https://d.tube/#!/v/megamovie/a82s7pkc) no [DTube](https://d.tube/) , semelhante ao YouTube, baseado no IPFS para armazenamento e no [Steemit](https://steemit.com/) para gerenciar conteúdo e recompensar autores. O FileCoin, no entanto, é muito mais jovem e ainda não está pronto para uso ([consulte a última atualização do roteiro](https://filecoin.io/blog/update-2018-q1-q2/) ).

**Indo além**: para uma boa introdução teórica e prática ao IPFS, recomendo este artigo:

### [Uma introdução prática ao IPFS](https://medium.com/coinmonks/a-hands-on-introduction-to-ipfs-ee65b594937)

>O sistema de arquivos interplanetário será um grande negócio.

[medium.com](https://medium.com/coinmonks/a-hands-on-introduction-to-ipfs-ee65b594937)


E se você estiver interessado em entender como o IPFS funciona sob o capô (com seu serviço de nomes e vários protocolos), assista a Juan Benet (fundador do IPFS e Filecoin) falando sobre os diferentes mecanismos que eles implementaram:

![](https://i.ytimg.com/vi/Bqs_LzBjQyk/hqdefault.jpg)

## 2. Swarm

### [Swarm](https://ethersphere.github.io/swarm-home/)

>Em outubro de 2017, cinco grupos de trabalho começaram. Estrutura de teste e simulação de rede Um projeto que visa testar…

[ethersphere.github.io](https://ethersphere.github.io/swarm-home/)

### Recursos:

Do ponto de vista funcional e técnico, o Swarm é muito semelhante ao IPFS, com duas grandes diferenças:

- O Swarm está profundamente integrado ao blockchain Ethereum. Isso pode ser visto como uma vantagem se você já estiver usando o Ethereum em seu projeto, mas também poderá complexificar sua pilha no outro caso.
- O Swarm possui um sistema de incentivos embutido para incitar as pessoas que hospedam dados. Funcionalmente, o uso do Swarm é equivalente ao uso do IPFS junto com o FileCoin.


Para entender mais as semelhanças e diferenças entre os dois projetos, [um bom resumo está disponível aqui](https://github.com/ethersphere/go-ethereum/wiki/IPFS-&-SWARM) . A escolha da Ethereum de iniciar seu próprio projeto tem sido objeto de muitos debates, mas esse tipo de concorrência também pode fazê-los produzir melhores resultados (espero que sim). Swarm é de [código aberto](https://github.com/ethereum/go-ethereum/tree/master/swarm) (parte da base de código Ethereum).

**Preços**: Mais uma vez, o preço dependerá do mercado

**Status**: Swarm ainda é experimental. [A Prova de Conceito 3 foi lançada](https://blog.ethereum.org/2018/06/21/announcing-swarm-proof-of-concept-release-3/) e uma rede de teste está disponível. O roteiro está disponível [aqui](https://github.com/orgs/ethersphere/projects/5) . Fique de olho neste projeto, mas ainda não o use em produção.

**Indo além**: para começar a usar o Swarm, [leia a documentação oficial](https://swarm-guide.readthedocs.io/en/latest/introduction.html) .

## 3. Storj

### [Armazenamento em nuvem descentralizado - Storj](https://storj.io/)

>Storj é a camada de armazenamento para a Internet. O armazenamento em nuvem descentralizado é um novo paradigma que remove intermediários…

[storj.io](https://storj.io/)

### Recursos:

- S3 compatível. Isso significa que ele terá o mesmo conceito de buckets e objetos, mas não haverá pastas como em um sistema de arquivos padrão. Isso tornará super fácil descentralizar a camada de armazenamento de um aplicativo existente usando o Amazon S3!
- Criptografia de ponta a ponta integrada.
- Código aberto.

**Preços**:

- Armazenamento: US $ 0,015 por GB por mês
- Largura de banda: $ 0,05 por GB baixado

Storj propõe um programa de parceria para código aberto . Em resumo, todo software de código aberto que usa o Storj será recompensado em 10% dos benefícios.

**Status**: a rede Storj será lançada no início de 2019. Veja o roteiro [aqui](https://storjlabs.aha.io/published/01ee405b4bd8d14208c5256d70d73a38?page=1) .

**Indo além**: [Whitepaper](https://storj.io/white-paper)

## 4. DADI

### [A rede global local](https://dadi.cloud/)

>DADI é a nova rede Edge para serviços de computação em nuvem, alimentada pela tecnologia blockchain.

[dadi.cloud](https://dadi.cloud/)

Uma boa descrição do DADI seria " **Um provedor de nuvem descentralizado** ". A DADI já propõe uma CDN e um serviço de armazenamento em nuvem está chegando muito em breve. Vamos nos concentrar no CDN aqui.


**Recursos**:

- Serve arquivos estáticos (ativos, sites, ...).
- Os dados são armazenados em cache na borda.
- Suporte completo para armazenamento em cache, controle de cabeçalho, manipulação de imagem, compactação de imagem e conversão de formato de imagem.
- [Código aberto](https://github.com/dadi/cdn).

**Preço**: Este documento detalha o preço que depende do volume de solicitações. O DADI é baseado na prova de aposta, portanto, para se tornar um host DADI, você deve apostar 5.000 $ tokens DADI (equivalente a 216 $ a partir de agora).

**Status**: a CDN já está disponível e o armazenamento em nuvem deve estar disponível a partir de 2019. Veja o roteiro extremamente ambicioso aqui . Recentemente, eles levantaram US $ 29 milhões com uma OIC.

**Indo além**: vários tutoriais estão disponíveis aqui (procure a tag CDN).

## 5. Projeto Dat

### [Projeto Dat - um protocolo Web orientado à comunidade](https://datproject.org/)

>Dat é a comunidade e a tecnologia sem fins lucrativos para criar aplicativos do futuro.

[datproject.org](https://datproject.org/)

**Características**: O que é Dat? Dat é um protocolo ponto a ponto. Ele oferece uma CLI, uma API do Node.js. e um aplicativo de desktop. Arquivos hospedados pode ser acessado através de um navegador web neste endereço: https://datproject.org/{dat-key}. Nada de novo? Bem, a particularidade aqui é que você compartilhar uma pasta em vez de arquivos individuais, como um repositório com git ( dat clone, dat create, dat share), e você também pode atualizar seus arquivos. Com isso em mente, podemos entender que não é o melhor ajuste para criar um aplicativo Web descentralizado (em comparação com as soluções anteriores). No entanto, pode ter um valor agregado real para pesquisadores e cientistas que desejam publicar dados (resultados de experimentos, banco de dados de treinamento ...) para a comunidade e aplicar alterações facilmente. As fontes estão disponíveis aqui .


**Preços**: Grátis para usar. No entanto, você é responsável por manter os dados ativos (os pares compartilham apenas os dados clonados, como em um sistema BitTorrent clássico).

**Status**: o Dat está pronto para uso. Veja [dat.land](https://dat.land/) para exemplos de uso.

**Indo além**: a documentação e os tutoriais do Dat estão disponíveis [aqui](https://docs.datproject.org/) .


## 6. Sia

### [Sia](https://sia.tech/)

>Sia é uma plataforma de armazenamento descentralizada protegida pela tecnologia blockchain. A plataforma de armazenamento Sia aproveita…

[sia.tech](https://sia.tech/)

**Características**: Mais uma vez, o Sia é baseado em blockchain e remunera hosts no SiaCoin. Ao fazer upload de um arquivo, é garantido que ele permanece ativo por um período de 3 meses, e o contrato pode ser renovado automaticamente. Também é de código aberto ( [movido recentemente para o GitLab](https://gitlab.com/NebulousLabs/Sia) ). Embora a Sia ofereça uma API, acredito que seu principal caso de uso é armazenar dados pessoais dos usuários e livrar-se de serviços como o Dropbox ou o Google Drive.


**Preço**: cerca de US $ 0,002 por GB por mês.

**Status**: o Sia está pronto para uso para armazenar arquivos não críticos. No próximo ano, eles planejam melhorar a velocidade, oferecer suporte a armazenamento quente e adicionar um recurso CDN.

**Indo além**: comece a usar a [API (CLI ou JS)](https://blog.sia.tech/api-quickstart-guide-f1d160c05235) ou a [GUI](https://blog.sia.tech/getting-started-with-private-decentralized-cloud-storage-c9565dc8c854) .


## 7. Blockstack

### [Blockstack](https://blockstack.org/)

>Blockstack está construindo um ecossistema que dá aos usuários controle sobre seus direitos digitais fundamentais: Identidade…

[blockstack.org](https://blockstack.org/)

O Blokstack é mais do que armazenamento. É um kit de ferramentas que visa fornecer tudo para criar uma nova internet descentralizada. Por enquanto, ele é composto por um sistema de nomes ( [BNS](https://docs.blockstack.org/core/naming/introduction.html) ), um sistema de armazenamento de arquivos ( [Gaia](https://github.com/blockstack/gaia) ), um sistema de autenticação (você pode usar o mesmo ID do Blockstack em todos os aplicativos criados no Blokstack) e um [navegador da web](https://github.com/blockstack/blockstack-browser) . Vamos nos concentrar na camada de armazenamento.

**Recursos**:

- [Sistema de drivers flexível](https://github.com/blockstack/gaia/tree/master/hub/src/server/drivers) (compatível com os provedores atuais de armazenamento em nuvem).
- Quando usados com o navegador Blockstack, os usuários podem escolher onde armazenar seus dados executando um hub Gaia e usando um driver (em um disco local ou em um provedor de nuvem). O interessante é que a solução de armazenamento que você escolher será usada por todos os aplicativos Blockstack que precisem armazenar dados. Portanto, você controla todos os seus dados, pode fazer backup deles, excluí-los, hospedá-los ou usar terceiros. **Você apenas possui seus dados**!
- [Código aberto](https://github.com/blockstack/gaia).

**Preço**: o provedor de armazenamento padrão é gratuito. Se você deseja armazenar todos os seus dados no S3, pagará as taxas do S3.
Se você é desenvolvedor, a Blockstack acaba de lançar seu programa App Mining: seja pago para desenvolver aplicativos no Blockstack. A partir de dezembro, serão distribuídos US $ 100.000 agregados todos os meses (20% para o primeiro aplicativo classificado, 20% dos 80% restantes para o segundo,…). Isso é muito, e você pode usar esse dinheiro para incentivar os usuários a usar seu aplicativo também (redistribuir parte do dinheiro). Mais informações em https://app.co/mining .


**Status**: Pronto para uso. No início de 2019, o Gaia será lançado como um projeto independente, para que possamos usar a camada de armazenamento em qualquer projeto.

**Indo além**: consulte a documentação do [Gaia README](https://github.com/blockstack/gaia/blob/master/README.md) e do [blockstack.js](http://blockstack.github.io/blockstack.js/) .

## Qual é o próximo?

Bem, agora você tem uma incrível variedade de tecnologias para armazenar seus arquivos, dependendo das necessidades de seu aplicativo. O [próximo capítulo](https://medium.com/@christophe.bougere/a-state-of-the-art-of-decentralized-web-part-3-7d901e09d06f) é sobre descentralizar a lógica do seu aplicativo usando o blockchain.

![](https://hackernoon.com/hn-images/0*_x3PmIQenLw--m3Y.gif)

>Espero que você esteja pronto, porque vai ser complicado

---

Autor: [Christophe Bougère](https://hackernoon.com/@christophe.bougere)

[Artigo Original](https://hackernoon.com/a-state-of-the-art-of-decentralized-web-part-2-ea630917332a)






