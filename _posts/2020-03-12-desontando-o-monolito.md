---
layout: post
title:  "Desmontando o Monolito"
date:   2020-03-12 17:59:38 -0200
categories: jekyll update
---

Nós completamos recentemente um projeto de um ano para migrar o tráfego na web US Groupon a partir de uma aplicação monolítica Ruby on Rails para uma nova pilha Node.js com resultados substanciais.

Todo o frontend da web do Groupon nos EUA tem sido uma única base de código Rails desde seu início. A base de código do front-end cresceu rapidamente, o que dificultou a manutenção e desafiou o envio de novos recursos. Como solução para esse monólito gigantesco, decidimos redesenhar o frontend dividindo-o em peças pequenas, independentes e mais gerenciáveis. No centro deste projeto, reconstruímos cada seção principal do site como um aplicativo Node.js independente. Também reconstruímos a infraestrutura para fazer todos os aplicativos independentes funcionarem juntos. O resultado foi o nível de interação (I-Tier).

Alguns dos destaques desta grande migração de arquitetura incluem o seguinte:
