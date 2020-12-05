---
layout: post
title:  "Como converter coleções do Postman para OpenAPI/Swagger"
date:   2020-03-14 17:59:38 -0200
categories: jekyll update
---

O [Postman](https://www.postman.com/) é uma ótima ferramenta para desenvolver e testar APIs RESTful criadas por outras pessoas ou testar e desenvolver as que você mesmo criou. Ele oferece uma interface de usuário elegante com a qual é possível fazer solicitações JSON, XML e até HTML, sem a necessidade de escrever um monte de código apenas para testar a funcionalidade de uma API.

O [Swagger](https://swagger.io/docs/specification/about/) é um conjunto de ferramentas de código aberto criadas em torno da Especificação OpenAPI que podem ajudá-lo a projetar, criar, documentar e consumir APIs REST. As principais ferramentas do Swagger incluem:

- Swagger Editor – editor no navegador onde você pode escrever as especificações OpenAPI.
- Swagger UI – renderiza as especificações do OpenAPI como documentação interativa da API no navegador.
- Swagger Codegen – gera stubs de servidor e bibliotecas de clientes a partir de uma especificação OpenAPI.

A especificação OpenAPI é um formato de descrição de API para APIs REST. Um arquivo OpenAPI permite que você descreva toda a sua API, incluindo:

- Endpoints disponíveis (/ usuários) e operações em cada endpoint (GET / usuários, POST / usuários)
- Parâmetros de operação Entrada e saída para cada operação
- Métodos de autenticação da API REST
- Informações de contato, licença, termos de uso e outras informações.

Bom, agora que entendemos o que cada ferramenta/serviço é e faz conseguimos entender onde aplicar cada uma. O OpenAPI vem se tornando um padrão da comunidade para compartilhar documentações de APIs RESTful, porém eu gosto muito da ferramenta do Postman para desenvolver e testar as APIs no dia a dia, porém as funcionalidades para times e compartilhamento da documentação do Postman são pagas, o que torna inviável o uso em pequenos projetos ou empresas com orçamento restrito, mas ao mesmo tempo manter duas bases de documentações é muito trabalhoso e pode chegar a ser inviável dependendo da quantidade de endpoints.

## A solução!

A solução que eu encontrei foi centralizar e desenvolver todas as documentações das APIs no formato OpenAPI, porque como essa especificação é desenvolvida em um arquivo YAML ou JSON, conseguimos versionar esses arquivos por projetos, no caso de uma arquitetura em microserviços isso é extremamente úteis, e como o Postman permite a importação da especificação do OpenAPI, fica fácil de atualizar sua versão local.

Bom, se você como eu começou a desenvolver toda a sua documentação no Postman e agora está buscando em uma solução fácil e rápida para converter de Postman para OpenAPI, fique tranquilo, pois podemos usar o [serviço gratuito da APIMatic](https://apimatic.io/transformer) para fazer essa conversão. Faça o registro no site e em poucos minutos tenha toda a sua documentação convertida!


---

Autor: [Henrique Marques Fernandes](https://marquesfernandes.com/author/shadowlik/)

[Artigo Original](https://marquesfernandes.com/desenvolvimento/como-converter-colecoes-do-postman-para-openapi-swagger/)
