---
layout: post
title:  "Como programar um computador quântico - Parte 2"
date:   2019-03-24 00:43:31 -0200
categories: jekyll update
---

Navios de guerra com medições quânticas

![IBM Research https://www.flickr.com/photos/ibm_research_zurich/33072160062/](https://miro.medium.com/max/2500/1*kiEAdMgK5BPC1JDLNXNOHw.jpeg)


Este artigo tem "Parte 2" no título por um bom motivo. Havia uma Parte 1, na qual analisamos a base para escrever e executar programas quânticos.

Eu vou assumir que você leu pelo menos a primeira metade antes de vir aqui.

A maior parte do conhecimento real de codificação necessário para este tutorial foi abordado na última vez. Este artigo se concentrará principalmente em algumas das coisas que podemos fazer com esses comandos.

## Como olhar para qubits

Nos programas, temos variáveis. Em algum momento, precisaremos olhar para eles.

Isso pode ser no final do programa quando obtivermos o resultado. Também pode ser durante o programa, quando usamos a variável como parte de uma instrução condicional. De qualquer maneira, isso acontece muito. E ao programar variáveis não quânticas, é um processo bastante normal.

Isso ocorre porque variáveis não quânticas têm valores definidos. Olhá-los apenas nos diz, ou outras partes do programa, qual é o valor. Nada sobre a variável em si mudará.

Isso não se aplica às variáveis quânticas, que podem ter valores indefinidos. Eles podem estar na chamada superposição quântica, o que lhes permite manter múltiplos valores contraditórios ao mesmo tempo.

Quando olhamos para eles, eles têm que desistir de toda essa estranheza. Eles são forçados a assumir um valor definido e depois nos dizem qual é esse valor. Como este não é apenas um processo passivo, ele precisa ser cuidadosamente considerado. E precisa de um nome. Nós chamamos isso de medição.

Neste artigo, exploraremos algumas das propriedades da medição. Também vamos usá-lo como base de uma mecânica de jogo e ver exatamente como programá-lo em um computador quântico. No final, teremos uma nova versão do encouraçado.

## Mapeando o mundo de um qubit

Antes de realmente começarmos a medir qubits, devemos tentar entender um pouco mais o mundo deles. A melhor maneira de visualizar um qubit é usando uma esfera. Qualquer estado de qubit possível corresponde a um ponto na superfície dessa esfera.

Os estados ```0``` e ```1``` são completamente diferentes, completamente disjuntos. Eles são os opostos um do outro. Eles viverão, portanto, em lados opostos da esfera. Geralmente escolhemos colocar ```0``` no polo norte e ```1``` no sul.

Vamos escolher um ponto equidistante entre os dois, em algum lugar ao longo do equador. Pode estar em qualquer lugar que você quiser. Vamos chamá-lo de ```+```. Por que ```+``` ? Por que não?

O estado + também tem um oposto, tão diferente quanto ```0``` é de ```1```. Isso vive no lado oposto, que também será um ponto ao longo do equador. Vamos chamar esse estado ```-``` .

![](https://miro.medium.com/max/553/1*9v7fyO_Tzr0t6bRJ_dDTdA.png)


Com os pontos ```0```, ```1```, ```+``` e ```-``` agora definidos, mais alguns pontos estão implorando por nossa atenção. Estes são os que são equidistantes entre ```0``` e ```1``` e também são equidistantes entre ```+``` e ```-```. Vamos chamar isso de ↻ e ↺. Por quê? Porque uma vez vi um cara que não escreveu o Código Da Vinci fazendo isso e gostei.

Agora, mapeamos o mundo do qubit com seis pontos. Estes não são de forma alguma os únicos que jamais usaremos. Eles são simplesmente os marcos pelos quais navegaremos.


