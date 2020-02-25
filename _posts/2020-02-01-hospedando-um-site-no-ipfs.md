---
layout: post
title:  "Hospedando um site no IPFS"
date:   2020-02-01 17:59:38 -0200
categories: jekyll update
---

Este é um tutorial rápido que ensinará como hospedar um site estático simples no IPFS e usar o IPNS para manter um único ID ao alterar o conteúdo do site

## Etapa 1. Instale o IPFS

Instale o IPFS conforme descrito em <https://ipfs.io/docs/install/>

## Etapa 2. Crie um site estático simples

Tudo o que você precisa é de uma página html estática simples, desde que TODOS os links sejam relativos. Para os propósitos deste tutorial, eu coloquei um [hello world simples no gist](https://gist.github.com/giodamelio/7f01283fafdffee2ce2e) ( [download direto](https://gist.github.com/giodamelio/7f01283fafdffee2ce2e/archive/6c06c2e55e0d1932bfb013f806378e7fee07654b.zip) , [visualização](http://bl.ocks.org/giodamelio/raw/7f01283fafdffee2ce2e/) ).

```html
<! DOCTYPE html >
< html  lang = " pt " >
< cabeça >
  < meta  charset = " UTF-8 " >
  < Título > Olá IPFS! </ title >
  < link  rel = " stylesheet " href = " ./style.css " />
</ cabeça >
< corpo >
  < h1 > Olá IPFS! </ h1 >
</ corpo >
</ html >
```

```css
h1 {
  cor : verde;
}
```

## Etapa 3. Adicione ao IPFS

Em seguida, você precisa adicionar o site ao IPFS.

```
$ ipfs add -r site/
```

Você deve ver algo assim

```
added QmTVJ4XtUhqb6KMW8kxDwArVweACcy7VXAfinEks9Fd8cJ site/index.html
added QmZL2UBTwnhcLv66fARL9UV8W8a9ZA4iwTLcaUCsB1u1yW site/style.css
added QmeYxwj4CwCeGVhwi3xLrmBZUUFQdftshSiGLrTdTnWEVV site
```

O hash na última linha é a raiz do seu site, você pode visitar é abrindo ```https://gateway.ipfs.io/ipfs/<your hash here>```. Portanto, o site de exemplo está em <https://gateway.ipfs.io/ipfs/QmeYxwj4CwCeGVhwi3xLrmBZUUFQdftshSiGLrTdTnWEVV>

## Etapa 4. Publique no IPNS

Agora você tem um site estático simples hospedado no IPFS. O problema é que, sempre que você atualiza seu site, o hash muda e os links compartilhados continuarão apontando para a versão antiga. Você precisa de uma maneira de compartilhar sempre o hash mais recente. É aí que entra o IPNS. Ele permite que você armazene uma referência a um hash IPFS no espaço de nome do seu peerID (hash da sua chave pública).

```
$ ipfs name publish <your site hash>
```

Isso retornará seu peerID e o hash que você está publicando nele. Você pode confirmar executando


```
$ ipfs name resolve <peerId>
```

ou visualizando ```https://gateway.ipfs.io/ipns/<peerID>``` (observe que o diretório ```ipns``` não é ```ipfs```).

## Etapa 5. Concluído

É isso aí. Você Terminou. Sempre que você atualizar seu site, basta executar a etapa 4 novamente, e o IPNS garantirá que qualquer pessoa que solicite seu peerID obtenha o hash do seu site mais recente.

---

Autor: [Gio d'Amelio](https://github.com/giodamelio)

[Artigo Original](https://ipfs.io/ipfs/QmdPtC3T7Kcu9iJg6hYzLBWR5XCDcYMY7HV685E3kH3EcS/2015/09/15/hosting-a-website-on-ipfs/)



  
  
