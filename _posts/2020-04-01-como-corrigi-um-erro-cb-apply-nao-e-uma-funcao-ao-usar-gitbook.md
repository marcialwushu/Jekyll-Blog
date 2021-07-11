---
layout: post
title:  "Como corrigi um erro "cb.apply não é uma função" ao usar o Gitbook"
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

cb.apply is not a function. O que isso significa? E o mais importante, por que eu tenho esse erro agora? Eu não atualizei o pacote de gitbook recentemente, e eu não... Acho que atualizei a versão .js Nó que corro. Mas não faço ideia por que esse deveria ser o problema. Talvez seja.

