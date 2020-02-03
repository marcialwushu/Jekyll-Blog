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


