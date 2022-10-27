GMailFiltrosLGPD
================

Filtros para classificação de mensagens abusivas no GMail

Conteúdo
========

-   [GMailFiltrosLGPD](#gmailfiltroslgpd)
-   [Conteúdo](#conteúdo)
    -   [O que é isso?](#o-que-é-isso)
    -   [O que estes filtros fazem?](#o-que-estes-filtros-fazem)
    -   [Como a base de remetentes indesejados é construída?](#como-a-base-de-remetentes-indesejados-é-construída)
    -   [Modo de usar](#modo-de-usar)
        -   [Como se faz para usar esses filtros?](#como-se-faz-para-usar-esses-filtros)
        -   [Por que preciso revisar os filtros antes de implementá-los num GMail?](#por-que-preciso-revisar-os-filtros-antes-de-implementá-los-num-gmail)
        -   [Como posso revisar os filtros antes de implementá-los num GMail?](#como-posso-revisar-os-filtros-antes-de-implementá-los-num-gmail)
    -   [Perguntas e respostas](#perguntas-e-respostas)
        -   [O que o desenvolvedor considera como "mensagem indesejada"?](#o-que-o-desenvolvedor-considera-como-mensagem-indesejada)
        -   [Por que não excluir imediatamente as mensagens?](#por-que-não-excluir-imediatamente-as-mensagens)
        -   [Não é mais fácil marcar as mensagens indesejadas como spam?](#não-é-mais-fácil-marcar-as-mensagens-indesejadas-como-spam)
        -   [Por que existe uma hierarquia de etiquetas?](#por-que-existe-uma-hierarquia-de-etiquetas)
        -   [Por que são destacados apenas remetentes de mensagens em português?](#por-que-são-destacados-apenas-remetentes-de-mensagens-em-português)
        -   [Os nomes de domínio ficam nessa lista de filtros para sempre?](#os-nomes-de-domínio-ficam-nessa-lista-de-filtros-para-sempre)
        -   [Meu nome, ou o da minha empresa, estão nessa lista. Isso quer dizer que eu estou irregular?](#meu-nome-ou-o-da-minha-empresa-estão-nessa-lista.-isso-quer-dizer-que-eu-estou-irregular)
        -   [Por que esses filtros foram criados?](#por-que-esses-filtros-foram-criados)

O que é isso?
-------------

É uma coleção de filtros para GMail, que ajudam a classificar mensagens indesejadas para análise posterior.

O que estes filtros fazem?
--------------------------

1)  Reconhecem mensagens recebidas de remetentes identificados pelo desenvolvedor como emissores contumazes de mensagens indesejadas;
2)  Etiquetam essas mensagens, de acordo com a hierarquia de etiquetas definida pelo desenvolvedor;
3)  Arquivam essas mensagens, retirando-as da caixa de entrada;
4)  Impedem que essas mensagens sejam consideradas pelo GMail como spam.

Todas as etiquetas criadas por este conjunto de filtros ficam agrupadas sob uma "etiqueta-mãe" chamada "LGPD", assim chamada em homenagem à Lei Geral de Proteção de Dados (LGPD) brasileira. A escolha do nome desta etiqueta se justifica porque a principal intenção por trás destes filtros é facilitar aos usuários o exercício de seus direitos de titulares de dados contra os remetentes de mensagens indesejadas.

Como a base de remetentes indesejados é construída?
---------------------------------------------------

Sempre que o desenvolvedor recebe uma mensagem sabidamente indesejada em uma de suas contas do GMail, dá início, pessoalmente, a um processo de verificação:

1)  Separa mensagens em português daquelas em outros idiomas;
2)  Localiza o nome de domínio do correio eletrônico remetente;
3)  Tenta acessar diretamente o nome de domínio, como se fosse um website normal;
4)  Submete o nome de domínio a uma pesquisa usando o comando "whois";
5)  Pesquisa em buscadores o nome da(s) pessoa(s) ou empresa(s) envolvida(s) com a mensagem indesejada.

Assim que termina este processo de verificação humana, dá início, também pessoalmente, ao processo de atualização dos filtros:

1)  Checa se a(s) pessoa(s) ou empresa(s) identificada(s) já se encontra(m) identificada(s) por alguma etiqueta;
2)  Se existe, adiciona o novo nome de domínio à etiqueta já existente;
3)  Se não existe, cria nova etiqueta.

Tais critérios são **absolutamente pessoais**. Pode ser que não se adequem às suas necessidades, ou que interfiram negativamente em suas comunicações. Por isso, **revise os filtros antes de implementá-los**. O desenvolvedor **não se responsabiliza** por qualquer interferência negativa causada por esses filtros se vocẽ não os revisar antes de implementá-los em seu GMail.

Modo de usar
------------

### Como se faz para usar esses filtros?

Todos os filtros estão num arquivo XML formatado de acordo com os [operadores de busca do próprio Google](https://support.google.com/mail/answer/7190?hl=en).

O arquivo XML foi criado usando um arquivo exportado do próprio GMail.

Para usar os filtros deste repositório, basta baixar o arquivo XML e importá-lo para seu GMail, seguindo as [orientações do Google para importação de filtros para o GMail](https://support.google.com/mail/answer/6579?hl=pt#zippy=%2Cedite-ou-elimine-filtros%2Cexporte-ou-importe-filtros).

A principal ferramenta usada são os coringas, como nos exemplos a seguir:

`*teste*@exemplo.com.br`</br>
`*teste*@exemplo.com`</br>
`*teste*@*exemplo*`</br>
`*teste*@exemplo.*`</br>
`*teste*@*.exemplo*`</br>
`*teste*@*.exemplo.*`

### Por que preciso revisar os filtros antes de implementá-los num GMail?

Porque foram construídos para responder ao que o desenvolvedor considera como mensagens indesejadas. Pode ser que uma mensagem considerada indesejada pelo desenvolvedor seja uma mensagem legítima para você.

Um exemplo: o desenvolvedor recebe pelo menos uma mensagem a cada dois dias de um determinado banco. Já pediu para retirarem seu correio eletrônico da lista de remetentes, mas continua recebendo as tais
mensagens. Já clicou no link/botão de descadastramento, mas segue recebendo mensagens. É evidente que tais mensagens, do ponto de vista do desenvolvedor, são indesejadas. Mas pode ocorrer de alguém que tentar usar esses filtros ser correntista desse mesmo banco; deste modo, é esperado, e legítimo, que o banco envie certas mensagens (alertas de aplicativo, notificação de movimentação, etc.). Se alguém usar estes filtros sem retirar este aqueles que capturam mensagens deste banco, poderá perder mensagens importantes.

Outro exemplo: o desenvolvedor recebe, de quinze em quinze dias, mensagens de determinada empresa de cobrança, onde não aparece qualquer link ou botão de descadastramento, telefone de contato, nada. É evidente que tais mensagens são indesejadas, e além disso não facilitam o contato com a empresa de cobrança para correção de cadastro equivocado. Mas pode ocorrer de alguém estar sendo cobrado por uma dívida real; neste caso, as comunicações sem resposta poderão servir como prova de que a empresa de cobrança tentou entrar em contato, sem sucesso.

Por isso, não custa repetir: **revise os filtros antes de implementá-los**. O desenvolvedor **não se responsabiliza** por qualquer interferência negativa causada por esses filtros se vocẽ não os revisar
antes de implementá-los em seu GMail.

### Como posso revisar os filtros antes de implementá-los num GMail?

Cada filtro está encapsulado entre etiquetas ```<entry>``` e ```</entry>```. Para revisá-los, o procedimento é simples:

1)  Baixe o arquivo XML que contém os filtros;
2)  Examine filtro a filtro;
3)  Faça as modificações necessárias.

É preciso, claro, que se tenha algum conhecimento em XML, e também sobre os [operadores de busca do Google](https://support.google.com/mail/answer/7190?hl=en).

Perguntas e respostas
---------------------

### O que o desenvolvedor considera como "mensagem indesejada"?

A mensagem será considerada indesejada pelo desenvolvedor nas seguintes situações:

1)  Faz cobranças em favor de empresas com quem o desenvolvedor nunca teve relação;
2)  Oferece serviços que o desenvolvedor nunca pesquisou;
3)  Oferece produtos pelos quais o desenvolvedor nunca se interessou;
4)  Faz menção a homônimos do desenvolvedor ("Manoel Antônio do Nascimento", "Manoel do Nascimento Rodrigues", etc.);
5)  Dá o endereço do desenvolvedor como inscrito em listas nas quais nunca o desenvolvedor nunca se inscreveu.

Tais critérios são **absolutamente pessoais**. Pode ser que não se adequem às suas necessidades, ou que interfiram negativamente em suas comunicações. Por isso, **revise os filtros antes de implementá-los**. O desenvolvedor **não se responsabiliza** por qualquer interferência negativa causada por esses filtros se vocẽ não os revisar antes de implementá-los em seu GMail.

### Por que não excluir imediatamente as mensagens?

O critério para considerar uma mensagem como "indesejada" tem como base interesses do próprio desenvolvedor. Pode ser que os critérios do desenvolvedor não atendam os seu critérios pessoais. Por isso, em vez de apagar as mensagens

### Não é mais fácil marcar as mensagens indesejadas como spam?

O desenvolvedor tentou por este caminho, mas não demora muito e volta a receber mensagens semelhantes àquelas de cuja lista de destinatários se retirou.

Além disso, em certos casos o desenvolvedor suspeita de compartilhamento irregular de dados entre certas empresas. As mensagens organizadas por estes filtros servirão como material para análise, cruzamento de informações, e eventuais medidas corretivas futuras.

### Por que existe uma hierarquia de etiquetas?

Para agrupar num só lugar as mensagens indesejadas. Fica mais fácil, e polui menos o visual da caixa de entrada.

Além da "etiqueta-mãe" chamada "LGPD", existe uma hierarquia de etiquetas, assim definida:

#### "em andamento"

Agrupam pessoas e empresas que o desenvolvedor já identificou, e com quem já tentou contato para fazer parar as mensagens indesejadas. Dentro desta etiqueta, existem outras duas:

##### "com encarregado"

Para as pessoas e empresas cujo encarregado pelo tratamento de dados (ETD, ou *data protection officer* -- DPO) foi identificado. No futuro, o desenvolvedor poderá apresentar aqui, ou em outro lugar, uma relação dos contatos destes ETD/DPO.

##### "sem encarregado"

Para as pessoas e empresas cujo ETD/DPO não foi possível de localizar, ou não tinha localização fácil. Para efeitos da LGPD, uma controladora/operadora cujos contatos de ETD/DPO não estão facilmente disponíveis não atende aos deveres legais, e pode-se considerar como se não tivesse, efetivamente, um ETD/DPO.

#### "a encaminhar"

Agrupam pessoas e empresas que o desenvolvedor ainda não contatou.

#### "resolvidas"

Agrupam pessoas e empresas que atenderam às solicitações de titular de dados do desenvolvedor, parando com o tratamento irregular de dados.

### Por que são destacados apenas remetentes de mensagens em português?

As mensagens indesejadas redigidas em outros idiomas além do português são descartadas porque o desenvolvedor já identificou a presença seu endereço de correio eletrônico em listas de dados vazados em incidentes de segurança, e porque é mais fácil para o desenvolvedor lidar com os remetentes contumazes sediados no Brasil, por causa da Lei Geral de Proteção de Dados (LGPD).

### Os nomes de domínio ficam nessa lista de filtros para sempre?

Não.

Assim que uma situação de tratamento irregular de dados é resolvida, o nome da(s) pessoa(s) ou empresa(s) envolvida(s) passa para a etiqueta "resolvidas", onde fica em *stand by* .

Se novas irregulares são cometidas, o nome volta para alguma das etiquetas indicativas de irregularidades.

Se se passa um prazo que o desenvolvedor considera razoável sem novas mensagens irregulares, o desenvolvedor retira o nome dos filtros e coloca-os num arquivo de *backup*, de onde podem ser recuperados em caso de reincidência.

### Meu nome, ou o da minha empresa, estão nessa lista. Isso quer dizer que eu estou irregular?

Esta lista de filtros diz respeito às mensagens consideradas irregulares porque recebidas por uma pessoa específica (o desenvolvedor), que as considerou irregulares por tê-las recebido sem que as desejasse, ou sem seu consentimento para tratamento de dados.

No que diz respeito a *esta pessoa* (o desenvolvedor), o tratamento de seus dados pessoais pelas pessoas e empresas citadas na lista é, sim, irregular.

Não se pode inferir daí, entretanto, a irregularidade de *todas* as operações de tratamento de dados pessoais feitas pelas pessoas e empresas cujos nomes estão nesta lista de remetentes.

Por outro lado, o tratamento irregular dos dados do desenvolvedor por você ou sua empresa pode ser entendido como sintoma da necessidade de correção de algum, ou alguns, dos seguintes erros no tratamento de dados pessoais:

1)  Cadastro de usuários feito sem algum mecanismo de autenticação do correio eletrônico cadastrado (p. ex., só liberar acesso depois de o novo usuário receber mensagem de confirmação do endereço e clicar no link);
2)  Uso de cadastros "frios", ou seja, recebido de terceiros (via compra, compartilhamento, doação, etc.) sem checagem e validação da base de dados em busca de consentimento;
3)  Erros de digitação no cadastro;
4)  Uso irregular de dados do desenvolvedor por homônimos ou parônimos;
5)  Cadastro, por homônimos ou parônimos, de endereços de correio eletrônico que não observam o fato de que [pontos são irrelevantes nos endereços do GMail](https://support.google.com/mail/answer/7436150), "criam" endereços que supõem serem seus, mas terminam [direcionando mensagens para alguma conta GMail do desenvolvedor](https://support.google.com/mail/answer/10313?hl=pt-BR#zippy=%2Crecebi-mensagens-enviadas-para-uma-vers%C3%A3o-com-pontos-do-meu-endere%C3%A7o).

Sobre este último ponto, necessária alguma explicação:

1)  Para o Google, pouco importa que um endereço seja dado como ```austregesilo.de.athayde\@gmail.com```, ```austregesilodeathayde\@gmail.com```, ```austregesilo.deathayde\@gmail.com``` ou qualquer outra variação com ponto; em todos estes casos, quem recebe as mensagens é ```austregesilodeathayde\@gmail.com```, porque [pontos são irrelevantes nos endereços do GMail](https://support.google.com/mail/answer/7436150).
2)  Para o Google, não adianta tentar criar o endereço ```austregesilo.de.athayde\@gmail.com``` depois de alguém já ter criado o endereço ```austregesilodeathayde\@gmail.com```; como [pontos são irrelevantes nos endereços do GMail](https://support.google.com/mail/answer/7436150), aquela primeira versão simplesmente não será criada.
3)  Para o Google, quem cria o endereço ```austregesilo.de.athayde\@gmail.com``` tem direito, automaticamente, a usar o endereço ```austregesilodeathayde\@gmail.com```, porque quem cria uma versão com ponto cria também a versão sem ponto, e vice-versa.

Se você ou sua empresa entrarem em contato via filtrosgmail\@mmnj.adv.br demonstrando que o tratamento irregular de dados pessoais do desenvolvedor foi resolvido, será um prazer retirar seu nome, ou o de sua empresa, da lista de remetentes contumazes de mensagens indesejadas.

### Por que esses filtros foram criados?

Meu primeiro correio eletrônico do Google é de 2004, quando ainda era possível conseguir nomes simples. Até hoje, ele é um de meus contatos pessoais e profissionais mais usados.

Acontece que meu nome é simples. Tenho muitos homônimos. Muitos deles dão meu correio eletrônico para inscrever-se em serviços, como se meu correio eletrônico fosse deles.

De 2019 para cá, a quantidade de mensagens indesejadas na minha caixa de entrada cresceu muito. Chegou um momento em que se tornou praticamente inviável usá-la. Eu precisava dedicar cerca de meia hora, todos os dias, a percorrer mensagens em busca das legítimas, que se perdiam em meio ao spam, à propaganda abusiva e às cobranças indevidas. Fiquei assim todos os dias, por uma semana, sem sucesso. Bastava passar dois ou três dias sem abrir o correio eletrônico, e voltava tudo ao estado anterior.

Percebi que filtros de mensagens poderiam servir para automatizar esta tarefa. Com certas alterações, eles me permitiram agrupar as mensagens indesejadas conforme os remetentes. Em alguns casos, entrei em contato com as empresas solicitando retirada de cadastro. Com isso, o fluxo de mensagens foi-se reduzindo.

Entendi que o mesmo problema acontece com outras pessoas quando vi a caixa de entrada dos correios eletrônicos de alguns amigos. Compartilhei meus filtros, e vi resultados muito rápidos.

Dada a utilidade pública desses filtros, resolvi compartilhá-los via GitHub.