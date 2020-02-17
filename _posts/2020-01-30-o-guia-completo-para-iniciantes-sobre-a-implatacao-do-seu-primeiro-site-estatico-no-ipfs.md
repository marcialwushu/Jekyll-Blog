---
layout: post
title:  "O guia completo para iniciantes sobre a implantação do seu primeiro site estático no IPFS"
date:   2020-01-30 17:59:38 -0200
categories: jekyll update
---

Este será o tutorial mais rápido de todos os tempos. Quase assombroso.

Você não precisa saber nada sobre IPFS ou distribuir nada, nem mesmo geradores de sites estáticos.

![](https://agentofuser.com/static/34db236b05664bdbed4ca48dce3ec0e1/c1dc5/spacex-merlin-rocket-engine-test-stand-bay-mcgregor-texas-cropped.webp)


Pronto? Ok, o primeiro passo é abrir o terminal e digitar:

```
mkdir -p dwebsite/public
cd dwebsite
echo '<h1>Hello, worlds!</h1>' >> public/index.html

yarn global add ipfs-deploy
# or: npm install -g ipfs-deploy
ipd
```

Você comigo? Ok, digitei isso. O quê mais? Nada.

O que? Sim. Você terminou aqui.

Agora, sente-se e observe o desfile da vitória por 😎

```
ℹ 🤔 No path argument specified. Looking for common ones…
✔ 📂 Found local public directory. Deploying that.
✔ 🚚 public weighs 24 B.
✔ 📌 It's pinned to Infura now with hash:
ℹ 🔗 QmQzKWGdjjQeTXrruYL2vLkCqRP8TyXnG1a9QEJjDM8WTY
✔ 📋 Copied HTTP gateway URL to clipboard:
ℹ 🔗 https://ipfs.infura.io/ipfs/QmQzKWGdjjQeTXrruYL2vLkCqRP8TyXnG1a9QEJjDM8WTY
✔ 🏄 Opened web browser (call with -O to disable.)
```

E aí está. Seu próprio site de [web](https://twitter.com/search?q=%23dweb) ao vivo no Merkleverse. [Confira](https://cloudflare-ipfs.com/ipfs/QmQzKWGdjjQeTXrruYL2vLkCqRP8TyXnG1a9QEJjDM8WTY) . Compartilhe com os seus amigos.

Doce, não é? 🍬

## Devagar, o que exatamente aconteceu?

Tudo bem, isso foi um pouco demais para entender de uma só vez. Vamos retroceder um pouco e analisar em câmera lenta, com comentários nos bastidores:


### 1. Onde estão as coisas?

Verdade seja dita, eu poderia ter chamado ipd ./public, passando o diretório a ser implantado ( public) explicitamente.

Mas você não vê o emoji de "reflexão" como sondas de implementação do ipfs de maneira inteligente para um dos muitos, muitas vezes não documentados, [destinos de construção comumente usados por geradores de sites estáticos](https://github.com/ipfs-shipyard/ipfs-deploy#usage).

```
ℹ 🤔 No path argument specified. Looking for common ones…
✔ 📂 Found local public directory. Deploying that.
```

Sim, eu realmente [vasculhei o staticgen.com](https://www.staticgen.com/) , instalei vários desses geradores de sites estáticos e construí pequenos sites de teste para poder reivindicar o título "zero-config". São as pequenas coisas, você sabe.

É isso que o ipfs-deploy procura quando estamos com preguiça de digitá-lo:


```js
const guesses = [
  '_site',         // jekyll, hakyll, eleventy
  'site',          // forgot which
  'public',        // gatsby, hugo
  'dist',          // nuxt
  'output',        // pelican
  'out',           // hexo
  'build',         // create-react-app, metalsmith, middleman
  'website/build', // docusaurus
  'docs',          // many others
]
```

Como você pode ver no nome de domínio deste blog, sou fã do Gatsby, mas o ipfs-deploy atende a todos os que precisam. Traga seu próprio SSG e daremos um tapa em um jetpack interplanetário e o faremos voar. 🚀


### 2. O upload

É para isso que estamos aqui, ou seja, colocando o site no espaço (figurativamente, por enquanto). Alguns segundos depois, o ipfs-deploy oferece:


```
✔ 📌 It's pinned to Infura now with hash:
ℹ 🔗 QmQzKWGdjjQeTXrruYL2vLkCqRP8TyXnG1a9QEJjDM8WTY

```

Jackpot! Esse é o dinheiro arremessado ali.

Que pouco desconexa de um [hash](https://multiformats.io/multihash/) de é o cerne de todo o judô dweb. O enunciado mágico que convoca o nome do seu site a partir das profundezas cavernosas das masmorras conectadas, cuidando não de onde ele está, mas apenas do que é .

Endereçamento intrínseco, não vinculado por local ou rota.

Bem-vindo <grave pausa> ao futuro distribuído.
  

**ESPERE UM MINUTO, PENSEI TER OUVIDO VOCÊ DIZER "DISTRIBUÍDO"**

Oh, seu leitor perspicaz.

Você está certo: se o IPFS deveria ser um protocolo ponto a ponto, por que estamos fazendo o upload , certo? Para um servidor !? 🤢

Não deveríamos apenas anunciar à rede que possuímos o hash e esperar para servi-lo a outros colegas, conforme eles o solicitem?

Sim, você pode fazer isso. Então você fecha o seu laptop, o wifi diminui, 💩 acontece, e poof ✨ lá vai o seu site.

É como torrents: você precisa de pelo menos um semeador para estar disponível para que o conteúdo seja alcançável. Se o seu site tiver um monte de pessoas que executam seu próprio nó IPFS e o reenvia para outras pessoas, em média, o tempo de atividade será bastante alto.


Mas ainda não existem muitos visitantes por aí (espero que o Brave resolva isso para nós) e, além disso, é um novo site! 🐣 Coitadinha não nasceu famosa. Dê um tempo.

Seria uma história diferente se os navegadores tivessem um [#asyncUX](https://twitter.com/search?q=%23asyncUX) decente e os visitantes pudessem facilmente pedir para colocarem o download na fila para quando um colega estiver disponível e notificar quando estiver pronto (como um fluxo contínuo de “leia depois”).

Mas, como está, se não houver ninguém vivo no momento em que uma solicitação é feita, as coisas ficam suspensas e o tempo limite termina. Definitivamente não está [pronto para o espaço](https://agentofuser.com/foreword/) .

Portanto, precisamos de uma semeadora de alta disponibilidade do nosso lado. Ou, na linguagem do IPFS, um “pinner”.

### FIXAÇÃO DE CONFIGURAÇÃO ZERO COM INFURA.IO

Um grande objetivo do projeto do ipfs-deploy é permitir que você tenha a primeira experiência feliz de ver algo criado no IPFS o mais rápido possível.

Uma maneira de fazer isso é executar um daemon IPFS local e você mesmo servir o conteúdo.

Mas, como vimos acima, isso seria um pouco complicado, pois não representa a aparência de uma implantação real que você pode compartilhar com seus amigos. Tem que ter um pinner estável.

A fixação de itens com um tempo de atividade decente custa muito dinheiro; portanto, a maioria dos serviços de fixação exige, pelo menos, que você se inscreva para uma camada gratuita antes de aceitarem hospedar seu site.

Mas não o [Infura.io](https://infura.io/docs/ipfs/get/block_get.md) !


Por alguma mágica de cuidadosa limitação de taxa, prevenção inteligente de abusos, capital de crescimento ou abandono imprudente, eles permitem que você carregue coisas do nada, não autenticadas , e elas servirão para você indefinidamente. (Mesmo contra a sua vontade, parece, pois não há uma maneira clara de desmarcar as coisas no momento.)

Por isso, devemos essa generosa mancha na rampa à sua generosidade: obrigado a todos na Infura, e continuem assim!

*Além disso, se você possui um serviço de pinagem e gostaria de fazer parte do pacote de boas-vindas de configuração zero, considere adicionar uma camada "ainda mais livre" que não exija inscrição.*

*Os sites estáticos recém-criados não ocupam muito espaço, têm muito pouco tráfego e são uma ótima porta de entrada para um maior consumo de IPFS*.


## Você fez isso! 🏁

Se você chegou até aqui, desculpas. Você é demais! 🗿

Não apenas você implantou seu primeiro site IPFS, mas agora pode se gabar de realmente entender como ele funciona, agitando as mãos e dizendo: “oh, é muito parecido com git + bittorrent, sabe, é fácil!”

Se você seguiu diligentemente as instruções, e de alguma forma as coisas explodiram na sua cara, isso é por minha conta, não por você. Este é o meu compromisso: sua primeira experiência feliz, ou é um bug!


Então, por favor, [diga-me o que deu errado](https://github.com/agentofuser/ipfs-deploy/issues/new) e eu resolvo tudo para você.

Temos tudo a ver com remover o atrito por aqui 

Se você não teve o suficiente, fique por aqui para obter um crédito extra.

E se você está satisfeito com o que chegamos por enquanto, compartilhe esse sentimento com outras pessoas espalhando e votando este guia em toda parte :) Obrigado!

---

## Capítulo bônus

### Redundância gratuita com Pinata.cloud

Ter um pinner estável é legal e tudo, mas não é muito diferente da hospedagem na web comum. (No sentido de “distribuição”, isto é. No sentido de “ [conteúdo endereçável](https://www.youtube.com/watch?v=YIc6MNfv5iQ) ”, é noite e dia.)

Uma maneira de obter uma amostra da natureza distribuída do IPFS é adicionar um segundo pinner, e o ipfs-deploy facilita isso.

Vamos implantar o Infura.io e o Pinata.cloud para que os visitantes possam fazer o download de ambos ao mesmo tempo ou de um caso o outro falhe.

Resiliência! 

[O Pinata.cloud](https://pinata.cloud/) é um serviço de fixação IPFS dedicado que oferece mais controle sobre o que está sendo hospedado.

Ele permite excluir pinos e adicionar metadados que você pode usar posteriormente para filtrar e gerenciar suas implantações.

Há um nível gratuito de 1 GB, suficiente para blogs de desenvolvimento, páginas de destino, documentação e [páginas de fãs](https://twitter.com/search?q=%23yanggang) #YangGang. Ele não requerem inscrição, mas é bastante simples e não requer cartão de crédito ou informações pessoais.

Depois de se [inscrever](https://pinata.cloud/signup) e obter as [chaves da API](https://www.pinata.cloud/documentation#GettingStarted) , acesse o diretório do seu site e copie as chaves em um .envarquivo da seguinte forma:

```
# dwebsite/.env
IPFS_DEPLOY__PINATA__API_KEY=paste-the-api-key-here
IPFS_DEPLOY__PINATA__SECRET_API_KEY=and-the-secret-api-key-here

```

**⚠ Você não deseja tornar essas informações públicas** so, portanto, ao fazer isso em um repositório que você hospedará publicamente, adicione o .envarquivo ao seu ```.gitignore```:

```
echo .env >> .gitignore

```

*[Atualização 2019-06-13: havia uma seção aqui sobre como você precisava fazer o encaminhamento manual de portas e outros enfeites para implantar a pinata, mas, felizmente, isso não é mais necessário. eles também habilitaram o upload HTTPS; portanto, agora não há necessidade de executar um nó, abrir uma porta e solicitar que eles se conectem a ele. O que é uma ótima notícia, porque agora este blog tem [implantação contínua com o Travis CI](https://twitter.com/agentofuser/status/1137364393308692480) 🙌]*

Agora que o Pinata está configurado, vamos voltar ao show. Aqui está o que você executa para implantar nos dois serviços de fixação:

```
ipd -p infura -p pinata

```

E é isso que você obtém:


```
ℹ 🤔 No path argument specified. Looking for common ones…
✔ 📂 Found local public directory. Deploying that.
✔ 🚚 public weighs 24 B.
✔ 📌 It's pinned to Infura now with hash:
ℹ 🔗 QmQzKWGdjjQeTXrruYL2vLkCqRP8TyXnG1a9QEJjDM8WTY
✔ 📌 It's pinned to Pinata now with hash:
ℹ 🔗 QmQzKWGdjjQeTXrruYL2vLkCqRP8TyXnG1a9QEJjDM8WTY

```

E aí está: o mesmo hash, locais diferentes.

```
✔ 📋 Copied HTTP gateway URL to clipboard:
ℹ 🔗 https://ipfs.infura.io/ipfs/QmQzKWGdjjQeTXrruYL2vLkCqRP8TyXnG1a9QEJjDM8WTY
✔ 🏄 Opened web browser (call with -O to disable.)
```

Você pode ver o mesmo conteúdo em qualquer gateway que desejar, substituindo "ipfs.infura.io" por:

- [gateway.pinata.cloud](https://gateway.pinata.cloud/ipfs/QmQzKWGdjjQeTXrruYL2vLkCqRP8TyXnG1a9QEJjDM8WTY)
- [ipfs.io](https://ipfs.io/ipfs/QmQzKWGdjjQeTXrruYL2vLkCqRP8TyXnG1a9QEJjDM8WTY)
- [cloudflare-ipfs.com](https://cloudflare-ipfs.com/ipfs/QmQzKWGdjjQeTXrruYL2vLkCqRP8TyXnG1a9QEJjDM8WTY)

Ou qualquer um dos listados aqui: https://ipfs.github.io/public-gateway-checker

Eu já disse isso antes, mas acho isso tão legal que vale a pena repetir:


>Endereçamento intrínseco, não vinculado por local ou rota.

Ou: chamar dados pelo que são, não onde estão.

Isso é hash criptográfico para você!

### A parte de contar para seus amigos 

Tudo bem, terminamos aqui, certo? Sentindo-se tudo ótimo e distribuído. Agora, conte aos seus amigos por telefone 📞


- Hey Jessie, adivinhe?
- O que?
- Eu tenho meu site nas dwebs !!
- Sim amigo, que legal! Aposto que foi super difícil.
- Não, existe esse pacote npm, você sabe ...
- Sim, sim, deixe-me ver o site, onde está?
- Oh, está em ipfs-dot-io-slash-ipfs-slash ... Er ...
- Slash what?
- É ... Você tem uma caneta? É… letras maiúsculas Q, letras minúsculas m, letras maiúsculas Q, letras maiúsculas… Ugh… Que tal enviar uma URL para você?
- Ok, claro, mas e se eu sou apenas uma pessoa aleatória que vê seu URL em um outdoor? Você não poderá me enviar uma mensagem de texto, não é?
- Acho que não.
- Você sabe o que dizer, e você me liga quando tem algo memorável que posso digitar no navegador?
- Uau, duro.

Ok, essa conversa muito realista foi muito rápida para o sul.


Acontece que o endereçamento de conteúdo por si [só não se adapta muito bem](https://en.wikipedia.org/wiki/Zooko's_triangle) ao limitado buffer de memória humana.

Além disso, os amigos podem ser difíceis.

O que fazemos então?


### UM URL BONITO

A nomeação legível por humanos para sites IPFS é definitivamente uma área que precisa ser suavizada.

Mas se (e isso é um grande se) você se mantiver dentro da restrição de usar o Cloudflare IPFS Gateway grátis por enquanto, o ipfs-deploy agrupa tudo de uma maneira bem organizada.

Aqui estão as imagens reais de mim implantando o interplanetarygatsby.com:

```
ipd -p infura -p pinata -d cloudflare

```

E é isso que vejo depois que os uploads terminam:

```
✔ 🙌 SUCCESS!
ℹ 🔄 Updated DNS TXT interplanetarygatsby.com to:
ℹ 🔗 dnslink=/ipfs/QmSNf4sScZUmpNqBWAAs9S5tC4XkQRNepA3KbF4aipGGeq
```

Isso me faz sorrir toda vez com o simples esforço dele 😌

Existem algumas etapas únicas que você precisa seguir para chegar lá:

1. Compre um domínio
2. Inscreva-se para uma conta Cloudflare
3. Mova a zona DNS do seu domínio para o Cloudflare
4. Conecte seu [domínio](https://www.cloudflare.com/distributed-web-gateway/#connectingyourwebsite) ao gateway IPFS
5. Obtenha suas [chaves de API](https://support.cloudflare.com/hc/en-us/articles/200167836-Where-do-I-find-my-CloudFlare-API-key-)

Entre executar essas etapas de configuração e aguardar a propagação das informações do DNS, tudo isso pode levar algumas horas.

É por isso que coloquei essa parte neste capítulo de bônus e deixei as instruções básicas zero-config. Com o tempo, removeremos cada vez mais atritos e tornaremos a primeira experiência feliz ainda mais feliz 😃⬅️🧹🥌

Portanto, depois que as etapas 1 a 5 forem concluídas, a última coisa a ser feita é adicionar as credenciais do domínio e da API Cloudflare ao .envarquivo do seu site :


```
# dwebsite/.env
IPFS_DEPLOY_CLOUDFLARE__ZONE=example.com
# _dnslink.subdomain.example.com also works below; zone stays the same
IPFS_DEPLOY_CLOUDFLARE__RECORD=_dnslink.example.com
IPFS_DEPLOY_CLOUDFLARE__API_KEY=paste-your-cloudflare-api-key-here
IPFS_DEPLOY_CLOUDFLARE__API_EMAIL=the-email-you-used-to-sign-up
```

Agora vá em frente, atire ```ipd -d cloudflare``` e conte a todos esses outdoors! 📣📣📣

៚


---

## Postface: Uma Chamada para Rolinhos 

Enquanto escrevia este guia, [deparei -me com o emoji “curling stone”](https://emojipedia.org/curling-stone/) e senti uma conexão instantânea com ele.


![](https://agentofuser.com/991c75c2e5be29ccfb7f243b83b1c18e/curling-simpsons-loop-once.gif)

Para ser sincero, sempre achei a idéia de enrolar um pouco ... estranha. Mas todo um esporte de equipe dedicado a remover freneticamente o atrito de um caminho apenas para que esse artefato peculiar possa graciosamente e sem esforço deslizar seu caminho para um objetivo é tão ... emocionante.

É assim que eu quero que o [ipfs-deploy](https://github.com/ipfs-shipyard/ipfs-deploy) se sinta para o usuário. Uma experiência suave como seda pousando-os na web distribuída sem suar a camisa e uma multidão selvagem e animada torcendo-os.

Se isso soa como o seu tipo de esporte, diga olá nas [questões](https://github.com/agentofuser/ipfs-deploy/issues?q=is%3Aissue+is%3Aopen+label%3A%22help+wanted%22+sort%3Aupdated-asc) e vamos polir algumas coisas!




---
Autor: [Helder S Ribeiro](https://twitter.com/agentofuser)

[Artigo Original](https://agentofuser.com/ipfs-deploy/)



