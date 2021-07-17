---
layout: post
title:  "Sincronização de Github e Gitlab"
date:   2021-07-13 17:59:38 -0200
categories: jekyll update
---


Tanto o Github quanto o Gitlab são ótimas maneiras de hospedar seus repositórios de git on-line. Ambos têm ótimas ferramentas para gerenciar seu projeto, seja de código aberto ou código privado.
Não vou comparar os dois serviços em profundidade, já que muitos guias já o fazem. Para mim, a diferença geral entre o Github e o Gitlab é que o Gitlab está focando mais esforço em pipelines de CI/CD e ferramentas para empresas, enquanto o Github está mais focado na comunidade e criando uma plataforma para compartilhar código-fonte aberto.
Ambos podem ser usados para qualquer cenário... o que torna muito difícil escolher entre eles!

Mas e se eu te dissesse que você não tem que escolher O_o?

## Por que eu quero usar tanto Gitlab quanto Github

>Apenas uma isenção rápida, este é o método que eu uso. Funciona para mim, mas pode não funcionar para todos. Eu recomendo experimentar com as coisas para si mesmo, fazer alguns testes.
>Estou compartilhando minha experiência porque sinto que pode ser útil para alguém na mesma posição que eu.

Gosto de poder organizar meus repositórios em projetos (ou grupos no Gitlab). Infelizmente, o Github não faz isso.
Eu também quero ser capaz de alcançar o maior número de pessoas possível com meus repositórios, o Github tem a maior comunidade.
Droga, estou preso, quero recursos de ambos os provedores.

Felizmente para mim, Gitlab tem duas coisas que tornam possível a simbiose entre as duas ferramentas:

1. Importação do repositório do Github Isso torna a importação de um repositório do Github super fácil
2. Sincronização do repositório do Gitlab -> Github (de graça) Isso me permite usar o Gitlab como a principal fonte da verdade, mas também ter o repositório no Github. Posso usar o rastreador de problemas do Github, wiki e fórum (discussão do Github)
3. Grande CI/CD (ok, eu menti quando disse duas coisas)

## Sincronizar Gitlab para Github (fácil)

Este é simples. Você mesmo pode criar um pouco de CI/CD. Mas Gitlab fará isso automaticamente por você.

1. Vá para "Configurações > repositório > repositórios de espelhamento"
2. Digite seu repo github com seu nome de usuário na frente ```https://<github username>@github.com/path/to/your/repo.git```
3. No campo de senha, digite seu token Github
4. Selecione o push (isso requer uma assinatura)
5. Repositório de espelho de imprensa
  
De agora em diante, as mudanças no Gitlab serão espelhadas no Github

## Sincronizar o Github com o Gitlab (intermediário, a menos que você pague)

Existem duas maneiras de fazer isso (ambas são equivalentes apenas a partir de plataformas opostas)

1. Ou você configura um pipeline CI/CD no Github que aciona usando um webhook (em solicitações de push and pull).
2. Ou você configura um pipeline CI/CD no Gitlab que aciona usando um webhook (em solicitações de pressão e tração). **Acontece que isso é realmente um recurso premium... Você não pode usar o webhook pull sem pagar agora**

Eu pessoalmente escolhi fazer isso do lado github, uma vez que o método Github é gratuito

## Método 1 Github CI/CD

- Crie os seguintes segredos em seu repositório do Github
    - ```TARGET_URL``` valor: a URL do repositório Gitlab
    - ```TARGET_TOKEN``` valor: Token Gitlab
    - ```TARGET_USERNAME``` valor: Nome de usuário Gitlab
- Crie uma ação do Github para o seu repositório com o seguinte código:

```yml
name: GitlabSync

on:
  - push
  - delete

jobs:
  sync:
    runs-on: ubuntu-latest
    name: Git Repo Sync
    steps:
    - uses: actions/checkout@v2
      with:
        fetch-depth: 0
    - uses: wangchucheng/git-repo-sync@v0.1.0
      with:
        # Such as https://github.com/wangchucheng/git-repo-sync.git
        target-url: ${{ secrets.TARGET_URL }}
        # Such as wangchucheng
        target-username: ${{ secrets.TARGET_USERNAME }}
          # You can store token in your project's 'Setting > Secrets' and reference the name here. Such as ${{ secrets.ACCESS\_TOKEN }}
        target-token: ${{ secrets.TARGET_TOKEN }}
  
```

- Certifique-se de que a branch para o qual você está fazendo o push no Gitlab não está protegido ou permite o push force.

## Método 2 Gitlab CI/CD (requer Gitlab premium)

Observe que se você tiver uma assinatura com o Gitlab, você também pode fazer isso em alguns cliques no mesmo dashion como configuramos a sincronização do Gitlab para o Github.

Vá para "Configurações > repositório > repositórios de espelhamento"

1. Digite seu repo github com seu nome de usuário na frente ```https://<github username>@github.com/path/to/your/repo.git```
2. No campo de senha, digite seu token Github
3. Selecione puxar (isso requer uma assinatura)
4. Repositório de espelho de imprensa
  
## Configuração manual

### Configurar os webhooks

Se você criou o projeto Gitlab através da ferramenta de importação Github, então você pode pular completamente esta etapa.  

- Em seu repositório do Github, vá para "Configurações > Webhooks"
    - Crie um novo webhook
    - Caminho de carga útil: (o id do projeto pode ser encontrado em "Configurações > Geral")https://gitlab.com/api/v4/projects/<gitlab project id>/mirror/pull
    - Tipo de conteúdo: application/json
    - Verificação SSL: desligado
    - Só enviar para: pull e push
- ativar
- No projeto Gitlab, vá para "Configurações > Webhooks"
- selecione empurrar eventos do repositório e entrar no repositório do Github (com um token se for privado)
  

## Configurar as variáveis CI/CD
  
- No projeto Gitlab, vá para "Configurações > Variáveis de > CI/CD"
- Crie uma variável com chave: e valor: (faça-a oculta porque isso é sensível) ACCESS_TOKEN
    - Crie uma variável com chave: e valor: (faça-a oculta porque isso é sensível)REMOTE_REPOSITORY_URL<your Github token>@<your repository URL>
  
## Configurar o CI/CD
  
Crie um pipeline indo para "CI/CD > Editor" ou criando um arquivo na raiz do projeto e adicione o seguinte conteúdo: ```.gitlab-ci.yml```
  
```yml
  sync-with-github:
  before_script:
    - git config --global user.name "${GITLAB_USER_NAME}"
    - git config --global user.email "${GITLAB_USER_EMAIL}"
  script:
    - git remote add github $REMOTE_REPOSITORY_URL
    - git checkout master
    - git pull origin master
    - git pull github master
    - git status
    - git push http://root:$ACCESS_TOKEN@$CI_SERVER_HOST/$CI_PROJECT_PATH.git HEAD:master
 
```
  

## Advertências
  
Isso não vem sem desvantagens. Aqui estão alguns que encontrei enquanto testando esta configuração.

- Wikis, Problemas, Discussões, conselhos, etc. não sincronizarão entre os dois provedores de hospedagem. Isso só sincronizará o que está no seu repositório. Existem maneiras de sincronizar as Wikis ( o Wiki é essencialmente um repositório .git oculto e tanto o Github quanto o Gitlab usam o mesmo formato Wiki )
- Pode ficar confuso ter dois repositórios remotos ao mesmo tempo
- Eles podem sair da sincronia se vários compromissos acontecerem em dois locais ao mesmo tempo e criar conflitos (eu só uso isso em repositórios I e somente eu uso)


  ---
  
  Autor: [Bruno Robert](https://dev.to/brunorobert)

  [Artigo Original](https://dev.to/brunorobert/github-and-gitlab-sync-44mn)
  
  
