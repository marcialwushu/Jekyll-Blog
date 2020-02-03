---
layout: post
title:  "Se Hemingway escrevesse JavaScript"
date:   2020-01-18 17:59:38 -0200
categories: jekyll update
---


>O artigo a seguir foi escrito pelo meu bom amigo e colega, [Angus Croll] (// twitter.com/angustweets). Angus trabalha na equipe principal da web no twitter, fala em conferências em todo o mundo e executa um [blog] incrível (// javascriptweblog.wordpress.com) em javascript. Além disso, ele também é um grande nerd de livros, então achei que seria divertido fazê-lo escrever sobre código a partir dessa perspectiva. Confira! E deixe-nos saber o que você pensa no [twitter] (// twitter.com/angustweets)!

O novo livro “[If Hemingway Wrote JavaScript ](https://www.amazon.com.br/Hemingway-Wrote-JavaScript-Angus-Croll/dp/1593275854)” será lançado em setembro de 2014


Eu amava literatura muito antes de escrever uma linha de código. Agora eu escrevo JavaScript, muito e estou escrevendo um livro sobre isso.

O que é o JavaScript que atrai tantos devotos da literatura? Eu tenho algumas teorias incompletas relacionadas ao potencial expressivo de uma sintaxe limitada, mas isso é para outra época. E os grandes escritores? O que eles teriam feito com JavaScript? Mesmo sendo um louco de longa data de Hemingway, eu seria o primeiro a admitir que o pai provavelmente odiaria a programação (e os programadores). No entanto, estou apostando que, entre todo esse desprezo geral, haveria um ponto fraco para o JavaScript, porque é o tipo de linguagem dele, estou certo? Uma superfície sobressalente e enganosamente plana, mascarando substância e drama embaixo.

 
 ## A Mãe de todas as revisões de código
 
 ![](https://trello-attachments.s3.amazonaws.com/5d7e8031eaec3e42c24aade0/5e376a07663eaa488ffabb77/793467a98b4d36a06cd811444bc4b331/inline_fat_24192442505358_raw.png)
 
Recentemente, tive um sonho em que pedi a Hemingway e quatro outras luminárias literárias que escrevessem algum JavaScript para mim; especificamente uma função que retornou uma série de fibonacci de um determinado comprimento. Curiosamente, cada autor optou por resolver o problema de uma maneira diferente. Na verdade, eles se saíram muito bem - até onde eu sei, todas as soluções funcionam como anunciadas (sim, até a de Andre Breton). Aqui está o que eu tenho:
 
 ## Ernest Hemingway
 
 
 ```js
function fibonacci(size) {

  var first = 0, second = 1, next, count = 2, result = [first, second];

  if(size < 2)
    return "the request was made but it was not good"

  while(count++ < size) {
    next = first + second;
    first = second;
    second = next;
    result.push(next);
  }
  return result;
}
```

Não há surpresas aqui. Código reduzido ao essencial, sem desperdício de palavra ou variável. Não é chique; talvez seja até um pouco pedante - mas essa é a beleza dos escritos de Hemingway. Não há necessidade de lógica elaborada ou nomes de variáveis ​​inteligentes. É simples e claro, e faz o que precisa - e nada mais.

Hemingway não sofreu tolos de bom grado, por isso, se você pedir uma série com menos de dois números, ele simplesmente o ignorará. "Estou cansado e essa pergunta é idiota".

## William Shakespeare

```js
function theSeriesOfFIBONACCI(theSize) {

  //a CALCKULATION in two acts.
  //employ'ng the humourous logick of JAVA-SCRIPTE

  //Dramatis Personae
  var theResult; //an ARRAY to contain THE NUMBERS
  var theCounter; //a NUMBER, serv'nt to the FOR LOOP

  //ACT I: in which a ZERO is added for INITIATION

  //[ENTER: theResult]

  //Upon the noble list bestow a zero
  var theResult = [0];

  //ACT II: a LOOP in which the final TWO NUMBERS are QUEREED and SUMM'D

  //[ENTER: theCounter]

  //Commence at one and venture o'er the numbers
  for (theCounter = 1; theCounter < theSize; theCounter++) {
    //By divination set adjoining members
    theResult[theCounter] = (theResult[theCounter-1]||1) + theResult[Math.max(0, theCounter-2)];
  }

  //'Tis done, and here's the answer.
  return theResult;

  //[Exuent]
}
```

O Bardo fica um pouco prolixo aqui, mas não teríamos outra maneira. Observe como os comentários (exceto as legendas dos titulares e as direções do palco) são escritos em pentâmetro iâmbico - um metro de dez sílabas emparelhadas, com o estresse caindo na segunda sílaba de cada par (ou pé ). Em suas peças, Shakespeare geralmente acrescenta ênfase dramática ao desviar-se do pentâmetro iâmbico estrito - ele pode adicionar uma sílaba extra ou usar um estresse alternativo. Parece que ele está usando o mesmo truque neste exercício de codificação. Muito bem, Will.

## Andre Breton

```js
function Colette(umbrella) {
  var staircase = 0, galleons = 0, brigantines = 1, armada = [galleons, brigantines], bassoon;
  Array.prototype.embrace = [].push;

  while(2 + staircase++ < umbrella) {
    bassoon = galleons + brigantines;
    armada.embrace(brigantines = (galleons = brigantines, bassoon));
  }

  return armada;
}
```

Como membro fundador do movimento surrealista, Breton acreditava que os sonhos eram mais interessantes que a realidade e deveriam formar a base de nossos esforços criativos. Substantivos são escolhidos de acordo. Embora seja fácil derrotar Breton, seu trabalho envelheceu bem e é invariavelmente sincero e bonito - uma ressurgência inconsciente de imagens dobrada em sua própria expressão consciente. Aqui está uma tradução do lindo poema Facteur Cheval .

Breton provavelmente nomeou seu exercício de fibonacci em homenagem a uma chama antiga, enquanto ele imagina a coleção resultante como uma frota de navios antigos. A solução é sublinhada pela lógica caracteristicamente elegante - ele está usando um operador de vírgula para alternar simultaneamente elementos entre galeões, brigantinos e fagotes. Tiremos o chapéu Andre!

## Roberto Bolano

```js

function LeonardoPisanoBigollo(l) {

  if(l < 0) {
    return "I'd prefer not to respond. (Although several replies occur to me)"
  }

  /**/

  //Everything is getting complicated.
  for (var i=2,r=[0,1].slice(0,l);i<l;r.push(r[i-1]+r[i-2]),i++)

  /**/

  //Here are some other mathematicians. Mostly it's just nonsense.

  rationalTheorists = ["Archimedes of Syracuse", "Pierre de Fermat (such margins, boys!)", "Srinivasa Ramanujan", "Rene Descartes", "Leonhard Euler", "Carl Gauss", "Johann Bernoulli", "Jacob Bernoulli", "Aryabhata", "Brahmagupta", "Bhaskara II", "Nilakantha Somayaji", "Omar Khayyám", "Muhammad ibn Mūsā al-Khwārizmī", "Bernhard Riemann", "Gottfried Leibniz", "Andrey Kolmogorov", "Euclid of Alexandria", "Jules Henri Poincaré", "Srinivasa Ramanujan", "Alexander Grothendieck (who could forget?)", "David Hilbert", "Alan Turing", "von Neumann", "Kurt Gödel", "Joseph-Louis Lagrange", "Georg Cantor", "William Rowan Hamilton", "Carl Jacobi", "Évariste Galois", "Nikolay Lobachevsky", "Rene Descartes", "Joseph Fourier", "Pierre-Simon Laplace", "Alonzo Church", "Nikolay Bogolyubov"]

  /**/

  //I didn't understand any of this, but here it is anyway.
  return r

  /**/

  //Nothing happens here and if it does I'd rather not talk about it.
}

```

Se você não lê pelo menos um livro de Bolano antes de morrer, desperdiça sua vida. Os escritos de Bolano são notáveis; ao mesmo tempo sem esforço sofisticado e charmosamente ingênuo - seu estilo narrativo é caracterizado por uma honestidade desarmante e cativante. Nenhum aspecto da fragilidade humana está fora dos limites, mas o calor e o humor com os quais todos os inimigos são transmitidos são ao mesmo tempo envolventes e edificantes.

Fiel à sua forma, o exame de Roberto é repleto de admissões de insegurança, vergonha e ignorância. A solução, embora brilhante, é apresentada como uma reflexão tardia. Sempre o obsessivo, sempre tangencial, ele é muito mais feliz, oferecendo-nos uma lista levemente interessante, mas finalmente inútil, de gênios matemáticos.

Existem outros traços de Bolano aqui - a justaposição de parágrafos longos e curtos, a ausência de ponto-e-vírgula (espelhando a ausência de aspas em seus romances) e o uso de globais implícitos - sugerindo que cada variável está destinada a fazer novas aparições em subseqüentes capítulos.

## Charles Dickens

```js
function mrFibbowicksNumbers(enormity) {
  var assortment = [0,1,1], tally = 3, artfulRatio = 1.61803;

  while(tally++ < enormity) {
    //here is an exceedingly clever device
    assortment.push(Math.round(assortment[tally-2] * artfulRatio));
  }

  //should there be an overabundance of elements, a remedy need be applied
  return assortment.slice(0, enormity);
}
```

Eu não sou fã de Dickens. Concordo principalmente com a avaliação condenatória de Henry James:

“Se pudermos arriscar uma definição de seu caráter literário, deveríamos chamá-lo de o maior dos romancistas superficiais. Estamos cientes de que essa definição o limita a uma posição inferior no departamento de cartas que ele adorna; mas aceitamos essa conseqüência de nossa proposição. Foi, em nossa opinião, uma ofensa à humanidade colocar o Sr. Dickens entre os maiores romancistas. Pois, para repetir o que já sugerimos, ele criou nada além de figura. Ele não acrescentou nada ao nosso entendimento do caráter humano. ”

- Henry James, sobre Charles Dickens, em uma resenha de Our Mutual Friend, em The Nation, 21 de dezembro de 1865:

A superficialidade de Boz é confirmada por sua solução de fibonacci. Sim, existem alguns nomes levemente divertidos, mas uma completa falta de substância e entendimento em seu coração. Ele falhou em apreciar a filosofia subjacente à série de fibonacci e, em vez disso, recorreu a espancar seu caminho no problema da multiplicação. Suspiro.

## Pensamentos finais

Seja o álbum protetor de Crockford ou os limites limitados e limitados das aulas de ciência da computação, doutrina e dogma são os inimigos do bom JavaScript. Alguns desenvolvedores gostam de livros de regras e clichê - e é por isso que temos Java. A alegria do JavaScript está enraizada na falta de rigidez e nas infinitas possibilidades que isso permite. As línguas naturais têm a mesma promessa. Os melhores autores e os melhores desenvolvedores de JavaScript são aqueles que ficam obcecados com a linguagem, que exploram e experimentam a linguagem todos os dias e, ao fazê-lo, desenvolvem seu próprio estilo, seus próprios idiomas e sua própria expressão.

Isso é tudo. Espero que você tenha aproveitado. É principalmente bobagem.


---

[Artigo Original](https://web.archive.org/web/20190123002450/http://byfat.xxx/if-hemingway-wrote-javascript)

 
