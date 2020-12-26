---
layout: post
title:  "Por que você deve usar um projeto de banco de dados SSDT para seu data warehouse"
date:   2020-03-16 17:59:38 -0200
categories: jekyll update
---

Neste post, tentarei convencê-lo de que usar projetos de banco de dados SSDT (SQL Server Data Tools) é realmente uma boa ideia. Recentemente, durante um projeto, tenho defendido que realmente vale a pena o esforço. Como sou um arquiteto de BI, estou estruturando esta conversa em torno de um data warehouse, mas certamente se aplica a qualquer tipo de banco de dados. 

## O que é um projeto de banco de dados no SQL Server Data Tools (SSDT)?

Um data warehouse contém vários objetos de banco de dados, como tabelas, visualizações, procedimentos armazenados, funções e assim por diante. Estamos muito acostumados a usar projetos SSDT BI (anteriormente BIDS) para SSIS (Integration Services), SSAS (Analysis Services) e SSRS (Reporting Services). No entanto, é menos comum usar SSDT para armazenar o DDL (linguagem de definição de dados) para objetos de banco de dados.

![](https://github.com/marcialwushu/Jekyll-Blog/blob/master/_posts/data/image-asset.jpeg?raw=true)

Abaixo está um exemplo de como você poderia estruturar seu projeto de banco de dados (estou mostrando apenas algumas tabelas e visualizações nas capturas de tela para abreviar). Você não precisa estruturá-lo dessa forma, mas neste projeto ele é classificado primeiro por esquema, depois por tipo de objeto (tabela, visão, etc), então por objeto (nome da tabela e seu DDL, etc).

![](https://github.com/marcialwushu/Jekyll-Blog/blob/master/_posts/data/image-asset-1.jpeg?raw=true)

O conteúdo dos itens no projeto SSDT DB são as instruções 'Criar Tabela', as instruções 'Criar Visualização', as instruções 'Criar Esquema' e assim por diante. Isso se baseia no “desenvolvimento de banco de dados declarativo” que se concentra no estado final desejado para um objeto. Por exemplo, aqui está o início para uma visualização DimDate:

![](https://github.com/marcialwushu/Jekyll-Blog/blob/master/_posts/data/image-asset-2.jpeg?raw=true)

Como a visão DimDate reside no esquema DW, o projeto de banco de dados me faria o favor de gerar um erro se o esquema DW ainda não existisse, como segue:

![](https://github.com/marcialwushu/Jekyll-Blog/blob/master/_posts/data/image-asset-3.jpeg?raw=true)

O Team Foundation Server se integra bem com projetos de banco de dados (ou seja, para armazenar scripts para objetos de banco de dados, como tabelas, exibições e funções), Integration Services, Analysis Services e Reporting Services.

Existe um modo online e também um modo offline; Pessoalmente, sempre uso o modo offline orientado a projetos.

Agora que sabemos sobre a estrutura do que está em um projeto, vamos falar a seguir sobre como gerenciamos as mudanças, como uma alteração para adicionar uma nova coluna.

## Gerenciando alterações em objetos de banco de dados

A próxima grande coisa a saber é que existe um mecanismo para gerenciar mudanças DDL, por exemplo, uma nova coluna ou uma mudança em um tipo de dados. Em vez de colocar uma instrução 'Alterar Tabela' no projeto de banco de dados, você edita a instrução 'Criar Tabela' original que se concentra no estado final que inclui a nova coluna.

Agora, digamos que você esteja pronto para promover essa nova coluna para Dev, QA ou Produção. É aqui que fica divertido. No projeto de banco de dados, você pode fazer uma operação de 'Comparação de esquema' que irá comparar os objetos de banco de dados entre o projeto e o banco de dados. Ele detectará a diferença e criará o script do script 'Alterar Tabela' necessário para usar em sua implantação na Produção.

![](https://github.com/marcialwushu/Jekyll-Blog/blob/master/_posts/data/image-asset-4.jpeg?raw=true)

A saída acima nos diz que há uma diferença de tipo de dados entre o projeto e o banco de dados para uma coluna de endereço. Isso nos ajuda a reconciliar as diferenças, então podemos gerar um script que teria uma instrução Alter Table para a coluna de endereço (embora, no caso acima, o endereço seja varchar (150) no banco de dados, o que provavelmente significa que o desenvolvedor ETL ampliou a coluna mas esqueci de voltar ao projeto de banco de dados - então ainda há muito julgamento ao comparar o projeto ao Dev).

Vamos dar um passo adiante. Quando estivermos prontos para promover para um novo ambiente, podemos fazer uma comparação de esquema entre Dev e QA, ou QA e Prod, e gerar um script que conterá todos os Cria e Altera que precisamos para sincronizar os ambientes . Se você está imaginando como isso é útil para fins de implantação, então já cumpri minha missão. (Continue lendo mesmo assim!)

Há muito mais a saber sobre como usar a comparação de esquema, mas vamos ver os benefícios de usar um projeto de banco de dados SSDT.

## Benefícios de usar um projeto de banco de dados nas ferramentas de dados do SQL Server (SSDT)

Os projetos de banco de dados têm os seguintes benefícios:

- Fácil disponibilidade de DDL para todos os objetos (tabelas, visualizações, procedimentos armazenados, funções, etc.) sem ter que fazer o script do servidor e / ou restaurar um backup. (Veja os benefícios adicionais na próxima lista se você também integrar com o controle de origem, o que é altamente recomendado.)
- Funcionalidade para criar scripts de diferenças de comparação de esquema para fins de implantação entre servidores. Se você já migrou uma alteração de pacote SSIS e depois deu um erro porque se esqueceu de implantar a alteração de tabela correspondente, você apreciará a funcionalidade de comparação de esquema (se você usá-la antes de todas as implantações).
- Excelente local para documentação de um banco de dados, que é mais fácil de ver do que em propriedades estendidas. Por exemplo, recentemente adicionei um comentário no topo da minha tabela DDL que explica por que não há uma restrição exclusiva para a tabela.
- Fornece um local para instruções DML (linguagem de manipulação de dados) relevantes também, como as linhas de membro desconhecido para uma tabela de dimensão. Nota: as instruções DML precisam ser excluídas da construção porque o projeto de banco de dados realmente só entende DDL.
- Instantâneo de DDL em um ponto no tempo. Se desejar, você pode gerar um instantâneo do DDL a partir de um ponto no tempo, como uma versão principal. 

Benefícios adicionais * se * você estiver usando um projeto de banco de dados também em conjunto com o controle de origem, como TFS:

- Controle de versão de alterações feitas ao longo do tempo, com a capacidade de reverter rapidamente para uma versão anterior se ocorreu um erro ou de recuperar um objeto excluído. Comentários úteis devem ser obrigatórios para todos os desenvolvedores que estão verificando as alterações, o que fornece um excelente histórico de quem, quando e por que uma alteração foi feita. As alterações também podem ser integradas opcionalmente aos processos de gerenciamento de projetos (por exemplo: associar um item de trabalho do plano do projeto ao conjunto de alterações verificado).
- Comunica-se à equipe (por meio de check-outs) que está trabalhando ativamente, o que melhora a eficácia da equipe e o impacto potencial nos itens de banco de dados relacionados.

## Dicas e sugestões para usar um projeto de banco de dados SSDT

Use sintaxe embutida. Para ser realmente eficaz para a tabela DDL, acho que realmente requer trabalhar -de- o projeto DB -para- o banco de dados, que é uma mudança de hábito se você está acostumado a trabalhar diretamente no SSMS (Management Studio). Para ser justo, ainda trabalho no SSMS o tempo todo, mas tenho o SSMS e o SSDT abertos ao mesmo tempo e não deixo o SSDT ficar obsoleto. O motivo pelo qual considero isso tão importante está relacionado à sintaxe embutida - se você acabar querendo gerar DDL a partir do SSMS para "recuperar" seu projeto de banco de dados, nem sempre será tão limpo quanto você deseja. Tome o seguinte, por exemplo:

![](https://github.com/marcialwushu/Jekyll-Blog/blob/master/_posts/data/image-asset-5.jpeg?raw=true)

No script acima eu tenho algumas restrições padrão (que são nomeadas porque quem quer os nomes de restrição geradas pelo banco de dados feios para nossos padrões e nossas chaves estrangeiras e tal, certo?!?). As restrições são todas embutidas - fáceis de ler. Se você fosse criar o script da tabela mostrada acima do SSMS, ele geraria instruções Alter Table para cada uma das restrições. Exceto para tabelas muito pequenas, torna-se impossível validar que o DDL é exatamente como você deseja que seja. Portanto, sugiro usar a sintaxe embutida para que as instruções SQL do seu projeto de banco de dados sejam todas claras e fáceis de ler.

**Armazene DML relevante no projeto (Build = None)**.  Se você tiver algumas instruções DML (linguagem de manipulação de dados) que são mantidas manualmente e precisam ser promovidas para outro ambiente, isso as torna uma excelente candidata para serem armazenadas no projeto de banco de dados. Como o projeto de banco de dados só entende DDL quando constrói o projeto, a propriedade 'Build' para cada script DML SQL precisará ser definida como Nenhum para evitar erros. Alguns exemplos:

![](https://github.com/marcialwushu/Jekyll-Blog/blob/master/_posts/data/image-asset-6.jpeg?raw=true)

**Construa o projeto com freqüência**. Você será impopular entre seus colegas de trabalho se verificar algo que não funciona. Então você vai querer desenvolver o hábito de fazer uma compilação com frequência (cerca de uma vez por dia se você estiver alterando ativamente os objetos de banco de dados), e sempre logo depois de fazer o check-in. Você pode encontrar as opções de compilação se clicar com o botão direito do mouse no projeto no Solution Explorer. Às vezes, você vai querer escolher Rebuild porque então validará todos os objetos na solução, independentemente de terem sido alterados ou não (enquanto a opção Build apenas cria objetos que detecta alterados, portanto, embora Rebuild demore mais, é mais completo).

![](https://github.com/marcialwushu/Jekyll-Blog/blob/master/_posts/data/image-asset-7.jpeg?raw=true)

Mais uma dica a respeito da construção - se uma operação de comparação de esquema achar que existe uma tabela no banco de dados, mas não no projeto, verifique a propriedade de construção. Se for definido como Nenhum para um objeto DDL real, ele será acidentalmente ignorado na operação de comparação de esquema. Resumindo: defina todos os objetos DDL para construir e qualquer DML relevante para não construir.

**Faça uma comparação de esquema com freqüência**. Executar regularmente uma comparação de esquema é um bom hábito para que não haja um grande esforço de limpeza logo antes da hora de implantar em outro ambiente. Digamos que eu seja responsável por criar uma nova dimensão. Assim que o pacote SSIS for concluído com o DDL para a tabela e visualizações conforme apropriado, farei uma comparação de esquema para garantir que peguei tudo. Se sua equipe for uma máquina bem lubrificada, se você vir algo na comparação de esquema entre o projeto e o Dev DB, deve ser algo em que você ou um colega de trabalho esteja trabalhando ativamente.

**Salve as configurações de comparação de esquema (SCMP) em seu projeto**.  Para torná-lo rápido e fácil de usar (e mais provavelmente toda a sua equipe vai aderir a ele), gosto de salvar as configurações de comparação de esquema diretamente no projeto. Você pode ter vários SCMPs salvos: Projeto para Dev DB, Dev DB para QA DB, QA DB para Prod DB e assim por diante. É uma grande economia de tempo porque você deseja dizer ao esquema compare para ignorar coisas como usuários, permissões e funções, porque quase sempre eles diferem entre os ambientes. Ao salvar o SCMP, você pode evitar a tediosa desmarcação desses itens toda vez que gerar a comparação.

![](https://github.com/marcialwushu/Jekyll-Blog/blob/master/_posts/data/SSDT_schemacompare2.jpg?raw=true)

**Faça um 'Gerar Script' para a Comparação de Esquema; Não use rotineiramente o botão Atualizar**.  Logo à direita do botão Atualizar (que eu gostaria que fosse menos proeminente) está o botão Gerar Script. Isso criará as instruções Create e Alter relevantes que ele detecta como necessárias com base nas diferenças encontradas. O script permite que você valide o script antes de ser executado e salve o histórico de exatamente quais mudanças estão sendo implementadas quando (assumindo que está sendo feito manualmente e você não está fazendo implementações contínuas automatizadas para Prod). Também prefiro gerar o script em vez de deixar o SSDT fazer uma publicação direta porque os itens que foram retirados ainda fazem parte de uma publicação e normalmente não queremos isso (embora dependa de como você lida com a ramificação do controle de origem). 

![](https://github.com/marcialwushu/Jekyll-Blog/blob/master/_posts/data/image-asset-8.jpeg?raw=true)

Já que estamos falando sobre os scripts gerados pelo projeto DB: algumas coisas a saber. Primeiro, você precisará executar o script no modo SQLCMD (no SSMS, ele se encontra no menu Consulta). Em segundo lugar, os scripts nem sempre são perfeitos. Para mudanças simples, eles funcionam muito bem, mas às vezes as coisas ficam complicadas e você precisa 'manipulá-las'. Por exemplo,  pode haver dados em uma tabela e o script tem uma instrução de verificação no início que evita qualquer alteração e pode precisar ser removido ou tratado de forma diferente.

**Instalação separada para SSDT vs SSDT-BI anterior ao SQL Server 2016**. Se você for criar um novo projeto em SSDT e não vir o Projeto de banco de dados do SQL Server como uma opção, isso significa que você não tem o 'sabor' certo de SSDT instalado ainda. Felizmente, as ferramentas estão sendo unificadas no SQL Server 2016, mas antes disso, você precisará fazer uma instalação separada. Os arquivos de instalação SSDT para Visual Studio 2013 podem ser encontrados aqui:  <https://msdn.microsoft.com/en-us/library/mt204009.aspx>.

Há muito mais para saber sobre projetos de banco de dados em SSDT, mas vou encerrar com esta introdução. Há uma curva de aprendizado e algumas mudanças de hábito, mas espero ter incentivado você a experimentar os projetos de banco de dados.

## Encontrar mais informações

- Blog de Jamie Thomson - [10 dias de SSDT](http://sqlblog.com/blogs/jamie_thomson/archive/tags/10+days+of+SSDT/default.aspx)
- Blog de Jamie Thomson - [Considerações ao iniciar um novo projeto SSDT](http://sqlblog.com/blogs/jamie_thomson/archive/2013/03/21/considerations-when-starting-a-new-ssdt-database-project.aspx)
- MSDN - [Desenvolvimento de banco de dados offline orientado a projetos](https://msdn.microsoft.com/en-us/library/hh272702(v=vs.103).aspx)

---

[Artigo Original](https://www.sqlchick.com/entries/2016/1/10/why-you-should-use-a-ssdt-database-project-for-your-data-warehouse)



