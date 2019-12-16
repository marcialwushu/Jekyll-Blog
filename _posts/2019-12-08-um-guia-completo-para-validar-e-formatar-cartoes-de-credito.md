---
layout: post
title:  "Um guia completo para validar e formatar cartões de crédito"
date:   2019-12-08 17:59:38 -0200
categories: jekyll update
---


Os formulários de cartão de crédito são um desses elementos que toda empresa on-line precisará implementar em um ponto ou outro, e geralmente podem ser um ponto problemático para desenvolvedores e usuários. Dito isto, é crucial que esses formulários sejam projetados para serem fáceis de usar e intuitivos, pois são o ponto de entrada para usuários pagantes: seria uma pena se uma empresa perdesse um cliente em potencial para um formulário de pagamento mal projetado, mesmo que eles fizeram tudo certo.

O objetivo deste post é explicar como implementar seu próprio formulário de cartão de crédito incrível, completo com validação e formatação sem erros. Se você está aqui apenas para obter o código, fique à vontade para rolar até o final para ver a implementação final.


# Índice

- Tipos de cartões de crédito
- Validando cartões
- Validando o CVV
- Formatação Cartões
- Embrulhando-o

## Tipos de cartões de crédito

|  Issuer     |    Length     |    Test Number      |     RegEx Pattern      |
|:-------------|--------------|----------------------|-----------------------|
|Mastercard	|16	|5555 5555 5555 4444	|  ```/^5[1-5][0-9]{14}$|^2(?:2(?:2[1-9]|[3-9][0-9])|[3-6][0-9][0-9]|7(?:[01][0-9]|20))[0-9]{12}$/```  |
|American Express	|15	|3782 822463 10005 |        ```/^3[47][0-9]{13}$/```       |
|Visa	|16	|4242 4242 4242 4242	|  ```/^4[0-9]{12}(?:[0-9]{3})?$/```   |
|Discover	|16	|6011 1111 1111 1117	|```/^65[4-9][0-9]{13}|64[4-9][0-9]{13}|6011[0-9]{12}|(622(?:12[6-9]|1[3-9][0-9]|[2-8][0-9][0-9]|9[01][0-9]|92[0-5])[0-9]{10})$/```  |
|JCB	|16	|3530 1113 3330 0000	| ```/^(?:2131|1800|35[0-9]{3})[0-9]{11}$/```   |
|Diner’s Club	|14	|3056 930902 5904	| ```/^3(?:0[0-5]|[68][0-9])[0-9]{11}$/```   |
|Maestro	|13-19	|6759 6498 2643 8453    	|        ```/^(5018|5081|5044|5020|5038|603845|6304|6759|676[1-3]|6799|6220|504834|504817|504645)[0-9]{8,15}$/``` |


Algumas coisas a serem observadas aqui:

- Como parte da expansão da série 2 da Mastercard , seus cartões agora podem começar com 2
- O American Express possui um CVV incomum de 4 dígitos
- Os cartões que você suporta devem depender do suporte do gateway de pagamento selecionado. É uma prática recomendada permitir que cartões não suportados passem pela validação do lado do cliente.
- O Maestro é uma tarefa difícil de lidar e não é suportado pela maioria dos gateways de pagamento. Como tal, o Maestro não será coberto no restante deste post.


Para obter uma lista dos gateways de pagamento comuns e dos cartões que eles suportam, consulte [esta lista da Aria Systems](https://developer.ariasystems.net/UserDocumentation/07Payments_and_Credits/Payment_Gateways/06_Supported_Payment_Gateways_and_Payment_Methods) . Para obter uma lista de cartões de teste, consulte [este repositório do Github](https://github.com/drmonkeyninja/test-payment-cards) . Para mais cartões e seus padrões RegEx, veja [esta lista no Github](https://gist.github.com/michaelkeevildown/9096cd3aac9029c4e6e05588448a8841).

