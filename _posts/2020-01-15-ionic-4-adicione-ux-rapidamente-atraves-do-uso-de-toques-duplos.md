---
layout: post
title:  "Ionic 4: adicione UX rapidamente através do uso de toques duplos!"
date:   2020-01-15 17:59:38 -0200
categories: jekyll update
---

A maioria dos usuários é treinada para fazer as coisas por instinto ao interagir com aplicativos. O Ionic, apesar de ser uma ótima estrutura, nem sempre possui todas as interações incorporadas por padrão. Para todas as sutilezas do Ionic, ainda falta muito ao Framework. Você provavelmente conhece a diretiva ```tap``` do Ionic e provavelmente a usou em toda a sua aplicação da seguinte maneira:

```html
<ion-item tappable (tap)="someFunction">... </ion-item>
```

Bem, e se você quiser fazer algo quando o usuário tocar duas vezes em vez de um toque, por exemplo: Gostar de uma foto no Instagram? Infelizmente, você encontrará problemas no Github que solicitam esse recurso, mas a maioria, se não todos, geralmente é fechada sem muita ajuda.

Não tenha medo, é sobre isso que trata o tópico de hoje! Vamos começar.


Primeiro, você precisará instalar ```hammerjs``` como uma dependência do projeto. Ele vem com o Ionic Framework, mas não está disponível para nós nativamente.

Podemos resolver isso rapidamente, executando ```npm install hammerjs```.

Em seguida, precisamos importar ```hammerjs``` para o nosso arquivo ```main.ts``` se ainda não estiver pronto:


### main.ts

```ts
import 'hammerjs';
```

Isso é literalmente tudo o que precisamos fazer para esse arquivo.


### app.module.ts

No seu arquivo ```app.module.ts```, precisamos adicionar a seguinte classe ```CustomHammerConfig```.

```ts
export class CustomHammerConfig extends HammerGestureConfig {
  overrides = {
    'press': {time: 500},  // default: 251 ms
    'pinch': {enable: false},
    'rotate': {enable: false},
  };
}
```

Os detalhes não são realmente importantes, mas precisamos informar ao Ionic/Angular que aproveitaremos os eventos do hammerjs. Na configuração acima, substitui o tempo limite da diretiva de timeout em 1/2um segundo, em vez do padrão de 251ms, apenas para nos dar espaço de manobra. Vou explicar o porquê, mais tarde.

Em seguida, no seu providers' array, adicione o ```CustomHammerConfig```

```
providers: [
  ...
  {provide: HAMMER_GESTURE_CONFIG, useClass: CustomHammerConfig},
],
```


### Create the double tap directive

Execute o comando ```ionic g directive directives/double-tap``` que criará o arquivo ```double-tap.directive.ts```  que usaremos para criar a funcionalidade de toque duplo em nosso aplicativo. Substitua o conteúdo desse arquivo por:

```ts
import { Directive, EventEmitter, HostListener, Output } from '@angular/core';

@Directive({
  selector: '[doubleTapable]'
})
export class DoubleTapDirective {

  @Output() doubleTap = new EventEmitter();
  @Output() tripleTap = new EventEmitter();

  constructor() {}

  @HostListener('tap',  ['$event'])
  onTap(e) {
    if (e.tapCount === 2) this.doubleTap.emit(e);
    if (e.tapCount === 3) this.tripleTap.emit(e);
  }
}
```

### Teste!

Agora você está pronto para experimentar sua nova diretiva doubleTap. Não foi tão difícil de montar, agora?


```html
<img tappable doubleTapable (doubleTap)="doSomething()" (tripleTap)="doAnotherThing()" src="https://source.unsplash.com/random" alt=""/>

```

Se você substituir ```doSomething()``` por alguma função e ```doAnotherThing()``` por outra, poderá ver facilmente que a diretiva está funcionando agora!

A parte importante a lembrar é que você declarar a directiva sobre o componente que você quiser usá-lo, o que é por isso que nós escrevemos ```doubleTappable``` e os eventos estão rodeados pelos parênteses ```(doubleTap)```, ```tripleTap```.


### O que está acontecendo por trás?

O HammerJS é uma ferramenta maravilhosa dentro da estrutura Ionic, e encorajo todos a dar uma olhada, se você tiver tempo. É realmente personalizável e facilitará sua vida no futuro, se você entender suas capacidades.

Por padrão, o **HammerJS** reconhece uma sequência de toques que ocorrem entre 300ms. É por isso que substituímos a ```press``` configuração 500ms, porque o padrão é 251ms. Existem algumas outras regras para a detecção de uma tap, como você pode ter apenas um dedo na tela de cada vez ```Required pointers```, e você só pode ter mover entre os taps dentro de um certo limte(threshold): 10. O limite é de 10% da distância da tela, a partir da tap de origem. Portanto, se você mover mais de 10% da tap original, o evento não será acionado.



---

Autor: [Jordan Benge](https://medium.com/@JordanBenge?source=follow_footer--------------------------follow_footer-)

[Artigo Original](https://medium.com/@JordanBenge/ionic-4-quickly-add-ux-through-the-use-of-double-taps-5f6e3216a289)

