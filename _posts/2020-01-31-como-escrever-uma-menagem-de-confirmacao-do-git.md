---
layout: post
title:  "Como escrever uma mensagem de confirmação do Git"
date:   2020-01-31 17:59:38 -0200
categories: jekyll update
---

![](https://imgs.xkcd.com/comics/git_commit_2x.png)


## Introdução: Por que boas mensagens de confirmação são importantes

Se você navegar no log de qualquer repositório aleatório do Git, provavelmente encontrará suas mensagens de confirmação mais ou menos uma bagunça. Por exemplo, dê uma olhada nessas joias dos meus primeiros dias no Spring:

```
$ git log --oneline -5 --author cbeams --before "Fri Mar 26 2009"

e5f4b49 Re-adding ConfigurationPostProcessorTests after its brief removal in r814. @Ignore-ing the testCglibClassesAreLoadedJustInTimeForEnhancement() method as it turns out this was one of the culprits in the recent build breakage. The classloader hacking causes subtle downstream effects, breaking unrelated tests. The test method is still useful, but should only be run on a manual basis to ensure CGLIB is not prematurely classloaded, and should not be run as part of the automated build.
2db0f12 fixed two build-breaking issues: + reverted ClassMetadataReadingVisitor to revision 794 + eliminated ConfigurationPostProcessorTests until further investigation determines why it causes downstream tests to fail (such as the seemingly unrelated ClassPathXmlApplicationContextTests)
147709f Tweaks to package-info.java files
22b25e0 Consolidated Util and MutableAnnotationUtils classes into existing AsmUtils
7f96f57 polishing
```


Caramba. Compare isso com esses commits [mais recentes](https://github.com/spring-projects/spring-framework/commits/5ba3db?author=philwebb) do mesmo repositório:

```
$ git log --oneline -5 --author pwebb --before "Sat Aug 30 2014"

5ba3db6 Fix failing CompositePropertySourceTests
84564a0 Rework @PropertySource early parsing logic
e142fd1 Add tests for ImportSelector meta-data
887815f Update docbook dependency and generate epub
ac8326d Polish mockito usage
```

Qual você prefere ler?

O primeiro varia em tamanho e forma; o último é conciso e consistente.
O primeiro é o que acontece por padrão; o último nunca acontece por acidente.

Enquanto os logs de muitos repositórios se parecem com os primeiros, há exceções. O [kernel do Linux](https://github.com/torvalds/linux/commits/master) e o [próprio Git](https://github.com/git/git/commits/master) são ótimos exemplos. [Veja Spring Boot](https://github.com/spring-projects/spring-boot/commits/master) , ou qualquer repositório gerenciado por [Tim Pope](https://github.com/tpope/vim-pathogen/commits/master) .

Os contribuidores desses repositórios sabem que uma mensagem de confirmação do Git bem elaborada é a melhor maneira de comunicar o contexto sobre uma mudança para colegas desenvolvedores (e de fato para seus futuros eus). Um diff lhe dirá o que mudou, mas apenas a mensagem de confirmação pode lhe dizer o porquê . Peter Hutterer destaca bem [este ponto](http://who-t.blogspot.co.at/2009/12/on-commit-messages.html) :


>Restabelecer o contexto de um pedaço de código é um desperdício. Não podemos evitá-lo completamente, por isso nossos esforços devem [reduzir](http://www.osnews.com/story/19266/WTFs_m) o máximo possível. As mensagens de confirmação podem fazer exatamente isso e, como resultado, uma mensagem de confirmação mostra se um desenvolvedor é um bom colaborador .


Se você não pensou muito no que faz uma ótima mensagem de confirmação do Git, pode ser que você não tenha passado muito tempo usando ```git log``` ferramentas relacionadas. Há um ciclo vicioso aqui: como o histórico de consolidação é desestruturado e inconsistente, não se gasta muito tempo usando ou cuidando dele. E, como não é usado ou tratado, permanece desestruturado e inconsistente.

Mas um registro bem cuidado é uma coisa bonita e útil. ```git blame```, ```revert```, ```rebase```, ```log```, ```shortlog``` E outros subcommands vir à vida. Revisar solicitações de confirmação e recebimento de outras pessoas se torna algo que vale a pena ser feito e, de repente, pode ser feito de forma independente. Entender por que algo aconteceu meses ou anos atrás se torna não apenas possível, mas eficiente.

O sucesso de longo prazo de um projeto repousa (entre outras coisas) em sua capacidade de manutenção, e um mantenedor tem poucas ferramentas mais poderosas do que o log de seu projeto. Vale a pena reservar um tempo para aprender a cuidar adequadamente de um. O que pode ser um aborrecimento a princípio logo se torna um hábito e, eventualmente, uma fonte de orgulho e produtividade para todos os envolvidos.

Nesta postagem, estou abordando apenas o elemento mais básico para manter um histórico de consolidação saudável: como escrever uma mensagem de consolidação individual. Existem outras práticas importantes, como o squash de commit, que não estou abordando aqui. Talvez eu faça isso em um post subseqüente.

A maioria das linguagens de programação possui convenções bem estabelecidas sobre o que constitui o estilo idiomático, ou seja, nomeação, formatação e assim por diante. Existem variações nessas convenções, é claro, mas a maioria dos desenvolvedores concorda que escolher uma e cumpri-la é muito melhor do que o caos que ocorre quando todos fazem suas próprias coisas.

A abordagem de uma equipe ao seu log de confirmação não deve ser diferente. Para criar um histórico de revisão útil, as equipes devem primeiro concordar com uma convenção de mensagem de confirmação que defina pelo menos as três coisas a seguir:


**Estilo**. Sintaxe de marcação, margens de quebra automática, gramática, letras maiúsculas e pontuação. Soletre essas coisas, remova as suposições e faça tudo o mais simples possível. O resultado final será um registro notavelmente consistente, que não é apenas um prazer de ler, mas que na verdade é lido regularmente.

**Conteúdo**. Que tipo de informação o corpo da mensagem de confirmação (se houver) deve conter? O que não deve conter?

**Metadados**. Como devem ser referenciados os IDs de rastreamento, os números de solicitação pull, etc.

Felizmente, existem convenções bem estabelecidas sobre o que faz um Git idiomático enviar uma mensagem. De fato, muitos deles são assumidos na maneira como certos comandos do Git funcionam. Não há nada que você precise reinventar. Basta seguir as [sete regras](https://chris.beams.io/posts/git-commit/#seven-rules) abaixo e você estará no caminho de se comprometer como um profissional.

## As sete regras de uma grande mensagem de confirmação do Git

>Tenha em mente: [Esta](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html) [tem](https://www.git-scm.com/book/en/v2/Distributed-Git-Contributing-to-a-Project#_commit_guidelines) [tudo](https://github.com/torvalds/subsurface-for-dirk/blob/master/README.md#contributing) [sido](http://who-t.blogspot.co.at/2009/12/on-commit-messages.html) [dito](https://github.com/erlang/otp/wiki/writing-good-commit-messages) [antes](https://github.com/spring-projects/spring-framework/blob/30bce7/CONTRIBUTING.md#format-commit-messages) .


1. [Separe o assunto do corpo com uma linha em branco](#separate)
2. [Limite a linha de assunto para 50 caracteres]()
3. [Coloque em maiúscula a linha de assunto]()
4. [Não termine o assunto com um período]()
5. [Use o humor imperativo na linha de assunto]()
6. [Enrole o corpo com 72 caracteres]()
7. [Use o corpo para explicar o que e por que versus como]()

Por exemplo:

```
Summarize changes in around 50 characters or less

More detailed explanatory text, if necessary. Wrap it to about 72
characters or so. In some contexts, the first line is treated as the
subject of the commit and the rest of the text as the body. The
blank line separating the summary from the body is critical (unless
you omit the body entirely); various tools like `log`, `shortlog`
and `rebase` can get confused if you run the two together.

Explain the problem that this commit is solving. Focus on why you
are making this change as opposed to how (the code explains that).
Are there side effects or other unintuitive consequences of this
change? Here's the place to explain them.

Further paragraphs come after blank lines.

 - Bullet points are okay, too

 - Typically a hyphen or asterisk is used for the bullet, preceded
   by a single space, with blank lines in between, but conventions
   vary here

If you use an issue tracker, put references to them at the bottom,
like this:

Resolves: #123
See also: #456, #789
```


## 1. Separe o assunto do corpo com uma linha em branco ##

Na página de ```git commit``` manual :

>Embora não seja obrigatório, é uma boa idéia iniciar a mensagem de confirmação com uma única linha curta (com menos de 50 caracteres) resumindo a alteração, seguida por uma linha em branco e uma descrição mais completa. O texto até a primeira linha em branco em uma mensagem de confirmação é tratado como o título de confirmação e esse título é usado em todo o Git. Por exemplo, o Git-format-patch (1) transforma um commit em email e usa o título na linha Subject e o restante do commit no corpo.

Em primeiro lugar, nem todo compromisso exige um sujeito e um corpo. Às vezes, uma única linha é boa, especialmente quando a mudança é tão simples que nenhum contexto adicional é necessário. Por exemplo:

```
Fix typo in introduction to user guide
```

Nada mais precisa ser dito; se o leitor se pergunta qual foi o erro de digitação, pode simplesmente dar uma olhada na mudança em si, ou seja, usar ```git show``` or ```git diff``` ou ```git log -p```.

Se você está cometendo algo assim na linha de comando, é fácil usar a opção ```-m```  para ```git commit```:

```
$ git commit -m"Fix typo in introduction to user guide"
```

No entanto, quando um commit merece um pouco de explicação e contexto, você precisa escrever um corpo. Por exemplo:

```
Derezz the master control program

MCP turned out to be evil and had become intent on world domination.
This commit throws Tron's disc into MCP (causing its deresolution)
and turns it back into a chess game.
```






