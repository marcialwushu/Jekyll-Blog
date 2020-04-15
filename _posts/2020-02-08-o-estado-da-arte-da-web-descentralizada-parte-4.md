---
layout: post
title:  "O estado da arte da web descentralizada - Parte 4"
date:   2020-02-08 17:59:38 -0200
categories: jekyll update
---

Este é o quarto e último capítulo de uma série sobre descentralização da web. Como vimos no capítulo anterior , o blockchain e os contratos inteligentes são ótimos para armazenar registros para alguns casos de uso específicos (como transações financeiras), mas eles não substituirão todo o banco de dados. Aqui vamos nos concentrar em **bancos de dados distribuídos e descentralizados** : Quais são os candidatos atuais e como eles se comparam. Em seguida, concluiremos esta série e recuaremos o que aprendemos.

![](https://miro.medium.com/max/1332/0*P34gqgaGo7aTwsmh.png)

>[SQL, que bom velho amigo!](https://xkcd.com/327/)

## Artigos da série

- Introdução
- Armazenamento de arquivo
- Blockchain e contratos inteligentes
- **Bases de dados**

## Introdução

Pela primeira vez, vamos começar com um teorema - o teorema da CAP :


>O teorema do CAP declara que é impossível para um armazenamento de dados distribuído fornecer simultaneamente mais de duas das três garantias a seguir:
>- **Consistency (Consistência)** : cada leitura recebe a gravação ou um erro mais recente
>- **Availability (Disponibilidade)** : toda solicitação recebe um (não erro ) - sem a garantia de que ele contém a gravação mais recente
>- **Partition tolerance (Tolerância de partição)** : o sistema continua a funcionar apesar de um número arbitrário de mensagens serem descartadas (ou atrasadas) pela rede entre os nós
>- [Origem](https://en.wikipedia.org/wiki/CAP_theorem)


Esse teorema não é perfeito, mas é simples e fornece uma idéia rápida da troca de design. Isso nos ajudará a classificar os diferentes candidatos.

Além disso, se você não tem idéia do que estamos falando, aqui está uma boa introdução:


[**Bancos de dados descentralizados e distribuídos, explicados**](https://cointelegraph.com/explained/decentralized-and-distributed-databases-explained)

1. Um banco de dados é uma coleção organizada de informações ou dados. Atualmente, existe um grande fluxo de informações e…

[cointelegraph.com](https://cointelegraph.com/explained/decentralized-and-distributed-databases-explained)

Tudo bom? Agora, vamos dar uma olhada nessas 5 soluções:

1. GUN
2. Fluence
3. Bluzelle
4. BigchainDB
5. Ties.DB

## 1. GUN

https://gun.eco

GUN é:

- Um banco de dados **gráfico em tempo real , descentralizado e offline , primeiro**.
- **AP** : garante **disponibilidade , tolerância de partição** , mas apenas consistência eventual . Isso o torna particularmente interessante em tempo real (bate-papo, jogo online, visualização de sensores ao vivo no IOT,…), mas você provavelmente deve evitar usá-lo quando a consistência for crítica, como no setor bancário. Leia mais [aqui](https://gun.eco/docs/CAP-Theorem).
- **Independente de armazenamento**. Os adaptadores atuais incluem armazenamento de arquivos, armazenamento local (no navegador), IPFS e S3.
- Codificado em **JavaScript** e super fácil de usar (consulte os [documentos da API](https://gun.eco/docs/API) ).
- **Altamente escalável** : capaz de realizar mais de 20 milhões de operações de API/s.
- Apoiado por VC e [levantou US $ 1,5 milhão em 2018](https://techcrunch.com/2018/05/23/gun-raises-more-than-1-5m-for-its-decentralized-database-system/).

O roteiro está disponível [aqui](https://gun.eco/docs/Roadmap).

Observe que o GUN pode ser usado sem nenhum servidor (exceto para a descoberta de pares), mas os dados persistirão apenas no armazenamento local do navegador. Portanto, se você precisar de persistência de dados, sempre mantenha alguns nós em execução.

>O universo não é fortemente consistente

A GUN fez uma troca interessante, concentrando-se na capacidade offline e em tempo real. Se você quer entender por que [esta apresentação](https://gun.eco/distributed/matters.html) explica bem os prós e os contras de uma maneira simples e divertida. O GUN pode não ser adequado para todas as aplicações, mas definitivamente vale a pena dar uma olhada!


## 2. Fluence

[**Fluence network - processamento de dados descentralizado que funciona.**](https://fluence.network/)

Os desenvolvedores podem usar a rede Fluence para criar uma camada de consulta sem confiança sobre as cadeias de bloco, criando dados…

[fluence.network](https://fluence.network/)

A Fluence começou como uma rede de banco de dados descentralizada e [mudou recentemente](https://medium.com/fluence-network/fluence-new-direction-and-the-first-proof-of-concept-cced6e4656e9) para se tornar uma camada de consulta sem confiança sobre a blockchain Ethereum .

>A Fluence cria uma rede independente com seu próprio consenso descentralizado para cada consulta, modelo de segurança e design de criptoeconomia. Essa rede é otimizada para recuperar e processar dados de fontes descentralizadas sem sacrificar a segurança e o desempenho. Bancos de dados, linguagens de consulta e algoritmos arbitrários podem ser criados e implantados na rede Fluence e podem ser executados completamente descentralizados na máquina virtual Fluence.


Com o Fluence, você poderá consultar dados do blockchain e do armazenamento a frio (Ethereum Swarm, IPFS) usando SQL, GraphQL ou uma linguagem de consulta personalizada.

Fluence é CP ( [veja aqui](https://www.reddit.com/r/Fluence/comments/99cvwb/fluence_first_ama/e53bm1k) ). A rede principal deve estar disponível em breve ( [roteiro](https://medium.com/fluence-network/fluence-new-direction-and-the-first-proof-of-concept-cced6e4656e9) ).

Da mesma forma, você pode estar interessado no [**EthQL**](https://github.com/ConsenSys/ethql) , uma interface GraphQL para o Ethereum (que não vou detalhar aqui porque depende de um servidor centralizado).

## 3. Bluzelle

>[**O banco de dados descentralizado para Dapps**](http://bluzelle.com/)

>Adicione Bluzelle à sua pilha de tecnologia, o banco de dados distribuído construído sobre a tecnologia blockchain ethereum; construído por uma…

>[bluzelle.com](http://bluzelle.com/)


Bluzelle fornece um **banco de dados descentralizado de armazenamento de valor-chave NoSQL com uma API CRUD**. De maneira semelhante à de [muitas soluções de armazenamento de arquivos](https://hackernoon.com/a-state-of-the-art-of-decentralized-web-part-2-ea630917332a) , os nós podem ser recompensados com **tokens BLZ** pela hospedagem de dados. Se você é consumidor, usa a mesma criptomoeda para alugar armazenamento de dados no enxame. Bluzelle também é de [código aberto](https://github.com/bluzelle/swarmDB).

Você pode [criar seu próprio cliente](https://devel-docs.bluzelle.com/client-development-guide/) que se comunica com o banco de dados por meio do WebSockets ou usar o [cliente Node.j existente](https://devel-docs.bluzelle.com/bluzelle-js/quickstart) . As [operações disponíveis](https://bluzelle.github.io/api/#js-api) são bastante semelhantes a outros bancos de dados NoSQL.

O Bluzelle ainda está na versão beta e você pode experimentá-lo gratuitamente no TestNet.


## 4. BigchainDB

[**BigchainDB * * O banco de dados blockchain.**](https://www.bigchaindb.com/)

Com alto rendimento, baixa latência, poderosa funcionalidade de consulta, controle descentralizado, armazenamento de dados imutável e…

[www.bigchaindb.com](https://www.bigchaindb.com/)


>Com alto rendimento, baixa latência, poderosa funcionalidade de consulta, controle descentralizado, armazenamento imutável de dados e suporte a ativos embutidos, o BigchainDB é como um banco de dados com características de blockchain.

O BigchainDB apresenta um novo paradigma nos bancos de dados. É focado em ativos (em vez de focado em tabela ou documento) e funciona com 2 tipos de transações: CREATE e TRANSFER:

![](https://miro.medium.com/max/1400/1*jZCRB3wbBprby-ZlvoH2aQ.png)

>[Principais conceitos do BigchainDB](https://www.bigchaindb.com/developers/guide/key-concepts-of-bigchaindb/)

O BigchainDB [agora é gerenciado](https://blog.bigchaindb.com/the-next-evolution-for-bigchaindb-software-a104185a8763) pela [fundação IPDB](https://ipdb.io/), que fornece um TestNet e mantém a base de código-fonte aberto. Um [monte de drivers](http://docs.bigchaindb.com/projects/server/en/latest/drivers-clients/) está disponível em diferentes idiomas, bem como em uma [interface GraphQL](https://github.com/bigchaindb/js-bigchaindb-graphql).

Agora está disponível na [v2.0.0b9](https://github.com/bigchaindb/bigchaindb/releases/tag/v2.0.0b9). Dê uma olhada [nesta introdução](https://www.bigchaindb.com/developers/guide/) se você quiser ir mais longe.

## 5. Ties.DB

[**Primeiro banco de dados público descentralizado para dApps**](https://tiesdb.com/database)

O primeiro banco de dados inteligente público descentralizado do mundo

[tiesdb.com](https://tiesdb.com/database)

>Um banco de dados público, distribuído e descentralizado com um segmento comum: confiança. Reforçada pela tolerância a falhas integrada, esquemas de incentivo e contratos inteligentes.

Como no Bluzelle, o Ties.DB incentiva os nós a processar consultas e hospedar dados, pagando-os em **tokens TIE**. Por enquanto, a rede está integrada ao Ethereum, mas eles planejam se integrar a outras blockchains no futuro. Ties.DB é [AP](https://github.com/TiesNetwork/ties-docs/wiki/Where-do-decentralized-applications-store-their-data%3F#distributed-databases). Você pode tentar a versão alfa [aqui](https://github.com/TiesNetwork/ties.db/releases/tag/0.1.2-ALPHA).

Você pode usar o [cliente Node.js](https://github.com/TiesNetwork/ties-docs/wiki/Usage-examples-%28NodeJS%29). (com algumas funções como ```putField```) ou buscar seus dados usando [TiQL](https://github.com/TiesNetwork/ties-docs/wiki/TiQL) (uma linguagem de consulta semelhante a SQL).

Ponto de bônus por oferecer uma [GUI amigável](https://github.com/TiesNetwork/ties.db-explorer/releases/tag/v0.1-alpha) (algo semelhante ao phpMyAdmin for MySQL):


![](https://miro.medium.com/max/1400/0*hLldtP1w5_E7cuaU.png)


>[Ties.DB explorer](https://github.com/TiesNetwork/ties.db-explorer)


## Conclusão

Examinamos os três blocos mais importantes da web descentralizada:

- Como armazenar arquivos
- Como obter um consenso
- Como armazenar dados relacionais

Então, qual é o estado atual dessas tecnologias? Você deve iniciar seu novo projeto de maneira descentralizada?

Bem, na minha opinião ... depende do seu projeto. Ainda estamos em um estágio muito inicial de descentralização da web, e é um paradigma totalmente novo comparado à web atual.

Se você estiver trabalhando em algo experimental, escolha e escolha qualquer uma dessas tecnologias. Você aprenderá muito. Embora algumas ferramentas ainda sejam instáveis ​​no momento, elas devem melhorar com o tempo e você fará parte dela!

Se seu projeto não visa gerar renda, mas você precisa armazenar uma grande quantidade de dados, eu recomendaria descentralizar a camada de armazenamento no IPFS. Você economizará muito dinheiro e ainda terá algo extremamente escalável. Você pode solicitar à sua comunidade que hospede alguns nós IPFS. Além disso, se o seu projeto morrer por algum motivo, os usuários ainda poderão ter acesso aos dados no IPFS.


Se o seu projeto precisar de dados em tempo real, mas não exigir consistência forte (como em um bate-papo), considere usar o GUN. É muito bom de usar, parece bastante estável e já está sendo usado por grandes dApps.

Em relação ao blockchain, [2018 viu muitos projetos realmente interessantes morrerem](https://www.technologyreview.com/s/612507/ethereum-thinks-it-can-change-the-world-its-running-out-of-time-to-prove-it/). Na maioria das vezes, o motivo não era "A blockchain é uma boa opção para esse fim?" mas "Vale a pena oferecer toda a complexidade que o blockchain traz para esse fim?". Eu acredito fortemente que o blockchain continuará evoluindo e melhorando nos próximos anos. No entanto, provavelmente levou alguns anos muito cedo para começar a usá-lo para todos os fins. Ainda existem algumas boas razões para iniciar um projeto usando o blockchain, cabe a todos equilibrar. Mas se você estiver disposto a usar o blockchain apenas para fins de rastreabilidade, algo como o BigchainDB provavelmente poderá fornecer o que você precisa de uma maneira mais simples.


Além disso, eu recomendo que você fique de olho em alguns projetos que estão desenvolvendo uma camada de abstração, facilitando muito a integração dos desenvolvedores com tecnologias descentralizadas. Eles ainda são jovens, mas se puderem cumprir o que prometem, construir um dApp será tão fácil quanto desenvolver um aplicativo normal! Aqui estão os meus 3 favoritos:

- [**DADI**](https://dadi.cloud/) : O provedor de nuvem descentralizado. Seu roteiro inclui armazenamento, camada de computação, CDN, API, filas e tudo o que você precisa.
- [**Blockstack**](https://blockstack.org/) : como no DADI, mas limitado à identidade e armazenamento.
- [**Textile**](https://github.com/textileio/) : Ao criar seu [dApp de fotos](https://www.textile.photos/) sobre o IPFS, eles enfrentaram muitos problemas, como gerenciamento de identidade, fixação de arquivos no IPFS, notificações, como fazê-lo funcionar em dispositivos móveis,… Todas essas coisas estão disponíveis em sua estrutura [go-textile](https://github.com/textileio/go-textile) . Eles também fornecem um [SDK do React Native](https://github.com/textileio/react-native-sdk).

![](https://miro.medium.com/max/998/0*RmZYqFoLMit_B3Uz.gif)


---

Autor: [Christophe Bougère](https://medium.com/@christophe.bougere?source=follow_footer--------------------------follow_footer-)

[Artigo Original](https://medium.com/hackernoon/a-state-of-the-art-of-decentralized-web-part-4-212732f74894)








