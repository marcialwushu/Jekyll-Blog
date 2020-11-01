---
layout: post
title:  "Notarização em Blockchain (Parte 3)"
date:   2020-03-09 17:59:38 -0200
categories: jekyll update
---

## Tipo 3: Transferência de propriedade do documento

O serviço notarial na última parte traz o conceito de propriedade. A propriedade é obtida por um sistema de conta de usuário externo ou contando com terceiros, como o sistema de Autoridade de Certificação em Infraestrutura de Chave Pública (PKI). Na implementação, podemos usar um espaço de dados maior na transação nativa ou capacidade de codificação de contrato em blockchains.

Em alguns cenários, é desejada uma transferência de propriedade . Vamos examinar primeiro os modelos anteriores e ver como eles podem conseguir a transferência de propriedade. Posteriormente, daremos uma olhada em como isso pode ser feito no blockchain do NEM usando seu serviço de notário integrado e conta com várias assinaturas.

### Propriedade registrada no banco de dados

Estamos nos referindo ao mesmo modelo no artigo anterior.

![](https://miro.medium.com/max/700/0*LDzpnDtPgxwRte7m)

Aqui, a propriedade é mantida em um banco de dados fora da cadeia. A mudança de propriedade é surpreendentemente simples: nós simplesmente mudamos o registro.

Diga se estamos alterando o hash gravado em TX ID # 3 para charlie.

![](https://miro.medium.com/max/700/0*ZURvmnQKn9wD8GX1)

Parece simples. Porém, como cartório, usuário e terceiros questionarão novamente a implementação utilizando uma base de dados central e externa. Uma solução descentralizada é mais desejada.

### Propriedade registrada no Blockchain

Todas as outras implementações no artigo anterior, exceto a mencionada acima, são classificadas como abordagem on-chain, ou seja, a propriedade é registrada dentro da blockchain de várias maneiras. Em resumo, eles são um dos seguintes,

1. registrar a ID do usuário no campo de dados dentro da transação e usar a ID da transação para verificação
2. registrar a assinatura criada por um usuário no campo de dados dentro da transação e usar o ID da transação para verificação
3. registrar assinatura em um contrato implantado e usar hash para verificação

Quando os dados são registrados dentro da transação (caso 1 e 2), a transferência da transação significa que uma nova transação é iniciada com o novo ID de usuário ou assinatura. Por exemplo, se o documento (hash) gravado em TX ID # 2 for transferido de Alice para Charles, é uma nova transação (digamos TX ID # 4) gravada em um bloco posterior.

![](https://miro.medium.com/max/700/0*pocINJsW-CbF8tZG)

Como há uma nova transação, a verificação agora está em TX ID # 4 em vez de TX ID # 2 como no passado. Observe que não há mecanismo para relacionar o mesmo hash de documento entre TX ID # 2 e TX ID # 4. Um sistema externo pode ajudar se a proveniência for necessária por documento. Precisamos de TX ID # 2 e # 4 para entender a mudança de propriedade no mesmo documento (hash).

A implementação no código do contrato é muito mais fácil. Uma nova função pode ser adicionada para atualizar o registro. Neste exemplo, temos uma nova função chamada updateRecord () que pode modificar a tabela de estados com uma nova assinatura.

![](https://miro.medium.com/max/700/0*xWZtKbLa3XEZwCNE)

O que acontece quando updateRecord () é chamado? A entrada da tabela de hash de índice é atualizada de acordo.

![](https://miro.medium.com/max/700/0*Y-EIEEuosyh9u0Hg)

Solidity apóia eventos com índice. Portanto, podemos adicionar a emissão de eventos ao sistema externo de forma que a proveniência possa ser facilmente verificada.

### Uma abordagem diferente da NEM: Apostille

O blockchain NEM é um livro-razão público que fornece alguns recursos exclusivos. E esses recursos fornecem uma maneira diferente de lidar com a transferência de propriedade de um documento.

#### Apostille

Apostille é o serviço notarial integrado no blockchain do NEM. Em vez de simplesmente colocar um hash no blockchain como um dado, Apostille cria uma conta de coletor que representa o documento. Essa conta de coletor é como uma conta de usuário normal, tem uma chave privada e, portanto, um endereço público. Podemos considerar, grosso modo, que este arquivo agora é representado como uma conta, com as informações apropriadas registradas em uma transação.

Aqui está como iniciar uma solicitação de serviço de apostilha da Nano Wallet.

![](https://miro.medium.com/max/700/0*QaN_VIxSHQt46pzO)

Depois de selecionar um arquivo (aqui está document.txt), podemos ver um endereço coletor ( TC4PYL… ) e o hash do arquivo é calculado (para ser preciso, um cabeçalho é adicionado na frente do valor real do hash).

Depois de enviarmos tal solicitação para o blockchain NEM e o bloco ser coletado, vemos uma transação registrada no blockchain, que é,

![](https://miro.medium.com/max/700/0*GjRVPBo-ptd03Pyq)

A partir dos detalhes da transação, vemos,

- a transação é iniciada a partir de uma conta primária, que é myFirstAccount na captura de tela acima.
- a transação é enviada para a conta do sink ( TC4PYL… ).
- a mensagem contém o hash do arquivo da imagem acima

e esta transação tem um ID de transação (mostrado como Hash aqui, bb5a63… ).

Para verificar se um determinado documento é o original, precisamos do ID da transação e deste documento fornecido. Recuperamos a mensagem do ID da transação e comparamos os dados registrados com o hash ou o documento fornecido. Se for uma correspondência, o documento é verificado.

### Conta com várias assinaturas

O NEM também oferece suporte nativo a contas com várias assinaturas (multisig). É criado convertendo uma conta normal e atribuindo os co-signatários para esta conta multisig. Durante a conversão, pode-se especificar o requisito de “aprovação” para esta conta, como m de n co-signatários necessários (m <= n). Por exemplo, uma conta multisig pode pertencer a 3 co-signatários e, para uma transação bem-sucedida, são necessárias 2 assinaturas.

![](https://miro.medium.com/max/700/0*i20ET_xdP9HpmeBE)

A conta Multisig, como outras contas, pode possuir XEM e Mosaics (ativos inteligentes em NEM). A única diferença é que a conta multisig não pode iniciar a transação. É um dos co-signatários que inicia a transação em nome, e a transação é processada apenas o número necessário de assinaturas (aprovações) recebidas dos co-signatários.

O co-signatário de uma conta multisig pode ser modificado em uma regra específica que,

- para adicionar mais um co-signatário, são necessárias aprovações de todos os co-signatários existentes.
- para remover um da lista de co-signatários, são necessárias aprovações de todos, exceto aquele a ser removido.

Como um caso especial, se definirmos apenas um co-signatário e uma assinatura exigida, é uma conta multisig 1 de 1 e equivalente a “uma conta possui outra conta (multisig)”.

![](https://miro.medium.com/max/700/0*jDb0ImlL2Q3DFjYG)

De forma equivalente, aqui myFirstAccount possui a conta coletor no documento. myFirstAccount pode realizar todas as execuções em nome desta conta de coletor.

Quando necessário, o proprietário ( myFirstAccount ) pode transferir a propriedade desta conta de coletor para outro. Por exemplo, myFirstAccount transfere a propriedade deste documento (conta de coletor) para mySecondAccount.

![](https://miro.medium.com/max/700/0*-ObF8FOUISGl65aU)


A partir de agora, myFirstAccount não pode mais interagir com o documento (conta de coletor), pois mySecondAccount agora o possui. É assim que a propriedade de um documento (representada pela conta coletor) é transferida.

## Resumo

Vemos várias maneiras de lidar com a transferência de propriedade de um documento no blockchain. Dependendo da implementação, pode ser simplesmente uma atualização em um banco de dados central, uma nova transação no mesmo valor de hash, a execução de uma função para atualizar o registro em um contrato ou uma maneira diferente usando recursos especiais em um blockchain.

---

Autor: [KC Tam](https://medium.com/@kctheservant?source=post_sidebar--------------------------post_sidebar-----------)

[Artigo Original](https://medium.com/@kctheservant/notarization-in-blockchain-part-3-ce176c1ac338)





