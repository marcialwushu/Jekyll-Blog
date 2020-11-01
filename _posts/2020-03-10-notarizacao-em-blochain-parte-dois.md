---
layout: post
title:  "Notarização em Blockchain (Parte 2)"
date:   2020-03-10 17:59:38 -0200
categories: jekyll update
---

## Tipo 2: Prova de existência e propriedade de um documento

No tipo anterior de serviço notarial, ou o que chamamos de serviço de Prova de Existência, após o processo de verificação, temos a certeza de dizer que o determinado documento existe desde um determinado momento com base no ID da transação. No entanto, não podemos dizer quem é o proprietário deste documento.

Agora estamos introduzindo outro tipo de serviço notarial que pode atender a esse requisito. Além da prova de existência, também queremos saber a quem pertence este documento.

### Alguma informação sobre o proprietário do documento?

Vamos revisitar a transação que mostramos anteriormente.

![](https://miro.medium.com/max/700/0*fiu1idvn5bLiN37V)

>Saída do explorador de blockchain Bitcoin

Entre todos os informar um ção registrado nesta transação, o único pedaço de informação que pode estar relacionado ao proprietário é o iniciador de transação, isto é, o endereço que fez esta transação. Nesta transação, é o endereço 1Jh65a… .

No entanto, existem alguns problemas se considerarmos este endereço como o proprietário.

1; No caso de ser um blockchain baseado em transação (não baseado em conta) como o blockchain Bitcoin aqui, a carteira sempre gera novos endereços para lidar com a transação. Portanto, é totalmente impossível relacionar um endereço ao proprietário desse endereço.
2. Em blockchain baseado em conta como Ethereum e NEM, a transação é iniciada por uma conta que pode permanecer a mesma. No entanto, o endereço geralmente é propriedade do provedor de serviços notariais, e não do usuário real. Novamente, não podemos dizer do iniciador da transação quem é o proprietário deste documento.

Obviamente, para vincular o proprietário a um documento, precisamos de um sistema para identificar quem é o usuário antes que o hash do documento seja registrado, ou pelo menos podemos vincular o registro a um usuário.

### Sistema de conta de usuário

Sem alterar o mecanismo no nível de transação do blockchain, a maneira mais direta é manter um registro entre uma conta de usuário e o registro da transação em algum lugar externo.

Muitos serviços notariais hoje requerem primeiro uma conta de usuário ou a criação de uma conta de login. Depois que uma conta é configurada, um mapa entre o ID da transação e o ID do usuário é mantido em um banco de dados. Com esse banco de dados, os provedores de serviço podem saber quem é o proprietário do documento com base no ID da transação.
Este é o modelo de uso de sistema de conta de usuário externo.


![](https://miro.medium.com/max/700/0*NmhAOfMVn_wzlOfm)

>Use banco de dados fora da cadeia para lidar com a propriedade

É quase a maneira mais simples de associar um proprietário ao documento. No entanto, podemos ver alguns desafios aqui.

1. O prestador de serviços notariais assume toda a responsabilidade pela gestão da conta do usuário. A reputação deste provedor de serviços determinará o nível de confiança da propriedade do documento. Minha confiança na propriedade do documento é porque confio neste provedor de serviços notariais.
2. O sistema de conta de usuário geralmente é implementado fora do sistema blockchain. Esta não é mais uma forma descentralizada. Essa abordagem centralizada está sujeita a muitas ameaças, como moderação de registros, negação de serviço distribuída (DDoS), ponto único de falha etc. Isso de alguma forma reduz o nível de confiança geral, embora parte do serviço esteja em blockchain.

### Mais informações no registro de transação

Outra solução óbvia é adicionar mais informações na transação.

No sistema de prova de existência, colocamos apenas o hash do documento. O que acontece se adicionarmos algumas informações mais relevantes nos dados da transação?
Um exemplo é adicionar o ID do usuário e o hash do documento em uma transação. Ele pode ser representado como um objeto em JSON (JavaScript Object Notation). Por exemplo,



![](https://miro.medium.com/max/552/0*DQDPCHhVJqr3qhCP)


Como mais espaço para dados é necessário na transação, precisamos do blockchain que suporte maior espaço para dados. Por exemplo, no Ethereum não há limite para o tamanho dos dados, mas a limitação é para o gás máximo por bloco. No NEM, o espaço de dados é de 1k Byte.

É assim que funciona esse modelo. Dado um TX ID, o registro é recuperado do blockchain. A partir dos dados recebidos, o hash do documento é recuperado para verificação de integridade do documento e o campo de ID do usuário é recuperado para verificação cruzada de quem é o proprietário deste documento.


![](https://miro.medium.com/max/700/0*k-8gJcQaj_n6Vn1l)

>A propriedade agora está dentro do registro da transação e mapeada para o banco de dados da conta do usuário.

Observe que neste modelo ainda temos um sistema de gerenciamento de contas de usuário para manter o ID do usuário. Opcionalmente, podemos remover a dependência de tal sistema por criptografia de chave pública: em vez de registrar a conta do usuário no primeiro dia, os dados gravados no blockchain contêm uma assinatura assinada pelo proprietário e podem ser verificados quando a chave pública do proprietário está disponível e confiável.

Aqui está JSON para usar assinatura em vez de ID de usuário externo:

![](https://miro.medium.com/max/700/0*Ck0KTxD-otpFlqZE)

O modelo de trabalho é semelhante a este e como a verificação funciona por um determinado ID de transação.

![](https://miro.medium.com/max/700/0*o3DG6lZZVj7hi5Ka)

>Usando assinatura para identificar o usuário.

De onde vem o par de chaves? Existem duas opções:

- use o sistema de conta nativa em blockchain: Quase a conta de usuário em todas as implementações de blockchain tem chave privada e par de chave pública.
- use Public Key Infrastructure (PKI): Na PKI, cada usuário recebe uma chave privada e um certificado. O certificado contém a identidade do proprietário do certificado e a chave pública. E este certificado em si é emitido por uma Autoridade de Certificação (CA) que fornece um certo nível de confiabilidade.

A implementação do uso da conta nativa no blockchain é bastante simples, pois não precisamos regenerar o par de chaves para este propósito. Mas a associação de assinatura depende do proprietário da chave privada, não do indivíduo real. Por outro lado, usando a PKI, a CA fornece um nível de garantia para o proprietário do certificado como indivíduo. Mas a PKI requer mais processo tanto na emissão quanto na verificação do certificado, e o nível de confiança agora é movido para a CA. Qualquer problema que aconteça nessa CA em particular terá impacto direto sobre o proprietário da identificação.

### Usando contrato inteligente

Todas as implementações acima ainda dependem do campo de dados dentro da transação. Alternativamente, isso também pode ser implementado em contrato se a plataforma blockchain fornecer capacidade de contrato. Isso adiciona certa flexibilidade ao projetar o aplicativo geral em comparação com as informações estáticas registradas em um registro de transação.

Uma plataforma comum é Ethereum. Ethereum permite a execução de código em uma Máquina Virtual Ethereum (EVM) que pode executar lógicas definidas no código. A linguagem de programação é Solidity in Ethereum world.

Aqui está um exemplo de contrato notarial em Solidity. Neste código de contrato,

- uma estrutura de dados de mapeamento com hash de documento como índice
- o registro de dados neste mapeamento inclui a assinatura e o carimbo de data/hora
- duas funções são definidas: getRecord () obtém um registro com base em um valor hash e writeRecord () grava um registro de assinatura e carimbo de data / hora com valor hash como índice


![](https://miro.medium.com/max/700/0*90Gqnvb5B64qy0td)

É assim que funciona o modelo e o processo de verificação do hash de um determinado documento.

![](https://miro.medium.com/max/700/0*RZqfXjvPBvpfonW7)


Observe o uso do código do contrato no Ethereum

- O contrato pode ser considerado uma camada acima do blockchain. Embora a transação ainda seja tratada na camada de blockchain (mineração), podemos ver o contrato como um sistema separado.
- Depois que o contrato é implementado, um ID de contrato é gerado. O ID do contrato é onde o aplicativo externo pode executar funções dentro do contrato.
- Como os dados não estão nativamente no registro da transação, não usamos o ID da transação para obter os dados. Em vez disso, estamos usando o hash do documento como índice para pesquisar os dados armazenados dentro do contrato.
- Um campo de carimbo de data / hora é adicionado. É porque não estamos usando TX ID para a verificação. A maneira mais fácil é incluir o carimbo de data / hora diretamente no registro. A partir do código do contrato, isso é feito usando uma palavra-chave “agora”.

Uma vantagem de usar o contrato para implementar o serviço notarial é a flexibilidade de processamento dos dados. Isso torna o desenvolvimento de aplicativos muito mais fácil. A desvantagem é que os dados não estão nativamente no blockchain e o verificador precisa do ID do contrato e da interface apropriada para obter os dados. Além disso, o proprietário do contrato se torna, de alguma forma, um ponto centralizado do projeto geral.

## Resumo

Este é o segundo tipo de serviço notarial. Além da existência de um documento, este serviço fornece um meio de vincular a propriedade a esse documento. À medida que mais dados são necessários, isso pode ser implementado em cadeias de blocos que permitem maior espaço de dados nos registros de transação. Alternativamente, isso também pode ser implementado com o código do contrato se o blockchain oferecer suporte à execução do contrato.
No próximo artigo falaremos como a propriedade pode ser transferida.

---

Autor: [KC Tam](https://medium.com/@kctheservant?source=post_sidebar--------------------------post_sidebar-----------)

[Artigo Original](https://medium.com/@kctheservant/notarization-in-blockchain-part-2-1a06d00eb72)



