---
layout: post
title:  "Criar projeto de banco de dados SQL Server com Visual Studio"
date:   2020-03-15 17:59:38 -0200
categories: jekyll update
---

## Introdução

Quando trabalhamos em qualquer projeto, um banco de dados desempenha um papel importante e depois de algum tempo, quando o número de tabelas, visualizações e procedimentos aumenta - torna-se muito difícil gerenciar os scripts.

E mesmo depois disso, quando gerenciamos os scripts, ainda precisamos comparar em qual script trabalhamos e quais permanecem em qualquer banco de dados específico. Existem muitas ferramentas boas disponíveis no mercado para comparar bancos de dados, mas a maioria delas é paga.

Portanto, neste artigo, aprenderemos como podemos gerenciar nossos scripts de banco de dados usando o projeto de banco de dados SQL Server do Visual Studio.

Podemos criar um novo projeto de banco de dados e importar o esquema do banco de dados de um banco de dados existente, um arquivo de script .sql ou um aplicativo da camada de dados (.dacpac). Podemos então invocar as mesmas ferramentas de designer visual (Transact-SQL Editor, Table Designer) disponíveis para o desenvolvimento do banco de dados conectado para fazer alterações no projeto de banco de dados offline e publicar as alterações de volta no banco de dados de produção. As alterações também podem ser salvas como um script a ser publicado posteriormente. Usando o painel Propriedades do projeto, podemos alterar a plataforma de destino para diferentes versões do SQL Server (incluindo SQL Azure).

## Pré-requisito

- VS2015 ou VS2017 deve ser instalado em sua máquina.
- Servidor SQL - para importar script de banco de dados e publicar scripts novos ou alterados.

Vamos começar!!

1. Abra o VS e crie um novo projeto a partir do Menu, selecione Arquivo >> Novo >> Projeto.

![](https://csharpcorner.azureedge.net/article/create-sql-server-database-project-with-visual-studio/Images/image001.png)

