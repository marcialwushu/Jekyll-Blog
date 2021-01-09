---
layout: post
title:  "Pix - Pagamentos Instantâneos no Brasil"
date:   2020-03-19 17:59:38 -0200
categories: jekyll update
---

Pix é a implementação do ecossistema de pagamentos instantâneos liderado pelo Banco Central do Brasil (BCB) para possibilitar transferências de dinheiro online com custos reduzidos, maior segurança e disponibilidade 24 horas por dia, 7 dias por semana. As transferências ocorrem diretamente da conta do pagador para a conta do beneficiário, sem a necessidade de intermediários, resultando em menores custos de transação.

Pix estará disponível para pessoas e empresas. Ambos precisam ter uma chave identificadora registrada em alguma entidade financeira - bancos, fintechs ou instituições de pagamento - para prosseguir com a transação. De acordo com os critérios de elegibilidade estabelecidos pelo BCB, certas entidades serão obrigadas a oferecer essa forma de pagamento, enquanto outras poderão oferecê-la opcionalmente ou não.

Nesta etapa, vamos explicar como estender a implementação do protocolo do provedor de pagamento para permitir que as lojas ofereçam Pix como um método de pagamento adicional para seus clientes.

![](data/bf3c11b-post_BCexplica_pagamentos_instantaneos_ingles_Features.jpg)

>Esses são alguns dos benefícios de um ecossistema de pagamentos instantâneos destacados pelo BCB

## Condições de integração

Se você está pronto para desenvolver o middleware que implementa nosso protocolo de provedor de pagamento, deve estar ciente destes requisitos:

- Todos os pontos de extremidade devem ser servidos por HTTPS na porta 443 com suporte TLS 1.2. Conexões por HTTP não protegido não serão aceitas em nenhuma circunstância.
- O integrador deve criar um subdomínio ou nome de domínio para os terminais do provedor. Os endereços IP não serão aceitos como nomes em nenhuma circunstância.
- O middleware deve responder de forma consistente dentro dos tempos de resposta estabelecidos. Aplicamos um tempo de resposta máximo de 5 segundos para testes de homologação, bem como um tempo de resposta máximo de 20 segundos para qualquer outra solicitação de API.

Embora nosso protocolo descreva dez pontos finais para implementação, nem todos eles são aplicáveis ​​ao integrar pagamentos instantâneos Pix. Em relação aos dois fluxos de provedor:

- [Fluxo de Pagamento](https://developers.vtex.com/vtex-developer-docs/reference-link/payment-flow): sua implantação é obrigatória .
- [Fluxo de configuração](https://developers.vtex.com/vtex-developer-docs/reference-link/configuration-flow): sua implementação é opcional e atualmente não está disponível para Pix .

A tabela abaixo fornece mais detalhes sobre a aplicabilidade de cada endpoint aos pagamentos instantâneos Pix. Mais detalhes sobre as etapas de integração são fornecidos no restante deste tutorial.

|Fluxo do Provedor|	Endpoint|	Aplicável ao Pix?|
|-----------------|---------|-------------------|
|Forma de pagamento	|Listar métodos de pagamento	|:warning: Obsoleto|
|Forma de pagamento	|Listar Manifesto do Provedor de Pagamento|	:white_check_mark: sim|
|Forma de pagamento	|Criar Pagamento|	:white_check_mark: sim|
|Forma de pagamento	|Cancelar Pagamento	|:white_check_mark: sim|
|Forma de pagamento	|Captura de Pagamento	|:white_check_mark: sim|
|Forma de pagamento	|Reembolsar Pagamento	|:white_check_mark: sim|
|Forma de pagamento|	Solicitação de entrada (BETA)|	:white_check_mark: sim|
|Configuração	|Criar token de autorização	|:x: Não|
|Configuração	|Autenticação de Provedor	|:x: Não|
|Configuração|	Obtenha credenciais	|:x: Não|

>Restrições de mercado

>Pix não está disponível para clientes de mercado que usam o Checkout Split.

---

>Exemplos de solicitação e resposta

>Os JSONs a seguir são apenas exemplos . Cada parceiro deve adaptar os modelos às suas realidades, com os dados necessários para realizar a integração.

## Etapas de integração

### Estabeleça os métodos de pagamento disponíveis

A primeira informação que seu provedor tem de nos informar é quais são os métodos de pagamento que ele administra. Para fazer isso, você pode fazer uma chamada de API usando a Lista de rota de manifesto do provedor de pagamento.

A resposta esperada é:

200 OK

```json
{
    "paymentMethods": [
        {
            "name": "Visa",
            "allowsSplit": "onCapture"
        },
        { 
            "name": "Pix",
            "allowsSplit": "disabled"
        },
        {
            "name": "Mastercard",
            "allowsSplit": "onCapture"
        },
        {
            "name": "American Express",
            "allowsSplit": "onCapture"
        },
        {
            "name": "BankInvoice",
            "allowsSplit": "onAuthorize"
        },
        {
            "name": "Privatelabels",
            "allowsSplit": "disabled"
        },
        {
            "name": "Promissories",
            "allowsSplit": "disabled"
        }
    ],
    "customFields": [
        {
            "name": "Merchant's custom field",
            "type": "text"
        },
        {
            "name": "Merchant's custom select field",
            "type": "select",
            "options": [
                {
                    "text": "Field option 1",
                    "value": "1",
                },
                {
                    "text": "Field option 2",
                    "value": "2",
                },
                {
                    "text": "Field option 3",
                    "value": "3",
                }
            ]
        }
    ]
}
```

>Divisão de pagamento para Pix

>Pix ainda não lida com parcelamento de pagamento, esta funcionalidade será lançada em breve.

## Criar método de pagamento Pix

Agora você precisa criar uma nova forma de pagamento e há apenas uma rota como opção.

Muitas informações necessárias derivam dos dados do carrinho no Smart Checkout, então tome cuidado e valide todas as informações da carga útil.

A solicitação é assim:

Pix Success aprovado

```json
{
    "reference": "32478982",
    "orderId": "v967373115140abc",
    "transactionId": "D3AA1FC8372E430E8236649DB5EBD08E",
    "paymentId": "F5C1A4E20D3B4E07B7E871F5B5BC9F91",
    "paymentMethod": "Pix",
    "paymentMethodCustomCode": null,
    "merchantName": "mystore",
    "value": 4307.23,
    "currency": "BRL",
    "installments": 31,
    "deviceFingerprint": "12ade389087fe",
    "card": {
        "holder": "John Doe",
        "number": "4682185088924788",
        "csc": "021",
        "expiration": {
            "month": "06",
            "year": "2029"
        }
    },
    "miniCart": {
        "shippingValue": 11.44,
        "taxValue": 10.01,
        "buyer": {
            "id": "c1245228-1c68-11e6-94ac-0afa86a846a5",
            "firstName": "John",
            "lastName": "Doe",
            "document": "01234567890",
            "documentType": "CPF",
            "email": "john.doe@example.com",
            "phone": "+5521987654321"
        },
        "shippingAddress": {
            "country": "BRA",
            "street": "Praia de Botafogo St.",
            "number": "300",
            "complement": "3rd Floor",
            "neighborhood": "Botafogo",
            "postalCode": "22250040",
            "city": "Rio de Janeiro",
            "state": "RJ"
        },
        "billingAddress": {
            "country": "BRA",
            "street": "Brigadeiro Faria Lima Avenue",
            "number": "4440",
            "complement": "10th Floor",
            "neighborhood": "Itaim Bibi",
            "postalCode": "04538132",
            "city": "São Paulo",
            "state": "SP"
        },
        "items": [
            {
                "id": "132981",
                "name": "My First Product",
                "price": 2134.90,
                "quantity": 2,
                "discount": 5.00
            },
            {
                "id": "123242",
                "name": "My Second Product",
                "price": 21.98,
                "quantity": 1,
                "discount": 1.00
            }
        ]
    },
    "url": "https://admin.mystore.example.com/orders/v32478982",
    "callbackUrl": "https://api.example.com/some-path/to-notify/status-changes?an=mystore",
    "returnUrl": "https://mystore.example.com/checkout/order/v32478982"
}'
```

Como resultado, esperamos a seguinte resposta:

>❗️Estabeleça um fluxo organizado

>Lembre-se que, por padrão, o QRCode deve ter um tempo de expiração de cinco minutos (300 segundos). Além disso, o parceiro deve respeitar o tempo de retorno da chamada (20 segundos).


```json
{
  "paymentId": "F5C1A4E20D3B4E07B7E871F5B5BC9F91",
  "status": "undefined",
  "tid": "TID1578324421",
  "authorizationId": null,
  "nsu": null,
  "code": "APP123",
  "paymentAppData": {
    "payload": "{\"code\":\"https://bacen.pix/pix/code\",\"qrCodeBase64Image\":\"iVBORw0KGgoAAAANSUhEUgAAAAIAAAACCAYAAABytg0kAAABQGlDQ1BJQ0MgUHJvZmlsZQAAKJFjYGDiSSwoyGFhYGDIzSspCnJ3UoiIjFJgf8LAxSDMwMkgwiCZmFxc4BgQ4ANUwgCjUcG3awyMIPqyLsgspwWXFu+Xeyundb6w0WL33C5M9SiAKyW1OBlI/wHihOSCohIGBsYYIFu5vKQAxG4AskWKgI4CsqeA2OkQ9goQOwnC3gNWExLkDGRfALIFkjMSU4DsB0C2ThKSeDoSG2ovCLAZGZkbhBNwKKmgJLWiBEQ75xdUFmWmZ5QoOAJDJ1XBMy9ZT0fByMDIgIEBFNYQ1Z9vgMOQUYwDIZapzMBgmQEUfIQQSxNmYNiZzsDAU4UQU5/PwMBrxMBw5GJBYlEi3AGM31iK04yNIGzu7QwMrNP+//8M9Ca7JgPD3+v////e/v//32UMDMy3GBgOfAMA4+RdqZ9YRkcAAABWZVhJZk1NACoAAAAIAAGHaQAEAAAAAQAAABoAAAAAAAOShgAHAAAAEgAAAESgAgAEAAAAAQAAAAKgAwAEAAAAAQAAAAIAAAAAQVNDSUkAAABTY3JlZW5zaG900Fpo3gAAAdJpVFh0WE1MOmNvbS5hZG9iZS54bXAAAAAAADx4OnhtcG1ldGEgeG1sbnM6eD0iYWRvYmU6bnM6bWV0YS8iIHg6eG1wdGs9IlhNUCBDb3JlIDUuNC4wIj4KICAgPHJkZjpSREYgeG1sbnM6cmRmPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5LzAyLzIyLXJkZi1zeW50YXgtbnMjIj4KICAgICAgPHJkZjpEZXNjcmlwdGlvbiByZGY6YWJvdXQ9IiIKICAgICAgICAgICAgeG1sbnM6ZXhpZj0iaHR0cDovL25zLmFkb2JlLmNvbS9leGlmLzEuMC8iPgogICAgICAgICA8ZXhpZjpQaXhlbFhEaW1lbnNpb24+MjwvZXhpZjpQaXhlbFhEaW1lbnNpb24+CiAgICAgICAgIDxleGlmOlVzZXJDb21tZW50PlNjcmVlbnNob3Q8L2V4aWY6VXNlckNvbW1lbnQ+CiAgICAgICAgIDxleGlmOlBpeGVsWURpbWVuc2lvbj4yPC9leGlmOlBpeGVsWURpbWVuc2lvbj4KICAgICAgPC9yZGY6RGVzY3JpcHRpb24+CiAgIDwvcmRmOlJERj4KPC94OnhtcG1ldGE+Cl89Cn4AAAASSURBVAgdY/wPBAxAwAQiQAAAPfgEAIAu9DkAAAAASUVORK5CYII=\"}"
  },
  "message": "The customer needs to finish the payment flow",
  "delayToAutoSettle": 1209600,
  "delayToAutoSettleAfterAntifraud": 120,
  "delayToCancel": 300
}
```

## Cancelar um pagamento

Para cancelar um pagamento, você já deve ter criado um. Para fazer isso, você fará uma chamada de API usando a rota POST Cancelar pagamento :

```json
{
    "paymentId": "F5C1A4E20D3B4E07B7E871F5B5BC9F91",
    "requestId": "1234"
}
```

Depois que o provedor realiza o cancelamento do pagamento, esperamos uma resposta como esta:

200 OK 

```json
{
    "paymentId": "F5C1A4E20D3B4E07B7E871F5B5BC9F91",
    "message": "Successfully cancelled",
    "code": null,
    "cancellationId": "1457BD07E6",
    "requestId": "1234"
}
```

## Captura de Pagamento

Se sua transação foi concluída com sucesso, o provedor pode capturar o pagamento.

Assim, para captar o pagamento, a VTEX enviará as informações abaixo por meio do POST Captura de rota de pagamento :

Sucesso

```json
{
    "paymentId": "5B127F1E0C944EF9ACE264FEC1FC0E91",
    "transactionId": "611966",
    "value": 20.0,
    "requestId": "5678"
}
```

A resposta deve ser semelhante ao seguinte corpo de resposta:

200 OK

```json
{
    "paymentId": "5B127F1E0C944EF9ACE264FEC1FC0E91",
    "settleId": "CEE16492C6",
    "value": 20.0,
    "code": null,
    "message": null,
    "requestId": "5678"
}
```

## Reembolsar Pagamento

O provedor deve estar pronto para receber a seguinte solicitação por meio do POST Rota de pagamento de reembolso :

Sucesso

```json
{
    "paymentId": "VQKIIBUVOFDBIDLKZPOWSKETDYWCMJSACDVXWFCJVSKXGYVBBVISZRJLLQEKERJEMDYEINOUMFAZZGNEDVBQBABLUKLFBSEEIGLCAQTOGOGURKLFCAHJQTDMBNKYBIST",
    "transactionId": "611966",
    "settleId": "31018A3281",
    "value": 10.0,
    "requestId": "5678"
}
```

A resposta esperada é:

200 OK

```json
{
    "paymentId": "VQKIIBUVOFDBIDLKZPOWSKETDYWCMJSACDVXWFCJVSKXGYVBBVISZRJLLQEKERJEMDYEINOUMFAZZGNEDVBQBABLUKLFBSEEIGLCAQTOGOGURKLFCAHJQTDMBNKYBIST",
    "refundId": null,
    "value": 0.0,
    "code": "refund-manually",
    "message": "Refund should be done manually",
    "requestId": "5678"
}
```

## Comunique-se com o Gateway

A última rota - POST Solicitação de entrada (BETA) - implementa uma URL que facilita uma conexão direta entre nosso serviço de gateway e o provedor de pagamento.

A solicitação será:

Sucesso

```json
'{
    "requestId": "LA4E20D3B4E07B7E871F5B5BC9F91",
    "transactionId": "D3AA1FC8372E430E8236649DB5EBD08E",
    "paymentId": "F5C1A4E20D3B4E07B7E871F5B5BC9F91",
    "authorizationId": "{{authorizationId}}",
    "tid": "{{tid}}",
    "requestData": {
        "body": "{{originalRequestBody}}"
    }
}'
```

Como resultado, o cliente deve enviar a seguinte resposta:

200 OK

```json
{
    "requestId": "{{requestId}}",
    "transactionId": "{{transactionId}}",
    "paymentId": "{{paymentId}}",
    "authorizationId": "{{authorizationId}}",
    "tid": "{{tid}}",
    "requestData": {
        "body": "{{originalRequestBody}}"
    }
}
```

## Empacotando

Se você concluiu todas as etapas de integração, deverá ter uma implementação funcional de nosso Protocolo de Provedor de Pagamento com pagamentos instantâneos Pix. A última etapa antes que as lojas VTEX possam usar seu fornecedor é concluir nosso processo de homologação.

---

[Artigo Original](https://developers.vtex.com/vtex-developer-docs/docs/pix-instant-payments-in-brazil)





