---
layout: post
title:  "Notarização em Blockchain (Parte 1)"
date:   2020-03-11 17:59:38 -0200
categories: jekyll update
---

Neste artigo de três partes, examinaremos vários tipos de reconhecimento de firma usando blockchain público. Os tipos incluem (1) prova da existência de um documento, (2) prova da existência e propriedade de um documento e (3) transferência da propriedade de um documento autenticado. Blockchains mencionados incluem Bitcoin, Ethereum e NEM.


## visão global

A notarização é sempre considerada um dos casos de uso que as tecnologias de razão distribuída (DLT) podem fornecer ou mesmo interromper. Embora em curto prazo não vejamos a substituição completa por tecnologia, existem algumas implementações que já prestam serviços notariais ao público.

Nesta série de artigos, vamos dar uma visão de alto nível no serviço notarial e DLTs, e examina os vários níveis de serviços notariais que podem ser entregues.

*(Observação: a partir de agora usarei blockchain em vez de DLT. Blockchain é um tipo de implementação e de longe o principal, embora os serviços notariais descritos abaixo também possam ser implementados em DLT não blockchain.)*

*(Nota novamente: o estudo do notário é inspirado em um artigo escrito por Sean e você pode encontrá-lo [aqui](https://decentralize.today/does-notarization-on-the-blockchain-actually-work-d8006443c0b9) . A partir deste artigo, estou explorando mais alguns modelos de serviços notariais disponíveis em outros blockchains.)*


## Notarização e Blockchain: uma introdução

De acordo com a National Notary Association ( [link](https://www.nationalnotary.org/knowledge-center/about-notaries/what-is-notarization) ),

>“A notarização é o processo oficial de dissuasão de fraudes que garante às partes de uma transação que um documento é autêntico e confiável. É um processo de três partes, executado por um Tabelião Público, que inclui verificação, certificação e manutenção de registros. ”

Na vida real, notarização é relevante para a lei. O tabelião desempenha um papel importante em todo o processo bem definido e o resultado é juridicamente vinculativo.
As pessoas continuam pensando em como usar a tecnologia da informação para obter capacidade semelhante. É altamente esperado que o surgimento e o desenvolvimento do blockchain facilite, senão interrompa o reconhecimento de firma.

A tecnologia Blockchain garante a integridade dos dados, uma vez gravados na cadeia. As promessas como resistência à violação, não repúdio e sua rastreabilidade tornam o blockchain um bom candidato para fornecer alguns dos recursos de notarização.

Existem diversos serviços notariais disponíveis no mercado. Eles têm certa semelhança em termos de oferta de serviço e também algumas diferenças, pois estão usando diferentes implementações de blockchain. Entre eles, o blockchain público é o mais preferido. Um serviço construído em cima de um blockchain privado pode estar sujeito ao encerramento do serviço por uma única organização. O blockchain público oferece melhor resiliência contra ataques como negação de serviço distribuída (DDoS).
Vamos examinar três tipos de serviços notariais, desde um simples até um mais complicado em termos de funções e requisitos de implementação.

Observe que esses serviços não podem substituir diretamente os serviços notariais existentes de acordo com a lei. Os serviços aqui por todos os meios para facilitar ou potencializar parte de todo o processo. Se eles são aceitáveis ​​em países, está sujeito à lei. Simplesmente nos concentramos em seus aspectos técnicos e mecanismos de implementação.


## Tipo 1: Prova de Existência

Este é o mais básico, mas ainda assim o reconhecimento de firma mais comum usando blockchain: para provar a existência de um documento desde um tempo. Qualquer modificação do documento pode ser detectada e podemos facilmente dizer a partir do carimbo de data/hora quando este documento começa a existir.
Este processo envolve duas etapas: hash do documento e manutenção de um registro no blockchain.

### Hashing do documento

Em vez de colocar todo o documento no blockchain, uma maneira mais prática é colocar o hash do documento. É devido a

1. a maioria dos blockchains vem com espaço de dados limitado.
2. pode ser muito caro se todo o documento for escrito, embora o blockchain suporte isso.
3. privacidade de dados sobre o documento.

O hash promete os seguintes recursos.

1. O mesmo documento sempre produzirá o mesmo resultado hash.
2. O resultado hash sempre tem um comprimento fixo, não importa o tamanho da entrada do documento.
3. Qualquer alteração de documento terá um valor de hash totalmente diferente e, portanto, pode ser detectada.
4. É impossível recuperar o documento original do resultado hash.

O hash é implementado como algoritmos abertos e qualquer pessoa pode implementá-lo em qualquer lugar. Um algoritmo comum é SHA256. Qualquer um pode fazer o “hash” de um documento de qualquer computador e usando qualquer idioma de programação. Um comum é feito no navegador: o hash é calculado sem enviar o documento para um repositório.

Aqui está um exemplo de como uma pequena mudança de documento (de T maiúsculo para t minúsculo) resultará em um valor hash totalmente diferente. Estamos usando o algoritmo SHA256.

![](https://miro.medium.com/max/700/0*ayTVeod11qBZgDcZ)

>O algoritmo de hash pode detectar até mesmo uma pequena alteração em um documento.

O hash é, portanto, amplamente aceito e implementado em quase todos os serviços notariais e sistemas de prova de existência.

Se um provedor de serviços mantém o documento de origem ou não, depende do modelo de negócios. Alguns podem fornecer repositório de documentos e, portanto, podem verificar a integridade dos dados sob demanda ou regularmente. Outros podem considerar isso indesejável quando a privacidade de dados é uma grande preocupação. Manter ou não o documento não tem impacto nas próximas discussões.


### Gravando no Blockchain

Assim que o resultado do hash for calculado, ele será gravado no blockchain. Como cada blockchain é construído com seu próprio propósito, a implementação pode ser um pouco diferente.

No tipo de serviço de prova de existência, apenas o valor hash é armazenado no blockchain. O requisito de espaço de dados é bastante baixo e, portanto, quase todos os blockchain podem lidar com isso.

Vários serviços notariais implementados na rede Bitcoin. O método é bastante simples: gaste um pequeno pagamento em bitcoin para o minerador processar o registro e coloque o valor de hash usando o recurso OP_RETURN.


A transação retorna um ID de transação. E este é o ID da transação associado ao hash que acabou de ser escrito no blockchain.

Aqui está o modelo.

![](https://miro.medium.com/max/700/0*RdAJI6rx7yd_CmL2)

Aqui é retirado de stampd.io ( [link](https://stampd.io/) ), um provedor de serviços de notário, que usa essa abordagem para registrar a rede Bitcoin. Vemos que o ID da transação foi retornado ( 7c3b97 ... )

![](https://miro.medium.com/max/700/0*_eWT6HBvOpaSRNOI)

>fonte: http://stampd.io/wp-content/uploads/2015/02/stampd_PDF_Receipt_Sample.pdf

Há mais alguns detalhes técnicos sobre o documento.

![](https://miro.medium.com/max/700/0*C7hJQ2atwoJnKPbU)

>fonte: http://stampd.io/wp-content/uploads/2015/02/stampd_PDF_Receipt_Sample.pdf

Aqui nós vemos,

1. O resultado hash do documento original ( 65728d… ).
2. O que está escrito no blockchain Bitcoin. Geralmente é o valor hash com um cabeçalho exclusivo (aqui é STAMPD ## para stampd.io).
3. Depois que esta transação é extraída no blockchain Bitcoin, esta transação é incluída em um bloco (o número do bloco aqui é 342489 ).
4. O ID da transação ( 7c3b97… ) é o mesmo que vemos acima.

### Verificação

Desde que o blockchain ainda esteja ativo e em execução, usando o ID de transação, sempre é possível recuperar o hash gravado no blockchain. Se recebermos um documento e desejarmos verificar se este é o original, podemos comparar o hash calculado do documento fornecido com este registro. Se o valor do hash for idêntico, o documento é exatamente o documento original cujo hash foi registrado anteriormente. Também a partir do ID da transação, podemos obter o momento em que a transação foi concluída. Isso serve como um carimbo de data/hora, como uma prova de quando o documento original é hash e gravado.

O detalhe técnico acima também mostra como verificar isso com base no ID da transação. Aqui está um dos vários links.

<https://blockchain.info/tx/7c3b974209609c6d10a6ad8d2bbff4e3ca4f695287c527a8d9bfff7dcab63b62>

É um explorador de blockchain público, não algo fornecido pelo provedor de serviços (stampd.io). O ID da transação está embutido no URL. Mesmo stampd.io não está mais em serviço, o registro ainda está no blockchain do Bitcoin e ainda pode ser verificado a qualquer momento.

Aqui está a saída do link.

![](https://miro.medium.com/max/700/0*xErZuEOHwoe1OIlH)

>Usando o ID da transação, o registro pode ser encontrado no explorador de blockchain Bitcoin

O que vemos do explorador de blockchain é que,

1. Este ID de transação é encontrado no blockchain Bitcoin.
2. A Hora Recebida serve como um carimbo de data / hora onde esta transação foi feita.
3. O Script de Saída mostra os dados sendo gravados em blockchain Bitcoin.
4. Os dados contêm (a) cabeçalho e (b) o valor hash, começa com 65728d...
5. Este valor hash é usado para verificar um determinado documento.


## Resumo

Este é o primeiro tipo de serviço notarial, principalmente na comprovação da existência de determinado documento com carimbo de data/hora. Como é bastante simples, o requisito de blockchain não é alto. Mesmo o blockchain de Bitcoin, que fornece um pouco de espaço para gravar dados, é bom o suficiente para esse tipo de serviço.

No próximo artigo falaremos sobre a prova de existência de documento com informações de propriedade.


---

Autor: [KC Tam](https://medium.com/@kctheservant?source=post_sidebar--------------------------post_sidebar-----------)


[Artigo Original](https://medium.com/@kctheservant/notarization-in-blockchain-part-1-a9795f19e28d)









