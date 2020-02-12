---
layout: post
title:  "Sistemas de pagamento móvel: como funciona o Android Pay"
date:   2020-01-26 17:59:38 -0200
categories: jekyll update
---

O Google Wallet, que foi sucedido pelo Android Pay em setembro de 2015, é o aplicativo de pagamento móvel para usuários do Android. Compatível com o Android KitKat e mais recente, o Android Pay suporta transações de toque e pagamento usando o recurso NFC (Near Field Communication) do dispositivo. Para fazê-lo funcionar, os usuários precisam [instalar o aplicativo](http://www.androidcentral.com/using-tap-and-pay-google-wallet) e inserir o número do cartão e outros detalhes necessários para a verificação do pagamento, como nome e endereço. Os usuários que possuem contas com os principais cartões de crédito ou débito nos EUA podem tirar uma foto instantânea do cartão usando a câmera do smartphone e ele insere automaticamente a data de vencimento.  

## Como o Google Wallet / Android Pay funciona?

O Google Wallet / Android Pay opera de duas maneiras: emulação de cartão com elemento seguro (SE) e emulação de cartão baseada em host. Na emulação de cartão com elemento seguro, o dispositivo é colocado no terminal NFC e todos os dados lidos serão roteados no SE, responsável pelas comunicações com o terminal NFC. Após a conclusão da transação, o aplicativo pode consultar o SE sobre o status e notificar o usuário.

![](https://trello-attachments.s3.amazonaws.com/5d7e8031eaec3e42c24aade0/5e4309c7705ce8308002aba4/23c7ab005277509d5abc84e250b9eb24/card-emulation-secure-element.png)

>Emulação de cartão com um elemento seguro (Fonte: developer.android.com )


Com a emulação de cartão baseada em host, o sistema operacional Android e o aplicativo estão diretamente envolvidos no processamento da transação de pagamento. Depois que o usuário leva o dispositivo ao terminal NFC, o aplicativo executa a emulação de cartão e lida com a comunicação com o terminal. Todos os dados são hospedados em um ambiente de nuvem, que efetua o processamento real da transação antes de retornar o status ao aplicativo.

![](https://trello-attachments.s3.amazonaws.com/5d7e8031eaec3e42c24aade0/5e4309c7705ce8308002aba4/0e30469a69ede2e5c60febd3fd63ebf3/host-based-card-emulation.png)

>Emulação de cartão baseada em host  (Fonte:  developer.android.com )

![](https://trello-attachments.s3.amazonaws.com/5d7e8031eaec3e42c24aade0/5e4309c7705ce8308002aba4/3fd60a22be0941d1341c944cb3d1259a/device-se-hce.png)

>Dispositivo operando SE e HCE  (Fonte:  developer.android.com )


## Quais são as suas vantagens?

Além da conveniência oferecida, uma vez que trabalha em conjunto com as principais empresas de crédito e débito e é suportado por muitos varejistas dos EUA, o Google Wallet / Android Pay hospeda os dados transmitidos durante as transações em um ambiente de nuvem seguro. Ele não armazena nenhum dado do usuário no próprio dispositivo, o que significa que, se o dispositivo Android estiver infectado com malware de roubo de informações, as informações e credenciais do usuário usadas por este aplicativo não serão necessariamente roubadas pelos criminosos cibernéticos.

## Quais são as suas desvantagens?

Não é segredo que a plataforma Android de código aberto sofreu uma longa lista de vulnerabilidades e explorações. E enquanto o Google envia atualizações para essas vulnerabilidades, nem todos os dispositivos de diferentes fabricantes podem receber esses patches devido à fragmentação móvel. Isso pode tornar esses dispositivos vulneráveis a ataques.

Há também relatos sobre o [ataque do Google Wallet Relay](http://arxiv.org/pdf/1209.0875.pdf) que exige que o cartão de destino esteja próximo de um dispositivo leitor, além de precisar instalar o software de retransmissão para funcionar. Com efeito, pode potencialmente comunicar os dados transmitidos pela rede ou ter acesso privilegiado a eles.


---

[Artigo Original](https://www.trendmicro.com/vinfo/us/security/news/mobile-safety/mobile-payment-systems-android-pay)

