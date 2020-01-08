---
layout: post
title:  "Entrevista exclusiva da AMD - Discutindo a arquitetura da GCN, o desempenho da computação e o futuro, parte 1"
date:   2019-12-23 17:59:38 -0200
categories: jekyll update
---


![](https://trello-attachments.s3.amazonaws.com/5d7e8031eaec3e42c24aade0/5d7e81516a6cc012940f6135/191b895cfed6689ae7b116879c5ddb14/exclusive-amd-interview-gpu-compute-and-more.jpg)

A AMD é uma das maiores forças nos jogos da próxima geração no momento. A AMD está produzindo os chips para os consoles da próxima geração, o Playstation 4, o Wii U e o Xbox One. Além disso, a Radeon R9 290X é uma das melhores GPUs do mercado atualmente para desempenho. Durante sua recente conferência da CES, eles anunciaram que o desempenho de Mantle no Battlefield 4 é bastante impressionante 45% maior em muitas circunstâncias do que com a API tradicional.

A AMD tem uma visão clara dos jogos para PC e console, buscando unificar e facilitar o desenvolvimento de jogos e resolver alguns dos maiores desafios atualmente enfrentados por jogos e desenvolvedores. Eles certamente não estão sozinhos na competição, com seus rivais logo atrás, mas a AMD está em uma posição muito boa.

Recentemente, tive a chance de entrevistar Robert Hallock, Comunicações técnicas, Jogos de mesa e gráficos da AMD e ele teve a gentileza de se submeter a uma entrevista. Durante a primeira parte desta entrevista, lançaremos luz sobre a arquitetura GCN da AMD, a visão que a AMD tem para o futuro dos jogos para PC e muito mais. Espero que tenhamos a próxima parte da entrevista da AMD em breve e tenhamos mais informações sobre APUs, CPU e algumas perguntas de acompanhamento sobre a GPU.

Nos próximos dois dias, farei algumas explicações e análises técnicas sobre as perguntas feitas e respondidas por mim e pelo Sr. Hallock para ajudar aqueles que não têm muita certeza do significado de parte dessa entrevista. Mas para aqueles de vocês que estão ansiosos para mergulhar, então leia abaixo.

![](https://trello-attachments.s3.amazonaws.com/5d7e8031eaec3e42c24aade0/5d7e81516a6cc012940f6135/4ffc15745e140b6de6bbe9db2ffef259/amd-mantle-dice-battlefield-frostbite-3-engine-performance-1024x575.jpg)

**Pergunta: Nos últimos três anos, as CPUs aumentaram apenas marginalmente no desempenho, em comparação com grandes avanços na tecnologia GPU. A AMD aumentou drasticamente o potencial de computação dos seus núcleos de GPU mais recentes, por exemplo, o Havaí (R9 290X). Como o PS4 e o Xbox One provavelmente descarregam muito trabalho de computação para a GPU, como você acha que a computação afetará o futuro do desenvolvimento de jogos no PC e no console?**

Robert Hallock: Você está certo, o desempenho dos jogos para PC percorreu um longo caminho em pouco tempo. Por exemplo, a ATI Radeon ™ HD 5870 era um produto emblemática há apenas três anos, com o preço correspondente. Hoje, um desempenho aproximadamente equivalente pode ser encontrado a partir de US $ 139 no AMD Radeon ™ R9 260X. Eu discordo, mas eu realmente queria enfatizar o quão duro estamos trabalhando para oferecer um desempenho significativamente melhor a todos os jogadores, ano após ano.

Para o seu ponto, a computação é mais importante agora do que nunca. Considere os seguintes efeitos usados ​​pelos desenvolvedores de jogos: oclusão ambiental de alta definição (HDAO), iluminação global, FXAA, MLAA, TressFX Hair, profundidade de campo de difusão e sombras de endurecimento por contato. O que eles têm em comum? Todos são efeitos controlados por computação da GPU. Essa é apenas uma pequena seleção dos efeitos que você pode acelerar com os recursos de computação, em vez do pipeline gráfico tradicional. Sempre que possível, o uso do computador GPU é uma maneira bastante eficiente de renderizar!

A tendência positiva do uso da computação em jogos é refletida em nossas arquiteturas, onde as GPUs AMD Radeon ™ R9, R7 e HD 7000 Series apresentam recursos de computação completa que podem ser usados para jogos ou outras atividades (como mineração de criptomoedas).

![](https://trello-attachments.s3.amazonaws.com/5d7e8031eaec3e42c24aade0/5d7e81516a6cc012940f6135/03c7e5e75cf7b4ee1e6435b4418430ac/amd-radeon-r9-290x-image.jpg)

O atual carro-chefe da AMD, o Radeon R9 290X GPU /.

**Existem inúmeros benefícios de desempenho na tecnologia Mantle da AMD, por exemplo, aumento do número de Chamadas Draw, o Mantle também pode beneficiar o desempenho de computação de uma GPU?**

Robert Hallock: Mantle foi projetado para solucionar deficiências na atual safra de API de gráficos. É bastante específico para aplicativos tradicionais de renderização de jogos. Há uma necessidade menos pronunciada de revisão no domínio da computação, onde os idiomas de hoje (como DirectCompute ou OpenCL) são bastante robustos.

[![](https://i.ytimg.com/vi/NSGsIZwonok/hqdefault.jpg)](https://youtu.be/NSGsIZwonok)

**Mantendo  o assunto da computação por mais um momento, qual o impacto da execução dos comandos de computação na arquitetura GCN 1.1 no desempenho do processamento gráfico? Você costuma achar que um comando de computação deve 'esperar' para ser processado porque a GPU está ocupada processando a cena ou que o desempenho gráfico sofre? Ou as melhorias na computação da arquitetura no GCN 1.1 ajudaram a eliminar esses problemas?**

Robert Hallock: Depende inteiramente do efeito. Com relação aos jogos, os recursos de pipeline de computação e gráficos são interdependentes. Ser muito agressivo com qualquer categoria de renderização acabará comprometendo o desempenho geral, mas isso vale para qualquer GPU. Os desenvolvedores de jogos talentosos entenderão os fundamentos de uma GPU e projetarão um mecanismo que adota uma abordagem equilibrada, não apenas da perspectiva total de recursos, mas também quando usar computação versus pipeline.

Com relação a produtos como o AMD Radeon ™ R9 290 ou R9 290X, refinamos a arquitetura GCN básica de duas maneiras principais: acomodando taxas de pixels mais altas para conteúdo UHD, melhorias no buffer sem chip para aprimorar o desempenho do mosaico, armazenamento de dados mais robusto em os processadores de geometria para melhorar o desempenho do sombreador de geometria, um controlador de memória menor e mais eficiente, a adição de nossa  [tecnologia “XDMA”](http://community.amd.com/community/amd-blogs/amd-gaming/blog/2014/01/03/modernizing-multi-gpu-gaming-with-xdma) , suporte para até quatro primitivas por relógio e, claro, fomos capazes de escalar o Graphics Core Next para 2816 no total unidades shader. No geral, porém, esta é a arquitetura básica da GCN que conhecemos e amamos, mas com uma dose extra de amor para torná-la um mecanismo mais significativo e capaz para o trabalho de múltiplos propósitos. (observe, a computação GCN 1.1 é semelhante ao PS4. [Confira o artigo aqui](http://www.redgamingtech.com/playstation-4-gpu-next-gen-amd-radeon-volcanic-island-gpu-compute-similarities/) )

**A tecnologia de áudio nos PCs está bastante estagnada há vários anos e requer alta sobrecarga da CPU para processamento. O processador TrueAudio da AMD cuida de todo o trabalho de processamento com áudio ou ainda resta algum processamento para a CPU executar no áudio?**

Robert Hallock: O AMD TrueAudio descarrega totalmente a CPU se o desenvolvedor utilizar ao máximo seus recursos. É um canal de áudio programável, portanto, suportará apenas a carga necessária. Independentemente disso, o AMD TrueAudio envia a (s) voz (s) que está sendo processada e renderizada ao hardware de áudio existente do usuário como uma passagem para o dispositivo de terminal (por exemplo, fones de ouvido).

![](https://trello-attachments.s3.amazonaws.com/5d7e8031eaec3e42c24aade0/5d7e81516a6cc012940f6135/220336cd0560f707c18fd70f5c9bc3eb/amd-true-audio-cpu-processing-budget-ps4-and-pc-1024x576.jpg)

**Com os consoles da próxima geração com 8 núcleos de CPU AMD Jaguar, você acha que mais jogos no PC se beneficiarão de um número maior de núcleos de CPU à medida que os desenvolvedores de jogos mudam seus mecanismos para melhor usar ambientes com vários núcleos?**

Robert Hallock: Não posso falar pelo futuro dos negócios de console, mas posso falar sobre o que a AMD está fazendo. O Mantle é uma maneira poderosa de melhorar a robustez dos recursos de multi-threading de um jogo. Vários desenvolvedores de jogos, principalmente Johan Andersson, da DICE ( [em seu discurso](http://youtu.be/N_6CAneoW-0?t=17m5s)  na APU13), foram bastante elogiosos à nossa API e sua escalabilidade entre núcleos. Toda a conversa é muito esclarecedora sobre esse tópico, mas o coração do Mantle está em abordar aspectos da camada de software (como threading) que ficaram para trás das capacidades de nosso hardware.

**Atualmente, a maioria dos PCs usa RAM DDR3 para a RAM do sistema principal, com a GPU usando GDDR5, embora o DDR4 comece lentamente a se tornar a norma nos próximos anos. Em situações em que você tem uma placa discreta como a Radeon R9 290x cuidando do processamento gráfico, uma CPU usando RAM DDR3 em uma largura de banda do PC é limitada, ao processar mecanismos de jogos altamente complexos devido ao número de diferentes tarefas e dados acessados?**

DDR3 é mais que suficiente para o cenário gráfico atual. Linus na LinusTechTips fez [um  vídeo muito informativo](http://www.youtube.com/watch?v=dWgzA2C61z4)  sobre esse tópico, na verdade. O veredicto final: as capacidades são iguais, qualquer coisa entre DDR3-1333 e DDR3-2400 teve um impacto insignificante no desempenho da GPU.

De fato, o excelente desempenho nos jogos tem tudo a ver com manter os recursos locais na GPU e no buffer de quadros. A busca de texturas agrícolas (por exemplo) na RAM do sistema é uma penalidade de desempenho muito substancial. Mais importante para o desempenho geral da GPU é o potencial da CPU para alimentar a fera - o subsistema gráfico. À medida que as resoluções e as taxas de preenchimento aumentam, é necessária uma CPU cada vez mais poderosa para alimentar a GPU com capacidade. Se a CPU não estiver preparada para a tarefa, o desempenho diminui. A maioria dos usuários chama isso de desempenho "gargalo" ou "CPU limitado".

Continue para a PRÓXIMA PÁGINA

# Entrevista exclusiva da AMD - Discutindo a arquitetura da GCN, o desempenho e o futuro Parte 1 Página 2

**Vamos assumir que sou desenvolvedor de jogos e estou no meio da criação de um jogo para o PS4. Há relatos de que o Mantle é semelhante à API do Playstation 4. Como o PS4 usa a tecnologia GCN, é relativamente fácil para mim portar meu jogo para o PC no PS4 usando a tecnologia Mantle, principalmente se eu estiver usando um mecanismo como o Frostbite 3 ou digamos Unreal?**

Robert Hallock: Projetamos tornar o modelo de programação de Mantle semelhante ao que os desenvolvedores de jogos já estão criando para outras plataformas. É claro que “facilidade” é relativa à complexidade do aplicativo, mas tentamos torná-lo o mais fácil possível com ferramentas robustas de detecção de erros, documentação saudável e suporte robusto dos cérebros da AMD por trás do Mantle. Todos os desenvolvedores de jogos que atualmente trabalham com o Mantle ficaram novamente satisfeitos com nossos esforços nessa categoria.

**Eu, juntamente com muitos outros da indústria, consideramos que foi uma grande jogada da AMD permitir aos proprietários da Nvidia e da Intel a chance de usar o TressFX. Embora seja uma fera muito diferente, você poderia esclarecer como a Nvidia seria capaz de implementar o Mantle se eles quisessem apoiá-lo?**

Robert Hallock: Não seria prudente da minha parte comentar em nome de outras empresas.

 

**Quais foram os fatores que levaram a AMD a criar a API Mantle? Foi apenas um caso de ajudar os desenvolvedores a resolver os principais pontos fracos da arquitetura de jogos para PC (a sobrecarga) na preparação para a próxima geração de consoles e mecanismos de jogos?**

Robert Hallock: Os desenvolvedores de jogos fizeram as rondas na indústria, pedindo a todos os fornecedores de hardware que se interessam por gráficos uma solução para tornar os PCs mais parecidos com um console com relação à eficiência na utilização de hardware e à simplicidade da programação. Eles reconheceram que os jogos para PC poderiam aprender muito com seus irmãos na sala de estar. Somente a AMD levou esses pedidos do estágio de negociação para a fase de mão de obra e dinheiro, e Mantle nasceu! ( [MAIS informações podem ser encontradas aqui no Mantle](http://www.redgamingtech.com/introducing-amd-mantle-low-level-api-from-amd/) )

![](https://trello-attachments.s3.amazonaws.com/5d7e8031eaec3e42c24aade0/5d7e81516a6cc012940f6135/ddd148da9b52b52e3e4330a400e929f1/mantle-execution-model.jpg)

**O fornecimento da tecnologia principal nos consoles Playstation 4 da Sony e Xbox One da Microsoft influenciou o design do seu futuro hardware, tanto na GPU quanto nas APUs?**

Robert Hallock: Eu não trabalho na unidade de negócios semi-personalizados da AMD, então não pude comentar de maneira inteligente. (nota dos entrevistadores - em breve tenho uma entrevista com o departamento da APU!)

**Com o lançamento do Radeon R9 290X, a largura de banda foi aumentada mudando para um barramento de memória de 512 bits de 384 e também dobrando a contagem de ROP da GPU, em relação à taxa, que é maior que o aumento nos processadores de fluxo. Você acha que o gargalo das GPUs está se tornando mais no ROP e na largura de banda de memória local (na GPU discreta) ou está tudo bastante equilibrado? Além disso, qual é a proporção ideal de ROP, unidades de textura e largura de banda em comparação com 8 núcleos GCN (ou 512 processadores de fluxo)?**

Robert Hallock: O design da GPU é análogo à pergunta sobre o design do mecanismo de jogo que você colocou anteriormente. Tudo tem que ser equilibrado. Você pode lançar um punhado de back-end de renderização em uma GPU, mas se a largura de banda da memória for insuficiente, esse hardware será desperdiçado. E vice-versa, é claro.

Eu acho que pode ser melhor explicado trabalhando de trás para frente, perguntando-se: “Qual meta de desempenho e resolução eu quero atingir?” Então você constrói um núcleo no papel que, pelos seus modelos matemáticos, produziria desempenho aproximadamente equivalente ao seu objetivo . Então você constrói!

Para 512 UCs, eu diria: 32 unidades de textura, 16 ROPs e um barramento de 128 bits.

**Como você acha que o SteamOS da Valve se encaixa no grande esquema dos jogos para PC? A Valve disse que obteve melhor desempenho com seus jogos no SteamOS do que no Windows. A AMD suportará Linux Gaming e SteamOS com Mantle e outras tecnologias no futuro?**

Robert Hallock: A posição final do SteamOS no ecossistema de jogos para PC é incerto, mas estamos entusiasmados com as Steam Machines e sua abordagem de ecossistema aberto aos jogos. Com relação ao Mantle, estamos avaliando como ele pode ser implementado, juntamente com como e quando o Mantle para Steam OS deve ser incluído em nosso plano de desenvolvimento. Por enquanto, estamos focados no OpenGL como plataforma de entrega para Linux.

Você pode ver outras evidências de nossos esforços no Linux com nossas contribuições para os kernels 3.11 e 3.12, ou o recente anúncio da iBuyPower de máquinas a vapor baseadas em AMD.

![](https://trello-attachments.s3.amazonaws.com/5d7e8031eaec3e42c24aade0/5d7e81516a6cc012940f6135/86c918219a6a7491d3bbbe55e9ec1d07/amd-jaguar-cpu-frontend1-1024x555.png)

**A AMD parece estar em uma ótima posição no momento para unificar o desenvolvimento de jogos, com sua CPU, APU e GPU sendo usadas em PCs e consoles da próxima geração. Desenvolvedores que desfrutam de codificação de baixo nível com o Mantle e outras tecnologias como TrueAudio e TressFX. Você pode falar um pouco da sua visão do desenvolvimento de jogos, tanto no PC quanto nos consoles?**

Robert Hallock: Estamos tremendamente orgulhosos do continuum que construímos no ecossistema de jogos. Os desenvolvedores de jogos já começaram a aproveitar os pontos em comum, como a recente decisão da Crystal Dynamics de dar vida ao TressFX Hair para todas as plataformas com o Tomb Raider Definitive Edition. Esperamos que os dividendos continuem sendo pagos dessa maneira nos próximos anos para todas as plataformas abordadas.

**Com relação ao TressFX, você o atualizou recentemente para simular mais do que apenas cabelos, por exemplo, grama e pêlo (que é uma tecnologia impressionante, devo acrescentar) e reduziu a sobrecarga associada à execução. Você pode nos dizer se planeja usar uma versão do Hardware Physics para fumaça e detritos?**

Robert Hallock: Não posso especular sobre tecnologias não anunciadas.

![](https://trello-attachments.s3.amazonaws.com/5d7e8031eaec3e42c24aade0/5d7e81516a6cc012940f6135/f5b72e7216f0b595213e17d76929df4f/tress-fx-2.0-conclusions-1024x558.jpg)

**Você poderia nos dar sua opinião atual sobre o estado do mercado de PCs? Parece que com a próxima geração de consoles usando CPUs baseadas em X86 e um desenvolvimento mais unificado, o PC está se beneficiando enormemente.**

Robert Hallock: os jogos para PC estão vivos e  saudáveis . Revelamos no Havaí, com o lançamento das séries AMD Radeon ™ R9 e R7, que o entusiasta hardware de PC está crescendo US $ 1 bilhão ano a ano até 2016. É um momento fabuloso para ser um jogador! Mas, novamente, quando  não  foi incrível ser um jogador?


**Como você vê a progressão das CPUs, especificamente para o PC de mesa (jogos) em desenvolvimento nos próximos 3 a 5 anos?** 

Robert Hallock: Receio não poder responder razoavelmente a essa pergunta, pois não trabalho na divisão de CPU da AMD. (Nota do entrevistador: tenho outra entrevista agendada, onde perguntarei isso e muito mais!)

 

Amanhã ou no dia seguinte será outra parte da entrevista. Robert voltou para mim com outra carga de respostas no último minuto.

Portanto, esse é o fim da primeira parte de nossa entrevista com comunicações técnicas, jogos e gráficos para desktop da AMD, Robert Hallock e AMD como um todo. Gostaria de estender meus agradecimentos à AMD pela entrevista e eu (junto com sem dúvida muitos leitores) estamos ansiosos pela próxima parte da entrevista. Portanto, fique atento e espero que você participe da análise técnica e da segunda parte da entrevista aqui mesmo na RedGamingTech!




---

Autor: CrimsonRayne

[Artigo Original](http://www.redgamingtech.com/exclusive-amd-interview-discussing-gcn-architecture-performance-the-future-part-1/)
