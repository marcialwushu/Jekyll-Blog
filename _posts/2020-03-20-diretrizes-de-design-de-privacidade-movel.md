---
layout: post
title:  "Diretrizes de design de privacidade para desenvolvimento de aplicativos móveis"
date:   2020-03-20 17:59:38 -0200
categories: jekyll update
---

## Índice

- [Introdução]()
- [Definições]()
- [Transparência, escolha e controle - colocando o usuário em primeiro lugar]()
- [Retenção de dados e segurança]()
- [Educação]()
- [Redes sociais e mídia social]()
- [Publicidade móvel]()
- [Localização]()
- [Crianças e adolescentes]()
- [Responsabilidade e fiscalização]()


## Introdução

### Background

O surgimento de plataformas móveis abertas e a convergência de celular e a ‘web’ criaram um celular vibrante e dinâmico ecossistema que permite aos indivíduos moldar e apresentar ricos
identidades pessoais online, conecte-se com comunidades de seus escolha e envolva-se com aplicativos e serviços inovadores.

Muito disso depende do acesso em tempo real e uso de pessoal informações que muitas vezes são transferidas globalmente entre aplicativos, dispositivos e empresas.

Embora essas habilidades sirvam como um capacitador poderoso para inovações modelos de negócios e personalização de aplicativos e serviços, eles também podem fornecer um veículo para programas maliciosos ou
acesso sub-reptício às informações pessoais de um usuário. Até aplicativos que acessam e usam informações pessoais de forma legítima pode deixar de atender às expectativas de privacidade dos usuários e prejudicar sua
confiança e confiança nas organizações e no ecossistema móvel mais amplo. Os problemas ocorrem quando os usuários não recebem informações claras e transparentes aviso de acesso de um aplicativo e uso de seu pessoal
informações, ou quando não têm a oportunidade de expressar escolha significativa e controle sobre o uso de suas informações para fins secundários e além do necessário para a operação de
um aplicativo ou serviço.

A GSMA publicou recentemente um conjunto de privacidade móvel universal princípios que descrevem a maneira como os consumidores de celular a privacidade pode ser respeitada e protegida. Essas diretrizes buscam articular esses princípios em termos funcionais para aplicativos móveis Projeto.

### Escopo

Essas diretrizes aplicam princípios de design de privacidade a aplicativos e seus serviços relacionados projetados para dispositivos móveis. Eles são destinados para se aplicar a todas as partes na aplicação ou cadeia de entrega de serviço que são responsáveis por coletar e processar as informações pessoais de um usuário informações - desenvolvedores, fabricantes de dispositivos, plataformas e sistema operacional empresas, operadoras móveis, anunciantes e empresas de análise.

### Objetivo

Aplicativos e seus serviços relacionados devem criar boa privacidade experiências e geram confiança e segurança. Chave para perceber estes objetivos é uma estrutura robusta e eficaz para a proteção de privacidade, baseada nos princípios de transparência, escolha e controle.

Essas diretrizes adotam uma abordagem de privacidade desde o design e são destinadas para ajudar a garantir que os aplicativos móveis sejam desenvolvidos de forma que respeitar e proteger a privacidade dos usuários e de seus em formação. Privacidade por Design também significa reconhecer que os usuários têm interesses de privacidade (expectativas, necessidades, desejos e preocupações) que deve ser abordado de forma proativa desde o início e não como um reflexão posterior ou um "complemento". As diretrizes encorajam o
desenvolvimento, entrega e operação de aplicativos móveis que coloque os usuários em primeiro lugar e ajude-os a compreender (no mínimo):

- quais informações pessoais um aplicativo móvel pode acessar, coletar e usar
- para que as informações serão usadas, e por que, e
- como os usuários podem exercer a escolha e o controle sobre esse uso.

Exemplos são fornecidos com cada diretriz e algumas casos de uso são apresentados em um anexo separado.

## Definições

**Consentimento ativo**: significa que o usuário tem uma oportunidade clara de concordar com um uso específico e notificado de suas informações pessoais. O consentimento ativo se aplicaria ao uso secundário não óbvio de um informações pessoais do usuário e/ou aplicativos que tenham implicações adicionais de privacidade para os usuários, como uma solicitação de aplicativo a localização de um usuário onde tais dados não são necessários para o funcionamento da aplicação. O consentimento ativo deve ser capturado em
uma forma de o consentimento não ser a opção padrão.

**Aplicativo**: onde usamos o termo 'Aplicativo' ou 'Aplicativo', nós pretendem ter um escopo amplo; pode incluir um aplicativo nativo, um aplicativo ou script em execução em um tempo de execução específico, ou um widget ou script em execução em um ambiente de navegador.

**Dados de localização**: informações que identificam a localização geográfica de o dispositivo de um usuário, que pode incluir Cell ID, GPS, Wifi ou outro menos informações granulares, como vila ou cidade.

**Informações pessoais**: Existem muitas definições legais de pessoal informações, mas em seus termos mais simples, significa informações que se relacionam a um indivíduo e que você pode usar para identificá-lo, contatar ou localize-os.

As informações pessoais podem incluir:

- dados coletados diretamente de um usuário por meio de um usuário do aplicativo interface (nome, endereço, data de nascimento)
- dados que são coletados indiretamente, como número de telefone celular, IMEI ou UDID
- dados coletados sobre o comportamento de um usuário, como dados de localização, dados de navegação na web ou os aplicativos usados que estão vinculados a um único perfil
- dados gerados pelo usuário, como listas de contatos, vídeos e fotos, mensagens, e-mails, notas e registros de chamadas.

Para ser identificado, um indivíduo não precisa ser conhecido pelo nome - um usuário podem ser identificados mesmo quando suas informações estão associadas apenas a um identificador exclusivo, como um identificador de dispositivo exclusivo.

Existem categorias de informações que podem ser consideradas "sensíveis" e que pode precisar de segurança adicional. Isso pode, por exemplo, incluem credenciais de logon, registro e detalhes financeiros e informações sobre a saúde de uma pessoa, por exemplo.

**Privacidade**: privacidade é um conceito dinâmico que pode significar diferentes coisas para pessoas diferentes. Para efeitos destas diretrizes, privacidade é definida como a capacidade dos indivíduos de saber como seus informações pessoais serão coletadas, compartilhadas e usadas, e para exercer escolha e controle sobre seu uso.

**Usuário**: o usuário final de aplicativos e serviços relacionados.

## Transparência, escolha e controle - colocando o usuário primeiro

Um aspecto fundamental para fomentar a confiança e a confiança nos aplicativos é ser abrir com os usuários e informá-los:

- quem está coletando e usando suas informações pessoais
- porque as informações pessoais estão sendo usadas
- quais informações pessoais estão sendo compartilhadas, com quem e para quem quais propósitos.

Os usuários devem ter informações suficientes para fazer uma escolha informada sobre se deve usar um aplicativo e as consequências de fazer isso. Algumas dessas informações podem ser óbvias antes que um usuário faça download ou ativa um aplicativo e, portanto, não faz divulgações adicionais sobre um aplicativo necessário.

### Em resumo:

- **Seja transparente**: diga aos usuários quem você é, o que informações pessoais de que você precisa, o que você pretendo fazer com isso e quem você pretende compartilhe com (e por quê!) - mas não sobrecarregue-os com instruções!
- **Ajude os usuários a gerenciar sua privacidade**: Torne-os ciente do padrão de privacidade de um aplicativo configurações.
- **Dê aos usuários escolhas fáceis de entender e mecanismos para gerenciar sua privacidade**: Faça é fácil, não é difícil - eles vão gostar mais de você por isso.

### Diretriz

**TCC1**

**Não acesse ou colete sub-repticiamente informação pessoal. Um aplicativo não deve secretamente acessar e coletar pessoal informações sobre usuários.**

Os usuários devem ser informados sobre o coleta e uso de seu pessoal informações antecipadamente, permitindo-lhes para tomar decisões informadas sobre usando um aplicativo ou serviço.

### Implementação

Antes que um usuário baixe ou ative um aplicação, ele ou ela deve ser apresentado com informação sobre:

- quais informações pessoais um o aplicativo acessará, coletará e usará
- quais informações pessoais serão armazenado (no dispositivo e remotamente)
- quais informações pessoais serão compartilhado, com quem será compartilhado
- e com que propósito
- quanto tempo serão as informações pessoais manteve
- quaisquer termos e condições de uso afetando a privacidade de um usuário.

Avisar o usuário e tornar esta informação fácil de descobrir e compreender. Mantê-la simples e facilitam a escolha do exercício. Permitir que o usuário rejeite a instalação ou
ativação se eles não desejarem seus informações a serem usadas conforme explicado a eles.

Garanta a usabilidade e evite o uso excessivo prompts que vão sobrecarregar o usuário. Considerar a experiência do usuário.

### Caso de uso e exemplos

Um aplicativo não deve acessar a localização de um usuário se o aplicativo não é um aplicativo de serviço baseado em localização. E se os dados de localização são secundários para o aplicativo e necessários para atender a outros objetivos comerciais, então você precisa obter o consentimento ativo de um usuário (consulte a seção ‘privacidade do local’
seção abaixo).

Um aplicativo não deve acessar e usar o contato detalhes mantidos no catálogo de endereços de um dispositivo, a menos que este seja parte da funcionalidade de aplicativos claramente explicada para do utilizador.

Transparência é a chave. Diga aos usuários quais informações você precisa e por que você precisa - mantenha sua palavra. Se você mudar de ideia posteriormente e quiser usar informações pessoais para outra finalidade que é diferente do que você disse originalmente aos usuários, então você precisará voltar a eles e contar sobre quaisquer novos usos e obtenha seu acordo.

### Diretriz

**TCC2**

**Identifique-se para os usuários**

Os usuários devem saber quem está coletando ou usando suas informações pessoais e como eles podem entrar em contato com essa entidade para mais informações ou para exercer seu
direitos

### Implementação

Antes que um usuário baixe ou ative um aplicação, ele ou ela deve ser informado a identidade de quaisquer entidades que irão coletar ou usar informações pessoais no âmbito do
aplicativo, incluindo uma empresa ou indivíduo nome e país de origem. Os usuários devem ter acesso fácil (por meio de um link ou item de menu) para resumir os detalhes de contato do organização.

### Caso de uso e exemplos

A página de destino do aplicativo é um excelente lugar para publicar principais fatos de privacidade, informações de contato e fornecer um hiperlink para uma declaração de privacidade mais detalhada. Não existe uma solução única para fornecer aos usuários informações sobre você, sua organização, seus privacidade e o que você fará com seus dados. Estar criativo e incentive os usuários a explorar a melhor forma de gerenciar sua privacidade - mas não os sobrecarregue e mantenha-o simples e fácil.

### Diretriz

**TCC3**

**Deixe os usuários exercerem seus direitos.**

Forneça aos usuários o suficiente informações para que eles possam razoavelmente deve saber como acessar e corrija qualquer informação pessoal você pode manter sobre eles.

### Implementação

Forneça um breve e genuinamente informativo declaração de privacidade explicando de forma clara e simples termos como as pessoas podem obter uma cópia de seus informações pessoais ou corrigir e atualizar informações fornecidas por eles ou mantidas por você.


### Caso de uso e exemplos

Como acima, a página de destino do aplicativo pode fornecer um lugar eficaz para fornecer aos usuários um aviso simples e claro ou direcione-os a informações mais detalhadas sobre como para exercer quaisquer direitos de privacidade.


### Diretriz

**TCC4**

**Minimize as informações que você coleta e limitar seu uso.**

Informações coletadas por um a aplicação deve ser razoável, não excessivo e usado dentro do escopo das expectativas do usuário e outras fins comerciais legítimos como notificados aos usuários.

### Implementação

Pense em quais informações pessoais você precisa e então justifica. É realmente necessário? Você é obrigado a coletá-lo, compartilhá-lo ou mantê-lo para atender a uma necessidade comercial ou obrigação legal? Um aplicativo deve acessar, coletar e usar apenas as informações mínimas exigidas:

- para fornecer, operar ou manter o inscrição
- para atender aos objetivos de negócios identificados que você disse ao usuário sobre ou para cumprir as obrigações legais.

Use informações pessoais de maneiras que os usuários fariam esperar quando eles tomaram a decisão de baixar ou ativar um aplicativo.


### Caso de uso e exemplos

Se você precisar de acesso aos dados da lista de contatos, identifique quais campos são necessários para preencher um determinado recurso do aplicativo e coletar não mais do que o campo (s) específico (s) obrigatório (s). Não use esses dados para finalidades não óbvias adicionais, a menos que o usuário tenha concordou com isso.


### Diretriz

**TCC5**

**Quando necessário, obtenha o ativo do usuário consentimento**

Às vezes, os usuários precisam dar seu consentimento ativo para o uso de seus informação pessoal.

- a) Coleta ou uso de pessoal informação não necessária para o aplicativo principal objetivo,

---

- b) Compartilhamento de informações pessoais com terceiros.

---

- c) Armazenamento de informações pessoais após o uso imediato do inscrição.

### Implementação

Na maioria dos casos, será óbvio para usuários quais serão as informações pessoais necessário para oferecer suporte a um aplicativo. Contudo, onde acesso, coleta e uso de pessoal informações não são necessárias para um aplicativo propósito principal e seria inesperado por o usuário, então os usuários devem ter uma escolha sobre se deve permitir estes secundários e usos não óbvios de suas informações. De outros situações também podem exigir consentimento ativo:

Redes sociais e mídia social, celular publicidade, localização, crianças e adolescentes (conforme detalhado nas seções abaixo). Onde for necessário obter consentimento ativo,
os usuários devem estar cientes de:

- por quanto tempo um consentimento é válido
- como eles podem gerenciar qualquer consentimento dado por eles
- as consequências da retenção ou retirando seu consentimento.

Os usuários devem ser capazes de retirar o consentimento até meios simples e eficientes, sem qualquer indevida atraso ou custo indevido.

---

Se terceiros irão coletar ou ter acesso a informações do usuário para seus próprios fins, o usuário deve ser informado o mais cedo possível oportunidade de que seus dados sejam compartilhados, indicando:

- com quem será compartilhado e para quais propósitos, e
- fornecer links para esses terceiros e seus avisos de privacidade.

Os usuários devem ter permissão para escolher se permitir esta coleta, acesso e uso por terceiros partidos.

---

Se os dados do usuário forem retidos após o uso imediato de um aplicativo, os usuários devem ser informações fornecidas sobre:

- os períodos para os quais as informações podem ser retido e por que
- como o usuário pode exercer direitos específicos sobre suas informações.


### Caso de uso e exemplos

Aplicativos que não usam localização para nenhum dos recursos ou funcionalidade de um aplicativo solicitado por um usuário não pode coletar localização para outros fins
- por exemplo, publicidade direcionada ou análises - a menos que o usuário dê seu consentimento ativo.

---

Os aplicativos não devem incluir código de terceiros que coleta e analisa informações pessoais para direcionar usuários com publicidade, sem o consentimento ativo de
o usuário.


### Diretriz

**TCC6**

**Dê aos usuários controle sobre solicitando.**

Sempre que possível, os usuários devem ter escolhas sobre como - e com que freqüência - eles são lembrados sobre recursos e funcionalidade que usa seus próprios em formação.


### Implementação

Sempre que tecnicamente possível, forneça aos usuários oportunidades para determinar como eles serão solicitado e com que frequência eles serão solicitado a tomar decisões sobre o acesso a, e uso de suas informações pessoais.

Privacidade por Design significa colocar o usuário em primeiro lugar e ajudando-os a se tornarem cientes e gerenciar as implicações de privacidade de aplicativos e serviços, de forma a aprimorar a capacidade do usuário experiência de privacidade.


### Caso de uso e exemplos

Os usuários podem ter a opção de "lembrar" de seus credenciais de logon, endereço de cobrança, endereços de e-mail, ou localização. É possível fornecer cobertor uma única vez
solicitando para cada tipo de dados ou mais granular comandos específicos do contexto.

Por exemplo, os usuários podem ter a escolha de permitindo que um aplicativo acesse a localização do dispositivo permanentemente, por um período especificado ou para selecionar ser solicitado periodicamente por e-mail, texto, aviso no aplicativo ou ícone.

### Diretriz

**TCC7**

**Sem atualizações silenciosas ('secretas').**

Os usuários devem concordar com quaisquer mudanças para um aplicativo que afeta seus privacidade.


### Implementação

Os usuários devem ser informados sobre uma mudança material para a forma como um aplicativo irá coletar ou usar seus informações pessoais, antes que tal mudança seja
implementado, para que eles possam fazer um escolha informada sobre continuar a usar o aplicativo.

O consentimento para mudanças pode ser obtido em dois maneiras:

1. Para mudanças que são essenciais para um operação contínua do aplicativo: Observe que uma mudança ocorrerá e um chance de desativar o aplicativo.
2. Para alterações que o usuário pode escolher adotar: um prompt com opções sobre se deve permitir a mudança ou continue com o anterior funcionalidade.



### Caso de uso e exemplos

Isso não impede o tipo remoto 'over the air' atualizações que são necessárias para manter o primário funcionalidade e integridade de um aplicativo ou serviço.

A diretriz se aplicaria, por exemplo, onde um aplicativo de repente desejou acessar e fazer upload de contato detalhes armazenados no dispositivo de um usuário ou localização do dispositivo dados.

# Retenção de dados e segurança

A segurança pode existir sem privacidade, mas não pode haver privacidade sem segurança. Certifique-se de que você está protegendo adequadamente o informações pessoais que um usuário confiou a você, no telefone e onde quer que armazene ou transmita informações pessoais.

Pense por que você precisa reter as informações pessoais de um usuário e quanto tempo você precisa para mantê-lo. Você pode justificar isso? Informações pessoais que são retidas indefinidamente diminuem de valor ao longo tempo, mas aumenta em custo e risco. Identifique quanto tempo um pedaço de informações pessoais continuam a ser necessárias para o seu modelo de negócios (como oposto ao desejável), e certifique-se de excluí-lo com segurança quando não for mais necessário. Definir períodos de retenção para seus dados (tão curtos quanto necessário) faz sentido para os negócios, pode ajudar a gerenciar riscos e custos, e para evitar ação regulatória ou publicidade negativa se as coisas correrem
errado (porque você o manteve por muito tempo e os dados foram comprometido).


### Diretriz

**DRS1**

**Gerenciar identificadores ativamente.**

Onde um aplicativo cria ou usa um identificador único, tome medidas para certifique-se de que o identificador está vinculado ao usuário correto do aplicativo e manter esta informação atualizada

### Implementação

Cada parte que usa identificadores é responsável para tomar medidas para:

- garantir que todos os identificadores exclusivos se apliquem apenas a um único usuário
- garantir que identificadores únicos sejam mantidos atualizados e mantido apenas pelo tempo necessário para cumprir a finalidade e os motivos dos aplicativos notificado aos usuários
- evitar que um identificador único seja associado com outro usuário, a menos que exigido por um necessidade de negócios justificada (consulte o caso de uso e
exemplos).

### Caso de uso e exemplos

As operadoras de celular podem reatribuir identificadores como MSISDN (números de celular) para outros clientes sem que o aplicativo esteja ciente disso. Se vocês capturar o MSISDN de um usuário, você deve tomar medidas para garantir que essas informações sejam precisas e atualizadas confirmando periodicamente com o usuário.

Da mesma forma, os fabricantes de dispositivos podem atribuir IDs de dispositivo (UDID). Os usuários de celular podem substituir seus telefones celulares e vendê-los para outros
indivíduos. A menos que se tome cuidado, o novo dono da o celular pode ser facilmente associado ao exclusivo Identificador de dispositivo ou outro identificador exclusivo associado com o proprietário anterior. Essa associação e a ligação pode ter consequências para o online experiências de privacidade do novo proprietário e seu uso do
dispositivo. Cada parte que coleta e usa UDIDs é
responsável por garantir que atendam a esta diretriz

### Diretriz

**DRS2**

**Mantenha os dados seguros.**

Tome as medidas adequadas para proteger informações pessoais dos usuários de divulgação ou acesso não autorizado.


### Implementação

Adote medidas técnicas e comerciais processos para prevenir o uso indevido ou corrupção de informações pessoais. Onde um aplicativo cria ou coleta informações pessoais consideradas confidenciais, como detalhes de logon, UDIDs, dispositivos móveis números, detalhes de contato, detalhes financeiros, tais as informações devem ser armazenadas e transmitidas em uma maneira segura.


### Caso de uso e exemplos

Coletar e manter certos tipos de informações quando simplesmente não é necessário, cria o risco de podem ser perdidos, roubados e mal utilizados. Se você precisar coletar, transmitir e reter informações confidenciais, como como detalhes de pagamento financeiro de um usuário ou detalhes de logon, então você deve proteger esses dados usando criptografia ou um mecanismo de hash adequado e excluí-lo quando não é mais necessário.

### Diretriz

**DRS3**

**Autentique onde a segurança exige isto.**

Autentique usuários sempre que possível usando métodos de autenticação apropriada ao risco .

### Implementação

Onde a afirmação de uma identidade do mundo real é um componente importante de um serviço, mais forte autenticação deve ser implementada, como autenticação de dois fatores usando um dispositivo móvel aparelho e UICC.

Considere o uso de CAPTCHAs e RECAPTACHAs para ajudar a diferenciar de boa-fé membros de spammers. Use ferramentas técnicas para restringir spidering e downloads em massa ou
acesso sem permissão de rede.

### Caso de uso e exemplos

### Diretriz

**DRS4**

**Defina os períodos de retenção e exclusão.**

Informações pessoais que devem ser retido deve estar sujeito a retenção e períodos de exclusão que são justificados de acordo com claramente identificado necessidades de negócios ou obrigações legais.

### Implementação

Justifique a coleta e retenção de pessoal informações de acordo com as necessidades comerciais ou obrigações legais identificadas. Defina uma política e implementá-lo em um departamento técnico e comercial nível de processo.

Uma vez que as informações pessoais não são mais necessário para atender a um negócio legítimo específico finalidade ou requisitos/obrigações legais, devem ser destruídos ou tornados anônimos.

Dados verdadeiramente anônimos podem ser retidos indefinidamente. Para tornar os dados anônimos, remova qualquer informações que poderiam ser usadas para identificar um indivíduo específico, garantindo que não seja possível para reidentificar o indivíduo e garantir que os dados não podem ser relacionados a um único, indivíduo não identificado por único identificadores.

### Caso de uso e exemplos

Dados armazenados em um perfil comportamental relacionado a um usuário único por um cookie ou outro identificador de dispositivo, mesmo sem outras informações identificáveis,
não ser considerado verdadeiramente anônimo. Um perfil com o identificador exclusivo removido ou hash pode ser considerado anônimo.

## Educação

É importante que os usuários possam entender a melhor forma de gerenciar sua privacidade e proteger suas informações pessoais, por fornecendo-lhes informações claras e simples sobre opções de privacidade e configurações de segurança de aplicativos. É ajudar os usuários a estarem cientes de questões de privacidade e segurança e como gerenciá-las.

### Diretriz
### Implementação
### Caso de uso e exemplos







---

[Artigo Original](https://iapp.org/resources/article/privacy-design-guidelines-for-mobile-application-development/)

[Download PDF](data/gsmaprivacydesignguidelinesformobileapplicationdevelopmentv1.pdf)



