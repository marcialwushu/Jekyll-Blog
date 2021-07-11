---
layout: post
title:  "Como corrigi um erro 'cb.apply não é uma função' ao usar o Gitbook"
date:   2020-04-01 17:59:38 -0200
categories: jekyll update
---

Eu uso regularmente o Gitbook, um pequeno software Node usado para gerar um ebook a partir de um conjunto de arquivos de marcação.

Eu uso para meus ebooks. Hoje eu estava tentando gerar um PDF, correndo, quando eu tive um erro muito estranho:gitbook pdf .

```
➜  ebook git:(master) ✗ gitbook pdf .
/usr/local/lib/node_modules/gitbook-cli/node_modules/npm/node_modules/graceful-fs/polyfills.js:287
      if (cb) cb.apply(this, arguments)
                 ^

TypeError: cb.apply is not a function
    at /usr/local/lib/node_modules/gitbook-cli/node_modules/npm/node_modules/graceful-fs/polyfills.js:287:18
 
```

cb.apply is not a function. O que isso significa? E o mais importante, por que eu tenho esse erro agora? Eu não atualizei o pacote de gitbook recentemente, e eu não... Acho que atualizei a versão .do Node.js que uso. Mas não faço ideia por que esse deveria ser o problema. Talvez seja.

de qualquer maneira.. o erro vem do arquivo. Este é o ```graceful``` pacote npm, um "substituto drop-in para o módulo node.js embutido, fazendo várias melhorias", instalado mais de 33 milhões de vezes por semana. ```/usr/local/lib/node_modules/gitbook-cli/node_modules/npm/node_modules/graceful-fs/polyfills.jsfs```

Uma dessas melhorias parece quebrar meu fluxo de trabalho, hoje!

Eu não tenho muito tempo livre para descobrir por que minha versão node.js dá problemas com este aplicativo que eu não criei e esta biblioteca.

Abri o arquivo, de onde vem o erro ```./usr/local/lib/node_modules/gitbook-cli/node_modules/npm/node_modules/graceful-fs/polyfills.js```

Aqui está a função que dá o problema:

```js
function statFix (orig) {
  if (!orig) return orig
  // Older versions of Node erroneously returned signed integers for
  // uid + gid.
  return function (target, cb) {
    return orig.call(fs, target, function (er, stats) {
      if (!stats) return cb.apply(this, arguments)
      if (stats.uid < 0) stats.uid += 0x100000000
      if (stats.gid < 0) stats.gid += 0x100000000
      if (cb) cb.apply(this, arguments)
    })
  }
}
```

Isso parece consertar algo na versão mais antiga de Node.js.. Não deveria ser necessário para mim.

Vejo que está sendo usado nas linhas 62-64 do mesmo arquivo:

```js
fs.stat = statFix(fs.stat)
fs.fstat = statFix(fs.fstat)
fs.lstat = statFix(fs.lstat)
```

Eu comentei essas linhas:

```js
// fs.stat = statFix(fs.stat)
// fs.fstat = statFix(fs.fstat)
// fs.lstat = statFix(fs.lstat)
```

e tudo funcionou bem, eu fui capaz de executar o comando novamente, e eu tenho o meu bom PDF Gitbook

---

Autor: [Flavio Copes](https://flaviocopes.com/)

[Artigo Original](https://flaviocopes.com/cb-apply-not-a-function/)

