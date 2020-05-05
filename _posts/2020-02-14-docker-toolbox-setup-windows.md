---
layout: post
title:  "Docker Toolbox Setup — Windows"
date:   2020-02-14 17:59:38 -0200
categories: jekyll update
---

>Artigo de 15 de agosto de 2015

Com o lançamento do Docker 1.8, os usuários do Windows que estão aprendendo o Docker usando o Boot2Docker VM Tool, precisam aprender alguns novos conceitos para colocar seu ambiente no lugar da jornada de aprendizado do Docker.

![](https://miro.medium.com/proxy/0*BvwhA2Qbw3sjItZ1.jpg)

O guia abaixo apresenta como obter a Configuração da Docker Toolbox no Windows e os conceitos gerais por trás da Docker Machine, para que, se você já conhecesse o Boot2Docker antes, sua jornada seja tranqüila. Se é a primeira vez que instala a cadeia de ferramentas Docker na sua caixa do Windows, você também veio ao lugar certo!

## Faça o download do instalador

Você precisa ter o Windows 7.1,8, 8.1 para executar a Docker Toolbox. A página de instalação está [aqui](https://docs.docker.com/installation/windows/) e faz sentido examiná-la para validar certas coisas sobre o seu sistema operacional.
O instalador está disponível [aqui](https://www.docker.com/toolbox) e você deve clicar no botão Download (Windows) para baixar a versão mais recente do instalador.

## Execute o instalador

Depois de baixar o binário do Instalador em sua máquina, inicie-o e preste atenção especial ao seguinte:

- Instale na unidade C: \ padrão e não em outra unidade. Isso evitará alguns problemas com a inicialização do Docker Machine posteriormente.
- Em Selecionar componentes, desmarque Kitematic por enquanto. É melhor instalar as ferramentas de linha de comando enquanto estiver aprendendo, para que você saiba o que acontece sob o capô. Eu gosto do Kitematic e sugiro que você olhe para ele, mas por enquanto, vamos nos ater às ferramentas de linha de comando.

Passe pela instalação, selecionando os padrões para as outras etapas.

## O que aconteceu?

Na instalação bem-sucedida, você deve ter o seguinte:

Uma pasta chamada C: \ Arquivos de Programas \ Docker Toolbox é criada e contém vários arquivos-chave, mas mencionaremos alguns deles aqui:

- **docker-machine.exe**: este é o utilitário a ser usado para criar / gerenciar VMs do docker no seu computador. Nós entraremos em contato com eles daqui a pouco, mas isso é um shell de comando que pode criar / gerenciar uma ou mais VMs do Docker em sua máquina e definir uma das VMs do Docker, ou seja, máquinas como destino, que você pode usar para executar o padrão comandos com o utilitário docker.exe que é o próximo.
- **docker.exe**: este é o cliente docker padrão (que, se você já usou antes - deve ser familiar). Agora, isso é usado diretamente na sua máquina Windows e pode se comunicar com a Docker Machine que você definiu como destino. Ele executará comandos do docker nessa máquina e mostrará os resultados.

Além da pasta acima, você tem mais duas coisas em mente:

- A pasta C: \ Arquivos de programas \ Docker Toolbox foi adicionada à sua variável PATH do ambiente . Isso significa que você pode executar os programas cliente docker-machine.exe e docker.exe de qualquer lugar. Isso é útil.
- Existe um atalho criado na sua área de trabalho chamado "Docker Quickstart Terminal" . Na verdade, isso iniciará o arquivo ./start.sh presente na pasta C: \ Arquivos de Programas \ Docker Toolbox .


O **Docker Quickstart Terminal** é uma boa coisa para iniciar em seguida. Clique duas vezes e inicie-o. Ele criará um Docker Machine padrão para você (nomeado padrão ). Isso significa que, se tudo correr bem, você já possui uma Máquina Docker, que nada mais é que uma VM Docker que está sendo executada em sua máquina com o Docker Daemon em execução, pronto para aceitar comandos. Pense nisso como nada além de sua VM Boot2Docker que está sendo executada (se você estiver familiarizado com isso).

## Docker Machine

Para aqueles que conhecem o Boot2Docker e como ele é executado no Windows, este diagrama deve estar familiarizado com a documentação oficial do Docker:

![](https://miro.medium.com/proxy/0*QVytIImU3tr8GaHO.png)


O DOCKER_HOST que você vê no diagrama acima nada mais é do que a VM boot2docker que estava sendo executada dentro do Virtual Box.

Com o [Docker Machine](https://docs.docker.com/machine/) , agora você pode conceitualmente pensar nele como uma instância do DOCKER_HOST. O que isso significa é que você pode ter várias máquinas Docker em execução no seu computador. Não é apenas isso, mas também é uma maneira genérica de criar Docker Hosts não apenas no seu computador, mas também em provedores de nuvem, seu próprio data center e muito mais.

Na máquina Windows, o driver é o sistema Oracle VirtualBox, que usará a VM Boot2Docker nos bastidores. Está começando a fazer sentido, não é?


Para entender melhor, consulte o diagrama abaixo (é uma versão simplificada de tudo e pode não ser muito preciso, mas me ajudou a entender e colocar as ferramentas em contexto em relação às suas funções):


![](https://miro.medium.com/proxy/0*wc23OZehkPqXONKg.)

Existem algumas coisas importantes aqui para ajudá-lo a entender a função do Docker Client (docker.exe) e por que existe uma única seta que está conectando-a a uma das Máquinas Docker (Docker Machine 1).

Mas primeiro, vamos esclarecer com a Docker Machine vis-à-vis o diagrama mostrado acima. Você pode ter um ou mais Docker Machines em execução no seu computador, conforme mostrado. Você cria e gerencia os Docker Machines (criar, parar, iniciar, etc) por meio do utilitário docker-machine.exe. Ele possui sua própria lista de comandos, alguns dos quais veremos na próxima seção. Pense neles como seus comandos do Boot2Docker (se você estiver familiarizado com isso).

Agora, cada Docker Machine é seu próprio chefe. Cada máquina ou host do Docker terá seu próprio endereço IP, ou seja, o endereço IP da VM.

Então, como você executa comandos do docker em cada um deles? É aí que o cliente docker.exe entra. Veremos os comandos daqui a pouco, mas o que precisamos fazer é que precisamos usar o utilitário docker-machine.exe para definir o ambiente do cliente Docker (docker.exe ) O ambiente nada mais é do que definir determinadas variáveis ​​de ambiente que definirão quem é o host do Docker (Docker Machine), a porta, o endereço IP e assim por diante. Então, quando você executar o "docker <comando>", ele entrará em contato com o daemon do Docker em execução no host do Docker (Docker Machine). Dessa forma, você pode alternar o ambiente para apontar para outra Docker Machine e executar comandos da janela de encaixe nessa. Essa é uma coisa legal.

**Nota** : Quando você executa o atalho do Docker Quickstart Terminal em sua máquina, ele cria uma Docker Machine para você denominada padrão . Eu recomendo fortemente que você siga os conceitos da Docker Machine , é um guia bem escrito.


## Comandos da máquina do Docker

Como mencionado, o Docker Machine é um utilitário chamado docker-machine.exe e está disponível na variável PATH , para que você possa invocá-lo de qualquer lugar.

Possui vários comandos que são bastante intuitivos e o que você esperaria. Por exemplo, criando novas Docker Machines, listando as atuais, encontrando o status das Docker Machines (em execução / paradas), excluindo-as, atualizando-as e muito mais. Você pode encontrar uma lista completa dos comandos do Docker Machine [aqui](https://docs.docker.com/machine/reference/) .

Vamos tentar alguns comandos agora. Abra uma janela do prompt de comando (cmd.exe).


Supondo que você executou o Docker Quickstart Terminal e que a máquina Docker 'padrão' foi criada, dê o seguinte comando:

```
docker-machine ls
```

Isso deve listar as máquinas Docker que você possui no seu computador.

```
NOME ACTIVE DRIVER STATE URL SWARM 
padrão caixa virtual padrão Executando tcp: //192.168.99.100: 2376 
dev virtualbox parado
```

Você pode ver na minha saída que eu tenho 2 Docker Machines (padrão e dev). Eu criei a máquina dev e, portanto, você vê uma máquina extra aqui.

Observe que o driver é mencionado como VirtualBox e no Windows, que é o Driver, ou seja, VirtualBox, que nos bastidores usará a imagem Boot2Docker.iso para iniciar o contêiner da VM do Linux. Para outros drivers, consulte os [drivers oficiais](https://docs.docker.com/machine/drivers/) suportados no momento em que escrevemos isso.

Observe o endereço IP que o Docker Machine padrão possui, juntamente com a porta padrão.

Como criamos outra máquina Docker. Bem, usamos o comando create, conforme indicado abaixo:


```
docker-machine create --driver máquina de caixa virtual007
```

Isso levará um tempo para criar uma máquina e você deverá ver a seguinte saída:

```
Creating VirtualBox VM...
Creating SSH key...
Starting VirtualBox VM...
Starting VM...
To see how to connect Docker to this machine, run: docker-machine env machine007
```

Aqui, demos o nome da Docker Machine como machine007 . Temos que fornecer o driver, que para nós no Windows é o VirtualBox.

Agora, se você executar um comando ls , verá as 3 Docker Machines listadas conforme indicado abaixo:


```
NAME         ACTIVE   DRIVER       STATE     URL                         SWARM
default               virtualbox   Running   tcp://192.168.99.100:2376
dev                   virtualbox   Stopped
machine007            virtualbox   Running   tcp://192.168.99.102:2376
```

Observe que o machine007 possui outro endereço IP. Você pode tentar outros comandos, como parar um Docker Machine ou iniciar um Docker Machine e assim por diante. Alguns exemplos são dados abaixo:


```
docker-machine start dev
docker-machine stop default
docker-machine status dev
```

Se você observar a GUI do Oracle Virtualbox, verá as VMs listadas como mostrado abaixo:

![](https://miro.medium.com/proxy/0*pjt-5_zGKvKbfsg5.png)


## Executando o cliente Docker

A parte final desse quebra-cabeça, mas que é muito importante, é como executamos o cliente docker.exe para direcionar uma máquina Docker específica. Se você estivesse prestando muita atenção ao criar uma Docker Machine por meio do comando `docker-machine create`, veria que a última linha de saída era a seguinte: Para ver como conectar o Docker a esta máquina, execute: docker- machine env machine007 Em resumo, precisamos usar o comando docker-machine env para definir algumas variáveis ​​de ambiente que são usadas pelo cliente docker.exe para conectar-se ao host do Docker específico. O que isso significa é que, logicamente, precisamos informar ao cliente onde está o host do Docker, a porta etc. Então, vamos assumir que queremos executar os comandos do docker na máquina do Docker chamada dev. Verifique se a máquina Docker está em execução antes de executar este comando. Na minha máquina, primeiro faço:

```
Prompt> docker-machine status dev
Stopped
```

Isso significa que está parado. Então eu inicio com o seguinte comando:

```
Prompt> docker-machine start dev
Starting VM...
Started machines may have new IP addresses. You may need to re-run the `docker-machine env` command.
```

Agora, deixe-me fazer um comando `ls` como mostrado abaixo:

```
docker-machine ls
NAME         ACTIVE   DRIVER       STATE     URL                         SWARM
default               virtualbox   Running   tcp://192.168.99.100:2376
dev                   virtualbox   Running   tcp://192.168.99.101:2376
machine007            virtualbox   Running   tcp://192.168.99.102:2376
```

Ótimo, então eu quero conectar agora à máquina dev , então eu dou o seguinte comando:

```
docker-machine env --shell cmd dev
```

Isso nos dá a seguinte saída:


```
set DOCKER_TLS_VERIFY=1
set DOCKER_HOST=tcp://192.168.99.101:2376
set DOCKER_CERT_PATH=C:\Users\irani_r\.docker\machine\machines\dev
set DOCKER_MACHINE_NAME=dev
# Run this command to configure your shell: copy and paste the above values into your command prompt
```


O que isso significa é que você precisa executar manualmente os comandos set acima. Copie e cole cada um dos comandos set acima no prompt de comando. Depois de concluir isso, o que você especificou são detalhes do Docker Machine que o cliente docker agora pode usar.

Agora, vá em frente e use seu cliente docker.exe como antes. Execute comandos como imagens do docker, docker ps, informações do docker e assim por diante. Os comandos serão executados apenas contra a máquina Docker desenv .

Se você deseja executar os comandos do docker em outra Docker Machine, use o comando docker-machine env novamente para obter as variáveis ​​de ambiente específicas, configure-as e pronto.


### Dica da máquina do Docker: SSH na máquina

Caso você queira fazer o SSH diretamente na máquina do Docker e não entrar em todo esse material de ambiente, escrevi um post sobre como fazer isso. [Confira](http://rominirani.com/2015/08/15/docker-machine-tip-ssh-into-the-docker-machine/) .

## Sumário

Espero que isso o prepare agora para sua jornada no Docker, se você já conhece o Boot2Docker e está tentando entender o Docker Machine e a nova caixa de ferramentas.

Lembre-se de que a Caixa de ferramentas do Docker está na versão beta. Então, espere que algumas coisas não funcionem às vezes e seja paciente.


---


Author: [Romin Irani](https://rominirani.com/@iromin?source=follow_footer--------------------------follow_footer-)


[Artigo Oeiginal](https://rominirani.com/docker-toolbox-setup-windows-4d65c3f691eb)







