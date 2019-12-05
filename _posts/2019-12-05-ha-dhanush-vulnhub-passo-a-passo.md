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


