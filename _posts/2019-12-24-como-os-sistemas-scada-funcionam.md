---
layout: post
title:  "Como os sistemas SCADA funcionam?"
date:   2019-12-24 17:59:38 -0200
categories: jekyll update
---

## Introdução:

SCADA significa controle de supervisão e aquisição de dados. É um tipo de programa de software para controle de processos. O SCADA é um sistema de controle central que consiste em interfaces de rede de controladores, entrada / saída, equipamentos de comunicação e software. Os sistemas SCADA são usados ​​para monitorar e controlar os equipamentos no processo industrial, que incluem manufatura, produção, desenvolvimento e fabricação. Os processos de infra-estrutura incluem distribuição de gás e óleo, energia elétrica, distribuição de água. Os serviços públicos incluem sistema de tráfego de ônibus, aeroporto. O sistema SCADA faz a leitura dos medidores e verifica o status dos sensores em intervalos regulares para que exija a mínima interferência humana.

![](https://www.elprocus.com/wp-content/uploads/2013/10/General-SCADA-Network.png)

Um grande número de processos ocorre em grandes estabelecimentos industriais. Todo processo que você precisa monitorar é muito complexo, porque cada máquina fornece resultados diferentes. O sistema SCADA costumava coletar os dados de sensores e instrumentos localizados na área remota. O computador processa esses dados e os apresenta em tempo hábil. O sistema SCADA reúne as informações (como ocorreu um vazamento em uma tubulação) e transfere as informações de volta para o sistema, enquanto fornece os alertas de que ocorreu o vazamento e exibe as informações de maneira lógica e organizada. O sistema SCADA costumava ser executado nos sistemas operacionais DOS e UNIX.

## Arquitetura:

Geralmente, o sistema SCADA é um sistema centralizado que monitora e controla toda a área. É puramente pacote de software que está posicionado em cima do hardware. Um sistema supervisório reúne dados sobre o processo e envia os comandos de controle para o processo. O SCADA é uma unidade terminal remota, também conhecida como RTU. A maioria das ações de controle é executada automaticamente por UTRs ou CLPs. As UTRs consistem em um conversor lógico programável que pode ser configurado para um requisito específico. Por exemplo, na usina termelétrica, o fluxo de água pode ser definido para um valor específico ou pode ser alterado de acordo com o requisito.

O sistema SCADA permite que os operadores alterem o ponto de ajuste do fluxo e habilitem condições de alarme em caso de perda de fluxo e alta temperatura, e a condição é exibida e registrada. O sistema SCADA monitora o desempenho geral do loop. O sistema SCADA é um sistema centralizado para se comunicar com a tecnologia sem fio e sem fio aos dispositivos Clint. Os controles do sistema SCADA podem executar completamente todos os tipos de processos industriais.
 
 EX: Se houver muita pressão na construção de uma tubulação de gás, o sistema SCADA pode abrir automaticamente uma válvula de liberação.
 
 
 ### 1. Arquitetura de hardware:
 
 
 O sistema geralmente SCADA pode ser classificado em duas partes:

- Camada de Clint
- Camada do servidor de dados

A camada Clint que atende à interação homem-máquina.

A camada do servidor de dados que lida com a maioria das atividades de dados do processo.

A estação SCADA refere-se aos servidores e é composta por um único PC. Os servidores de dados se comunicam com os dispositivos em campo através de controladores de processo, como PLCs ou RTUs. Os CLPs são conectados aos servidores de dados diretamente ou via redes ou barramentos. O sistema SCADA utiliza redes WAN e LAN, a WAN e LAN consistem em protocolos da Internet usados ​​para comunicação entre a estação mestre e os dispositivos. Os equipamentos físicos, como sensores conectados aos CLPs ou UTRs. As RTUs convertem os sinais do sensor em dados digitais e enviam dados digitais para o mestre. De acordo com o feedback mestre recebido pela RTU, aplica o sinal elétrico aos relés. A maioria das operações de monitoramento e controle é realizada por UTRs ou CLPs, como podemos ver na figura.

![](https://www.elprocus.com/wp-content/uploads/2013/10/SCADA-Diagram.png)

### 2. Arquitetura de Software:

A maioria dos servidores é usada para multitarefa e banco de dados em tempo real. Os servidores são responsáveis ​​pela coleta e manipulação de dados. O sistema SCADA consiste em um programa de software para fornecer tendências, dados de diagnóstico e gerenciar informações como procedimento de manutenção agendada, informações logísticas, esquemas detalhados para um sensor ou máquina em particular e guias especializados para solução de problemas do sistema. Isso significa que o operador pode exibir uma representação esquemática da planta que está sendo controlada.

EX: verificação de alarme, cálculos, registro e arquivamento; controladores de polling em um conjunto de parâmetros, esses geralmente são conectados ao servidor.

![](https://www.elprocus.com/wp-content/uploads/2013/10/Architecture-of-SCADA-system.png)

### Procedimento de trabalho do sistema SCADA:

O sistema SCADA executa as seguintes funções:

- Aquisições de dados
- Comunicação de dados
- Apresentação de informações / dados
- Monitoramento / Controle

Essas funções são executadas por sensores, RTUs, controlador, rede de comunicação. Os sensores são usados ​​para coletar informações importantes e as RTUs são usadas para enviar essas informações ao controlador e exibir o status do sistema. De acordo com o status do sistema, o usuário pode dar comando para outros componentes do sistema. Esta operação é realizada pela rede de comunicação.

### Aquisições de dados:

O sistema em tempo real consiste em milhares de componentes e sensores. É muito importante conhecer o status de componentes e sensores específicos. Por exemplo, alguns sensores medem o fluxo de água do reservatório para o tanque de água e alguns sensores medem o valor da pressão conforme a água é liberada do reservatório.

### Comunicação de dados:

O sistema SCADA usa rede com fio para se comunicar entre usuário e dispositivos. As aplicações em tempo real usam muitos sensores e componentes que devem ser controlados remotamente. O sistema SCADA utiliza comunicações pela Internet. Todas as informações são transmitidas através da Internet usando protocolos específicos. O sensor e os relés não conseguem se comunicar com os protocolos de rede, portanto, as UTRs são usadas para comunicar sensores e a interface de rede.

### Apresentação de informações / dados:

As redes de circuitos normais possuem alguns indicadores que podem ser visíveis para controle, mas no sistema SCADA em tempo real, existem milhares de sensores e alarmes que são impossíveis de serem manipulados simultaneamente. O sistema SCADA usa a interface homem-máquina (HMI) para fornecer todas as informações coletadas dos vários sensores .

### Interface homem-máquina:

O sistema SCADA usa interface homem-máquina. As informações são exibidas e monitoradas para serem processadas pelo ser humano. A HMI fornece o acesso a várias unidades de controle que podem ser PLCs e RTUs. A IHM fornece a apresentação gráfica do sistema. Por exemplo, fornece a imagem gráfica da bomba conectada ao tanque. O usuário pode ver o fluxo da água e a pressão da água. A parte importante da HMI é um sistema de alarme que é ativado de acordo com os valores predefinidos.

![](https://www.elprocus.com/wp-content/uploads/2013/10/SCADA-Experimental-diagram.png)

Por exemplo: O alarme do nível da água do tanque está configurado para valores de 60% e 70%. Se o nível da água atingir acima de 60%, o alarme emitirá um aviso normal e se o nível da água atingir acima de 70%, o alarme emitirá um aviso crítico.

### Monitoramento / Controle:

O sistema SCADA usa comutadores diferentes para operar cada dispositivo e exibe o status na área de controle. Qualquer parte do processo pode ser LIGADA / DESLIGADA a partir da estação de controle usando esses interruptores. O sistema SCADA é implementado para funcionar automaticamente sem intervenção humana, mas em situações críticas é tratado pelo poder do homem.

### SCDA para instalações industriais remotas:

Em grandes estabelecimentos industriais, muitos processos ocorrem simultaneamente e cada um precisa ser monitorado, o que é realmente uma tarefa complexa. Os sistemas SCADA são usados para monitorar e controlar os equipamentos nos processos industriais, que incluem distribuição de água, distribuição de óleo e distribuição de energia. O principal objetivo deste projeto é processar os dados em tempo real e controlar o ambiente industrial remoto em larga escala. No cenário em tempo real, é adotado um sistema de registro de temperatura para uma operação remota da planta.

![](https://www.elprocus.com/wp-content/uploads/2013/10/Temperature-Control-industrial-plant.png)

Os sensores de temperatura estão conectados ao microcontrolador, que está conectado ao PC no front-end e o software é carregado no computador. Os dados são coletados dos sensores de temperatura. Os sensores de temperatura enviam continuamente o sinal ao microcontrolador, que exibe esses valores em seu painel frontal. Pode-se definir parâmetros como limite baixo e limite alto na tela do computador. Quando a temperatura de um sensor ultrapassa o ponto de ajuste, o microcontrolador envia um comando ao relé correspondente. Os aquecedores conectados através dos contatos do relé são desligados e ligados.

### Por exemplo, SCADA para Planeta Industrial Remoto:

Este é um sistema de registro de temperatura. Aqui, 8 sensores de temperatura no modo de multiplexação são conectados ao microcontrolador através do ADC 0808. Em seguida, os valores de todos os sensores são enviados serialmente pelo microcontrolador através do Max 32 à porta de comunicação do PC. Um software “DAQ System” carregado no PC pega esses valores e os mostra em seu painel frontal, além de registrá-los no banco de dados “daq.mdb”. É possível definir de maneira interativa alguns parâmetros como ponto de ajuste, limite baixo, e limite alto na tela do computador. Quando a temperatura de algum sensor aumenta além do ponto de ajuste, o microcontrolador envia comandos para retransmitir o IC do driver. Os aquecedores conectados através dos contatos do relé são (específicos para esse sensor) DESLIGADOS (ou LIGADOS no caso oposto). Limites alto e baixo são para alarme.

![](https://www.elprocus.com/wp-content/uploads/2013/10/SCADA-for-Remote-Industrial-Planet.png)

###  Aplicações :

- Geração, transmissão e distribuição de energia
- Sistema de distribuição e reservatório de água
- Edifícios públicos, como aquecimento elétrico e sistema de refrigeração.
- Geradores e turbinas
- Sistema de controle de semáforo

### Vantagens:

- O sistema SCADA fornece informações mecânicas e gráficas a bordo
- O sistema SCADA é facilmente expansível. Podemos adicionar um conjunto de unidades de controle e sensores de acordo com o requisito.
- A capacidade do sistema SCADA de operar situações críticas.

---

[Artigo Original](https://www.elprocus.com/scada-systems-work/)
