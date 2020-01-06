---
layout: post
title:  "Apresentando o AltStore"
date:   2019-12-18 17:59:38 -0200
categories: jekyll update
---

Por: Riley Testut

Sinceramente, não acredito que finalmente estou escrevendo sobre tudo isso. Tudo neste post é algo em que tenho trabalhado de uma forma ou de outra nos últimos anos. No entanto, para garantir que eu não me desse um tiro no pé revelando demais, não me permiti falar sobre nada além de Delta durante todo o processo. Mas agora, finalmente, é hora de revelar o outro. grande projeto em que trabalho: [AltStore](https://altstore.io/)

![](https://user-images.githubusercontent.com/705880/65605569-30ca6080-df5e-11e9-8dfb-15ebb00e10cb.PNG)

Então, o que é o AltStore? O AltStore é uma loja de aplicativos alternativa para dispositivos sem jailbreak . Ao contrário de outras lojas de aplicativos não oficiais hoje em dia, o AltStore não depende de certificados corporativos, que a Apple vem reprimindo mais e mais recentemente. Em vez disso, conta com um recurso de desenvolvedor menos conhecido que permite que você use seu Apple ID para instalar aplicativos que você mesmo desenvolveu com o Xcode, o kit de ferramentas de desenvolvimento da Apple. Isso é destinado a pessoas que, de outra forma, poderiam não conseguir comprar uma conta de desenvolvedor de US $ 99 / ano (como estudantes) - mas, como se vê, não há motivo técnico para isso se limitar a apenas aplicativos instalados no Xcode.

O AltStore é um aplicativo iOS totalmente nativo e em área restrita que permite que você carregue de lado os aplicativos, basicamente "enganando" o telefone para pensar que está instalando aplicativos que você mesmo criou, quando na verdade eles podem ser quaisquer aplicativos. Como esse é um método de instalação realmente suportado pela Apple, é muito menos frágil do que outros métodos de distribuição no passado (como nosso velho amigo, o Date Trick, para instalar o GBA4iOS 💜). Da mesma forma, como não há um único certificado corporativo a ser revogado (porque tecnicamente todos os usuários agora têm seu próprio certificado de desenvolvedor usando esse processo), a Apple não pode simplesmente desligá-lo pressionando um botão, como acontece com algumas lojas de aplicativos de terceiros ( até que recebam um novo certificado dentro de uma semana, é claro).

Para esse método de distribuição, o AltStore exige seu ID e senha da Apple para se comunicar em seu nome com os servidores de desenvolvedor da Apple. Fiz todo o possível para garantir que essas credenciais sejam tratadas corretamente (ou seja, nunca são enviadas para nenhum servidor de terceiros, são enviadas diretamente para a Apple para autenticação e armazenadas com segurança no chaveiro do dispositivo para que nada mais possa recuperá-lo), mas como não importa qual ID Apple é fornecido, você pode criar contas descartáveis, se desejar. Depois que o AltStore configura sua conta para você, o AltStore "renuncia" (ou como eu o chamo no AltStore, "atualiza") o aplicativo com seu ID Apple para garantir que todas as verificações normais de segurança do iOS sejam aprovadas e tratem o aplicativo como se fosse um aplicativo você se construiu.

No entanto, esse método certamente não ficou isento de desafios; A Apple impôs várias restrições para esse método de distribuição para impedir exatamente esse caso de uso, o que (eles esperavam) limitaria severamente o que as pessoas poderiam fazer com ele. Acontece que essas restrições são exatamente o que eu tenho tentado solucionar nos últimos anos e estou muito feliz com os resultados.

## AltServer

Ao contrário dos aplicativos distribuídos com uma conta paga de desenvolvedor da Apple, você não pode instalar aplicativos distribuídos com um ID Apple gratuito por via aérea. Isso significa que, embora possamos preparar aplicativos para instalação a partir do aplicativo AltStore, infelizmente não há como realmente instalar aplicativos diretamente do dispositivo iOS. No entanto, como se vê, essa restrição não se aplica à instalação de aplicativos via sincronização Wi-Fi do iTunes, que é onde o AltServer entra.

O AltServer é um aplicativo complementar de desktop para macOS / Windows que não faz nada além de ser executado silenciosamente em segundo plano, escutando as conexões recebidas do AltStore. Quando uma conexão é formada, o AltStore envia um aplicativo renunciado / atualizado ao AltServer por WiFi, que usa a mesma infraestrutura de sincronização do iTunes WiFi subjacente que a Apple para instalar o aplicativo sem fio no dispositivo.

Como (obviamente) não existe o AltStore no dispositivo para instalar o AltStore, o AltServer também é responsável pela instalação inicial do AltStore no dispositivo. Depois de instalar o AltStore, no entanto, você pode fazer tudo o mais a partir do próprio aplicativo (desde que esteja na mesma rede Wi-Fi que o AltServer e a sincronização Wi-Fi do iTunes estão ativadas).  

## Atualizando aplicativos

Todos os aplicativos assinados com um ID Apple gratuito são válidos apenas por 7 dias, quando expiram e não podem mais ser iniciados. Para compensar isso, o AltStore atualizará periodicamente todos os aplicativos instalados em segundo plano ou, alternativamente, você poderá atualizar manualmente os aplicativos no AltStore. Uma vez atualizados, eles não expirarão por mais uma semana.

No momento, isso está usando a API de busca em segundo plano do iOS existente, que permite que um aplicativo seja executado em breves rajadas em segundo plano, a critério do sistema. Infelizmente, não há muito mais controle além disso, e é aleatório se o sistema escolhe um horário em que o dispositivo está conectado ao mesmo WiFi do AltServer. No entanto, quanto mais você usar o AltStore, mais frequentemente o iOS tentará atualizar os aplicativos em segundo plano. Desde que você abra o aplicativo de vez em quando, o AltStore e o AltServer poderão se encontrar pelo menos uma vezao longo da semana. Ainda melhor, o iOS 13 introduziu novas APIs de segundo plano muito melhores para este caso de uso, e pretendo usá-las o mais rápido possível. Imagine um atalho para atualizar seus aplicativos que são executados automaticamente em segundo plano sempre que você se conectar ao seu WiFi doméstico……

## Instalando mais de 3 aplicativos

A última grande restrição é que um dispositivo iOS só pode ter no máximo 3 aplicativos instalados usando esse método, mesmo que sejam provenientes de diferentes IDs da Apple. Essa foi de longe a mais frustrante de se lidar, mas felizmente consegui encontrar uma solução alternativa a tempo. Sempre que um aplicativo é instalado usando esse método, seu “perfil de provisionamento” também é armazenado no dispositivo ao lado de outros perfis de provisionamento de outros aplicativos em um local separado. Na verdade, o iOS não verifica a presença de aplicativos para ver se você excedeu seu limite, mas verifica a presença desses perfis de provisionamento.

Embora não haja nada que eu possa fazer sobre isso no próprio dispositivo iOS, pois a mesma infraestrutura de sincronização subjacente do iTunes (WiFi) que estou usando permite instalar e remover perfis de provisionamento dos dispositivos (já que o Xcode também requer essa capacidade de gerenciar perfis para desenvolvedores). Antes de instalar um aplicativo, removo todos os perfis existentes no dispositivo para parecer que não existem outros aplicativos instalados no sistema e, depois que o aplicativo é instalado, reinstalo todos os perfis. É muito simples, mas funciona.

## Quais aplicativos estão disponíveis?

Desde o início, o AltStore pretendia servir como uma maneira para os desenvolvedores distribuírem aplicativos totalmente novos que ultrapassam os limites do iOS de maneiras que não são possíveis com o sistema de revisão de aplicativos da Apple. O AltStore será iniciado inicialmente com dois dos meus aplicativos: Delta , meu emulador multifuncional em que trabalho nos últimos 4 anos, além do Clip , um aplicativo simples de gerenciamento de área de transferência.

É claro que o Delta não é permitido na App Store devido à posição da Apple emular, mas por que criar um gerente de área de transferência quando tantos já existem na App Store? Simples: não existe uma maneira aprovada pela App Store para que os aplicativos sejam executados continuamente em segundo plano, o que significa que você precisa se lembrar de abrir manualmente esses aplicativos para salvar seu histórico. No entanto, como não preciso aderir à revisão de aplicativos, posso ser um pouco mais ... criativo. Tecnicamente, os aplicativos de mídia podem ser executados indefinidamente em segundo plano, para que o usuário possa continuar ouvindo música enquanto executa outras tarefas. O Clip tira vantagem disso ao reproduzir áudio silencioso em loop enquanto em segundo plano, mas de uma maneira que não afeta o que mais você estiver ouvindo no telefone ao mesmo tempo. Isso permite que o Clip monitore constantemente a área de transferência do dispositivo,

Após o lançamento, e depois de verificar que poderei acompanhar a demanda, começarei a trabalhar na capacidade de qualquer pessoa listar seus próprios aplicativos no AltStore, semelhante ao Cydia (mas de uma maneira mais amigável) caminho!). É aí que entra o verdadeiro poder do AltStore, e é com isso que estou definitivamente mais animado 🎉

## Quando posso começar a usar o AltStore‽

Delta, Clip e AltStore estão todos lançando oficialmente neste sábado, 28 de setembro. No entanto, como quero garantir que o lançamento ocorra da maneira mais tranquila possível, estou lançando uma pré-visualização do AltStore que você pode baixar agora, para que eu possa resolver qualquer questões restantes. Se você quiser ajudar, [acesse o site oficial da AltStore e siga as instruções](https://altstore.io/).

Para oferecer a todos algo para baixar e testar tudo, [revivi o Delta Lite, meu Swift Playground](http://rileytestut.com/blog/2018/06/21/introducing-delta-lite/) como um aplicativo iOS nativo. Então, faça o download do Delta Lite e me ajude a testar tudo revivendo alguns jogos divertidos da NES! Com sua ajuda, posso me preparar melhor para o grande dia em pouco mais de 72 horas 🙏

## Ótimo, a Delta finalmente chegou! O que vem depois?

Bem, tenho muitas idéias para AltStore, Delta e Clip, e agora que construí essa base, será muito mais fácil criar rapidamente sobre ela. No entanto, há apenas um problema: eu tenho tentado descobrir como posso me apoiar trabalhando no AltStore, Delta, Clip e em qualquer outro aplicativo que eu possa criar. Durante quase todo o desenvolvimento da Delta, eu me apoiei trabalhando em vários trabalhos freelancers e depois gastando o tempo livre em meus próprios aplicativos. Isso funciona, mas significa que não posso investir tanto tempo quanto gostaria nos meus aplicativos, o que, por sua vez, leva muito mais tempo para finalizá-los (consulte: período de desenvolvimento de quase 5 anos para a Delta).

Já recebi muitas pessoas me perguntando ao longo dos anos se havia uma maneira oficial de apoiar meu trabalho que [finalmente decidi experimentar o Patreon](https://patreon.com/rileytestut) . Ainda estou planejando o freelancer para me sustentar, mas a esperança é que o Patreon subsidie ​​a quantia de dinheiro que preciso ganhar com o freelancer, me liberando mais para trabalhar em meus próprios aplicativos. Em troca de se tornar um patrocinador, você poderá fazer o download das versões beta dos meus aplicativos , que serão listadas e instaladas no AltStore como as versões não beta (mas identificadas com o emblema "Beta"). Dessa forma, AltStore, Delta e Clip podem permanecer livres para todos, mas quem doa apenas obtém acesso aos novos recursos mais cedo.

Inicialmente, o AltStore será lançado com estes betas para clientes:

## AltStore Beta - Aplicativos de carregamento lateral

Este recurso permite que você use AltStore instalar quaisquer aplicativos - e não apenas os enumerados no AltStore - e tê-los ser atualizado em segundo plano como um aplicativo AltStore. Atualmente, ele funciona para a maioria dos aplicativos, mas os aplicativos um pouco mais complexos (como aqueles com determinadas extensões de aplicativo) podem falhar. Minha prioridade após o lançamento é fazer com que esse recurso de carregamento lateral trabalhe com o máximo de aplicativos possível, antes de adicionar suporte para listagens de aplicativos de terceiros diretamente no AltStore.

## Delta Beta - Suporte para Nintendo DS

Surpresa, o suporte do Nintendo DS está chegando à Delta depois de tudo 🎉 O suporte inicial para jogos do DS estará disponível no lançamento na versão beta do Delta, incluindo suporte para jogos salvos, estados salvos e Hold Button. Como ainda está na versão beta, ainda não adicionei suporte aos recursos restantes, como Fast Forward e cheats, mas espero adicioná-los mais cedo ou mais tarde após o lançamento (porque também os quero para mim!).

## Delta Lite Beta - Suporte para Gameboy Color

Além do Delta Lite, também haverá uma versão "beta" que suporta jogos NES e jogos GBC . É assim que as pessoas que doam no Patreon durante a pré-visualização recebem algo especial, em vez de esperar alguns dias para receber a versão beta do Delta.

Então, sim, se você quiser me ajudar a trabalhar nesses aplicativos como meu emprego em período integral, espero que você tenha acesso antecipado ao que estiver trabalhando working

## Um grande encerramento

Ok, eu sei que isso era muito, então aqui está uma versão resumida com o que você precisa saber:

- O método de distribuição da Delta é o AltStore, uma loja de aplicativos alternativa para dispositivos sem jailbreak.
- O AltStore usa seu próprio ID Apple para preparar aplicativos para instalação, não alguns certificados corporativos (possivelmente roubados) que podem ser revogados.
- O AltStore usa um aplicativo de desktop AltServer para instalar aplicativos de volta ao telefone usando o iTunes WiFi Sync.
- O AltStore atualiza os aplicativos para você em segundo plano, para que você nunca precise atualizá-los manualmente ou se preocupar com o vencimento.
- Você pode instalar mais de 3 aplicativos com o AltStore.
- AltStore, Delta e Clip estão sendo lançados simultaneamente neste sábado, 28 de setembro .
- Visualização do AltStore disponível para download no momento.
- Você pode receber acesso às versões beta do AltStore, Delta e muito mais, apoiando-me no Patreon .
- A versão beta do AltStore inclui a capacidade de carregar qualquer aplicativo (arquivo .ipa).
- A versão beta do Delta inclui suporte para jogos do Nintendo DS.

E eu acho ... isso é tudo que eu tenho mantido em segredo nos últimos anos. Fique atento à medida que continuo adicionando recursos ao AltStore, Delta e Clip, e em breve abra o AltStore para que qualquer pessoa possa fazer parte dele. O iOS é uma plataforma tremenda, mas definitivamente existem oportunidades perdidas para criar aplicativos incríveis . Meu sonho é que a AltStore promova um ecossistema de aplicativos iOS totalmente novo, determinado a levar a plataforma a seus limites, e estou comprometido em tornar isso uma realidade com toda a sua ajuda 💜

---

Autor: Riley Testut

[Artigo Original](http://rileytestut.com/blog/2019/09/25/introducing-altstore/)
