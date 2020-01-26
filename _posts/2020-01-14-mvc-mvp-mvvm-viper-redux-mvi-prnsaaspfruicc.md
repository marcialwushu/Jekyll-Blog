---
layout: post
title:  "MVC / MVP / MVVM / CLEAN / VIPER / REDUX / MVI / PRNSAASPFRUICC - construindo abstrações para criar abstrações (e porque são bonitas e populares)"
date:   2020-01-14 17:59:38 -0200
categories: jekyll update
---


![](https://miro.medium.com/max/1760/1*WyNyQHxQZyB9V5azQDCiNQ.png)

**EDIT no futuro: MVP / MVVM provavelmente não está correto aqui. De fato, também não está correto em nenhum outro lugar (e é por isso que está errado aqui). Confira, por exemplo, a [arquitetura de componentes NetFlix](https://www.youtube.com/watch?v=dS9gho9Rxn4) . A maioria desses padrões apenas introduz um acoplamento rígido nas costuras erradas.**

**Esteja ciente do seguinte: pessoalmente, não estou aplicando nenhum desses padrões da forma que eles estão dispostos aqui.**


Este pode ser o post mais controverso que eu já escrevi até agora.

>TL; DR e take-away: se você suportar armazenamento de dados offline, então:

>- observe sua camada de dados através do suporte LiveData / SQLDelight / etc da sala - o que importa é que ele pode ser observado para alterações

>- se você armazenar em cache os dados nas alterações de configuração (ViewModel), armazene os dados em algo que possa ser observado nas alterações (BehaviorSubject ou LiveData). Consulte o "Guia de arquitetura de aplicativos" do Google , as idéias são úteis.
Sempre certifique-se de persistir o estado do apresentador via onSaveInstanceState () . Atividade é um ponto de entrada do processo, não apenas "uma visualização".

>Além disso, eu não gosto do Redux, e de nenhuma das suas variantes. Realmente. Há uma seção muito longa dedicada ao motivo de eu não gostar do Redux.

>No geral, acho que se você quiser usar algum padrão de camada de apresentação, use o MVVM por enquanto ou crie algo melhor (que não vincule uma tela à sua abstração). Até lá, siga o guia Architecture Components . Confira os codelabs .

>Comparado ao Redux, o AAC MVVM é muito mais limpo, mais enxuto, mais fácil de entender e possui muito menos custos ocultos envolvidos, além de dificultar tarefas cotidianas triviais. Mas você ainda precisa estar ciente do onSaveInstanceState.


As pessoas adoram padrões de arquitetura de aplicativos.

É verdade! Caso contrário, não teríamos tantos deles.

Embora mesmo o termo ```application architecture pattern``` nesse caso seja um pouco impróprio, considerando que a maioria desses padrões no título se aplica apenas à camada de apresentação, e essa é apenas uma camada do aplicativo.

Às vezes (e sinceramente, inclusive eu), construímos amostras que seguem um desses padrões para segui-lo, olhamos para ele e dizemos: "Nossa, isso é bonito!"

Pontos negativos extras se a amostra não tiver testes de unidade - [também algo que eu próprio sou um ofensor](https://github.com/Zhuinden/xkcd-example/blob/b1f20ed680ce5c1c36b17a3f9aae0594530d997d/app/src/test/java/com/zhuinden/xkcdexample/ExampleUnitTest.java#L16) .

Talvez essa seja minha suposição pessoal, mas muitos de nós somos influenciados pela descrição de [uma arquitetura limpa com camadas separadas estritamente aplicadas, conforme lemos o artigo de Fernando Cejas sobre como construir um aplicativo em camadas e quais regras ele deve obedecer](https://fernandocejas.com/2014/09/03/architecting-android-the-clean-way/).

De fato, até lemos o próximo artigo que diz que devemos [implementar cada caso de uso como um transformador observável RxJava](https://fernandocejas.com/2015/07/18/architecting-android-the-evolution/) . Claro, por que não? Faz sentido.

E assim que tivermos o ```abstract class UseCase``` local, podemos [até enviar argumentos para eles com um ```Params``` objeto que é basicamente um Bundle](https://fernandocejas.com/2016/12/24/clean-architecture-dynamic-parameters-in-use-cases/)!

Ok, as pessoas na verdade geralmente não levaram isso a sério .


## Prefácio suficiente, qual é o objetivo aqui?

Há uma coisa muito importante a ter em mente em relação a essas "arquiteturas" da camada de apresentação.

Eles foram criados para impor a separação, a fim de introduzir a indireção (criar uma nova “costura”), para que o comportamento da interface do usuário possa se tornar testável por unidade .

Se jogarmos que ao redor, nós não realmente precisa que indireto , se nós não teste de unidade lógica UI .

- - - - - - - - - -

Eu posso ouvir os alarmes sair já, então eu vou tomar nota de que fazer o seu melhor para aderir a princípios sólidos - especialmente o Dependency Inversion Principle - normalmente é uma boa idéia.

Padrões naturalmente emergentes, como o fornecimento de dependências para construtores, a introdução de ID se o gráfico de objetos for suficientemente complexo - tudo isso é útil.

- - - - - - - - - -


No entanto, a introdução de padrões emergentes “artificialmente” pode nos levar à abstração errada. Cada arquitetura tem um preço e um custo ainda maior se a arquitetura for feita de maneira errada. E não vamos esquecer os possíveis custos ocultos resultantes da complexidade oculta e das curvas de aprendizado.

>Por natureza, o "ganho" padrão desses padrões seria a testabilidade unitária por níveis de indireção. Se não fizermos o teste de unidade, estamos construindo para tornar as coisas "bonitas". Mas qual é o custo? Qual é o trade off? Qual é o problema que pretendemos resolver introduzindo a indireção? Qual é o indireto que introduzimos em primeiro lugar?

## Visão geral dos padrões populares mencionados acima

### MVC: Model View Controller

Os pontos principais do MVC são:

- As interações do usuário chamam métodos no Controller
- O controlador atualiza o modelo (onde o modelo é o que realmente armazena o estado)
- O Modelo expõe ouvintes de mudança para notificar os observadores de que ele mudou
- O View assina as alterações emitidas pelo modelo para atualizar-se

O que as pessoas costumam chamar de "MVC" ou "controlador de exibição massivo" não tem nada a ver com o MVC real. Não, o XML do layout não é uma "Visualização".

O Modelo deve ter a capacidade de emitir eventos de mudança, e a Visualização deve ser assinada.

Não vi muitos exemplos de MVC para Android, exceto nesta discussão. Portanto, não posso julgá-lo com precisão, pois realmente não o vi em ação! :)


### MVP: Model View Presenter

Os pontos principais do MVP são:

- As interações do usuário chamam métodos no Presenter
- O Presenter armazena estado, gerencia estado e chama métodos na exibição para notificá-lo para atualizar-se
- O modelo é apenas dados
- O View recebe chamadas de método do apresentador para serem notificadas sobre alterações para se atualizar


O suposto benefício do MVP é que existe um contrato bem definido entre o Presenter e o View, e pode-se verificar que "nas circunstâncias certas, o Presenter chama os métodos certos no View".

Alguns custos ocultos:

- o Presenter normalmente está vinculado a uma única Visão, portanto, a discussão entre os Apresentadores e as relações hierárquicas das próprias Exibições pode apresentar dificuldades: manter a existência e a comunicação entre apresentadores filhos e apresentadores irmãos (se existirem) é complicado. Isso pode ser evitado se o Apresentador for compartilhado entre Exibições do mesmo fluxo.

A desvantagem é que:

- o Presenter armazena o estado, portanto, devemos poder persistir / restaurar o estado do apresentador quando o processo é recriado (que geralmente é específico do Android - e algumas vezes ignorado!)
- o View é atualizado por meio de retornos de chamada, o que é mais trabalho manual do que ouvir alterações
- se o Presenter puder sobreviver às alterações de configuração, é possível que a Visualização seja desanexada quando o Presenter receber resultados assíncronos e há uma chance de que as chamadas de método para a Visualização possam ser descartadas ( ```if(view != null```) {alguém?)

Para eliminar a capacidade de descartar eventos, precisamos poder enfileirar esses eventos até que o View se inscreva novamente, adiando sua execução. Mas se estamos emitindo eventos e ouvindo-os, então não é mais um apresentador, é? :)

### VIPER: Exibir roteamento de entidade do apresentador do Interactor

Na verdade, isso é apenas uma reviravolta adicional no MVP, a saber, que eles têm uma ```Router``` interface definida para lidar com a navegação.

A variante do iOS também tinha um "Wireframe", mas isso é essencialmente injeção de dependência.

Quaisquer limitações existentes ```Presenter``` no MVP ainda se aplicam.

### MVVM: Model View ViewModel

Os pontos principais do MVVM são:

- As interações do usuário chamam métodos no ViewModel
- O ViewModel armazena estado, gerencia estado e expõe eventos de alteração quando o estado é alterado
- O Modelo são os dados mapeados nos campos observáveis ​​(ou qualquer outra forma de emissão de evento)
- O View assina eventos de mudança expostos pelo viewmodel para atualizar-se

O suposto benefício é que o View pode ser "burro", pois tudo o que faz é exibir o que está no ViewModel e, em seguida, o que está no ViewModel pode ser verificado como "os valores certos nas condições certas".

A desvantagem é:


- Todo o estado deve ser movido para o ViewModel (e ser um pouco "duplicado", motivo pelo qual o ViewModel e o View devem ser mantidos em sincronia - é com isso que as estruturas de ligação de dados ajudam)
- o ViewModel armazena o estado, portanto, devemos poder persistir / restaurar o estado do ViewModel quando o processo é recriado (que geralmente é específico do Android)
- As chamadas de método para o View são substituídas pela emissão de eventos; portanto, é necessário implementar alguma forma do padrão Observer - normalmente a combinação de PublishSubject / BehaviorSubject, mas as pessoas tentam fazer com que o LiveData funcione como um PublishSubject e isso não acontece.




---

[Artigo Original](https://proandroiddev.com/mvc-mvp-mvvm-clean-viper-redux-mvi-prnsaaspfruicc-building-abstractions-for-the-sake-of-building-18459ab89386)

