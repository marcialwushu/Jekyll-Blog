---
layout: post
title:  "Como deletar um commit no git, local e remoto"
date:   2018-11-08 23:39:31 -0200
categories: jekyll update
---

Postado por adrian.ancona em 8 de julho de 2011

Já aconteceu comigo mais de uma vez fazer um commit sem verificar as alterações que estou cometendo. Tempo depois disso eu reviso o commit e percebo que há algo no commit que não pertence a ele.

Nesses momentos o que eu quero fazer é fazer um patch com as alterações do commit, deletar o commit, aplicar o patch e depois refazer o commit apenas com as mudanças que eu pretendia. Nesta postagem, explicarei apenas como excluir um commit no seu repositório local e em um repositório remoto, caso você já tenha enviado o commit.

### Excluir um commit local

>Anthony Dentinger me mostrou nos comentários que você pode excluir um commit local fazendo:

>git reset –hard HEAD ~

>Abaixo está minha postagem original, mas você provavelmente só quer usar a linha acima

Vamos dizer que há um repositório com 4 commits.

```
1|$git log --pretty=oneline --abbrev-commit
2|46cd867 Changed with mistake
3|d9f1cf5 Changed again
4|105fd3d Changed content
5|df33c8a First commit

```

Commit 46cd867 é o commit mais recente e o que queremos deletar, por isso, usaremos o rebase.

```
1|$git rebase -i HEAD~2

```

Esse comando abrirá seu editor de texto padrão com seus dois commits mais recentes (Altere o número 2 com o número de commits que você deseja obter):

```

1|pick d9f1cf5 Changed again
2|pick 46cd867 Changed with mistake
3|
4|# Rebase 105fd3d..46cd867 onto 105fd3d
5|#
6|# Commands:
7|#  p, pick = use commit
8|#  r, reword = use commit, but edit the commit message
9|#  e, edit = use commit, but stop for amending
10|#  s, squash = use commit, but meld into previous commit
11|#  f, fixup = like "squash", but discard this commit's log message
12|#  x, exec = run command (the rest of the line) using shell
13|#
14|# If you remove a line here THAT COMMIT WILL BE LOST.
15|# However, if you remove everything, the rebase will be aborted.
16|#

```

Uma coisa a notar aqui é que o commit mais recente é o que está embaixo. Os comentários na parte inferior do arquivo fornecem uma descrição das coisas que podem ser feitas com o comando rebase, mas desta vez nenhuma dessas opções será usada, basta excluir a linha que corresponde ao commit desejado para apagar e salvar o arquivo.

Podemos ver que a alteração foi aplicada corretamente:


```

1|$git log --pretty=oneline --abbrev-commit
2|d9f1cf5 Changed again
3|105fd3d Changed content
4|df33c8a First commit

```

### Excluir um commit remoto

Para remover uma confirmação que você já enviou para sua origem ou para outro repositório remoto, primeiro é necessário excluí-la localmente, como na etapa anterior, e depois enviar as alterações para o controle remoto.

```
1|$git push origin +master

```

Observe o sinal + antes do nome do ramo que você está empurrando, isso diz ao git para forçar o push. Vale a pena mencionar que você deve ser muito cuidadoso ao excluir os commits porque, uma vez feito, eles desaparecem para sempre. Além disso, se você estiver excluindo algo de um repositório remoto, certifique-se de coordenar com sua equipe para evitar problemas.

[[]git  github](https://ncona.com/tag/git)


ARTIGO ORIGINAL: [NCONA.COM](https://ncona.com/2011/07/how-to-delete-a-commit-in-git-local-and-remote/)















