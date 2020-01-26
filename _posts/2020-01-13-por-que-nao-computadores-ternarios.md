---
layout: post
title:  "Por que não computadores ternários?"
date:   2020-01-13 17:59:38 -0200
categories: jekyll update
---


![](https://www.techopedia.com/images/uploads/text-word-alphabet-ampersand-building-office-building-logo-trademark.jpg)


>Resumo: a computação ternária depende de "trits" de três estados em vez de bits de dois estados. Apesar das vantagens deste sistema, ele raramente é usado.

Qualquer pessoa familiarizada com a computação digital conhece zeros e uns - incluindo caracteres do desenho animado “Futurama”. Zeros e uns são os blocos de construção da linguagem [binária](https://www.techopedia.com/definition/6144/binary) . Mas nem todos os computadores são digitais, e nada diz que os computadores digitais precisam ser binários. E se usássemos um sistema base 3 em vez da base 2? Um computador poderia conceber um terceiro dígito?

Como observou o ensaísta Brian Hayes, cientista da computação, “as pessoas contam por dezenas e as máquinas contam por dois.” Algumas almas corajosas ousaram considerar uma alternativa [ternária](https://www.techopedia.com/definition/14613/ternary) . Louis Howell propôs a [linguagem de programação TriINTERCAL](https://esolangs.org/wiki/TriINTERCAL) usando o sistema de numeração base 3 em 1991. E os inovadores russos construíram algumas dezenas de máquinas base 3 há mais de 50 anos. Mas, por alguma razão, o sistema de numeração não pegou no mundo da computação.

## Um olhar sobre a matemática

Dado o espaço limitado aqui, apenas tocaremos em algumas idéias matemáticas para nos dar uma base. Para uma compreensão mais aprofundada do assunto, dê uma olhada no excelente artigo de Hayes, “Third Base”, na edição de novembro / dezembro de 2001 da American Scientist.

Agora vamos ver os termos. Você provavelmente já entendeu (se ainda não sabia) que a palavra “ternário” tem a ver com o número três. Geralmente, algo que é ternário é composto de três partes ou divisões. Uma forma ternária na música é uma forma de música composta de três seções. Em matemática, ternário significa usar três como base. Algumas pessoas preferem a palavra trinário, talvez porque rima com binário.

Jeff Connelly cobre mais alguns termos em seu artigo de 2008, “[Ternary Computing Testbed 3-Trit Computer Architecture](http://xyzzy.freeshell.org/trinary/CPE%20Report%20-%20Ternary%20Computing%20Testbed%20-%20RC6a.pdf)”. Um “trit” é o equivalente ternário de um [bit](https://www.techopedia.com/definition/2678/binary-digit-bit) . Se um bit é um dígito binário que pode ter um dos dois valores, um trit é um dígito ternário que pode ter qualquer um dos três valores. Um trit é um dígito base-3. Um "tryte" seria 6 trits. Connelly (e talvez ninguém mais) define "tribble" como meio trit (ou um dígito com base 27) e ele chama um dígito com base 9 como "nit". (Para mais informações sobre medição de dados, consulte [Noções básicas sobre bits, bytes) e seus múltiplos](https://www.techopedia.com/2/29184/development/programming-languages/understanding-bits-bytes-and-their-multiples) .)

Tudo pode se tornar um pouco esmagador para os leigos matemáticos (como eu), então vamos apenas olhar para outro conceito para nos ajudar a entender os números. A computação ternária lida com três estados distintos, mas os próprios dígitos ternários podem ser definidos de maneiras diferentes, de acordo com Connelly:


- Trinário Unbalanced  - {0, 1, 2}
- Trinário Fracionado Unbalanced  - {0, 1/2, 1}
- Trinário Balanceado - {-1, 0, 1}
- Lógica de estado desconhecido - {F,?, T}
- Binário codificado em trinário - {T, F, T}

## Computadores ternários na história

Não há muito a ser abordado aqui, porque, como Connelly disse, “a tecnologia Trinary é um território relativamente inexplorado no campo da arquitetura de computadores ”. Embora possa haver um tesouro escondido de pesquisas universitárias sobre o assunto, poucos computadores de base 3 o fizeram. em produção. Na Superconferência de Hackaday de 2016, Jessica Tank deu uma palestra no computador ternário em que trabalha nos últimos anos. Ainda não se sabe se seus esforços vão aumentar da obscuridade.

Mas nós vamos encontrar um pouco mais se olharmos para trás para a Rússia em meados da década de 20 th século. O computador chamava-se SETUN e o engenheiro era Nikolay Petrovich Brusentsov (1925–2014). Trabalhando com o notável matemático soviético Sergei Lvovich Sobolev, Brusentsov criou uma equipe de pesquisa na Universidade Estadual de Moscou e projetou uma arquitetura de computador ternária que resultaria na construção de 50 máquinas. Como afirma o pesquisador Earl T. Campbell [em seu site](https://earltcampbell.com/2014/12/29/the-setun-computer/) , o SETUN "sempre foi um projeto universitário, não totalmente endossado pelo governo soviético e visto com desconfiança pela gerência da fábrica".


## O caso de ternário

SETUN usou lógica ternária balanceada, {-1, 0, 1} como observado acima. Essa é a abordagem comum ao ternário, e também é encontrada no trabalho de Jeff Connelly e Jessica Tank. "Talvez o sistema numérico mais bonito de todos seja a notação ternária equilibrada", escreve Donald Knuth [em um trecho de seu livro](https://go.skimresources.com/?id=128808X1590707&isjs=1&jv=13.25.4-stackpath&sref=https%3A%2F%2Fwww.techopedia.com%2Fwhy-not-ternary-computers%2F2%2F32427&url=http%3A%2F%2Fwww.informit.com%2Farticles%2Farticle.aspx%3Fp%3D2221791&xguid=aa48571e649f0c02d182970ba1fb2c52&xs=1&xtz=180&xuuid=0685933172c0f4aacc8df00b131dae96) "A arte da programação de computadores".

Brian Hayes também é um grande fã de ternário. “Aqui quero oferecer três aplausos para a base 3, o sistema ternário. … Eles são a opção Goldilocks entre os sistemas de numeração: quando a base 2 é muito pequena e a base 10 é muito grande, a base 3 é perfeita. ”

Um dos argumentos de Hayes para as virtudes da base 3 é que é o sistema de numeração mais próximo da base-e, “a base dos [logaritmos](https://www.techopedia.com/definition/8118/logarithm-ln) naturais , com um valor numérico de cerca de 2.718”. Com destreza matemática, o ensaísta Hayes explica como base-e (se fosse prático) seria o sistema de numeração mais econômico. É onipresente na natureza. E lembro-me claramente dessas palavras do Sr. Robertson, meu professor de química do ensino médio: "Deus conta por e".

A maior eficiência do ternário em comparação ao binário pode ser ilustrada pelo uso do computador SETUN. Hayes escreve: “Setun operava em números compostos por 18 dígitos ternários, ou trits, dando à máquina um intervalo numérico de 387.420.489. Um computador binário precisaria de 29 bits para atingir essa capacidade…. ”

## Então, por que não ternário?

Agora voltamos à pergunta original do artigo. Se a computação ternária é muito mais eficiente, por que não estamos todos usando-a? Uma resposta é que as coisas simplesmente não aconteceram dessa maneira. Chegamos tão longe na computação digital binária que seria muito difícil voltar atrás. Assim como o robô Bender não tem idéia de como contar além de zero e um, os computadores de hoje operam em um sistema lógico diferente do que qualquer computador ternário em potencial usaria. É claro que o Bender poderia, de alguma forma, entender o ternário - mas provavelmente seria mais uma simulação do que um redesenho.

E o próprio SETUN não percebeu a maior eficiência do ternário, segundo Hayes. Ele diz que, porque cada trit foi armazenado em um par de núcleos magnéticos "a vantagem ternária foi desperdiçada". Parece que a implementação é tão importante quanto a teoria.

Uma citação extensa de Hayes parece apropriada aqui:

>Por que a base 3 não conseguiu entender? Um palpite fácil é que dispositivos confiáveis ​​de três estados simplesmente não existiam ou eram muito difíceis de desenvolver. E uma vez que a tecnologia binária se estabelecesse, o tremendo investimento em métodos para fabricar chips binários teria superado qualquer pequena vantagem teórica de outras bases.

## O sistema de numeração do futuro

Nós conversamos sobre bits e trits, mas você já ouviu falar em [qubits](https://www.techopedia.com/definition/2742/quantum-bit-qubit) ? Essa é a unidade de medida proposta para a computação quântica . A matemática fica um pouco confusa aqui. Um bit quântico, ou qubit, é a menor unidade de informação quântica. Um qubit pode existir em vários estados ao mesmo tempo. Portanto, embora possa representar mais do que apenas os dois estados do binário, não é o mesmo que ternário. (Para saber mais sobre a [computação quântica](https://www.techopedia.com/definition/679/quantum-computing), consulte [Por que a computação quântica pode ser a próxima curva na Big Data Highway](https://www.techopedia.com/2/29014/storage/why-quantum-computing-may-be-the-next-turn-on-the-big-data-highway) .)

E você pensou que binário e ternário eram difíceis! A física quântica não é intuitivamente óbvia. O físico austríaco Erwin Schrödinger ofereceu um experimento mental, conhecido como o gato de Schrödinger. Você deve supor por um minuto um cenário em que o gato esteja vivo e morto simultaneamente.

É aqui que algumas pessoas saem do ônibus. É ridículo propor que um gato possa estar vivo e morto, mas essa é a essência da superposição quântica. O ponto crucial da mecânica quântica é que os objetos têm características de ondas e partículas. Os cientistas da computação estão trabalhando para tirar proveito dessas propriedades.

A superposição de qubits abre um novo mundo de possibilidades. Espera-se que os computadores quânticos sejam exponencialmente mais rápidos que os computadores binários ou ternários. O paralelismo de múltiplos estados de qubit poderia tornar um computador quântico milhões de vezes mais rápido que o PC de hoje.

## Conclusão

Até o dia em que a revolução da computação quântica mudar tudo, o status quo da computação binária permanecerá. Quando perguntaram a Jessica Tank que casos de uso poderiam surgir para a computação ternária, a platéia gemeu ao ouvir uma referência à "internet das coisas". E esse pode ser o cerne da questão. A menos que a comunidade de computação concorde com um motivo muito bom para perturbar o carrinho da Apple e peça que seus computadores contem três em vez de dois, robôs como o Bender continuarão pensando e sonhando em binário. Enquanto isso, a era da computação quântica está além do horizonte.

---

Autor: [David Scott Brown](https://www.techopedia.com/contributors/david-scott-brown)

[TECNOPEDIA](https://www.techopedia.com/why-not-ternary-computers/2/32427)
