---
layout: post
title:  "Sistemas de pagamento móvel: como funciona o Apple Pay"
date:   2020-01-25 17:59:38 -0200
categories: jekyll update
---

Introduzido pela primeira vez em 2014, o Apple Pay é um aplicativo de pagamento exclusivo para determinadas iterações do ecossistema de dispositivos móveis da Apple, a saber, o iPhone 6 (e posterior), o iPad 2 (e posterior), o iPad Mini 3 (e posterior) e o Apple Watch. Isso envolve o uso de um Elemento Seguro separado (um chip semelhante aos cartões de crédito com chip) para armazenar as informações do cartão de crédito do usuário no dispositivo - que é separado do processador principal em que os aplicativos são executados. Ele também funciona com o recurso de leitor de impressão digital Touch ID integrado, um dos recursos mais recentes a serem projetados para essa geração específica de dispositivos Apple.

## Como funciona?

O Apple Pay usa dois métodos: um criptograma, semelhante às transações EMV, e tokenização. Quando o usuário insere seu cartão de crédito pela primeira vez no aplicativo Apple Pay, as marcas de cartão de crédito (Visa, MasterCard ou American Express) enviarão um token e um criptograma para o dispositivo Apple. O token é um número de 16 dígitos que substitui o número real do cartão de crédito. O token e o criptograma são armazenados no chip Secure Element e enviados à rede da marca do cartão para verificação sempre que o usuário autoriza uma transação (por meio do scanner de impressões digitais, o único elemento autorizador necessário para isso).

A rede da marca do cartão recebe os dois elementos, descriptografa o criptograma e verifica sua autenticidade. Se o criptograma for autêntico, a rede passará o token para o banco emissor do cartão de crédito. O emissor descriptografa o token e, após uma verificação final de autenticidade, conclui a transação. Algumas transações nesta linha também exigem que o usuário insira seu código postal, para maior segurança e verificação.


![](https://trello-attachments.s3.amazonaws.com/5d7e8031eaec3e42c24aade0/5e4309c7705ce8308002aba4/48cd8aec7baa73899854f068ce3b4335/apple-pay.jpg)

>Fluxo de pagamento do Apple Pay (Fonte: developer.apple.com )

## Quais são as suas vantagens?

O próprio Apple Pay pode ser considerado muito seguro devido ao uso de certos recursos. Por um lado, o fato de o iOS ser de código fechado. Ao contrário do sistema operacional Android de código aberto do Google, é improvável que uma versão maliciosa do aplicativo seja lançada em seu ecossistema. O uso de impressões digitais para autorizar transações também evita fraudes por phishing, pois qualquer invasor em potencial precisa ter acesso ao dispositivo e às impressões digitais do usuário para executar qualquer esquema. Obviamente, os dispositivos Apple com jailbreak, que permitem aplicativos não assinados ou não verificados, são vulneráveis ​​a malwares que podem interceptar transações do Apple Pay.

## Quais são as suas desvantagens?

Existe uma desvantagem potencial para os usuários do Apple Watch. Sua versão do Apple Pay usa autorização PIN, devido à falta de um dispositivo de digitalização de impressões digitais, o que teoricamente pode torná-lo vulnerável a fraudes nas transações. Por outro lado, um usuário do Apple Watch pode fazer qualquer quantidade de transações com o Apple Pay sem precisar digitar novamente seu PIN - desde que não o tire, pois isso desautoriza a conta. Portanto, um invasor em potencial teria que fraudar o número PIN do usuário e roubar o dispositivo para realizar qualquer tipo de fraude, o que é altamente improvável mesmo com os usuários mais descuidados.


---

[Artigo Original](https://www.trendmicro.com/vinfo/us/security/news/mobile-safety/mobile-payment-systems-apple-pay)
