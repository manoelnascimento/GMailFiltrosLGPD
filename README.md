# GMailFiltrosLGPD
Filtros para classificação de mensagens abusivas no GMail

## O que é isso?

É uma coleção de filtros para GMail, que ajudam a filtrar mensagens indesejadas para posterior análise. 

## O que estes filtros fazem?

1) Etiquetam mensagens recebidas de remetentes identificados pelo desenvolvedor como emissores contumazes de mensagens indesejadas;
2) Arquivam essas mensagens, retirando-as da caixa de entrada;
3) Impedem que essas mensagens sejam consideradas como spam.

Todas as etiquetas criadas por este conjunto de filtros ficam agrupadas sob uma "etiqueta-mãe" chamada "LGPD", assim chamada em homenagem à Lei Geral de Proteção de Dados (LGPD) brasileira. A escolha do nome se justifica porque a principal intenção por trás destes filtros é facilitar aos usuários o exercício de seus direitos de titulares de dados contra os remetentes de mensagens indesejadas.

## Como a base de remetentes indesejados é construída?

Sempre que o desenvolvedor recebe uma mensagem sabidamente indesejada em uma de suas contas do GMail, dá início, pessoalmente, a um processo de verificação:

1) Separa mensagens em português daquelas em outros idiomas;
2) Localiza o nome de domínio do e-mail remetente;
3) Submete o nome de domínio a uma pesquisa usando o comando "whois";
4) Pesquisa o nome da(s) pessoa(s) ou empresa(s) envolvida(s) em buscadores.

Assim que termina este processo de verificação humana, dá início, também pessoalmente, ao processo de atualização dos filtros:

1) Checa se a(s) pessoa(s) ou empresa(s) identificada(s) já se encontra(m) identificada(s) por alguma etiqueta;
2) Se existe, adiciona o novo nome de domínio à etiqueta já existente;
3) Se não existe, cria nova etiqueta.

Tais critérios são **absolutamente pessoais**. Pode ser que não se adequem às suas necessidades, ou que interfiram negativamente em suas comunicações. Por isso, **revise os filtros antes de implementá-los**. O desenvolvedor **não se responsabiliza** por qualquer interferência negativa causada por esses filtros se vocẽ não os revisar antes de implementá-los em seu GMail.

## Modo de usar

### Como se faz para usar esses filtros?

Todos os filtros estão num arquivo XML formatado de acordo com os [operadores de busca do próprio Google](https://support.google.com/mail/answer/7190?hl=en).

O arquivo XML foi criado usando um arquivo exportado do próprio GMail.

Para usar os filtros deste repositório, basta baixar o arquivo XML e importá-lo para seu GMail, seguindo as [orientações do Google para importação de filtros para o GMail](https://support.google.com/mail/answer/6579?hl=pt#zippy=%2Cedite-ou-elimine-filtros%2Cexporte-ou-importe-filtros).

### Como posso revisar os filtros antes de implementá-los num GMail?

1) Baixe o arquivo XML que contém os filtros;
2) Examine filtro a filtro;
3) Faça as modificações necessárias.

Cada filtro está encapsulado entre etiquetas <entry> e </entry>.

## Perguntas e respostas

### O que o desenvolvedor considera como "mensagem indesejada"?

A mensagem será considerada indesejada pelo desenvolvedor nas seguintes situações:

1) Faz cobranças em favor de empresas com quem o desenvolvedor nunca teve relação;
2) Oferece serviços que o desenvolvedor nunca pesquisou;
3) Oferece produtos pelos quais o desenvolvedor nunca se interessou;
4) Faz menção a homônimos do desenvolvedor ("Manoel Antônio do Nascimento", "Manoel do Nascimento Rodrigues", etc.);
5) Dá o endereço do desenvolvedor como inscrito em listas nas quais nunca o desenvolvedor nunca se inscreveu.

Tais critérios são **absolutamente pessoais**. Pode ser que não se adequem às suas necessidades, ou que interfiram negativamente em suas comunicações. Por isso, **revise os filtros antes de implementá-los**. O desenvolvedor **não se responsabiliza** por qualquer interferência negativa causada por esses filtros se vocẽ não os revisar antes de implementá-los em seu GMail.

### Por que não excluir imediatamente as mensagens?

O critério para considerar uma mensagem como "indesejada" tem como base interesses do próprio desenvolvedor. Pode ser que os critérios do desenvolvedor não atendam os seu critérios pessoais. Por isso, em vez de apagar as mensagens

### Nâo é mais fácil marcar as mensagens indesejadas como spam?

O desenvolvedor tentou por este caminho, mas não demora muito e volta a receber mensagens semelhantes àquelas de cuja lista de destinatários se retirou.

Além disso, em certos casos o desenvolvedor suspeita de compartilhamento irregular de dados entre certas empresas. As mensagens organizadas por estes filtros servirão como material para análise, cruzamento de informações, e eventuais medidas corretivas futuras.

### Por que existe uma hierarquia de etiquetas?

Além da "etiqueta-mãe" chamada "LGPD", existe uma hierarquia de etiquetas, assim definida:

#### "em andamento"

Agrupam pessoas e empresas que o desenvolvedor já identificou, e com quem já tentou contato para fazer parar as mensagens indesejadas. Dentro desta etiqueta, existem outras duas:

##### "com encarregado"

Para as pessoas e empresas cujo encarregado pelo tratamento de dados (ETD, ou *data protection officer* -- DPO) foi identificado. No futuro, o desenvolvedor poderá apresentar aqui, ou em outro lugar, uma relação dos contatos destes ETD/DPO.

##### "sem encarregado"

Para as pessoas e empresas cujo ETD/DPO não foi possível de localizar, ou não tinha localização fácil. Para efeitos da LGPD, uma controladora/operadora cujos contatos de ETD/DPO não estão facilmente disponíveis não atende aos deveres legais, e pode-se considerar como se não tivesse, efetivamente, um ETD/DPO.

#### "a encaminhar"

Agrupam pessoas e empresas que o desenvolvedor ainda não contatou.

### Por que são destacados apenas remetentes de mensagens em português?

As mensagens indesejadas redigidas em outros idiomas além do português são descartadas porque o desenvolvedor já identificou a presença seu endereço de correio eletrônico em listas de dados vazados em incidentes de segurança, e porque é mais fácil para o desenvolvedor lidar com os remetentes contumazes sediados no Brasil, por causa da Lei Geral de Proteção de Dados (LGPD).

### Por que esses filtros foram criados?

Meu e-mail do Google é de 2004, quando ainda era possível conseguir nomes simples.

Acontece que meu nome é simples. Tenho muitos homônimos. Muitos deles dão meu e-mail para inscrever-se em serviços, como se meu e-mail fosse deles.

De 2019 para cá, a quantidade de mensagens indesejadas na minha caixa de entrada cresceu muito. Chegou um momento em que se tornou praticamente inviável usá-la. Eu precisava dedicar cerca de meia hora, todos os dias, a percorrer mensagens em busca das legítimas, que se perdiam em meio ao spam, à propaganda abusiva e às cobranças indevidas. Fiquei assim todos os dias, por uma semana, sem sucesso. Bastava passar dois ou três dias sem abrir o correio eletrônico, e voltava tudo ao estado anterior.

Percebi que filtros de mensagens poderiam servir para automatizar esta tarefa. Com certas alterações, eles me permitiram agrupar as mensagens indesejadas conforme os remetentes. Em alguns casos, entrei em contato com as empresas solicitando retirada de cadastro. Com isso, o fluxo de mensagens foi-se reduzindo.

Entendi que o mesmo problema acontece com outras pessoas quando vi a caixa de entrada dos correios eletrônicos de alguns amigos. Compartilhei meus filtros, e vi resultados muito rápidos.

Dada a utilidade pública desses filtros, resolvi compartilhá-los via GitHub.
