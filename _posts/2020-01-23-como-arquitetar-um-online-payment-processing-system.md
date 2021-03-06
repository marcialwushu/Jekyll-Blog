---
layout: post
title:  "Como arquitetar um Online Payment Processing System para uma loja online?"
date:   2020-01-23 17:59:38 -0200
categories: jekyll update
---


![](https://trello-attachments.s3.amazonaws.com/5d7e8031eaec3e42c24aade0/5e4309c7705ce8308002aba4/509805f525f8ef2122d758e7606929d1/1_D-oiAFXjZb6p79BRUpbnGw.jpeg)


Olá!


Portanto, se você decidiu desenvolver um sistema de pagamentos on-line para o seu comércio eletrônico, aconselho você a ler este pequeno artigo.

## Quais aspectos devo considerar antes de criar o Sistema de processamento de pagamentos?

1. **PCI DSS para processamento de cartão de crédito (CC)**, que significa Padrão de segurança de dados do setor de cartões de pagamento que possui 12 regras que impõem algum nível de segurança para proteger as informações do cartão de crédito, mas podem ser aplicadas a qualquer informação pessoal identificável. Para processar cartões de crédito, você pode estar sujeito à auditoria e certificação do PCI DSS, o que pode implicar grandes custos ou responsabilidades pessoais.
2. **Segurança e criptografia**. Esse aspecto está intimamente relacionado ao PCI DSS, que aplica vários processos ao seu processo de desenvolvimento de software. No entanto, você não precisa processar cartões de crédito para se preocupar com a segurança, mas a segurança deve ser muito importante para sua equipe e para todos os membros da equipe, porque é muito difícil ganhar confiança e super fácil de se perder.
3. **Geografia** . Esse é um assunto muito importante, do qual dependerá a lista de métodos de pagamento que você deve aceitar, quais localizações e culturas devem ser suportadas, onde seus servidores devem estar e com que rapidez eles devem executar.
4. **Tráfego e escalabilidade** . Os requisitos de software, bem como o processamento de pagamentos, diferem dependendo da escala do seu sistema. Se você realizar algumas vendas por dia, poderá terceirizar 100% o Processamento de pagamentos para um provedor de serviços de pagamento (também conhecido como Stripe), mas se precisar processar milhões ou bilhões por ano, a arquitetura do sistema e a quantidade de parceiros serão diferentes. a complexidade disparará comparativamente ao caso básico.
5. **Códigos da MCC Ou o setor em que você atua**. Dependendo do setor em que sua empresa atua, sua arquitetura pode ser dramática, o design do sistema e as implicações legais. Se você realizar o processamento de pagamentos de pôquer, jogos de azar ou adulto (18 anos ou mais), verá grandes diferenças e riscos comparativamente a uma loja de comércio eletrônico, além do conhecimento necessário e restrições e regulamentos legais.
6. **Processadores de pagamento de backup**. Se você precisar manipular tentativas e fazer backup de provedores de serviços de pagamento, poderá ser forçado a ter diferentes restrições de arquitetura e segurança.
7. **Operações e suporte ao cliente**. Pensando na arquitetura de pagamento, não se esqueça da equipe de Felicidade do cliente, bem como dos analistas de fraudes e negócios que precisam consumir e reconfigurar o sistema "durante o voo".
8. **Aquisição e fusão de negócios**. Se sua empresa possui relacionamentos pai-filho com outras empresas e eles criaram uma plataforma de processamento de pagamentos que pode ser reutilizada, você pode economizar muito tempo e dinheiro. Por outro lado, se você é um CTO de uma empresa guarda-chuva, pode precisar trabalhar em um sistema de processamento que pode ser um gateway para outras empresas do grupo.
9. **Nuvem vs Local**. Esse ponto é mais parecido com “Ser ou não ser” nos dias atuais e, antes de dizer que a nuvem não é segura ou confiável, aconselho verificar esta [página](https://aws.amazon.com/compliance/published-certifications/) . E a confiabilidade depende principalmente da engenharia que governa o sistema.
10. **Analytics**. Se você quiser ser lucrativo e melhorar com o tempo, precisará ter análises que possam influenciar drasticamente a arquitetura do sistema para ajudar sua equipe a responder a muitas perguntas. Outro ponto importante aqui é a duração do seu período de espera antes de você precisar de suas respostas (minutos x dias), que podem ter diferenças entre as abordagens OLAP ou Data Streaming.
11. **Fraude (externa ou interna)**. Sim, a fraude também pode ser interna; portanto, ao desenvolver um sistema de processamento de pagamentos, você sempre precisa pensar em violações internas e externas, negociação de dados ou problemas semelhantes. Aqui você pode empregar sistemas já baseados em regras padrão e ampliá-los com sistemas de aprendizado de máquina e revisões ad-hoc manuais.
12. **Mobile**. Se você precisa dar suporte ao Aplicativo Móvel Nativo ou não, o dispositivo móvel pode ter implicações adicionais de arquitetura e implantação. Por exemplo, você tem um aplicativo nativo, mas não pode controlar quando o usuário irá atualizá-lo; portanto, você pode ser forçado a oferecer suporte a um grande conjunto de versões e API, mas saber disso com antecedência pode ajudá-lo muito. E não esqueça que, nas AppStores, você não pode usar seu sistema de pagamento para pagar compras no aplicativo (e talvez não queira isso), que possui 30% de participação na receita, mas se você vender bens ou serviços consumidos fora de um Aplicativo que você pode optar por processar de pagamento fora do aplicativo, o que traz complexidade adicional.

Pode haver mais aspectos que você precisa considerar ao arquitetar o sistema de processamento de pagamentos, mas acredito que abordei os mais importantes.

![](https://trello-attachments.s3.amazonaws.com/5d7e8031eaec3e42c24aade0/5e4309c7705ce8308002aba4/49e51e3af577ae9eeceacdb208ba5124/1_kNCD0Jm2_Jbh9GqI25FcVg.jpeg)

>Escopo dos requisitos do PCI DSS

Deixe-me continuar com a evolução da arquitetura do Processamento de pagamentos (uma das possíveis ramificações e eu ficaria feliz em ouvir nos comentários mais versões).

## Evolução arquitetônica dos sistemas de processamento de pagamentos.

É aconselhável começar com a solução pragmática mais simples, mas sempre tenha em mente escalabilidade e crescimento futuros (desenvolva serviços isolados em proc que podem ser ainda mais dissociados/extraídos).

>Não faça isso nem terceirize o máximo possível.

1. **Não faça isso nem terceirize o máximo possível**. Eu escolheria esta solução se ela satisfaz os requisitos técnicos e de negócios. Por quê? Como o domínio Payments é complexo e regulamentado até certo ponto, o que pode consumir muito tempo e nem sempre é gratificante. A terceirização pode ser tão simples quanto redirecionar um usuário ao seu parceiro de pagamento para fazer uma transação na qual seu cliente verá a página de seleção da forma de pagamento com marca que retorna para o seu lado após a conclusão ou cancelamento da transação. Nesse caso, você precisa manipular o redirecionamento e um pouco do Estado do pagamento para não permitir duplicatas e receber notificações corretamente. Os exemplos aqui podem ser Stripe, Adyen, GlobalCollect etc., no entanto, normalmente as empresas de Processamento de pagamentos cobram taxas adicionais apenas pela página da marca na parte superior do processamento e outras taxas.**Portanto, se você acabou de iniciar seu negócio, a terceirização de 100% do processamento de pagamentos é a melhor opção, ou eu diria que é a ÚNICA opção responsável**.
2. **Processe tudo sozinho, mas terceirize cartões de crédito**. Quando você cresce, pode precisar / desejar / desejar mais controle sobre o processamento de pagamentos, mas ainda não deseja ou não está pronto para se preocupar com a certificação PCI DSS (mesmo nos níveis 3 e 4 para comerciantes); portanto, você pode escolher pagine a página de seleção da forma de pagamento e armazene todas as Contas de pagamento/PII (informações pessoais identificáveis), mas terceirize os formulários e o processamento dos cartões de crédito. Para este fim, soluções anteriores, você provavelmente começará com o **sistema monolítico e armazenará contas de pagamento** no banco de dados local, que faz parte do banco de dados principal. Portanto, você enfrentará alto acoplamento, mas facilidade de implantação e, até certo ponto, desenvolvimento. No entanto, mesmo tendo o sistema implantado como um monólito, eu recomendaria começar a pensar em dissociação, testabilidade e escalabilidade desde o início, porque é muito mais fácil fazer isso quando você inicia.
3. **SOA e empregar lotes**. Nesse caso, é uma evolução natural da etapa anterior, na qual você vê que algumas partes do seu sistema precisam ser dimensionadas / protegidas de forma independente. Por exemplo, você deseja prestar mais atenção à segurança das Contas de pagamento e dos dados do usuário, para extrair os serviços da Conta de pagamento e da Conta do usuário, onde pode criptografar dados e armazenados em bancos de dados separados OU colocar um HAProxy para esses serviços separadamente e implantá-los em um fazenda de back-end separada por trás da DMZ. Um benefício adicional pode ser empregar o processamento em segundo plano em lotes (ou não) para descarregar um pouco o front-end; no entanto, aqui você pode ter outros problemas que talvez não enfrentasse antes - processamento de pagamento assíncrono e complexidade. Mas se você pode começar com o Processamento de pagamento assíncrono,isso implica que seu processo de checkout é assíncrono, mas oferece enormes benefícios. Por exemplo, Amazon e PokerStars fazem isso, para que tenham tempo para lidar com escalabilidade e outros problemas.
4. **Utilize filas** para tornar seu sistema mais confiável e resistente a alterações e carregamento. Como parte desta etapa, você pode criar um design de software onde toda a comunicação, ou a maior parte, entre componentes é feita através de filas (onde a assíncrona é permitida). Por exemplo, você pode ter filas para pontuação interna de fraude, pontuação externa de fraude (também conhecida como MaxMind ou ThreadMetrics), armazenamento, notificações de outros sistemas, uma fila para cada Processador de pagamento e muitas outras partes móveis.
5. **Microsserviços e peças relacionadas**. Isso está muito na moda agora, mas tem muitos benefícios, além de desvantagens, principalmente para pagamentos. Se for bem-sucedido, pode ser muito benéfico e econômico, porém, para fazê-lo bem, é necessário considerar todos os aspectos do sistema, como: implantação, monitoramento, descoberta de serviço, confiabilidade, segurança, administração, automação etc. (I não diga que todos os sistemas acima devem esquecer esses aspectos, mas quando houve comunicação interna nessas arquiteturas, pode haver problemas de comunicação e redes fora de processo). Este artigo não é sobre Mircoservices, mas eles podem ser usados e fazem sentido apenas em grandes comerciantes ou prestadores de serviços de pagamento. Ao contrário, mesmo em empresas de médio porte, se a equipe de desenvolvimento de software tiver experiência em gerenciar Mircoservices.
6. **Implantações da Zona de Multi Disponibilidade (AZ)**. Ao processar pagamentos em todo o mundo, você precisa pensar melhor sobre a latência e a confiabilidade que podem ser alcançadas com as instalações do Multi AZ. Coloquei isso como um ponto separado apenas para destacar a complexidade, mas muito provavelmente ele será empregado a partir da arquitetura monolítica para ter maior tempo de atividade e melhorar a implantação (Vermelho-Verde-Azul). Existem muitos problemas provenientes de vários AZ, como replicação, cérebro dividido e sincronização, coleta e análise de dados, roteamento e monitoramento de tráfego e, claro, segurança.

>Os microsserviços funcionarão perfeitamente para o domínio Payments, mas adicionam muita complexidade adicional.

Em relação a outros aspectos do seu sistema, como o móvel, você precisará considerar os clientes móveis como outra interface do usuário para o seu sistema; no entanto, há uma diferença de que você não controla as versões e o ciclo de vida do cliente, portanto, pode ser necessário oferecer suporte a vários versões da sua API de pagamentos.

>Em resumo, considere o Sistema de processamento de pagamentos on-line como um sistema de software com requisitos mais altos de segurança e confiabilidade, porque literalmente todas as chamadas têm impacto financeiro direto nos resultados da sua empresa .

---

Autor: Leo Kyrpychenko

[Artigo Original](https://medium.com/get-ally/how-to-architect-online-payment-processing-system-for-an-online-store-6dc84350a39)

