doc AWS : 

https://aws.amazon.com/pt/dms/ :check_mark: 

How AWS Database Migration Service works - AWS Database Migration Service:check_mark: 

High-level view of AWS DMS - AWS Database Migration Service  :check_mark: 

Components of AWS DMS - AWS Database Migration Service :check_mark: 

Choosing the right AWS DMS replication instance for your migration - AWS Database Migration Service 

Working with an AWS DMS replication instance - AWS Database Migration Service 

Sources for AWS DMS - AWS Database Migration Service :check_mark: 

Targets for AWS DMS - AWS Database Migration Service :check_mark: 

Working with AWS DMS endpoints - AWS Database Migration Service 

Creating a task - AWS Database Migration Service 

Setting LOB support for source databases in an AWS DMS task - AWS Database Migration Service 

Using table mapping to specify task settings - AWS Database Migration Service 

Specifying table selection and transformations rules using JSON - AWS Database Migration Service 

Working with AWS DMS tasks - AWS Database Migration Service

https://docs.aws.amazon.com/dms/index.html :check_mark: 

Usar o AWS DMS com outros serviços da AWS - AWS Database Migration Service :check_mark: 

Getting started with AWS Database Migration Service - AWS Database Migration Service 

Setting up for AWS Database Migration Service - AWS Database Migration Service 

Prerequisites for AWS Database Migration Service - AWS Database Migration Service 

Getting started with DMS Schema Conversion - AWS Database Migration Service 

Migrating your source schema to your target database using AWS SCT - AWS Database Migration Service 

Creating source and target endpoints - AWS Database Migration Service 

Setting up replication for AWS Database Migration Service - AWS Database Migration Service 

Creating a task - AWS Database Migration Service 

Criação de projetos de migração no AWS Database Migration Service - AWS Database Migration Service 

Overview
O AWS Database Migration Service (AWS DMS) é um serviço de replicação que facilita a migração de bancos de dados para a nuvem AWS de forma segura e com o mínimo possível de inatividade e zero perda de dados. Ele suporta migrações de bancos de dados homogêneos (por exemplo, Oracle para Oracle) e migrações heterogêneas (por exemplo, Oracle para MySQL). Além disso, ele também permite a replicação contínua de bancos de dados para a migração em tempo real ou para fins de backup, mas não oferece recursos avançados de gerenciamento de dados, como a definição de políticas de expurgo/purge.

Replicação
Existem duas abordagens principais que você pode adotar:

Replicação inicial completa seguida de replicação contínua: Nessa abordagem, você realiza uma replicação inicial completa de todos os dados existentes na fonte para o destino. Isso garante que todos os dados sejam copiados inicialmente. Após a replicação inicial, o DMS pode ser configurado para continuar replicando as alterações subsequentes na fonte, garantindo que o destino esteja sempre atualizado.

Filtro de dados durante a replicação: O DMS permite configurar filtros para selecionar apenas um subconjunto específico de dados com base em critérios como colunas, tabelas ou intervalo de datas. Por exemplo, você pode configurar o DMS para replicar apenas os dados criados ou atualizados após uma determinada data, descartando os dados mais antigos. Isso pode ser feito usando as opções de filtragem fornecidas pelo DMS durante a configuração da tarefa de migração.

É importante notar que o DMS suporta uma variedade de opções de filtragem e configurações avançadas que permitem personalizar ainda mais a replicação de dados de acordo com as suas necessidades.

Uma possivel alternativa é fazer um misto das duas abordagens, realizando uma replicação inicial com base em um filtro de intervalo de datas e, em seguida, configurando a replicação contínua para manter os dados atualizados.

Para configurar isso de forma a evitar duplicidade de dados:

Configuração inicial com filtro de intervalo de datas:

Ao configurar a tarefa de migração no AWS DMS, defina um filtro para selecionar apenas os dados que estão dentro do intervalo de datas desejado. Isso pode ser feito usando as opções de filtragem disponíveis, como filtros de tabela ou filtros de seleção. :warning: 

Por exemplo, você pode definir uma condição WHERE nas opções de filtro para replicar apenas as linhas que tenham uma coluna de data dentro do intervalo desejado.

Realize a replicação inicial:

Execute a tarefa de migração para realizar a replicação inicial dos dados que atendem ao filtro de intervalo de datas. Isso copiará apenas os dados selecionados durante a migração inicial.

Configuração da replicação contínua:

Após a conclusão da replicação inicial, você pode configurar a tarefa de migração para continuar a replicação contínua das alterações subsequentes na fonte.

O DMS possui um recurso chamado "CDC (Change Data Capture)" que permite capturar as alterações nos bancos de dados fonte e replicá-las para o destino em tempo real. Você pode habilitar o CDC para as tabelas relevantes na sua configuração do DMS.

Com esse misto das abordagens, a replicação inicial será realizada apenas para os dados que atendem ao filtro de intervalo de datas. A replicação contínua capturará e replicará as alterações posteriores na fonte, garantindo que o destino esteja sempre atualizado.

No entanto, é importante observar que a configuração precisa ser cuidadosa para evitar a duplicidade de dados durante a replicação contínua. Certifique-se de que as tabelas e colunas relevantes estejam corretamente configuradas para o CDC e que você não esteja duplicando dados já existentes na tarefa de migração.

No AWS Database Migration Service (DMS), é possível configurar a replicação inicial e a replicação contínua ao mesmo tempo. Não é necessário esperar que a replicação inicial seja concluída antes de iniciar a replicação contínua.

Durante a configuração da tarefa de migração no DMS, você pode especificar tanto a opção de replicação inicial quanto a opção de replicação contínua. O DMS começará replicando os dados da replicação inicial e, simultaneamente, iniciará a captura das alterações para a replicação contínua.

No processo de replicação inicial, o DMS copiará todos os dados iniciais da fonte para o destino, garantindo que o destino comece com uma cópia completa dos dados. Enquanto isso, o DMS também estará capturando as alterações na fonte usando o recurso Change Data Capture (CDC).

Uma vez que a replicação inicial é concluída, o DMS passa a focar na replicação contínua das alterações. O CDC captura as transações de alteração ocorridas na fonte e as replica para o destino em tempo real ou em intervalos regulares, dependendo da configuração definida.

Essa abordagem permite que a replicação inicial e a replicação contínua ocorram simultaneamente, reduzindo o tempo necessário para migrar e manter os dados atualizados. No entanto, é importante garantir que a configuração do DMS esteja correta para evitar possíveis conflitos ou problemas durante o processo de replicação.

CUSTO
O custo do AWS Database Migration Service (DMS) é baseado em vários fatores, como a região da AWS em que você está usando o serviço, o tipo de instância usada para a tarefa de migração, a quantidade de dados transferidos e o tempo de execução da tarefa.

Para obter informações sobre o custo da migração de banco de dados : https://aws.amazon.com/pt/dms/pricing/ [LER]

Existem dois componentes principais que contribuem para o custo do DMS:

Instâncias do DMS: O custo está relacionado ao tipo de instância de banco de dados usada para executar a tarefa de migração. A AWS oferece diferentes tipos de instâncias do DMS com preços diferentes, e o custo varia com base nas características de desempenho e capacidade de cada instância.

Transferência de dados: O custo também está associado à quantidade de dados transferidos durante a migração. A AWS cobra pelo tráfego de dados entre a fonte e o destino, levando em consideração tanto a quantidade de dados transferidos como a região da AWS em que ocorre a transferência.

Além disso, é importante considerar outros custos associados ao ambiente em que você está executando o DMS, como o custo de armazenamento de dados no destino, custos de monitoramento e possíveis custos adicionais para recursos auxiliares, como AWS Lambda ou Amazon CloudWatch, caso sejam utilizados em conjunto com o DMS.

Para obter informações atualizadas sobre os preços específicos do AWS DMS, recomenda-se consultar a página de preços da AWS (https://aws.amazon.com/pt/dms/pricing/) e utilizar a calculadora de preços da AWS (AWS Pricing Calculator ) para estimar os custos com base nas suas necessidades e configurações específicas.

Lembre-se de que os preços podem variar com o tempo e é importante verificar as informações mais recentes diretamente na documentação oficial da AWS para obter uma compreensão completa dos custos associados ao uso do AWS DMS.

 

Visão de alto nível do AWS DMS[2]
Para realizar uma migração de banco de dados, o AWS DMS se conecta ao banco de dados de origem, lê os dados e os formata para serem consumidos pelo banco de dados de destino. Em seguida, ele carrega os dados no destino. A maioria desse processamento acontece em memória (2a), embora grandes transações possam exigir algum armazenamento em buffer no disco. As transações em cache e os arquivos de log também são gravados no disco.

Em um alto nível, ao usar o AWS DMS é preciso realizar os seguintes passos:

Converção dos schemas da origem e dos database code objects  para um formato compativel com o banco de dados de destino.

Criar  um servidor de  replicação;

Criar endpoint de origem e destino que tenham as infos de conexão com ambos os bancos de dados;

Criar a(s) tarefa(s) de migração para migrar os dados entre origem e destino;

A tarefa pode ser composta por três fases:

Migração dos dados existentes (Full load / carga completa);

Aplicação de alterações em cache;

Replicação contínua (Captura de Dados de Alteração/Change Data Capture))

Durante a full load migration, em que os dados existentes da origem são movidos para o destino, o AWS DMS carrega dados das tabelas do DB de origem para as tabelas do DB de destino. Enquanto o full load  está em andamento, quaisquer alterações feitas nas tabelas sendo carregadas são armazenadas em cache no servidor de replicação; essas são as alterações em cache. É importante observar que o AWS DMS não captura alterações para uma determinada tabela até que a carga completa para essa tabela seja iniciada. Em outras palavras, o ponto em que a captura de alterações começa é diferente para cada tabela individual.

Quando o full load é concluido, imediatamente é iniciada a aplicação das alterações que estão em cache. 

Depois que o AWS DMS aplica todas as alterações em cache, as tabelas são transacionalmente consistentes. Nesse ponto, o AWS DMS passa para a fase de replicação contínua, aplicando as alterações como transações.

:warning:  No início da fase de replicação contínua, um backlog de transações geralmente causa algum atraso entre os bancos de dados de origem e destino. A migração eventualmente atinge um estado estável após processar esse backlog de transações. Neste ponto, você pode desligar suas aplicações, permitir que quaisquer transações restantes sejam aplicadas ao destino e iniciar suas aplicações, agora apontando para o banco de dados de destino.

AWS DMS creates the target schema objects necessary to perform a data migration. You can use AWS DMS to take a minimalist approach and create only those objects required to efficiently migrate the data. Using this approach, AWS DMS creates tables, primary keys, and in some cases unique indexes, but it won't create any other objects that are not required to efficiently migrate the data from the source.

Alternatively, you can use DMS Schema Conversion within AWS DMS to automatically convert your source database schemas and most of the database code objects to a format compatible with the target database. This conversion includes tables, views, stored procedures, functions, data types, synonyms, and so on. Any objects that DMS Schema Conversion can't convert automatically are clearly marked. To complete the migration, you can convert these objects manually.

 

o que são database code objects nos bancos de dados?
No contexto de bancos de dados, os "database code objects" (objetos de código de banco de dados) são elementos que são criados e armazenados em um banco de dados para executar determinadas funcionalidades ou lógica de negócio. Esses objetos são escritos em uma linguagem de programação específica para bancos de dados, como SQL (Structured Query Language) ou PL/SQL (Procedural Language/SQL).

Alguns exemplos comuns de database code objects são:

Tabelas: São objetos que armazenam os dados em um banco de dados, com colunas que definem os tipos de dados a serem armazenados.

Visões (Views): São consultas armazenadas como objetos no banco de dados. Elas são uma representação virtual dos dados em uma ou mais tabelas, permitindo aos usuários consultar os dados de maneira simplificada, como se estivessem consultando uma tabela real.

Procedimentos Armazenados (Stored Procedures): São blocos de código que contêm instruções SQL e podem receber parâmetros. Eles são armazenados no banco de dados e podem ser chamados por outros programas ou scripts para executar tarefas específicas, como inserção, atualização ou exclusão de dados.

Funções (Functions): São semelhantes aos procedimentos armazenados, mas retornam um valor. Elas podem ser usadas em expressões SQL para realizar cálculos ou transformações de dados.

Gatilhos (Triggers): São código associado a uma tabela e acionado automaticamente quando ocorrem determinados eventos, como inserção, atualização ou exclusão de dados na tabela. Os gatilhos permitem executar ações adicionais antes ou depois de um evento ocorrer.

Esses objetos de código de banco de dados são fundamentais para implementar a lógica de negócios e a funcionalidade do sistema em um banco de dados. Eles ajudam a garantir a consistência dos dados, facilitar a reutilização de código e melhorar o desempenho das operações de banco de dados.

[Fonte: ChatGPT]

Componentes do AWS DMS [2b]
Replication instance
A figura a seguir mostra um exemplo de instância de replicação executando várias tarefas de replicação associadas.


                            Get started with AWS DMS
                        
 

Uma única instância de replicação pode hospedar uma ou mais tarefas de replicação, dependendo das características da sua migração e da capacidade do servidor de replicação. Uma única instância de replicação pode hospedar uma ou mais tarefas de replicação, dependendo das características da sua migração e da capacidade do servidor de replicação. O AWS DMS fornece uma variedade de instâncias de replicação para que você possa escolher a configuração ideal para o seu caso de uso. Para obter mais informações sobre as várias classes de instâncias de replicação, consulte Choosing the right AWS DMS replication instance for your migration. [LER]

O AWS DMS cria a instância de replicação em uma instância do Amazon EC2. Algumas das classes de instância menores são suficientes para testar o serviço ou para migrações pequenas. Se a sua migração envolver um grande número de tabelas ou se você pretende executar várias tarefas de replicação simultaneamente, você deve considerar o uso de uma das instâncias maiores. Recomendamos essa abordagem porque o AWS DMS pode consumir uma quantidade significativa de memória e CPU.

A Change data capture (CDC) ode fazer com que os dados sejam gravados no disco, dependendo da rapidez com que o destino pode gravar as alterações. dependendo da velocidade com que o destino consegue gravar as alterações.  Como os arquivos de log também são gravados no disco, aumentar o nível de severidade do log também levará a um maior consumo de armazenamento.

O AWS DMS pode fornecer suporte de alta disponibilidade e failover usando uma implantação Multi-AZ. provisiona e mantém automaticamente uma réplica de espera da instância de replicação em uma Zona de Disponibilidade diferente. A instância de replicação primária é replicada de forma síncrona para a réplica de espera. Se a instância de replicação primária falhar ou ficar indisponível, a réplica de espera retomará qualquer tarefa em execução com interrupção mínima. Como a instância primária está constantemente replicando seu estado para a réplica de espera, a implantação Multi-AZ incorre em alguma sobrecarga de desempenho.

Para obter informações mais detalhadas sobre a instância de replicação do AWS DMS, consulte Working with an AWS DMS replication instance.

Endpoint
O AWS DMS usa um endpoint para acessar seu armazenamento de dados de origem ou destino. Em geral, são fornecidas as seguintes informações ao criar um endpoint:

Endpoint type – Origem (Source) ou destino (target);

Engine type – Qual o database engine, como Oracle ; PostgreSQL;

Server name – Nome do servidor ou IP que o AWS DMS pode acessar;

Porta – Número da porta usado para conexão com o servidor de banco ed dados;

Encryption –  Modo Secure Socket Layer (SSL), se o SSL for usado para criptografar a conexão.

Credenciais - Nome de usuário e senha para uma conta com os direitos de acesso necessários.

Quando você cria um endpoint usando o console do AWS DMS, o console exige que você teste a conexão do endpoint. Se o teste de conexão for bem-sucedido, o AWS DMS baixa e armazena as informações do schema para usar posteriormente durante a configuração da task.  As informações do schema podem incluir definições de tabela, definições de primary key e definições de unique key, por exemplo.

Mais de uma task de replicação pode usar um único endpoint. Por exemplo, você pode ter dois applications logicamente distintos hospedados no mesmo banco de dados de origem que deseja migrar separadamente. Nesse caso, você cria duas tasks de replicação, uma para cada conjunto de applications tables. Você pode usar o mesmo endpoint do AWS DMS em ambas as tasks.  

Cada data store engine tem diferentes configurações de endpoint disponíveis. Para obter uma lista de armazenamentos de dados de origem e destino compatíveis, consulte Sources for AWS DMS . [LER] e  Targets for AWS DMS . [LER]..

Replication tasks
A replications task do AWS DMS move um conjunto de dados do source endpoint (endpoint de origem)  para o target endpoint ( endpoint de destino)  Criar uma replication task  é o último passo que você precisa tomar antes de iniciar a migração. 

Ao criar uma tarefa de replicação, você especifica as seguintes configurações da tarefa::

Replication instance  – a instância para hospedar e executar a tarefa;

Source endpoint;

Target endpoint;

Opções de tipo de migração, conforme listado a seguir. Para obter uma explicação completa das opções de tipo de migração, consulte Creating a task.

Full load (Migrate existing data) – Se você puder pagar uma interrupção longa o suficiente para copiar seus dados existentes, essa opção é uma boa escolha. Esta opção simplesmente migra os dados de seu banco de dados de origem para seu banco de dados de destino, criando tabelas quando necessário.

Full load + CDC (Migrate existing data and replicate ongoing changes) – Esta opção executa um carregamento de dados completo (full data load)  enqaunto captura de alterações na origem (source). Após a conclusão do carregamento completo (full data load) , as alterações capturadas são aplicadas ao destino (target). Eventualmente, a aplicação de mudanças atinge um estado estacionário. Nesse ponto, você pode desligar suas aplicações, permitir que as alterações restantes fluam para o destino e, em seguida, reiniciar suas aplicações direcionadas ao destino.

CDC only (Replicate data changes only) : Em algumas situações, pode ser mais eficiente copiar dados existentes usando um método diferente do AWS DMS. Por exemplo, em uma migração homogênea, o uso de ferramentas nativas de exportação e importação pode ser mais eficiente para carregar dados em massa. Nessa situação, você pode usar o AWS DMS para replicar as alterações a partir do momento em que inicia a carga em massa, para manter seus bancos de dados de origem e destino em sincronia.

Opções de modo de preparação da tabela de destino (target):

Do nothing (Não fazer nada)  - O AWS DMS assume que as tabelas de destino foram pré-criadas no destino.

Drop tables on target (Excluir tabelas de destino) - O AWS DMS exclui e recria as tabelas de destino.

Truncate - Se você criou tabelas de destino, o AWS DMS fara o truncates antes de iniciar a migração. Se nenhuma tabela existir e você selecionar essa opção, o AWS DMS criará as tabelas ausentes.

Opções de modo de LOB (Large binary objects), conforme listadas a seguir. 

Não incluir colunas LOB - As colunas LOB são excluídas da migração.

Modo LOB completo - Migrar LOBs completos, independentemente do tamanho. O AWS DMS migra LOBs em partes controladas pelo parâmetro Max LOB Size. Esse modo é mais lento do que usar o modo LOB limitado.

Modo LOB limitado - Truncar LOBs para o valor especificado pelo parâmetro Max LOB Size. Esse modo é mais rápido do que usar o modo LOB completo.

Mapeamentos de tabela – indica as tabelas a serem migradas e como elas são migradas. + info Usando mapeamento de tabela para especificar configurações de tarefa.

Data transformations – + info Specifying table selection and transformations rules using JSON.

Data validation

Amazon CloudWatch logging

Conceitualmente, uma tarefa de replicação do AWS DMS realiza duas funções distintas, como mostrado no diagrama a seguir.


O processo de carga total é fácil de entender. Os dados são extraídos da origem em uma extração em massa e carregados diretamente no destino. Você pode especificar o número de tabelas para extrair e carregar em paralelo no console do AWS DMS em Configurações avançadas.

Replicação contínua ou change data capture (CDC)
O processo de change capture usa ao replicar alterações contínuas de um endpoint  de origem coleta alterações nos logs do banco de dados usando a API nativa da engine do banco de dados.

No processo de CDC, a task de replicação é projetada para transmitir as alterações da origem para o destino, usando buffers em memória para armazenar dados em trânsito. Se os buffers em memória ficarem esgotados por qualquer motivo, a tarefa de replicação irá armazenar as alterações pendentes no Change Cache no disco. Isso pode ocorrer, por exemplo, se o AWS DMS estiver capturando alterações da origem mais rápido do que elas podem ser aplicadas no destino. Nesse caso, você verá a latência do destino da tarefa superar a latência da origem da tarefa.

Você pode verificar isso navegando até a sua tarefa no console do AWS DMS e abrindo a guia "Task Monitoring". Os gráficos "CDCLatencyTarget" e "CDCLatencySource" são exibidos na parte inferior da página. Se você tiver uma tarefa que esteja mostrando latência no destino, é provável que seja necessário ajustar o endpoint de destino para aumentar o application rate.

A task de replicação também usa armazenamento task logs. O espaço em disco que vem pré-configurado com a sua instância de replicação geralmente é suficient. Se você precisar de espaço em disco adicional, por exemplo, ao usar debugging para investigar um problema de migração, você pode aumentar o espaço em disco.

 

Getting started with AWS Database Migration Service
Getting started with AWS Database Migration Service - AWS Database Migration Service 

 