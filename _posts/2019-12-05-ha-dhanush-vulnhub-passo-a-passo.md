---
layout: post
title:  "HA: Dhanush Vulnhub Passo a passo"
date:   2019-12-05 17:59:38 -0200
categories: jekyll update
---

Hoje vamos resolver nosso desafio de inicialização para raiz chamado "HA Dhanush". Desenvolvemos este laboratório com o objetivo de práticas de penetração online. É baseado na arma que fazia parte de todas as guerras da época medieval. O arco e flecha. Como o laboratório é intitulado Dhanush. Algumas informações sobre a mitologia indiana e os arcos podem ajudar. Vamos resolver isso !!

**Faça o Download** [Aqui](https://www.vulnhub.com/entry/ha-dhanush,396/)

**Nível: Intermediário**

**Tarefa: Enumerar a máquina de destino e obter o acesso raiz.**

### Metodologias de penetração

- Digitalização em rede
    - Descoberta da Net
    - Nmap Scan
- Enumeração
    - Navegando no serviço HTTP
    - Criando um dicionário a partir da página da Web
- Exploração
    - Bruteforce o SSH
    - Gerando chave pública SSH para outro usuário
    - Efetuando login como outro usuário
- Escalonamento de privilégios
    - Identificar direitos do Sudo para o comando zip
    - Abusando dos direitos do Sudo
- Leitura da flag raiz

**Passo a passo**

### Digitalização em rede

Após o download, execute a máquina na estação de trabalho VMWare. Para trabalhar na máquina, precisaremos do seu endereço IP. Para isso, usaremos o comando netdiscover. Depois de corresponder o endereço MAC e IP, descobrimos que o endereço IP da máquina virtual era 192.168.1.101

```
netdiscover
```

![](https://i1.wp.com/1.bp.blogspot.com/-NmgSmoTI3aA/Xd_RdjqlNZI/AAAAAAAAhs0/HlmwYc0J_9cf76oYqt3PTvOVcPhnHkOkgCLcBGAsYHQ/s1600/1.png?w=687&ssl=1)

Agora que temos o endereço IP da máquina de destino, nosso próximo passo lógico seria fazer uma varredura de porta no destino para obter informações sobre os vários serviços em execução na máquina de destino. Geralmente fazemos apenas a verificação agressiva, mas, neste caso, estamos indo para a verificação de todas as portas. Por padrão, o Nmap verifica as 1.000 portas mais comuns para cada protocolo. Portanto, podemos especificar -p- para verificar as portas de 1 a 65535. Isso é feito, pois é seguro praticar mudar a porta de um serviço para uma porta incomum. Após a verificação de todas as portas, vemos que temos o serviço HTTP (80), serviço SSH (65345) em execução na máquina de destino.

```sh
nmap -p- -A 192.168.1.101
```

![](https://i0.wp.com/1.bp.blogspot.com/-FGb8gfbyQ8Y/Xd_RdqmuJ4I/AAAAAAAAhs4/yMBTh209ccUF1HadDuYZLAS5MZebIQlagCLcBGAsYHQ/s1600/2.png?w=687&ssl=1)

### Enumeração

Seguindo em frente, observamos que temos o serviço HTTP em execução. É provável que uma página da web esteja hospedada. Então, decidimos dar uma olhada no nosso navegador da web. Navegamos minuciosamente na página da web. Examinamos o código fonte e as imagens, mas não havia nenhuma maneira ou dica.

![](https://i0.wp.com/1.bp.blogspot.com/-Y282-jlxmn4/Xd_RdWGXpDI/AAAAAAAAhsw/g74UagRC3kktypo8XG21iiel32UQ72xdACLcBGAsYHQ/s1600/3.jpg?w=687&ssl=1)

Agora, antes de avançar, pensamos que esta página contém toneladas de informações sobre o Dhanush. Além disso, esses nomes provavelmente podem ser nomes de usuário ou senhas. Então, decidimos criar um dicionário usando o comando cewl.

```
cewl http://192.168.1.101/ -w dict.txt
cat dict.txt
```

![](https://i2.wp.com/1.bp.blogspot.com/-MZuWNn5zVA8/Xd_ReHDKHgI/AAAAAAAAhs8/-dsHeIyN7EgE_e6D68ZnaFQW5OIjP5QXQCLcBGAsYHQ/s1600/4.png?w=687&ssl=1)



#### Exploração

Decidimos iniciar nossa tentativa de explorar essa máquina de destino a partir da porta que o autor se esforçou para proteger a olho nu. O número da porta 65345 com o serviço SSH. Como não temos nomes de usuário ou senhas, decidimos aplicar força nesse login ssh usando o dicionário que acabamos de criar. Usaremos a hidra para o bruteforce de login. Estamos com sorte; obtivemos as credenciais de login para o SSH.

```
Username: pinak
Password: Gandiv
hydra -L user.txt -P dict.txt 192.168.1.101 ssh -s 65345 -e nsr

```

![](https://i0.wp.com/1.bp.blogspot.com/-Hc3jJR6tjhs/Xd_ReWvlp6I/AAAAAAAAhtA/58IR_YmNECALTavbSQ1eIFGxdcPIpWauQCLcBGAsYHQ/s1600/5.png?w=687&ssl=1)

Agora que temos as credenciais de login para o SSH, decidimos fazer o login e dar uma olhada. Executamos o comando sudo -l para verificar a lista de sudoers e descobrimos que o comando cp, que funciona como usuário sarang, sem nenhuma senha, pode ser usado. Então, decidimos dar uma olhada no usuário sarang. No diretório inicial do sarang, vemos um diretório oculto chamado ".ssh". Tentamos abrir, mas estava restrito.

```
ssh pinak@192.168.101 -p 65345
sudo -l
cd /home/sarang
ls -la
cd .ssh
```

![](https://i1.wp.com/1.bp.blogspot.com/-UvGb7B1z6WA/Xd_RerRGjHI/AAAAAAAAhtE/sYVQwlHmceg2kMsaAfwbWQlqhogd1EwtACLcBGAsYHQ/s1600/6.png?w=687&ssl=1)

Decidimos usar o comando cp para entrar no usuário sarang. Para fazer isso, precisaremos que as chaves ssh estejam presentes no diretório .ssh dentro do diretório inicial do usuário sarang. Agora, embora o arquivo esteja restrito à leitura, podemos usar o comando cp para enviar as chaves dentro desse diretório. Para fazer isso primeiro, precisamos gerar essas chaves. Usaremos o ssh-keygen para esse fim específico. Depois de trabalhar com ssh-keygen, passamos para o diretório .ssh dentro do diretório inicial do usuário pinak para encontrar a chave pública id_rsa. Demos permissões apropriadas. E mova-o para o diretório inicial do usuário pinak, como mostra a imagem fornecida.

```
ssh-keygen
cd .ssh
ls
chmod 777 id_rsa.pub
cp id_rsa.pub /home/pinak
```

![](https://i1.wp.com/1.bp.blogspot.com/-5beNO_y2Hts/Xd_RfIl53ZI/AAAAAAAAhtI/jyga9pv0BcA7hBUq8dDdpkRgMWENHShLgCLcBGAsYHQ/s1600/7.png?w=687&ssl=1)

Agora que transferimos a chave pública, é hora de usar o comando cp como usuário sarang para copiar a chave pública dentro do diretório .ssh no diretório inicial do usuário sarang. Precisamos usar o sudo junto com o comando cp e fornecer o diretório de origem e o diretório de destino. Depois de fazer isso, tudo o que precisamos é logar como sarang com a chave que acabamos de transferir. Podemos ver que funciona bem. Após o login bem-sucedido como o usuário sarang, executamos o comando sudo -l novamente, pois esse usuário não é root e nosso objetivo é obter root. Vemos que o comando zip possui o direito sudo que pode ser abusado para aumentar o privilégio nesta máquina.

```
sudo -u sarang /bin/cp ./id_rsa.pub /home/sarang/.ssh/authorized_keys
ssh sarang@127.0.0.1 -i /.ssh/id_rsa -p 65345
sudo -l
```

![](https://i0.wp.com/1.bp.blogspot.com/-4wWVbk0mWaE/Xd_RfUWoRqI/AAAAAAAAhtM/jZ3E9RSUr3M-mBhv0BDZ8gJ2ZPh-kd25ACLcBGAsYHQ/s1600/8.png?w=687&ssl=1)


### Escalonamento de privilégios

Utilizamos recentemente o login através do ssh como usuário sarang. Em seguida, usamos o comando sudo para listar todos os comandos que o usuário pode executar com privilégios de root e podemos ver que o usuário pode executar comandos zip como root sem a necessidade de digitar qualquer senha.

Então, agora no processo de escalar os privilégios de "sarang" para "root". Inicialmente, criamos um arquivo 'raj' e executamos três tarefas diferentes em uma única linha de código: primeiro, compactamos o arquivo 'raj' e depois o movemos para a pasta /home/raj.zip e, por fim, descompactamos o arquivo que será exibido o shell raiz.


```
touch raj
pwd
sudo zip /tmp/raj.zip /home/sarang/raj -T --unzip-command="sh -c /bin/bash"
cd /root
ls
cat flag.txt
```

Finalmente, obtemos 'flag.txt' dentro do diretório raiz. Por isso, cumprimos nossa missão de obter o shell raiz nesta máquina Boot2Root.

![](https://i1.wp.com/1.bp.blogspot.com/-NOjCzRKtBbM/Xd_RfpoUxmI/AAAAAAAAhtQ/5nDzwxmnbkk8uHpqZKnvOo28Ly0bR1OxwCLcBGAsYHQ/s1600/9.png?w=687&ssl=1)

Autor: Pavandeep Singh  é um escritor técnico, pesquisador e Penetration Tester Contactar  [aqui](https://www.linkedin.com/in/pavandeep-singh-6b1074132)

--- 

[ORIGINAL](https://www.hackingarticles.in/ha-dhanush-vulnhub-walkthrough/)
