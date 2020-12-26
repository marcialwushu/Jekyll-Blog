---
layout: post
title:  "Por que você deve usar um projeto de banco de dados SSDT para seu data warehouse"
date:   2020-03-16 17:59:38 -0200
categories: jekyll update
---

Neste post, tentarei convencê-lo de que usar projetos de banco de dados SSDT (SQL Server Data Tools) é realmente uma boa ideia. Recentemente, durante um projeto, tenho defendido que realmente vale a pena o esforço. Como sou um arquiteto de BI, estou estruturando esta conversa em torno de um data warehouse, mas certamente se aplica a qualquer tipo de banco de dados. 

## O que é um projeto de banco de dados no SQL Server Data Tools (SSDT)?

Um data warehouse contém vários objetos de banco de dados, como tabelas, visualizações, procedimentos armazenados, funções e assim por diante. Estamos muito acostumados a usar projetos SSDT BI (anteriormente BIDS) para SSIS (Integration Services), SSAS (Analysis Services) e SSRS (Reporting Services). No entanto, é menos comum usar SSDT para armazenar o DDL (linguagem de definição de dados) para objetos de banco de dados.

