---
layout: post
title:  "GDPR - UM GUIA PRÁTICO PARA DESENVOLVEDORES"
date:   2020-02-21 17:59:38 -0200
categories: jekyll update
---

Você provavelmente já ouviu falar sobre o GDPR. O novo regulamento europeu de proteção de dados que se aplica praticamente a todos. Especialmente se você estiver trabalhando em uma grande empresa, é mais provável que já exista um processo para obter seus sistemas em conformidade com a regulamentação.

O regulamento é basicamente uma lei que deve ser seguida em todos os países europeus (mas também se aplica a empresas de fora da UE que possuem usuários na UE). Nesse caso específico, aplica-se a empresas que não estão registradas na Europa, mas têm clientes europeus. Então, isso é a maioria das empresas. Não vou abordar ainda mais outros “12 fatos sobre o RGPD” ou “7 mitos sobre o RGPD”, pois eles geralmente são direcionados a gerentes ou pessoas jurídicas. Em vez disso, vou me concentrar no que o GDPR significa para os desenvolvedores.

Por que estou qualificado para fazer isso? Algumas razões - fui conselheiro do vice-primeiro ministro de um país da UE e, por isso, fui exposto e escrevi alguma legislação. Eu estou familiarizado com o "legalese" e como o quadro regulatório opera em geral. Eu também sou um defensor da privacidade e escrevi sobre coisas relacionadas ao GDPR no passado, ou seja, "antes que fosse legal" ( proteger dados confidenciais , o direito de ser esquecido ). E, finalmente, estou atualmente trabalhando em um projeto que (entre outras coisas) visa ajudar a cobrir alguns aspectos do GDPR (a saber, registros seguros de auditoria).

Desta vez, tentarei ser um pouco mais abrangente e abranger o máximo de aspectos do regulamento que preocupam os desenvolvedores. E embora os desenvolvedores se preocupem principalmente com a forma como os sistemas em que estão trabalhando precisam mudar, não é improvável que um gerente menos informado atinja no final da primavera, percebendo que o GDPR entrará em vigor amanhã, perguntando “o que devemos fazer para obtenha nosso sistema / site compatível ”.

Os direitos do usuário / cliente (referidos como "titular dos dados" no regulamento) que considero relevantes para os desenvolvedores são: o direito de apagar (o direito de ser esquecido / excluído do sistema), o direito a restrições de processamento (você ainda mantém os dados, mas os marca como "restritos" e não os toca sem o consentimento do usuário), o direito à portabilidade dos dados (a capacidade de exportar os dados em um formato legível por máquina), o direito à retificação (a capacidade de consertar dados pessoais), o direito de ser informado (obtendo informações legíveis por humanos, em vez de termos e condições longos), o direito de acesso (o usuário deve poder ver todos os dados que você tem sobre eles).

Além disso, os princípios básicos relevantes são: minimização de dados (não se deve coletar mais dados do que o necessário), integridade e confidencialidade (todas as medidas de segurança para proteger os dados em que você pode pensar + medidas para garantir que os dados não foram modificados inadequadamente).

