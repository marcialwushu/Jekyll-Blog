---
layout: post
title:  "ANÁLISE QUALITATIVA DE CÓDIGO COM SONARQUBE"
date:   2020-01-20 17:59:38 -0200
categories: jekyll update
---

![](https://trello-attachments.s3.amazonaws.com/5d7e8031eaec3e42c24aade0/5e376a07663eaa488ffabb77/dcb1fa2fe36d2779ac760dbc2efb816d/resultado-analise-05.png)

## INTRODUÇÃO


Qualidade de código é um assunto, por vezes, pouco debatido. Muitas vezes, nos limitamos a entender este tema por um simples “código que funciona”. Mas, isto é realmente suficiente?


## AFINAL, O QUE É QUALIDADE DE CÓDIGO?


Existem muitas definições sobre o que é um bom código. Recentemente, li o excelente livro Clean Code (Robert Martin, 2009) e lá temos diversas definições sobre o tema. Mas um ponto em comum entre os autores que contribuíram para o livro é: um bom código é simples e eficiente. Para alcançar tal objetivo, diversos programadores ao longo dos anos criaram algumas dezenas de regras e design patterns, a fim de resolver este problema.


## O SONARQUBE

O SonarQube é uma plataforma de código aberto desenvolvida pela SonarSource para inspeção contínua da qualidade do código para realizar revisões automáticas com análise estática de código para detectar bugs, códigos cheirosos e vulnerabilidades de segurança em 20+ linguagens de programação.

Ele oferece relatórios sobre código duplicado, padrões de codificação, testes de unidade, cobertura de código, complexidade de código, comentários, bugs e vulnerabilidades de segurança. (Fonte: Wikipedia)


## VAMOS FAZER UM PROJETO DE EXEMPLO…


Agora, vamos criar um projeto de exemplo. O código fonte deste projeto pode ser encontrado em https://gitlab.com/orlandoburli/calculadora-de-impostos.

