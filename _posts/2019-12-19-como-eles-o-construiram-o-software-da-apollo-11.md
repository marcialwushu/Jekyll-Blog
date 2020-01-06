---
layout: post
title:  "Como eles o construíram: O Software da Apollo 11"
date:   2019-12-19 17:59:38 -0200
categories: jekyll update
---

Quando o Módulo Lunar da [Apollo 11](http://www.pcworld.com/article/168605/apollos_40th_anniversary_shows_true_wonder_of_the_internet.html) [pousou na Lua, há 40 anos](http://www.nasa.gov/mission_pages/apollo/40th/index.html), hoje , o software que ajudou a levar os seres humanos a outro corpo celeste foi essencialmente construído usando rolos de fita de papel e cartolina grossa que foi perfurada por furos especiais.

Não era de código aberto no sentido que conhecemos hoje, mas foi construído para a NASA sob contrato e, em seguida, foi testado, modificado e ajustado pelos engenheiros da NASA de maneiras semelhantes aos projetos de código aberto atualmente.

"Bem, na definição de hoje, era de código aberto - o código-fonte estava disponível ao público", para os engenheiros da missão, disse [John "Jack" Garman](http://klabs.org/mapld05/invited/garman_bio.htm) , engenheiro de computação da NASA de 24 anos quando o Apollo 11 decolou em 16 de julho de 1969 , a caminho da lua. "Mas 'código aberto' 'no sentido do Linux geralmente significa que qualquer pessoa pode contribuir com adições e melhorias, e é claro que esse não foi o caso do software Apollo".

Garman ajudou a testar e reescrever o software antes que o Apollo 11 deixasse o chão, e continuou a monitorá-lo enquanto era usado nos computadores de bordo. “O software foi programado em cartões perfurados da IBM. Eles tinham 80 colunas e foram 'montados' para instruções binárias em mainframes, e isso levou horas. ”

Durante a missão, a maior parte do código do software não pôde ser alterada porque estava codificada no hardware, como a ROM de hoje, disse ele. Porém, durante as simulações de design de pré-lançamento, os problemas que surgiam no código às vezes podiam ser solucionados por Garman e outros engenheiros de computação, usando uma pequena quantidade de memória apagável disponível para os programas.

“Alguns de nós, engenheiros da NASA que também trabalhavam no Controle de Missões, [literalmente adivinharam] e 'compuseram' pequenas alterações no software para contornar [hipotéticas] 'falhas' lançadas na equipe de controle de vôo durante simulações Garman disse. “De certa forma, isso se encaixa no modelo de código aberto, mas apenas dentro do domínio NASA e NASA Contractor.” Os funcionários da NASA tiveram acesso total ao código do programa através de seus contratos com os fornecedores de hardware da Apollo, para que pudessem alterar o código para fazer o programa se comportar de maneira diferente conforme necessário.

O software usava uma [linguagem de montagem](http://www.osdata.com/topic/language/asm/asmintro.htm) de baixo nível e era controlado usando pares ou segmentos de números inseridos em um teclado quadrado, apenas numérico chamado [Unidade de Display e Teclado](http://authors.library.caltech.edu/5456/1/hrst.mit.edu/hrs/apollo/public/images/Plate_37_small.jpg) , ou DSKY, dentro de cada cápsula da Apollo e do Módulo Lunar. Os códigos de dois dígitos representavam 'substantivos' ou 'verbos' e eram usados ​​para inserir [comandos (verbos) ou dados (substantivos)](http://klabs.org/history/history_docs/ech/agc_scott.pdf) , como ângulos de ancoragem de naves espaciais ou intervalos de tempo para operações.

Os [sistemas Apollo Guidance Computer (AGC)](http://klabs.org/history/history_docs/mit_docs/1707.pdf) em cada nave foram projetados e construídos por equipes de pesquisadores e estudantes do [Instituto de Tecnologia de Massachusetts (MIT)](http://klabs.org/history/history_docs/mit_docs/index.htm) , liderado pelo falecido [Dr. Charles Stark Draper](http://authors.library.caltech.edu/5456/1/hrst.mit.edu/hrs/apollo/public/people/csdraper.htm) , sob contrato com a NASA. Garman foi um dos muitos funcionários da NASA que ajudaram a executar, testar e depurar o código do MIT que executaria a missão Moon desde o lançamento até o splashdown. Alguns entusiastas dedicados chegaram a [projetar e construir seus próprios computadores](http://www.galaxiki.org/web/main/_blog/all/build-your-own-nasa-apollo-landing-computer-no-kidding.shtml) para [replicar os dispositivos Apollo originais](http://klabs.org/history/build_agc/) .

"O AGC foi muito lento, mas muito confiável e muito pequeno para a época na história dos computadores digitais", disse Garman. "Foi o primeiro a usar circuitos integrados."

O software como ele foi projetado foi construído basicamente do zero pelo MIT, disse ele. Como eles sabiam com o que começar? “O MIT realmente não - eles meio que inventaram isso enquanto avançavam. Nem a NASA nem o MIT haviam desenvolvido software para controle digital de vôo e sistemas de orientação no passado - ninguém tinha essa magnitude. Por isso, foram necessárias algumas investigações da parte da NASA e do MIT para anotar os requisitos e criar cronogramas e planos de teste difíceis. ”

Uma ampla gama de módulos diferentes foi necessária para diferentes fases da missão Moon, desde o sistema operacional até a interface do usuário e os programas para cada fase do vôo no computador do módulo de comando e no computador do módulo lunar. Isso significava pedidos de subida, órbita, injeção trans-lunar no caminho para a Lua, costa, órbita lunar, injeção trans-Terra no retorno à Terra e reentrada. Os mesmos tipos de aplicações eram necessários para o Módulo Lunar, incluindo descida, operações de superfície, subida, encontro e anulação de descida, se necessário.

Mas enquanto a maioria dos programas de software não pôde ser reescrita durante uma missão, uma vez que estavam em grande parte na ROM e não pôde ser alterada durante o voo, a ordem na qual os programas foram executados pode ser reorganizada durante a missão, se necessário. Isso permitiu que os controladores de voo mudassem quando e como os programas eram executados para fornecer resultados diferentes durante o voo. Não é como as missões tripuladas do Ônibus Espacial de hoje, mas funcionou.

Durante a descida do Módulo Lunar da Apollo 11 à Lua, há 40 anos, Garman desempenhou um papel direto na prevenção do abortamento de uma missão. Várias [luzes de aviso e alarmes de sobrecarga de computador acenderam](http://klabs.org/history/apollo_11_alarms/eyles_2004/eyles_2004.htm) quando a nave desceu logo acima da superfície da Lua, causando preocupação no Controle da Missão, mas todas as experiências de simulação pré-vôo de Garman lhe disseram que os alarmes não eram críticos e o pouso poderia continuar. Sem hesitar e sem entrar em pânico, o engenheiro de computação da NASA, de 24 anos, deu confiança ao 'ir' para continuar a missão.

Granville Paules, era um oficial de orientação de 32 anos de uma das equipes da missão Apollo 11 e lembra bem esse momento.

"Os alarmes dispararam durante a descida", disse Paules. “Havia um conflito entre os sistemas de bordo e o computador estava começando a ficar sobrecarregado. Garman fez uma simulação em que algo semelhante havia ocorrido cerca de três semanas antes, então ele sabia o que fazer. Provavelmente teria sido muito mais assustador, possivelmente até um abortamento para o pouso, se não tivéssemos essa simulação. Posso dizer que as chances de abortar esse pouso lunar eram muito maiores do que as pessoas querem acreditar. Essa simulação deu a todos a confiança necessária para desligar o alarme e ignorá-lo. ”

Enquanto tudo isso acontecia, "todo o Centro de Controle da Missão era como o interior de um mausoléu", disse ele. “Você não podia ouvir um som até que ele pousou e todos exalaram ao mesmo tempo. Foi palpável.

Foi realmente um marco incrível, disse [Gene Kranz](http://www.pbs.org/wgbh/nova/tothemoon/kranz.html) , um dos vários diretores de vôo da Apollo 11.

"Aterrissamos na Lua com menos de 17 segundos de combustível restante", lembrou Kranz. "Quando desligamos o motor, cumprimos a promessa que fizemos ao presidente (John F.) Kennedy e à tripulação da Apollo 1." [Kennedy lançou a meta dos EUA de desembarcar um homem na Lua em um discurso de maio de 1961 mas foi assassinado dois anos depois e nunca viu seu sonho realizado, enquanto a tripulação de três homens da Apollo 1 morreu em um incêndio na plataforma de lançamento em janeiro de 1967 enquanto treinava o que seria o primeiro vôo da Apollo em órbita terrestre.]

Sete meses após a missão Apollo 11, Kranz desempenharia outro grande papel no programa Apollo da NASA. Ele foi um dos principais heróis que ajudou a levar a tripulação da Apollo 13 para a Terra em abril de 1970, depois que um tanque de oxigênio explodiu quando a nave se dirigiu para Moon.

"A verdadeira chave [para o sucesso do primeiro pouso na lua da Apollo 11] foi o treinamento absolutamente espetacular que tivemos, as equipes que tínhamos e a liderança de confiança que tínhamos", disse Kranz. "Ainda fico maravilhado com a confiança que tinha naquele dia e com a minha equipe."

[Jerry Bostick](http://www.jsc.nasa.gov/history/oral_histories/BostickJC/bostickjc.pdf) tinha 30 anos e era membro da Equipe Branca de Kranz para a Apollo 11.

"Comecei na divisão de planejamento de missões, projetando missões", disse ele. "Escreveríamos os requisitos para todo o software nos computadores terrestres e integrados, trabalhando principalmente com o MIT e a IBM."

"Daríamos instruções aos programas perfurando cartões", disse Bostick. “Você teve que esperar pelo menos 12 horas para ver se funcionaria corretamente.” A programação inicial foi feita no complexo de computação em tempo real em Houston usando computadores [IBM 7094](http://www-03.ibm.com/ibm/history/exhibits/mainframe/mainframe_PP7094.html) com 64K de memória. Não havia discos rígidos. Todos os dados foram armazenados em fita magnética, com cada computador tendo cerca de oito unidades de fita. A maioria dos programas usados ​​para a missão foram escritos em Fortran, disse Bostick. “Após o Apollo 1, atualizamos para o maior e o melhor equipamento que o dinheiro do governo poderia comprar, o [IBM 360](http://www-03.ibm.com/ibm/history/exhibits/mainframe/mainframe_intro2.html), com 1 MB de memória inédito. Fomos de 64K a 1MB. ”

Hoje, Bostick diz que ainda está surpreso. "Eu tenho que admitir, às vezes me pergunto, oh cara, nós realmente fizemos isso?", Ele disse. “Reconheço que estava envolvido em uma das maiores realizações da humanidade na época, mas nenhum de nós se ocupou disso naquela época. Era apenas um trabalho que tínhamos que fazer, que o presidente havia estabelecido e nos disse para sair e descobrir como fazê-lo. ”

[Jay H. Greene](http://www.nasa.gov/offices/nac/members/greene-bio.html) era um oficial de dinâmica de voo de 27 anos da Apollo 11 para a descida do Módulo Lunar à Lua. "Nunca pensamos no que não podíamos fazer", disse Greene. "Estávamos tão envolvidos na realização do trabalho que não duvidamos que isso fosse possível."

“Foi uma coisa bastante primitiva”, disse Greene sobre os computadores e programas que levaram os americanos à Lua para a Apollo 11. “Eu não diria que é bruto. Eu diria elegante. Sim, o Apollo 11 foi legal. Eu me considero muito afortunado por estar envolvido nisso.

---

Autor: [Todd R. Weiss](https://www.linux.com/author/trwhouse/)

[Artigo Original](https://www.linux.com/news/how-they-built-it-software-apollo-11/)
