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

Nesse caso, a curva de aprendizado é a sobrecarga possível e não há problemas / limitações reais inerentes à idéia real por trás dela (exceto que vincula um ViewModel a uma única exibição, da mesma forma que o MVP). Vá MVVM!

### CLEAN: Arquitetura Limpa

Na verdade, esse é o item mais estranho da lista, pois na verdade é uma arquitetura. Nomeadamente “[Camada de apresentação de domínio de dados](https://martinfowler.com/bliki/PresentationDomainDataLayering.html)” (ou [Arquitetura hexagonal](http://java-design-patterns.com/patterns/hexagonal/) ). Assim, você pode ter uma "arquitetura limpa" enquanto segue o MVVM na camada de apresentação, por exemplo.

Os pontos principais da arquitetura CLEAN são:

- Separação estrita de "recuperação de dados", "lógica de negócios" real + gerenciamento do estado do aplicativo e "estado de exibição"
- Todas as implementações específicas usadas (por exemplo, carregamento de imagens, acesso ao banco de dados) estão ocultas em interfaces que não vazam detalhes da implementação: isolamento de dependências

O suposto benefício é que você pode conectar qualquer módulo a qualquer momento e substituí-lo por outro. Além disso, os módulos de dados / domínio podem teoricamente ser compartilhados entre diferentes versões do mesmo aplicativo (pense em telefone vs TV).
Além disso, ter objetos específicos da camada significa que o mapeamento entre eles pode ser testado.

A desvantagem é:


- Se você não precisar compartilhar módulos com vários projetos, forçar a separação é uma sobrecarga: pois você precisa de objetos específicos de camada e mapeamento entre
- Mencionei o mapeamento entre objetos definidos em 3 camadas diferentes? Isso é muito código clichê.
- A navegação deve ser uma responsabilidade da camada de domínio, mas é um problema comum que as pessoas abusem das Atividades e tornem o estado da navegação implicitamente parte da pilha de tarefas. Se quiséssemos ter controle completo sobre o estado do nosso aplicativo, teríamos apenas 1 Atividade que exibe o estado atual. Isso geralmente é ignorado, deixando a implementação "limpa" impura.
- Ocultar certas coisas sob interfaces pode ser difícil, muitas vezes as pessoas ainda vazam detalhes ou sua abstração não lida adequadamente com o funcionamento de sua biblioteca de opções (por exemplo, SQLite vs Realm - instância global singleton versus instâncias contadas ref-local).

Pessoalmente, aconselho manter as respostas da API e os objetos do banco de dados separados. Esse é um mapeamento que normalmente vale a pena introduzir: a resposta do servidor não deve definir acidentalmente quais dados estamos tentando armazenar e em qual formato.

A ideia é boa, mas às vezes [você simplesmente não vai precisar](https://martinfowler.com/bliki/Yagni.html) .

Mas também esteja ciente de que às vezes você faz.

### REDUX: bem, apenas Redux, embora deva ser chamado de ActionCreator-Action-Dispatcher-Middleware-Reducer-Store-Middleware-View

O Redux é uma das mais recentes “arquiteturas” que vieram à luz, uma visão do [padrão Flux](https://github.com/facebook/flux/) original que possuía uma Loja por Visualização (“componente”).

Fluxo , em poucas palavras:

- Actions: o objeto que encapsula uma ação, basicamente a Visualização emitindo um evento em vez de chamar um método em um apresentador / modelo de exibição
- Dispatcher: uma fila de eventos (onde as ações são colocadas), é semelhante ao contrato que permitiu à View chamar métodos no apresentador / viewmodel
- Store: armazena o estado e emite eventos de alteração (basicamente o viewmodel) e também se inscreve para ações no expedidor
- View: observa as alterações de estado emitidas pela loja


Portanto, o Flux era basicamente o MVVM com emissão de eventos da View para o ViewModel (agora Store) via Dispatcher (uma fila de eventos).

- - - - -

**O Redux** "aprimora" o design original, criando um único armazenamento global único que armazena o estado de todas as visualizações existentes no aplicativo e o estado do aplicativo, incluindo o estado de navegação e tudo o mais, dados carregados no momento, independentemente de os dados serem carregados. sendo carregado no momento ou se você deve mostrar um indicador de carregamento em algum segmento do aplicativo. Tudo em um grande objeto.

No Redux, esse estado é modificado por Reducers que modifica os bits e partes do estado global do aplicativo - mas não existe: um novo objeto é criado com as alterações aplicadas. Geralmente, tem a assinatura ```(State, Action) -> State``` e pode ser modelado com o ```scan()``` operator.

Os supostos benefícios são os seguintes:

- o Estado é imutável e cada alteração feita nele cria um novo Estado; portanto, se mantivermos um histórico de Ações e Estados, teremos um instantâneo de tudo no aplicativo - e se algo der errado, podemos “ver o que está errado "(time-travel debugging)
- cada ação emitida pela Visualização é adiada para permitir enfileirá-las: o processamento de cada ação é forçado a ser uma execução serial (um requisito necessário para sempre ter o estado mais recente no redutor e sempre fornecer o estado mais recente para os assinantes do store)
- ele tenta imitar certos aspectos de programação funcional e outras linguagens como [Elm](https://guide.elm-lang.org/architecture/), então provavelmente é ótimo

Considerando a maioria das amostras disponíveis envolvendo Redux não são mais complexos do que uma aplicação Todo que não tem ligações de rede, há a persistência do estado, e operações de outra forma não assíncronas em geral, pode ser tentador para começar a usá-lo - especialmente se você já viu  [time-travel debugging (de Todo apps) em live action.](https://www.youtube.com/watch?v=xsSnOQynTHs)

Mas há muitas desvantagens, especialmente se você tentar usar o Redux no contexto do Android:

- Implementações comuns do Redux agrupar o estado do aplicativo e os dados carregados no momento, **impossibilitando salvar o estado do aplicativo no Bundle ```onSaveInstanceState()``` , o que pode resultar em erros enigmáticos**.
- Carregar dados de fontes de dados locais ou remotas é difícil, porque deve ser implementado como um Middleware (pois é uma operação assíncrona de "efeito colateral") para garantir que a ordem de execução da ação esteja correta ~ e a explicação dos middlewares é que “Você consegue curry a função para que você possa, por exemplo, adicionar um registrador que imprima texto”.
- Qualquer forma de ação assíncrona requer a introdução de elementos mágicos como ```redux-thunk```, o que introduz uma curva de aprendizado adicional.
- A execução de operações pontuais (como "mostrar um brinde") é difícil, porque você só observa o "estado atual", o que significa que uma ação deve de alguma forma emitir um estado para "START_SHOWING_TOAST" e "STOP_SHOWING_TOAST" para que o efeito seja semelhante a chamando ```view.showToast()``` ou ```showToastEvent.call()```.
- A única loja contém todo o estado do aplicativo; portanto, o estado resultante pode ser facilmente uma grande árvore com muitos dados, onde devemos garantir que cada visualização tenha seu próprio ID exclusivo para que não substituam acidentalmente os estados uns dos outros. Cada visualização deve saber como acessar o subestado pretendido apenas para eles.
- Também devemos garantir que cada elemento no Estado seja imutável, incluindo listas / coleções (ajuda do Kotlin).
- Criar uma nova cópia imutável do estado só é útil se você realmente reter os valores anteriores como "história"; caso contrário, a mutação no local + a notificação dos observadores é um mecanismo muito mais simples (e menos dispendioso).


Então Redux desvantagens no Android em suma:

- todas as ações são serializadas e inevitavelmente atrasadas, aguardando o middleware executar operações assíncronas - criando um UX lento
- apesar de tentar facilitar a gestão do estado, apenas torna a gestão do estado mais difícil
- torna as operações assíncronas e as operações pontuais simples muito mais difíceis
- se isso ainda não estiver evidente, CURVA SUPER ALTA DE APRENDIZAGEM, se você quiser tornar QUALQUER COISA mais complexa do que um simples aplicativo Todo
- agrupar dados e estado transitório em um único "objeto imutável" torna a persistência adequada do estado Android muito difícil ou impossível


No geral, o que o Redux tenta fazer é abstrair as chamadas de método da View para o Presenter / ViewModel, criando um objeto que é passado para uma fila (como o Flux) - substitua as chamadas de método pela emissão de eventos.

Em seguida, mescle todos os apresentadores para armazenar seu estado em um único local e crie cópias do estado sempre que for alterado.
O suposto benefício, é claro, seria a facilidade de teste do redutor. Mas você geralmente exige alguma forma de estrutura para obter um "loop de eventos imutáveis" confiável para o seu estado.

Se você me perguntar, há tanto "para desenhar o resto da porra da coruja", que eu argumentaria que o Redux não está pronto para produção , e é preciso muito esforço para entrar em uma forma que possa modelar adequadamente os requisitos do mundo real.



### MVI: intenção de exibição do modelo

O MVI é praticamente a mesma coisa que o Flux (várias lojas, o view emite ações), com alguns aspectos do Redux (cópias de estado imutáveis ​​e redutores de estado), implementados no RxJava.
Os pontos principais:

- Intentions: o mesmo que Actions in Flux - emissão de eventos da View. O "despachante" é o Observável que resulta da mesclagem das ações em um único fluxo.
- Model: o estado da visualização que é imutável e copiado cada vez que é alterado
- Reducers: igual ao Redux - avalia o novo valor do estado atual com base na chamada atual do método

Desvantagem:

- Cada chamada de método é substituída por uma classe de dados selada e fluxos de eventos modelados pelo Observables, para que cada ação seja implementada por meio de operadores RxJava. Isso pode resultar em alta curva de aprendizado e difícil de raciocinar.

Obviamente, também temos a desvantagem mencionada junto com o Redux:

- Implementações comuns agrupam dados e estados juntos, tornando a persistência do pacote difícil / impossível.

Se lermos a página sobre MVI, veremos o seguinte:



>DO ARTIGO “APLICATIVOS REATIVOS COM INTENÇÃO DE MODELO - PARTE1 - MODELO”:

>Contudo, Pessoalmente, acho que na maioria das vezes é melhor não salvar o estado, mas recarregar a tela inteira, como estamos fazendo no primeiro aplicativo.Pense em um aplicativo NewsReader exibindo uma lista de artigos de notícias. Quando nosso aplicativo é encerrado e salvamos o estado e 6 horas depois o usuário reabre nosso aplicativo e o estado é restaurado, nosso aplicativo pode exibir conteúdo desatualizado. Talvez não armazenar o modelo / estado e simplesmente recarregar os dados seja melhor nesse cenário.

O que é uma loucura, porque eu posso induzir a morte de qualquer aplicativo que eu abra apenas abrindo o Skype e / ou a Câmera, e tenho certeza que iniciar a câmera leva menos tempo que 6 horas - e eu tenho um Nexus 5X com 2,5 GB de RAM.

Ignorar o [contrato de atividade](https://plus.google.com/+DianneHackborn/posts/FXCCYxepsDU) é uma solução abaixo do ideal, especialmente se estamos tentando melhorar a capacidade de manutenção e a confiabilidade, em vez de apenas introduzir bugs e frustração do usuário.

Se você vir uma classe ViewState e ela não tiver @Parcelize anotações, provavelmente não é uma implementação pronta para produção.

Sempre [teste seu aplicativo contra a morte do processo para saber o que acontece em caso de baixa memória](https://stackoverflow.com/questions/49046773/singleton-object-becomes-null-after-app-is-resumed/49107399#49107399) .

Para mais informações sobre essa arquitetura, consulte [a cadeia de comentários abaixo](https://medium.com/@chessmani/you-really-dont-need-to-understand-that-much-and-there-really-no-need-for-all-those-functional-4c50f6c495ac).


### PRNSAASPFRUICC: Production-Ready Native Single-Atom-State Purely Functional Reactive Composable UI Components

Sinceramente, acabei de adicionar isso à lista para o valor de choque da abreviação.

Mas você pode conferir a [proposição original](https://gist.github.com/bkase/dbfc79353ed67a27a822) e a [biblioteca que o acompanha: cyklic](https://github.com/bkase/cyklic) (razoavelmente sem manutenção), também é outra visão sobre a emissão de eventos a partir da visualização, executando-os através de um redutor (desta vez chamado de "Driver") e possui um start/stopmétodo . No geral, é MVI-ish.

### Menção honrosa: RIBs (Router Interactor Builder)

Embora eu não tenha usado [RIBs](https://github.com/uber/RIBs) , o Uber supostamente resolveu o problema de construtor automático e quebra de [hierarquias profundas de escopo](https://eng.uber.com/deep-scope-hierarchies/) , além de fornecer eventos adequados (via RxJava) para informar quando isso acontece.

Isso é mencionado como um padrão de arquitetura da camada de apresentação, pois possibilita que a hierarquia do escopo contenha o estado, enquanto as visualizações são apenas uma exibição do estado atual.

Para que isso aconteça, eles usam uma arquitetura de atividade única, para que a árvore do escopo forneça as informações de navegação para "que exibição deve estar mostrando" também. Com isso, eles realmente resolvem o problema "a exibição atual determina o atual Presenter / ViewModel em vez do contrário".


### Menção honrosa: Reactive Workflows

Não havia um exemplo de código-fonte aberto de fluxos de trabalho reativos, mas foi com isso que a [Square trocou seus ViewPresenters originais do MVP do tipo Mortar](https://www.youtube.com/watch?v=mvBVkU2mCF4).

Desde então, fui informado de que alguém chamado Blake Oliveira tentou recriar uma parte dessa arquitetura [neste repositório](https://github.com/blakelee/ReactiveWorkflows).

A essência disso é que um "fluxo de trabalho" pode ser compartilhado em várias telas, e o "fluxo de trabalho" contém uma máquina de estados para descrever o estado atual (um pouco redutor neste aspecto).

Mais importante ainda, o fluxo de trabalho define um contrato para quais eventos ele pode emitir, e a visualização os assina.
E os fluxos de trabalho podem ser encadeados, mas não tenho certeza sobre essa parte :)

Para fazer com que os fluxos de trabalho gerenciem o estado do aplicativo independentemente da camada de apresentação, eles usam uma arquitetura de atividade única.


### A recomendação atual: Componentes da arquitetura Android do Google - LiveData (e ViewModel)

O Google lançou o [Architecture Components para Android](https://developer.android.com/topic/libraries/architecture/index.html) , certo? Eles têm [documentação sobre como usá-lo](https://developer.android.com/topic/libraries/architecture/guide.html) e até [exemplos que mostram como usá-lo na vida real e até escrevem testes para ele](https://github.com/googlesamples/android-architecture-components) .

![](https://miro.medium.com/max/960/1*-yY0l4XD3kLcZz0rO1sfRA.png)


>A arquitetura final fornecida pelo Architecture Components ( [daqui](https://developer.android.com/topic/libraries/architecture/guide.html) )

Ele lida com casos de borda melhor que o MVP, e exige menos mágica do que o MVI, e é definitivamente mais pronto para produção (e menos confuso!) Que o Redux.

E tudo isso torna mais fácil seguir o [guia oficial do Android sobre “salvar estado”](https://developer.android.com/topic/libraries/architecture/saving-states.html) , em vez de usar atalhos como implementadores de MVP / MVI / Redux - e encher nosso aplicativo de comportamento imprevisível e erros frustrantes para o usuário final.

Sempre teste contra a [morte do processo](https://stackoverflow.com/questions/49046773/singleton-object-becomes-null-after-app-is-resumed/49107399#49107399) . Esquecer a entrada do usuário é um bug. Afinal, a Atividade não é apenas uma visualização.

## Conclusão

Isso pode ter sido um artigo longo e muito demorado (também demorou muito para ser escrito!), Mas no geral, eu diria que, por enquanto, o AAC é o vencedor claro - que é uma variante do MVVM específica para Android .

Enquanto usamos ```LiveData``` para emitir dados e ```PublishSubject``` para eventos pontuais, as coisas devem funcionar como esperado (exceto em fragmentos: sempre remova os observadores ```onDestroyView()``` em Fragmentos).

O AAC resolve alguns problemas comuns que podem surgir ao escrever um aplicativo Android. No entanto, ao fazê-lo, ele visa reduzir a complexidade da solução, em vez de adicionar camadas adicionais de complexidade (como Redux e “currying com middlewares” apenas para chamar uma declaração de log, etc.).


Portanto, até que os coordenadores de fluxo ou os fluxos de trabalho reativos apareçam no uso diário, eu diria que, por enquanto, o MVVM é o vencedor, e o AAC ajuda com isso de maneira bastante elegante. A biblioteca de paginação será incrível.


---

Autor: [Gabor Varadi](https://proandroiddev.com/@Zhuinden?source=follow_footer--------------------------follow_footer-)


[Artigo Original](https://proandroiddev.com/mvc-mvp-mvvm-clean-viper-redux-mvi-prnsaaspfruicc-building-abstractions-for-the-sake-of-building-18459ab89386)

