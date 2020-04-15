
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


