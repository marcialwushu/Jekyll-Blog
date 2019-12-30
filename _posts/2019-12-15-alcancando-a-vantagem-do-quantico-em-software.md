---
layout: post
title:  "Alcançando a vantagem do Quantico em software"
date:   2019-12-15 17:59:38 -0200
categories: jekyll update
---

O Departamento de Defesa (DoD) enfrenta uma série de problemas de engenharia de software com desafios computacionais, incluindo aprendizado de máquina e [inteligência artificial (IA)](https://www.sei.cmu.edu/research-capabilities/artificial-intelligence/), além de validar e verificar sistemas de software cada vez mais complexos. Encontrar a solução ideal para esses desafios, conhecidos como [problemas de otimização combinatória](http://www.cs.cmu.edu/afs/cs.cmu.edu/project/learn-43/lib/photoz/.g/web/glossary/comb.html) , é um [polinômio não determinístico](https://www.scottaaronson.com/blog/?p=459) e, com paradigmas clássicos de computação, pode levar bilhões de anos para ser resolvido. No [Centro de Tecnologia Emergente (ETC)](https://www.sei.cmu.edu/about/divisions/emerging-technology-center/index.cfm) do SEI , estamos trabalhando para aplicar a computação quântica para resolver esses problemas de missão crítica do DoD. Conforme descrito neste post, nosso último esforço se concentra na [computação quântica de curto prazo para verificação e validação de software](https://www.sei.cmu.edu/research-capabilities/all-work/display.cfm?customel_datapageid_4050=179161) dentro do Departamento de Defesa.

Desde o início da [era de escala pós-Dennard](https://en.wikipedia.org/wiki/Dennard_scaling) e o [fim da Lei de Moore](https://www.technologyreview.com/s/601441/moores-law-is-dead-now-what/) , o paradigma da computação em circuito integrado atingiu seus limites fundamentais. Ao mesmo tempo, o Departamento de Defesa precisa de um novo paradigma de computação para ajudá-lo a obter uma vantagem de missão em aprendizado de máquina e inteligência artificial (ML / AI). Michael Hayduk, chefe da divisão de computação e comunicações do Laboratório de Pesquisa da Força Aérea, disse ao Defense Innovation Board em julho de 2018 que " [o Pentágono está especialmente intrigado com o potencial da computação quântica em desenvolver comunicações seguras e navegação inercial no GPS negado e ambientes contestados](https://spacenews.com/pentagon-sees-quantum-computing-as-key-weapon-for-war-in-space/) ".

O governo federal também fez da computação quântica uma prioridade. Em dezembro de 2018, o Congresso aprovou a [Lei Nacional de Iniciativa Quântica](https://www.congress.gov/bill/115th-congress/house-bill/6227) , que estabelece um plano de 10 anos para acelerar o avanço das iniciativas de computação quântica e [direciona US $ 1,2 bilhão para o esforço](https://futurism.com/the-byte/quantum-computing-bill-congress) .

Os computadores quânticos funcionam fundamentalmente de maneira diferente dos computadores clássicos, alavancando os fenômenos quânticos de superposição e emaranhamento para construir [os elementos fundamentais da computação, os qubits](http://mmrc.amss.cas.cn/tlb/201702/W020170224608150244118.pdf) . O recente aumento na pesquisa de computação quântica se deve em grande parte às melhorias das Unidades de processamento de portas universais (UG QPU) conectadas a erros, que são NPQ (Noisy Intermediate Scale QPU). [Veja a página 20](https://doi.org/10.22331/q-2018-08-06-79) do artigo de John Preskill, [Computing in the NISQ Era and Beyond](https://arxiv.org/pdf/1801.00862.pdf) .

Um problema desafiador enfrentado pelo Departamento de Defesa ao qual a computação quântica pode ser aplicada é a [satisfação](https://en.wikipedia.org/wiki/Boolean_satisfiability_problem) (SAT), que é um algoritmo comum usado na verificação e validação de software. Exemplos incluem os [problemas de desafio da Lockheed Martin](http://mys5.org/Proceedings/2016/Day_2/2016-S5-Day2_0945_Elliott.pdf) , que envolvem componentes de software complicados dos controles de vôo da aeronave que automatizam manobras evasivas se a aeronave estiver em perigo. Como descrevemos [aqui](https://www.sei.cmu.edu/research-capabilities/all-work/display.cfm?customel_datapageid_4050=179161) , como resultado da complexidade do código e das manobras que ele controla, os computadores clássicos não conseguem verificar e validar se o código é seguro. A computação quântica permite um novo paradigma de algoritmos de otimização e recursos computacionais para resolver esses problemas em um momento crítico para a segurança e o sucesso da missão.

### Alcançando uma vantagem quântica na era NISQ

Conforme descrito em [um paper de fato publicada sobre este trabalho](https://resources.sei.cmu.edu/library/asset-view.cfm?assetid=540763) , algoritmos quânticos e computadores prometem aceleração polinomial e superpolynomial para algoritmos como [Grover](https://en.wikipedia.org/wiki/Grover%27s_algorithm) e [Shor](https://en.wikipedia.org/wiki/Shor%27s_algorithm), mas [estes algoritmos necessitam em excesso de O (10 5 -10 6 ) qubits com correção de erro quântico](https://ieeexplore.ieee.org/document/8490171) . Embora os computadores quânticos reais estejam disponíveis em diversas empresas, atualmente estamos na era do [Noisy Intermediate-Scale Quantum (NISQ)](https://arxiv.org/abs/1801.00862) . O número de qubits nos computadores quânticos atuais e de curto prazo é pequeno (O (10 1 -10 2)) e suas operações são barulhentas (ou seja, os bits têm uma alta probabilidade de virar à medida que interagem entre si e com o ambiente). Os computadores quânticos de hoje não têm qubits suficientes para executar a correção de erros quânticos; portanto, são necessários algoritmos que mitigam o ruído de outra maneira.

Especificamente, estamos investigando algoritmos de otimização de curto prazo que podem executar efetivamente em QPUs NISQ, como [Variational Quantum Eigensolver (VQE) e Quantum Approximation Optimization Algorithm (QAOA)](https://arxiv.org/abs/1411.4028) . Como escreveu Preskill em [Computação na era NISQ e além](https://arxiv.org/pdf/1801.00862.pdf) ,

>A tecnologia Quantum de escala intermediária ruidosa (NISQ) estará disponível em um futuro próximo. Computadores quânticos com 50 a 100 qubits podem ser capazes de executar tarefas, que superam as capacidades dos computadores digitais clássicos atuais, mas o ruído nos portões quânticos limitará o tamanho dos circuitos quânticos que podem ser executados de maneira confiável. Os dispositivos NISQ serão ferramentas úteis para explorar a física quântica de muitos corpos e podem ter outras aplicações úteis.

Trabalhar na [era NISQ](https://quantum-journal.org/papers/q-2018-08-06-79/) apresenta uma série de desafios para nós, incluindo os seguintes:

- O número de qubits é pequeno, portanto os tamanhos dos problemas não são grandes
- As soluções que os computadores quânticos apresentam nem sempre são boas

Nosso desafio é descobrir como usar dispositivos NISQ não apenas para resolver aplicativos de missão específicos para o Departamento de Defesa, mas também para ajudar a determinar quando eles demonstrarão a chamada vantagem quântica: um computador quântico resolvendo um problema de interesse prático mais rapidamente do que um computador clássico . Para ajudar o Departamento de Defesa a alcançar a vantagem quântica, nosso trabalho atual se concentra no seguinte:

- comparando técnicas de otimização quântica variacional, como QAOA, e sua capacidade de tolerar QPUs da era NISQ
- melhorando a geração de circuitos para QPUs da era NISQ
- analisando a hierarquia dos problemas de interesse e identificando quais partes podem ser mapeadas efetivamente para QPUs
- enfrentar os desafios de escalar até O (10 2 -10 3 ) qubits e prever / projetar vantagem quântica
- desenvolvimento de ferramentas de software para ajudar cientistas e engenheiros de dados a usar computadores quânticos
- criação de material para facilitar uma força de trabalho qualificada em computação quântica no DoD

### Olhando para o futuro

À medida que continuamos a explorar esses problemas, estenderemos nosso trabalho para novas aplicações, incluindo o estudo de aprendizado de máquina quântica envolvendo algoritmos quânticos para executar tarefas de aprendizado de máquina e inteligência artificial. Além disso, estamos trabalhando em sistemas de prova interativa quântica, usando QPUs para formar sistemas de prova interativa e verificando e validando a computação quântica.

Esperamos que este trabalho nos forneça melhores maneiras de verificar a solução para problemas complexos mais rapidamente, além de confirmar com segurança que os problemas terceirizados para serviços de computação quântica foram realmente resolvidos usando computadores quânticos. Nosso trabalho também tornará possível o uso de um computador quântico como núcleo de treinamento ou modelo de classificação para aprendizado de máquina, para que possamos treinar algoritmos e classificações muito mais rapidamente do que o anteriormente possível.

Como esta é uma das primeiras grandes incursões na computação quântica para o SEI, continuamos a prestar atenção às oportunidades que avançam neste novo ecossistema.

Em 2020, procure postagens de blog que abordem tópicos relacionados à computação quântica, incluindo ciência quântica de materiais, internet, comunicações e detecção.

### Recursos adicionais

Veja a ficha técnica, [Computação Quântica para Missão: Computação Quântica de Desempenho no SEI](https://resources.sei.cmu.edu/library/asset-view.cfm?assetid=540763) , que serviu como uma das fontes para este post.

Leia [Computação Quântica na era NISQ e mais adiante](https://doi.org/10.22331/q-2018-08-06-79) por John Preskill.

Visite nosso [site JupyterHub](https://quantum.etchub.xyz/hub/login) .

---

Autor: [Jason Larkin](https://insights.sei.cmu.edu/author/jason-larkin)

[Artigo Original](https://insights.sei.cmu.edu/sei_blog/2019/12/achieving-the-quantum-advantage-in-software.html)


