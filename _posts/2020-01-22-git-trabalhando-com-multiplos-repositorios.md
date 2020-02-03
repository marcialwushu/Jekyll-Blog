---
layout: post
title:  "Git - Trabalhando com múltiplos repositórios"
date:   2020-01-22 17:59:38 -0200
categories: jekyll update
---

Neste artigo pretendo demonstrar a funcionalidade subtree do git para trabalhar com múltiplos repositórios.

- Introdução
- Projeto
- Criando os repositórios dos projetos
- Linkando os projetos
- Realizando uma mudança nos projetos através do projeto principal
- Realizando uma alteração direta no repositório awesome-backend
- Realizando uma alteração e enviando push para outra branch
- Atualizando os repositórios filhos
- Conclusão


## Introdução

Um cenário muito comum hoje em dia na área de desenvolvimento de software para a web é a construção de um projeto para o Backend e outro para o Frontend. Esses projetos normalmente são criados em dois repositórios distintos e as equipes trabalham de forma separada. No entanto, utilizando a funcionalidade subtree do git é possível criar um repositório principal e linkar os dois projetos em um só.


## Projeto

Para a demonstração dessa funcionalidade, vou criar o projeto principal awesome e dois projetos dentro dele: awesome-backend e awesome-frontend. A estrutura final do projeto ficará assim:

```
awesome
   |--- awesome-backend
   |    |--- index.js
   |    |--- README.md
   |--- awesome-frontend
   |    |--- index.html
   |    |--- README.md
   |--- README.md
   
```

## Criando os repositórios dos projetos

Nesse passo iremos criar 03 repositórios no GitHub:

- **awesome**: repositório principal
- **awesome-backend**: repositório para os arquivos do backend
- **awesome-frontend**: repositório para os arquivos do frontend

### Crie o repositório awesome com as configurações descritas abaixo

- **Name**: awesome
- **Description**: Awesome Project
- [x] Initialize this repository with a README

![](https://showmethecode.com.br/images/posts/git-subtree/01-awesome-create.png)

### Crie o repositório awesome-backend com as configurações descritas abaixo

- Name awesome-backend
- Description: Awesome Backend
- [x] Initialize this repository with a README

![](https://showmethecode.com.br/images/posts/git-subtree/01-awesome-backend-create.png)

### Crie o repositório awesome-frontend com as configurações descritas abaixo

- Name awesome-frontend
- Description: Awesome Frontend
- [x] Initialize this repository with a README

![](https://showmethecode.com.br/images/posts/git-subtree/01-awesome-frontend-create.png)


## Linkando os projetos

Nesse passo iremos linkar os dois projetos no repositório principal.

- Clone o repositório awesome

```
$ git clone https://github.com/robertoachar/awesome.git

Cloning into 'awesome'...
remote: Counting objects: 3, done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.

```

- Altere para o diretório awesome

```
$ cd awesome

```

Para não precisar ficar repetindo o endereço dos repositórios sempre que formos utilizar, iremos adicionar um remote para cada um deles.

- Adicione os remotes para ambos os repositórios

```
# awesome-backend
$ git remote add awesome-backend https://github.com/robertoachar/awesome-backend.git

# awesome-frontend
$ git remote add awesome-frontend https://github.com/robertoachar/awesome-frontend.git

```

- Adicione o repositório awesome-backend utilizando a funcionalidade ```subtree```

```bash

$ git subtree add --prefix=awesome-backend/ awesome-backend master

git fetch awesome-backend master
warning: no common commits
remote: Counting objects: 3, done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
From https://github.com/robertoachar/awesome-backend
 * branch            master     -> FETCH_HEAD
 * [new branch]      master     -> awesome-backend/master
Added dir 'awesome-backend'

```

- Verifique se o repositório foi adicionado

```
$ ls

awesome-backend/  README.md

```

- Adicione o repositório awesome-frontend utilizando a funcionalidade subtree

```
$ git subtree add --prefix=awesome-frontend/ awesome-frontend master

git fetch awesome-frontend master
warning: no common commits
remote: Counting objects: 3, done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
From https://github.com/robertoachar/awesome-frontend
 * branch            master     -> FETCH_HEAD
 * [new branch]      master     -> awesome-frontend/master
Added dir 'awesome-frontend'

```

- Verifique se o repositório foi adicionado

```
$ ls

awesome-backend/  awesome-frontend/  README.md


```

- Abra o diretório awesome no seu editor de código. Eu estou utilizando o VS Code

![](https://showmethecode.com.br/images/posts/git-subtree/02-vscode-explorer.png)


- Verifique o status do repositório


```
$ git status

On branch master
Your branch is ahead of 'origin/master' by 4 commits.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean

```

O status do git mostra que tem 04 commits para serem enviados para o repositório remoto. Para exibir mais informações sobre os commits, execute o comando abaixo.


```

$ git log

commit 2e856fb7f43ace12c6286a8db0618aef90e2c283 (HEAD -> master)
Merge: cb872e1 ca6c577
Author: Roberto Achar <robertoachar@gmail.com>
Date:   Sun Oct 29 17:10:29 2017 -0200

    Add 'awesome-frontend/' from commit 'ca6c57763043b7c894f249802b0a12b9e8af3101'

    git-subtree-dir: awesome-frontend
    git-subtree-mainline: cb872e12523c9f8637eeefcafd7b90ea2df94fbf
    git-subtree-split: ca6c57763043b7c894f249802b0a12b9e8af3101

commit cb872e12523c9f8637eeefcafd7b90ea2df94fbf
Merge: 23b87d0 f0f1c1b
Author: Roberto Achar <robertoachar@gmail.com>
Date:   Sun Oct 29 17:08:46 2017 -0200

    Add 'awesome-backend/' from commit 'f0f1c1bcf69552d705699a560b8cfe71ada8b72f'

    git-subtree-dir: awesome-backend
    git-subtree-mainline: 23b87d0338ec4e04e5b781a2611378d3f56943e3
    git-subtree-split: f0f1c1bcf69552d705699a560b8cfe71ada8b72f

commit ca6c57763043b7c894f249802b0a12b9e8af3101 (awesome-frontend/master)
Author: Roberto Achar <robertoachar@gmail.com>
Date:   Sun Oct 29 16:58:42 2017 -0200

    Initial commit

commit f0f1c1bcf69552d705699a560b8cfe71ada8b72f (awesome-backend/master)
Author: Roberto Achar <robertoachar@gmail.com>
Date:   Sun Oct 29 16:56:00 2017 -0200

    Initial commit
    
```

Analisando os logs podemos entender o que está acontecendo. O git incorporou os commits dos dois repositórios que acabamos de adicionar. Envie esses commits para o repositório remoto.


```
$ git push

Counting objects: 10, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (6/6), done.
Writing objects: 100% (10/10), 1.79 KiB | 1.79 MiB/s, done.
Total 10 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), done.
To https://github.com/robertoachar/awesome.git
   23b87d0..2e856fb  master -> master
   
```

- Abra o repositório awesome no GitHub

![](https://showmethecode.com.br/images/posts/git-subtree/03-awesome-repository.png)


Reparem que agora o repositório tem 05 commits.

![](https://showmethecode.com.br/images/posts/git-subtree/03-awesome-commits.png)


Nesse momento, nenhuma alteração foi feita em nenhum dos dois projetos que foram adicionados. As alterações foram feitas apenas no repositório principal.

## Realizando uma mudança nos projetos através do projeto principal

Nesse passo iremos alterar o projeto awesome-backend através do repositório principal.

- Crie um arquivo index.js dentro do diretório awesome-backend

```
console.log('Backend');

```

- Crie um arquivo index.html dentro do diretório awesome-frontend


```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Frontend</title>
</head>
<body>
</body>
</html>

```

- A estrutura dos arquivos deve ficar assim:

![](https://showmethecode.com.br/images/posts/git-subtree/04-index.png)

- Verifique o status do repositório


```
$ git status
On branch master
Your branch is up-to-date with 'origin/master'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        awesome-backend/index.js
        awesome-frontend/index.html

nothing added to commit but untracked files present (use "git add" to track)

```

Nesse ponto é importante notar que adicionamos um arquivo no diretório awesome-backend e outro arquivo no diretório awesome-frontend. Agora vamos enviar esses arquivos para o repositório remoto.


```
$ git add .
$ git commit -m "[awesome] add index.js and index.html"
$ git push

```

Reparem que eu utilizei [awesome] no início do commit para ficar fácil de visualizar que esse commit foi feito através do repositório principal. Agora vamos dar uma olhada como ficaram os arquivos e os commits do repositório awesome.

- Diretório awesome-backend do repositório awesome

![](https://showmethecode.com.br/images/posts/git-subtree/05-awesome-files-backend.png)


- Diretório awesome-frontend do repositório awesome

![](https://showmethecode.com.br/images/posts/git-subtree/05-awesome-files-frontend.png)


- Commits do repositório awesome

![](https://showmethecode.com.br/images/posts/git-subtree/05-awesome-commits.png)


Como vocês podem observar, os arquivos e o commit estão disponíveis no repositório awesome. Essas alterações só foram enviadas para o repositório principal. Os arquivos e commits permanecem os mesmos nos outros dois repositórios.

## Atualizando os repositórios filhos

Agora nós vamos enviar as atualizações para os dois repositórios através do repositório principal.

- Envie as alterações para o repositório awesome-backend

```
$ git subtree push --prefix=awesome-backend awesome-backend master

git push using:  awesome-backend master
Counting objects: 3, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 319 bytes | 319.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/robertoachar/awesome-backend.git
   f0f1c1b..bb5f972  bb5f972a6a904b963f7a884a296c8e1b86417422 -> master
   
```

- Commits do repositório awesome-backend

![](https://showmethecode.com.br/images/posts/git-subtree/06-awesome-backend-commits.png)


- Arquivos do repositório awesome-backend

![](https://showmethecode.com.br/images/posts/git-subtree/06-awesome-backend-files.png)

- Envie as alterações para o repositório awesome-frontend

```

$ git subtree push --prefix=awesome-frontend awesome-frontend master

git push using:  awesome-frontend master
Counting objects: 3, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 376 bytes | 376.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/robertoachar/awesome-frontend.git
   ca6c577..ad9d55d  ad9d55df746e56764136e42eca1c7e462c7d1914 -> master
  
```

- Commits do repositório awesome-frontend

![](https://showmethecode.com.br/images/posts/git-subtree/06-awesome-frontend-commits.png)



- Arquivos do repositório awesome-frontend


![](https://showmethecode.com.br/images/posts/git-subtree/06-awesome-frontend-files.png)


O ponto mais importante a observar é a descrição do commit que foi feito através do repositório principal utilizando [awesome] no início.


## Realizando uma alteração direta no repositório awesome-backend

Embora os repositórios estejam linkados no repositório principal, é possível fazer qualquer tipo de alteração como fazemos normalmente com qualquer outro repositório. Para isso, clone o repositório awesome-backend em outro diretório fora do repositório principal. Esse procedimento é para simular como se outro usuário estivesse fazendo uma alteração direto no repositório filho.

- Clone o repositório

```
$ git clone https://github.com/robertoachar/awesome-backend.git

```

- Edite o arquivo index.js incluindo uma nova linha


```
console.log('Backend');
console.log('New feature');

```

- Envie essas alterações para o repositório remoto

```
$ git add .
$ git commit -m "[backend] add new feature"
$ git push

```

- Verifique o commit no GitHub

![](https://showmethecode.com.br/images/posts/git-subtree/07-awesome-backend-commits.png)


Nós só atualizamos o repositório awesome-backend. Agora precisamos que essas alterações sejam refletidas no repositório principal. Acesse o diretório do repositório principal antes de executar o comando abaixo.

- Atualize o repositório principal

```
$ git subtree pull --prefix=awesome-backend awesome-backend master

From https://github.com/robertoachar/awesome-backend
 * branch            master     -> FETCH_HEAD
Auto-merging awesome-backend/index.js
CONFLICT (add/add): Merge conflict in awesome-backend/index.js
Automatic merge failed; fix conflicts and then commit the result.

```


Em alguns casos, o pull gera conflitos. Resolva o conflito, aceitando o que está vindo do repositório awesome-backend. Após aceitar, faça um commit para o repositório principal. Não estudei à fundo o motivo de gerar conflito nesse caso, mas andei lendo algo relacionado ao git --squash.


## Realizando uma alteração e enviando push para outra branch


Nesse passo, iremos realizar uma alteração no repositório awesome-frontend através do repositório principal e enviar as alterações para uma nova branch.

- Altere o arquivo awesome-frontend/index.html

```html

<!DOCTYPE html>
<html lang="en">
<head>
    <title>Frontend</title>
</head>
<body>
    <h1>Frontend</h1>
</body>
</html>

```

- Abra o Terminal no diretório do repositório principal e envie as alterações para o próprio repositório principal e para a branch feature do repositório awesome-frontend


```
$ git add .

$ git commit -m "[awesome] add h1"

$ git push

$ git subtree push --prefix=awesome-frontend awesome-frontend feature

git push using:  awesome-frontend feature
Counting objects: 3, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 370 bytes | 370.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/robertoachar/awesome-frontend.git
 * [new branch]      d724637d24da48f708048eebd23fd0bf78a07562 -> feature
 
```


- Abra o projeto awesome-frontend no GitHub para visualizar a nova branch


![](https://showmethecode.com.br/images/posts/git-subtree/08-awesome-frontend-feature.png)


Para dar merge nas alterações, clique no botão Compare & pull request, na próxima tela clique em Create pull request, na tela seguinte escolha Merge pull request e Confirm merge.

Pronto, a nova funcionalidade já está disponível na master branch


![](https://showmethecode.com.br/images/posts/git-subtree/09-awesome-frontend-commits.png)


Por último, só precisamos atualizar o repositório principal.


```
$ git subtree pull --prefix=awesome-frontend awesome-frontend master

remote: Counting objects: 1, done.
remote: Total 1 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (1/1), done.
From https://github.com/robertoachar/awesome-frontend
 * branch            master     -> FETCH_HEAD
   ad9d55d..f17505f  master     -> awesome-frontend/master
Merge made by the 'recursive' strategy.

``` 

Nesse caso, o git conseguiu realizar o merge automaticamente. Agora é só enviar o merge para o repositório principal e todos os repositórios estarão sincronizados.

- Envie o merge para o repositório principal

```
$ git push

```

- Verifique o commit do repositório principal no GitHub

![](https://showmethecode.com.br/images/posts/git-subtree/10-awesome-commits.png)


## Conclusão

Eu acho muito legal a funcionalidade subtree do git que possibilita trabalhar em vários repositórios simultaneamente. No momento estou estudando bastante sobre Docker e senti a necessidade de linkar alguns repositórios em um repositório centralizado. Minha ideia é utilizar esse repositório centralizado para manter a documentação do sistema como um todo e armazenar o docker-compose.yml, por exemplo.

Espero que tenham gostado do conteúdo e gostaria muito de ouvir a opinião de vocês com relação a esse assunto.


- Você gosta da ideia de centralizar repositórios?

- Acredita que essa é uma boa prática para trabalhar com Docker Compose?

- Tem alguma sugestão de melhoria no processo?

- Conhece algum caso de uso específico?

Vamos em frente!

>"Talk is cheap. Show me the code." - Linus Torvalds


---

Autor: ROBERTO ACHAR

[Artigo Original](https://showmethecode.com.br/git-subtree/)



