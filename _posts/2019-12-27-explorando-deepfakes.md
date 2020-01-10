---
layout: post
title:  "Explorando o DeepFakes"
date:   2019-12-27 17:59:38 -0200
categories: jekyll update
---

![](https://trello-attachments.s3.amazonaws.com/5d7e8031eaec3e42c24aade0/5e18b20f20a8d10e1aa0bba6/9c2f3b9f91dec916462e46df6ea731dc/1_CKb1y7IC8LFcdMYj4yOdAQ.png)

Em dezembro de 2017, um usuário chamado “DeepFakes” postou vídeos explícitos com aparência realista de celebridades famosas no Reddit. Ele gerou esses vídeos falsos usando aprendizado profundo, o mais recente em IA, para inserir rostos de celebridades em filmes adultos.

Nas semanas seguintes, [a internet explodiu com artigos](https://www.economist.com/news/science-and-technology/21724370-generating-convincing-audio-and-video-fake-events-fake-news-you-aint-seen) sobre os perigos da tecnologia de troca de rostos: assediar inocentes, divulgar notícias falsas e prejudicar a credibilidade das evidências em vídeo para sempre.


>É verdade que maus atores usarão essa tecnologia para causar danos; mas, como o gênio está fora da garrafa, não devemos parar para pensar no que mais o DeepFakes poderia ser usado?

Nesta postagem, exploro os recursos dessa tecnologia, descrevo como ela funciona e discuto os aplicativos em potencial.

## Mas primeiro: o que é o DeepFakes e por que isso importa?

O DeepFakes oferece a capacidade de trocar uma face por outra em uma imagem ou vídeo. A troca de rosto é realizada em filmes há anos, mas exigia que editores de vídeo e especialistas em CGI passassem muitas horas para obter resultados decentes.

>A nova inovação é que, usando técnicas de aprendizado profundo, qualquer pessoa com uma GPU poderosa e dados de treinamento, pode criar vídeos falsos críveis.

Isso é tão notável que vou repetir: qualquer pessoa com centenas de imagens de amostra, da pessoa A e da pessoa B, pode alimentá-las em um algoritmo e produzir trocas de rosto de alta qualidade - não são necessárias habilidades de edição de vídeo.

Isso também significa que isso pode ser feito em escala e, como muitos de nós temos nossos rostos on-line, é fácil inserir quase qualquer pessoa em vídeos falsos. Assustador, mas espero que não seja só tristeza, afinal de contas, nós, como sociedade, passamos a aceitar que as fotos podem ser falsificadas facilmente.

![](https://trello-attachments.s3.amazonaws.com/5d7e8031eaec3e42c24aade0/5e18b20f20a8d10e1aa0bba6/d8c59e0a9ca006cd9480bf8a9a8cc192/1_fJGhISycAP9eoz1cQx3tlA.png)

>Gerar rostos não é novidade: em Star Wars Rogue One, uma atriz, juntamente com um pouco de magia CGI, foi usada para recriar uma jovem Carrie Fisher. Os pontos ajudaram a mapear seu rosto com precisão ( [saiba mais aqui](https://hellogiggles.com/reviews-coverage/movies/princess-leia-rogue-one-behind-the-scenes/) ). Isso não é o DeepFakes, mas esse é o tipo de coisa que o DeepFakes permite que você faça sem nenhuma habilidade.

## Explorando o que o DeepFakes é capaz

Antes de pensar em como usar essa tecnologia, eu queria saber como ela funciona e como ela é executada.

Escolhi dois apresentadores de TV populares à noite, Jimmy Fallon e John Oliver, porque posso encontrar muitos vídeos deles com poses e iluminação semelhantes - e também variação suficiente (como batalhas de sincronização labial ) para mantê-lo interessante.

![](https://trello-attachments.s3.amazonaws.com/5d7e8031eaec3e42c24aade0/5e18b20f20a8d10e1aa0bba6/1b76edb4d57ab5440eb48e57ae982545/1_FAe7GFL-Qi5l9rfUSRmGfg.png)

Felizmente para mim, há um repositório [ativo do GitHub](https://github.com/deepfakes/faceswap) que contém o código original do DeepFakes e muitas outras melhorias. É bastante simples de usar, mas o ônus ainda é de o usuário coletar e preparar dados de treinamento.

Para facilitar a experimentação, escrevi um script para trabalhar diretamente com os vídeos do YouTube. Isso torna a coleta e o pré-processamento de dados de treinamento simples e a conversão de vídeos em uma etapa. [Clique aqui para ver meu repositório do Github](https://github.com/goberoi/faceit) e ver com que facilidade geramos os vídeos abaixo (também compartilho meus pesos de modelo).

![](https://trello-attachments.s3.amazonaws.com/5d7e8031eaec3e42c24aade0/5e18b20f20a8d10e1aa0bba6/bbfed353f415b162a9b3a561f72f55ed/1_0yCuz4af30ol9Vd5DNBsUQ.png)

>Fácil: o meu script faceit.py permite que você especifique uma lista de vídeos do YouTube para cada pessoa. Em seguida, execute comandos para pré-processar (baixar vídeos do YouTube, extrair quadros, encontrar rostos), treinar e converter vídeos com áudio e opções para redimensionar, mostrar lado a lado etc.

## Resultados: Jimmy Fallon e John Oliver

Os vídeos a seguir foram gerados treinando um modelo em cerca de 15 mil imagens do rosto de cada pessoa (30 mil imagens no total). Eu tenho rostos para cada celebridade de 6 a 8 vídeos do YouTube, de 3 a 5 minutos cada, com 20 quadros por segundo por vídeo e filtrando os quadros que não têm o rosto presente. Tudo isso foi feito automaticamente - tudo o que fiz foi especificar uma lista de URLs de vídeo do YouTube.

O tempo total de treinamento foi de aproximadamente 72 horas em uma GPU NVIDIA GTX 1080 TI. O treinamento é restrito principalmente pela GPU, mas o download de vídeos e a divisão deles em quadros é vinculado à E / S e pode ser paralelo.

Observe que, embora eu tenha milhares de imagens de cada pessoa, é possível obter trocas de rosto decentes com apenas 300 imagens. Eu segui esse caminho porque extraí imagens de rosto de vídeos e é muito mais fácil escolher um punhado de vídeos como dados de treinamento do que encontrar centenas de imagens.

As imagens abaixo são de baixa resolução para manter pequeno o tamanho do arquivo GIF animado. Há um vídeo do YouTube abaixo com maior resolução e som.


![](https://giphy.com/gifs/fo23NLu9hCqAZYi4Eh/html5)


