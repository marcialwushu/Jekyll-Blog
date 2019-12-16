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
|Mastercard	|16	|5555 5555 5555 4444  	|            ```/^5[1-5][0-9]{14}$|^2(?:2(?:2[1-9]|[3-9][0-9])|[3-6][0-9][0-9]|7(?:[01][0-9]|20))[0-9]{12}$/```                   |
|American Express	|15	|3782 822463 10005 |        ```/^3[47][0-9]{13}$/```                   |
|Visa	|16	|4242 4242 4242 4242	|  ```/^4[0-9]{12}(?:[0-9]{3})?$/```                |
|Discover	|16	|6011 1111 1111 1117	|            ```/^65[4-9][0-9]{13}|64[4-9][0-9]{13}|6011[0-9]{12}|(622(?:12[6-9]|1[3-9][0-9]|[2-8][0-9][0-9]|9[01][0-9]|92[0-5])[0-9]{10})$/```  |
|JCB	|16	|3530 1113 3330 0000	|            ```/^(?:2131|1800|35[0-9]{3})[0-9]{11}$/```           |
|Diner’s Club	|14	|3056 930902 5904	|              ```/^3(?:0[0-5]|[68][0-9])[0-9]{11}$/```            |
|Maestro	|13-19	|6759 6498 2643 8453    	|        ```/^(5018|5081|5044|5020|5038|603845|6304|6759|676[1-3]|6799|6220|504834|504817|504645)[0-9]{8,15}$/```        |




Algumas coisas a serem observadas aqui:

- Como parte da expansão da série 2 da Mastercard , seus cartões agora podem começar com 2
- O American Express possui um CVV incomum de 4 dígitos
- Os cartões que você suporta devem depender do suporte do gateway de pagamento selecionado. É uma prática recomendada permitir que cartões não suportados passem pela validação do lado do cliente.
- O Maestro é uma tarefa difícil de lidar e não é suportado pela maioria dos gateways de pagamento. Como tal, o Maestro não será coberto no restante deste post.


Para obter uma lista dos gateways de pagamento comuns e dos cartões que eles suportam, consulte [esta lista da Aria Systems](https://developer.ariasystems.net/UserDocumentation/07Payments_and_Credits/Payment_Gateways/06_Supported_Payment_Gateways_and_Payment_Methods). Para obter uma lista de cartões de teste, consulte [este repositório do Github](https://github.com/drmonkeyninja/test-payment-cards). Para mais cartões e seus padrões RegEx, veja [esta lista no Github](https://gist.github.com/michaelkeevildown/9096cd3aac9029c4e6e05588448a8841).


## Validando cartões

Por quê?

- O usuário recebe feedback imediato sobre um erro de entrada; se um cartão inválido for inserido, ele não precisará clicar no botão enviar, aguardar o servidor retornar um erro e preencher o formulário novamente.
- Isso diminui a carga do servidor e impede que solicitações inválidas sejam contadas no limite de taxa da API.

### O algoritmo de Luhn

Os números dos cartões de crédito podem parecer aleatórios, mas na verdade há um significado oculto por trás de cada grupo de números.

![](https://miro.medium.com/max/460/0*2sYEHfIj5UHkF3CI)

No diagrama acima:

1. **Identificador principal da indústria (MII - Major Industry Identifier)** - identifica a indústria do cartão. Veja [aqui](https://en.wikipedia.org/wiki/ISO/IEC_7812#Major_industry_identifier) uma lista de setores e seus dígitos correspondentes.
2. **Número de identificação do emissor (IIN - Issuer Identification Number)** - identifica o emissor do cartão. O American Express começa com 34 ou 37, o Mastercard começa com 2221–2720 ou 51–55, o Visa começa com 4. Veja [aqui](https://en.wikipedia.org/wiki/Payment_card_number#Issuer_identification_number_(IIN)) uma lista de todas as faixas de IIN. Isso é especialmente útil para futuras atualizações se os emissores de cartões decidirem expandir seus intervalos de IIN.
3. **Número da conta** - identifica a conta do cliente
4. **Soma de verificação** - garante que o número da conta é válido

O algoritmo Luhn determina a validade de um cartão usando o número da conta e a soma de verificação (rótulos 3 e 4). Funciona quase como mágica:

- No dígito mais à direita do número do seu cartão, dobre todos os outros dígitos.
- Se o dígito dobrado for maior que 9 (ex. 8 * 2 = 16), subtraia 9 do produto (16–9 = 7).
- Soma os dígitos.
- Se não houver resto após dividir por 10 (soma% 10 == 0), o cartão é válido.

Usando o cartão acima, aqui está o algoritmo de Luhn em ação:

![](https://miro.medium.com/max/627/1*g3-dgbQsemeq1FqtOu4SMw.png)

Resumindo a última linha, obtemos um valor de 90, que é um múltiplo de 10. Este cartão é válido!

Aqui está uma implementação Javascript do algoritmo Luhn:

```js
function checkLuhn(value) {
  // remove all non digit characters
  var value = value.replace(/\D/g, '');
  var sum = 0;
  var shouldDouble = false;
  // loop through values starting at the rightmost side
  for (var i = value.length - 1; i >= 0; i--) {
    var digit = parseInt(value.charAt(i));
    
    if (shouldDouble) {
      if ((digit *= 2) > 9) digit -= 9;
    }

    sum += digit;
    shouldDouble = !shouldDouble;
  }
  return (sum % 10) == 0;
}
```

[Demo](https://codepen.io/kelvinzhang/pen/rrgaxK?editors=1010)

Você pode visualizar implementações do algoritmo Luhn em outras linguagens como Java, Swift, PHP e Python [aqui](https://en.wikipedia.org/wiki/Luhn_algorithm#Implementation_examples).

**Verificando cartões suportados**

Com referência à lista de cartões acima e suas especificações, podemos criar um validador com base no RegEx para cada cartão específico.

A melhor maneira de acompanhar diferentes cartões e seus padrões é armazená-los em um objeto literal:

```js

var acceptedCreditCards = {
  visa: /^4[0-9]{12}(?:[0-9]{3})?$/,
  mastercard: /^5[1-5][0-9]{14}$|^2(?:2(?:2[1-9]|[3-9][0-9])|[3-6][0-9][0-9]|7(?:[01][0-9]|20))[0-9]{12}$/,
  amex: /^3[47][0-9]{13}$/,
  discover: /^65[4-9][0-9]{13}|64[4-9][0-9]{13}|6011[0-9]{12}|(622(?:12[6-9]|1[3-9][0-9]|[2-8][0-9][0-9]|9[01][0-9]|92[0-5])[0-9]{10})$/,
  diners_club: /^3(?:0[0-5]|[68][0-9])[0-9]{11}$/,
  jcb: /^(?:2131|1800|35[0-9]{3})[0-9]{11}$/
};

```

Em seguida, podemos criar uma função que testa o valor inserido em relação a todos os padrões RegEx para determinar a validade do cartão:


```js

function checkSupported(value) {
  // remove all non digit characters
  var value = value.replace(/\D/g, '');
  var accepted = false;
  
  // loop through the keys (visa, mastercard, amex, etc.)
  Object.keys(acceptedCreditCards).forEach(function(key) {
    var regex = acceptedCreditCards[key];
    if (regex.test(value)) {
      accepted = true;
    }
  });
  
  return accepted;
}
```

[Demo](https://codepen.io/kelvinzhang/pen/NBmPjX?editors=1010)

**Juntar as peças**

Por fim, podemos combinar o algoritmo Luhn com nosso verificador de cartões de crédito compatível para concluir nossa fórmula mágica de validação.

```js

function validateCard(value) {
  // remove all non digit characters
  var value = value.replace(/\D/g, '');
  var sum = 0;
  var shouldDouble = false;
  // loop through values starting at the rightmost side
  for (var i = value.length - 1; i >= 0; i--) {
    var digit = parseInt(value.charAt(i));

    if (shouldDouble) {
      if ((digit *= 2) > 9) digit -= 9;
    }

    sum += digit;
    shouldDouble = !shouldDouble;
  }
  
  var valid = (sum % 10) == 0;
  var accepted = false;
  
  // loop through the keys (visa, mastercard, amex, etc.)
  Object.keys(acceptedCreditCards).forEach(function(key) {
    var regex = acceptedCreditCards[key];
    if (regex.test(value)) {
      accepted = true;
    }
  });
  
  return valid && accepted;
}
```

[Demo](https://codepen.io/kelvinzhang/pen/LBoEWK?editors=1010)

---

## Validando o CVV

**Por quê?**

- Pelas mesmas razões exatas da validação de números de cartão de crédito: para reduzir o número de solicitações inválidas feitas ao servidor.

O valor de verificação do cartão (CVV) é um conjunto de números de 3 a 4 dígitos na parte de trás do seu cartão e é usado por razões de segurança. A maioria dos CVVs possui três dígitos, com exceção do Maestro, [que pode nem exigir um CVV](http://www.maestrocard.com/gateway/where/where_faqs.html), e da American Express, que possui um CVV de 4 dígitos. Como não apoiamos o Maestro, a American Express é a única exceção que teremos que fazer.

Um CVV não tem nada parecido com um algoritmo de Luhn para verificar sua validade, então tudo o que precisamos fazer é verificar seu comprimento:


```js

function validateCVV(creditCard, cvv) {
  // remove all non digit characters
  var creditCard = creditCard.replace(/\D/g, '');
  var cvv = cvv.replace(/\D/g, '');
  // american express and cvv is 4 digits
  if ((acceptedCreditCards.amex).test(creditCard)) {
    if((/^\d{4}$/).test(cvv))
      return true;
  } else if ((/^\d{3}$/).test(cvv)) { // other card & cvv is 3 digits
    return true;
  }
  return false;
}

```

Vamos também definir um comprimento máximo para ele:

```js
$('#cvv').attr('maxlength', 4);
```

Podemos então integrar isso à validação do cartão de crédito.

[Demo](https://codepen.io/kelvinzhang/pen/zLQMmP?editors=1010)

**Alternando o botão Enviar**

Quando o cartão de crédito ou o CVV é inválido, devemos desativar o botão Enviar, pois não queremos que dados inválidos do formulário sejam enviados ao servidor. Isso é tão fácil quanto mudar o ```#status``` elemento para um ```submit``` botão e alternar o ```disabled``` suporte.

[Demo](https://codepen.io/kelvinzhang/pen/bjPOXW?editors=1010)

--- 

## Formatação Cartões

Por quê?

- O usuário pode ver rapidamente se perdeu ou adicionou um caractere extra
- É mais fácil para o usuário voltar e alterar um dígito no caso de erros de digitação

Há também algumas metas de UX que queremos alcançar ao adicionar a formatação automática:

1. Não queremos proibir o usuário de digitar espaços ao inserir o número do cartão
2. O usuário deve poder inserir e remover dígitos antes e depois de um espaço formatado
3. A posição do cursor deve ser mantida ao inserir e remover dígitos
4. Quando a formatação é alterada (por exemplo, American Express → Visa), os dígitos devem ser reformatados para corresponder ao novo layout

Com esses objetivos em mente, seguem algumas abordagens para formatar cartões:

**Bibliotecas de máscaras de entrada**

Vantagens:

- muitas bibliotecas para escolher
- fácil de implementar
- grande variedade de máscaras pré-fabricadas

Desvantagens:

- alguns são volumosos e lentos para carregar
- muitos têm bugs difíceis de corrigir sem modificar a fonte
- tudo lhe dá menos controle sobre o que está acontecendo

Aqui estão algumas das bibliotecas de mascaramento de entrada que eu testei:

Plain Javascript: https://github.com/RobinHerbots/Inputmask (180KB)
React: https://github.com/estelle/input-masking (5KB)
Angular, Ember, Vue: https://github.com/text-mask/text-mask (4KB)

Independentemente da biblioteca usada, a lógica por trás de cada implementação deve ser semelhante:

```js

$("#cc").on("input propertychange paste", function() {
  var value = $("#cc").val().replace(/\D/g, '');
  var mask;
  if ((/^3[47]\d{0,13}$/).test(value)) { // American Express
    // set mask to 4-6-5
  } else if ((/^3(?:0[0-5]|[68]\d)\d{0,11}$/).test(value)) { // Diner's Club
    // set mask to 4-6-4
  } else if ((/^\d{0,16}$/).test(value)) { // Other Credit Cards
    // set mask to 4-4-4-4
  }
  
  // apply your input mask to #cc
});

```


[Aqui está uma implementação](https://codepen.io/kelvinzhang/pen/XBQOxK?editors=1010) do Inputmask de RobinHerbots, que acredito ser a melhor biblioteca da lista acima. Embora tenha um tamanho significativamente maior e venha com uma variedade de recursos desnecessários, permite a entrada de espaços pelo usuário, inserção / remoção de dígitos após espaços e re-formatação de cartões.

No entanto, a posição do cursor não é mantida se o cartão for formatado novamente. Se você começar digitando um número da American Express (ex. 3782 822463 10005) e excluir os 3 no início, o cartão será re-formatado corretamente, mas o cursor pulará para o final.

Embora esse não seja um problema tão grande, eu não estava feliz com isso. Parecia que qualquer biblioteca que eu usasse perderia pelo menos um dos quatro objetivos. No final, fiquei cansado e decidi implementar minha própria máscara de entrada.

**Máscara de entrada personalizada**

Eu queria que minha máscara de entrada personalizada atingisse todos os quatro objetivos, além de manter alguns recursos de qualidade de vida das bibliotecas de máscara de entrada, como limitar o comprimento. Em sua essência, uma máscara de entrada atualiza o valor de entrada atual com o valor formatado corretamente.

Para fazer isso, criei uma função que recebe um número de cartão e gera o número formatado corretamente. Nesta função, também limito o comprimento da entrada, dependendo do tipo de cartão:

```js

function formatCardNumber(value) {
  // remove all non digit characters
  var value = value.replace(/\D/g, '');
  var formattedValue;
  var maxLength;
  // american express, 15 digits
  if ((/^3[47]\d{0,13}$/).test(value)) {
    formattedValue = value.replace(/(\d{4})/, '$1 ').replace(/(\d{4}) (\d{6})/, '$1 $2 ');
    maxLength = 17;
  } else if((/^3(?:0[0-5]|[68]\d)\d{0,11}$/).test(value)) { // diner's club, 14 digits
    formattedValue = value.replace(/(\d{4})/, '$1 ').replace(/(\d{4}) (\d{6})/, '$1 $2 ');
    maxLength = 16;
  } else if ((/^\d{0,16}$/).test(value)) { // regular cc number, 16 digits
    formattedValue = value.replace(/(\d{4})/, '$1 ').replace(/(\d{4}) (\d{4})/, '$1 $2 ').replace(/(\d{4}) (\d{4}) (\d{4})/, '$1 $2 $3 ');
    maxLength = 19;
  }
  
  $('#cc').attr('maxlength', maxLength);
  return formattedValue;
}

```

A funcionalidade principal é alcançada por uma cadeia de ```.replace``` métodos. Isso permite que o cartão seja formatado conforme está sendo digitado. Como tal, também não estamos fazendo uso do ```acceptedCreditCards``` objeto que definimos anteriormente. O RegEx é modificado para corresponder aos intervalos IIN de cada emissor. Por exemplo, podemos alterar a máscara para 4–6–5 assim que 34 ou 37 forem inseridos (American Express). Além disso, para os cartões que apoiamos, apenas American Express (15 dígitos) e Diner's Club (14 dígitos) requerem formatação especial.

Podemos então atualizar nossa entrada para refletir o valor formatado:

[Demo](https://codepen.io/kelvinzhang/pen/ZjdVQy?editors=1010)

Para 25 linhas de código, isso não é tão ruim. Permite a entrada de espaços pelo usuário e reformata os números de cartão de crédito. No entanto, excluir qualquer dígito ou inserir um dígito antes que um espaço mova o cursor para o final. Você também não pode excluir espaços.

Todos esses erros acontecem porque a atualização do valor de uma entrada move o cursor para o final. Podemos consertar isso armazenando a posição do cursor e atualizando-a. Existem também dois blocos aqui que ajustam a posição do cursor para permitir a remoção de espaços e a inserção de dígitos antes de um espaço.


```js
$('#cc').on('input', function() {
  var node = $('#cc')[0]; // vanilla javascript element
  var cursor = node.selectionStart; // store cursor position
  var lastValue = $('#cc').val(); // get value before formatting
  
  var formattedValue = formatCardNumber(lastValue);
  $('#cc').val(formattedValue); // set value to formatted
  
  // keep the cursor at the end on addition of spaces
  if(cursor === lastValue.length) {
    cursor = formattedValue.length;
    // decrement cursor when backspacing
// i.e. "4444 |" => backspace => "4444|"
    if($('#cc').attr('data-lastvalue') && $('#cc').attr('data-lastvalue').charAt(cursor - 1) == " ") {
      cursor--;
    }
  }

  if (lastValue !== formattedValue) {
    // increment cursor when inserting character before a space
// i.e. "1234| 6" => "5" typed => "1234 5|6"
    if(lastValue.charAt(cursor) == " " && formattedValue.charAt(cursor - 1) == " ") {
      cursor++;
    }
  }
  
  // set cursor position
  node.selectionStart = cursor;
  node.selectionEnd = cursor;
  // store last value
  $('#cc').attr('data-lastvalue', formattedValue);
});

```

[Demo](https://codepen.io/kelvinzhang/pen/jpoRMm?editors=1010)

Perfeito! Agora, os usuários podem digitar espaços à medida que digitam o número do cartão, inserir / remover dígitos antes e depois de um espaço formatado, manter a posição do cursor quando um dígito é inserido ou removido e, quando a formatação é alterada, formata novamente o cartão enquanto preservando a posição do cursor.


## Wrapping It Up

Agora que concluímos a validação e a formatação dos cartões de crédito, vamos combiná-los no formato final de cartão de crédito.

[Resultado final](https://codepen.io/kelvinzhang/pen/GBawbV?editors=1010)

---

[Artigo Original](https://medium.com/hootsuite-engineering/a-comprehensive-guide-to-validating-and-formatting-credit-cards-b9fa63ec7863)
[Kelvin Zhang](https://medium.com/@polunom)


