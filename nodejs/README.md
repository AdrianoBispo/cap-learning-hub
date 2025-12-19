# Análise Abrangente do CAP Node.js Runtime

Este documento sintetiza os principais conceitos, APIs e melhores práticas do SAP Cloud Application Programming Model (CAP) para o ambiente Node.js. A análise abrange desde a definição e consumo de serviços, manipulação de dados e transações, até aspectos operacionais como autenticação, logging, testes e segurança. O runtime do CAP oferece um framework robusto e automatizado que gerencia grande parte da complexidade do desenvolvimento de aplicações, permitindo que os desenvolvedores foquem na lógica de negócio.

Os principais pontos abordados incluem:

* Arquitetura de Serviços: O CAP distingue diferentes tipos de serviços, como cds.ApplicationService (para lógica de negócio com handlers genéricos), cds.DatabaseService (para persistência) e cds.RemoteService (para consumo de APIs externas), cada um com configurações e funcionalidades específicas.
* Manipulação de Dados e Consultas: A biblioteca cds.ql fornece uma API fluente e segura para construir e executar consultas (CQN), protegendo contra injeção de SQL por padrão e tratando consultas como objetos de primeira classe que podem ser compostos e reutilizados.
* Gestão de Transações e Contexto: O framework gerencia transações de banco de dados (ACID) automaticamente. O cds.context utiliza o async local storage do Node.js para propagar informações de contexto (usuário, tenant, locale) ao longo da cadeia de chamadas, garantindo isolamento e consistência. Para casos de uso avançados, APIs como cds.tx() e cds.spawn() oferecem controle manual sobre transações e jobs em background.
* Autenticação e Autorização: Uma gama de estratégias de autenticação é fornecida, desde mocked para desenvolvimento até jwt, xsuaa e ias para produção. A identidade do usuário é representada pela classe cds.User, que é fundamental para a aplicação de regras de autorização definidas no modelo CDS.
* Operações e Melhores Práticas: O CAP inclui uma fachada de logging (cds.log) que se adapta a ambientes de desenvolvimento e produção, uma biblioteca de testes (@cap-js/cds-test) que facilita testes de API e HTTP, e um conjunto de melhores práticas para gerenciamento de dependências, segurança da aplicação (CSP, CSRF, CORS) e tratamento de erros.

1. Arquitetura e Tipos de Serviço

O CAP Node.js estrutura a lógica da aplicação em serviços, que são proxies para diferentes tipos de funcionalidades. Cada serviço estende a classe base cds.Service.

1.1. cds.ApplicationService

É a implementação padrão para provedores de serviço, adicionando handlers genéricos que automatizam funcionalidades comuns.

* Inicialização: Os handlers genéricos são registrados no método init() da classe, chamando métodos estáticos com o prefixo handle_.
* Handlers Genéricos:
  * handle_authorization(): Aplica verificações de autorização com base nas anotações do modelo CDS.
  * handle_etags(): Implementa controle de concorrência usando ETags.
  * handle_validations(): Realiza validações de entrada com base em anotações como @assert.
  * handle_temporal_data(): Gerencia dados temporais.
  * handle_localized_data(): Suporta dados localizados.
  * handle_managed_data(): Automatiza o preenchimento de campos de auditoria (criado por/em, modificado por/em).
  * handle_paging(): Adiciona paginação e ordenação implícita.
  * handle_fiori(): Gerencia funcionalidades específicas de Fiori, como rascunhos (Drafts).
  * handle_crud(): Implementa as operações CRUD (Create, Read, Update, Delete), incluindo operações profundas.
* Customização: É possível sobrescrever ou adicionar novos handlers estáticos (handle_*) para estender ou modificar o comportamento padrão.

1.2. cds.DatabaseService

Representa serviços técnicos para armazenamento persistente e interage diretamente com o banco de dados.

* Gerenciamento de Transações: O framework chama automaticamente o método $srv.begin() para adquirir uma conexão do pool e iniciar uma transação (ex: BEGIN TRANSACTION) na primeira consulta.
* Resultado de Inserção (InsertResult): Operações INSERT retornam um objeto InsertResult (atualmente em beta) que contém:
  * Um iterador para as chaves das entradas criadas.
  * affectedRows: O número de registros inseridos.
* Pool de Conexões: Utiliza generic-pool para reutilizar conexões de banco de dados, melhorando a performance. A configuração do pool pode ser ajustada com os seguintes parâmetros:
  * acquireTimeoutMillis: Tempo máximo de espera para obter uma conexão.
  * min / max: Número mínimo e máximo de conexões no pool.
  * idleTimeoutMillis: Tempo que uma conexão pode permanecer ociosa antes de ser removida.
  * fifo: Define a estratégia de alocação (LIFO ou FIFO).
* Operação UPSERT:
  * Caso de Uso: Principalmente para replicação de dados. Atualiza registros existentes ou insere novos.
  * Semântica: Possui semântica de "PATCH", atualizando apenas os valores fornecidos.
  * Requisitos: Os dados devem conter todos os elementos da chave da entidade. Não possui cláusula where.
  * Tradução: É traduzido para comandos nativos do banco de dados (UPSERT no SAP HANA, INSERT ON CONFLICT no SQLite).
  * Limitações: UUIDs não são gerados e handlers genéricos do CAP (como auditoria) não são invocados. Deep upserts não são suportados no runtime de Node.js.

1.3. cds.RemoteService

É uma classe proxy para consumir serviços remotos através de diferentes protocolos, como OData ou REST.

* Configuração: As configurações são feitas na seção cds.requires do package.json.
* Manipulação de CSRF-Token: Pode ser habilitada para serviços que a exigem, utilizando as opções csrf e csrfInBatch.
  * Básica: csrf: true e csrfInBatch: true.
  * Avançada: Permite customizar o método HTTP (method) e a URL (url) para obter o token.
* Timeout: A opção requestTimeout define o tempo máximo de espera (em milissegundos) por uma resposta do serviço remoto. O padrão é 60000 ms.

2. Eventos, Requisições e Contexto

O fluxo de execução no CAP é orientado a eventos. As classes cds.EventContext, cds.Event e cds.Request formam a base para representar o contexto e os dados de uma invocação.

2.1. cds.context

Uma propriedade de acesso global (continuation-local) que fornece acesso ao cds.EventContext atual de qualquer lugar do código. É implementada usando a técnica de async local storage do Node.js.

* Propriedades Acessíveis: tenant, user, locale, id, timestamp, http.
* Uso: Embora conveniente, é recomendado acessar essas propriedades através do objeto req local nos handlers para evitar o overhead de AsyncLocalStorage.getStore().

2.2. cds.EventContext

Representa o contexto de invocação de requisições e mensagens de evento. cds.Event e cds.Request herdam desta classe.

* Propriedades Chave:
  * .http: Acesso aos objetos req e res do Express, se a requisição veio de um canal HTTP.
  * .id: Um ID de correlação único, propagado através do cabeçalho x-correlation-id.
  * .locale: O locale do usuário, extraído do cabeçalho Accept-Language.
  * .tenant: O identificador do tenant atual (se em modo multitenant).
  * .timestamp: Um Date constante para a requisição, usado para preencher a variável $now.
  * .user: O usuário autenticado, uma instância de cds.User.

2.3. cds.Event

Representa mensagens de evento em cenários de mensageria assíncrona e é a classe base para cds.Request.

* Propriedades:
  * .event: O nome do evento (ex: CREATE, READ, OrderedBook).
  * .data: O payload do evento (ex: corpo da requisição HTTP).
  * .headers: Os cabeçalhos da mensagem ou requisição.
* Eventos de Ciclo de Vida: Permite registrar handlers para o final do ciclo de vida da requisição.
  * before('commit'): Executado imediatamente antes do commit, pode vetar a requisição.
  * on('succeeded'): Executado após o commit bem-sucedido.
  * on('failed'): Executado após um rollback.
  * on('done'): Executado ao final, independentemente do resultado.
  * Aviso: Os eventos succeeded, failed e done ocorrem fora da transação gerenciada pelo framework.

2.4. cds.Request

Estende cds.Event com funcionalidades para requisições síncronas.

* Propriedades Adicionais:
  * .method: Mapeia o evento CRUD para um método HTTP (ex: CREATE → POST).
  * .target: A definição da entidade alvo da requisição.
  * .path: O caminho completo da requisição, incluindo navegações.
  * .entity: Um atalho para req.target.name.
  * .params: Acesso aos parâmetros da URL.
  * .query: A requisição de entrada capturada como uma consulta CQN.
  * .subject: Um ponteiro para a instância específica alvo de uma requisição (para READ, UPDATE, DELETE em um único registro).
* Métodos de Resposta:
  * req.reply(results): Envia uma resposta bem-sucedida. Retornar um valor do handler tem o mesmo efeito.
  * req.reject({...}): Constrói e lança um erro, rejeitando a requisição. Aceita um objeto com status, code, message, target, etc.
  * req.error({...}): Registra um erro para ser enviado posteriormente, sem interromper o fluxo imediatamente. Os erros são coletados em req.errors.
  * req.warn(), req.info(), req.notify(): Registram mensagens informativas que são enviadas junto com uma resposta bem-sucedida, geralmente em cabeçalhos HTTP como sap-messages.

3. Consultas com cds.ql

O módulo cds.ql fornece uma API para construir consultas em Core Query Notation (CQN) de forma segura e flexível.

3.1. Construção de Consultas

Existem quatro formas principais de construir consultas:

1. API Fluente: SELECT.from('Books').where({ID:201})
2. Tagged Template Literals (TTL): cds.ql \SELECT from Books where ID=${201}``
3. API Fluente com TTLs: SELECT.from \Books`.where`ID=${201}``
4. Objetos CQN Manuais: Construção direta de objetos JSON que representam a consulta.

Segurança: A API é projetada para evitar Injeção de SQL por padrão. Os valores passados em TTLs ou na API fluente são tratados como parâmetros de bind, e não por concatenação de strings.

3.2. Execução de Consultas

* srv.run(query): Executa uma consulta em um serviço específico (ex: cds.db.run(query)).
* await query: Uma consulta construída é "thenable" e pode ser aguardada diretamente, o que a executa no serviço de banco de dados primário (cds.db).
* API de Conveniência CRUD: db.read('Books').where(...).

Consultas são objetos de primeira classe e podem ser atribuídas a variáveis, modificadas e compostas, permitindo a criação de consultas complexas e otimizadas (ex: late materialization).

3.3. Classes de Consulta da API

A API cds.ql fornece classes globais para cada tipo de operação:

Classe	Métodos Principais	Descrição
SELECT	.from(), .columns(), .where(), .orderBy(), .limit(), .forUpdate()	Constrói consultas de leitura. Suporta projeções complexas, filtros, ordenação, paginação e bloqueio de registros.
INSERT	.into(), .entries(), .values(), .rows(), .from()	Constrói operações de inserção. Pode inserir múltiplos registros de um array, stream ou subconsulta.
UPSERT	.into(), .entries()	Constrói operações de "update or insert".
UPDATE	.entity(), .set() ou .with(), .where()	Constrói operações de atualização.
DELETE	.from(), .where()	Constrói operações de exclusão.

4. Gerenciamento de Transações

O CAP gerencia automaticamente transações de banco de dados, propagação de contexto e isolamento de tenants.

* Transações Automáticas: Para qualquer operação de serviço (ex: db.read()), o framework garante que ela se junte a uma transação existente ou crie uma nova. Dentro de um event handler, o código sempre está em uma transação.
* Transações Aninhadas: Chamadas para outros serviços dentro de um handler criam transações aninhadas, que são sincronizadas (commit/rollback) com a transação raiz. No entanto, não são transações distribuídas atômicas.
* Transações Manuais com srv.tx(): Para casos onde múltiplas operações precisam ser executadas em uma única transação fora de um handler, cds.tx() pode ser usado.
  * Com Bloco de Função: cds.tx(async (tx) => { ... }) cria uma transação, executa o código e realiza commit/rollback automaticamente.
  * Sem Bloco de Função: const tx = cds.tx() retorna um objeto de transação que deve ser manualmente finalizado com tx.commit() ou tx.rollback().
* Jobs em Background com cds.spawn(): Executa uma função como uma continuação desacoplada, em uma nova transação raiz e com um contexto específico. Útil para tarefas que devem ser executadas fora da transação da requisição atual.

5. Autenticação

O CAP integra-se a middlewares de autenticação que preenchem cds.context.user, permitindo a aplicação de regras de autorização.

5.1. Classe cds.User

Representa o usuário autenticado.

* Propriedades:
  * .id: O ID único do usuário.
  * .attr: Atributos do usuário (ex: de um token JWT).
  * .authInfo: Informações específicas da biblioteca de autenticação (ex: SecurityContext do @sap/xssec).
* Método .is(<role>): Verifica se o usuário possui uma determinada role.
* Subclasses:
  * cds.User.Privileged: Um usuário que passa em todas as verificações de autorização.
  * cds.User.Anonymous: Um usuário anônimo.

5.2. Estratégias de Autenticação

Configuradas em cds.requires.auth.

Estratégia	Descrição	Configuração (kind)
Dummy	Cria um usuário que passa em todas as verificações. Útil para desabilitar temporariamente a segurança.	dummy
Mocked	Autenticação básica com usuários pré-definidos em package.json. Padrão em desenvolvimento.	mocked
Basic	Autenticação básica similar à mocked, mas sem usuários padrão.	basic
JWT	Padrão em produção. Valida um JWT token de um serviço UAA. Requer @sap/xssec.	jwt
XSUAA	Estratégia baseada em XSUAA que também fornece acesso a atributos SAML. Requer @sap/xssec.	xsuaa
IAS	Usa o Identity Authentication Service (IAS). Requer @sap/xssec.	ias
Custom	Permite implementar uma lógica de autenticação personalizada através da propriedade impl.	N/A

5.3. Configuração em Produção (XSUAA Hybrid Setup)

Para testar a autenticação XSUAA localmente (modo híbrido), são necessários os seguintes passos:

1. Preparar o Ambiente Local: Fazer login no Cloud Foundry via CLI.
2. Configurar a Aplicação: Usar cds add xsuaa --for hybrid, ajustar o xs-security.json e criar uma instância de serviço XSUAA e uma chave de serviço.
3. Fazer o Binding: Usar cds bind para conectar a aplicação localmente à chave de serviço, o que cria um arquivo .cdsrc-private.json.
4. Configurar Roles: Criar uma "Role Collection" no SAP BTP Cockpit para atribuir as roles definidas no xs-security.json aos usuários.
5. Executar com App Router: Adicionar e executar o App Router, que gerencia o fluxo de login interativo e encaminha o token JWT para a aplicação CAP.

6. Logging com cds.log

O CAP fornece uma fachada de logging minimalista para unificar a saída de logs.

* Obtenção de um Logger: const LOG = cds.log('sql'). Loggers com o mesmo ID são compartilhados.
* Níveis de Log: SILENT, ERROR, WARN, INFO, DEBUG, TRACE. Podem ser configurados no package.json em cds.log.levels.
* Formato de Log:
  * Desenvolvimento (Padrão): Formato "plain", legível para humanos (ex: [cds] - server listening...).
  * Produção (Padrão): Formato JSON, estruturado para ser consumido por serviços de logging como SAP Cloud Logging ou SAP Application Logging Service (Kibana).
* Integração: Pode ser integrado com frameworks avançados como winston através da fábrica cds.log.Logger.
* Correlação de Requisições: O formatador JSON inclui o correlation_id (de cds.context.id) nos logs, permitindo rastrear uma requisição através de múltiplos componentes.

7. Testes com @cap-js/cds-test

Uma biblioteca de utilitários para escrever testes para aplicações CAP Node.js.

* Execução de Servidor: cds.test() inicia um servidor CAP em um hook beforeAll() e o desliga em afterAll(), simplificando a configuração dos testes.
* Testes de API de Serviço: Como o servidor roda no mesmo processo, os serviços podem ser acessados programaticamente via cds.connect.to().
* Testes de API HTTP: Fornece métodos como GET, POST, etc., que são funções vinculadas ao cliente HTTP (axios) pré-configurado com a URL base do servidor.
* Autenticação: Usa a estratégia mocked por padrão, permitindo passar credenciais de mock nas chamadas HTTP (ex: GET('/admin/Books', { auth: { username: 'alice' } })).
* Portabilidade: Projetado para funcionar com runners como Jest e Mocha, utilizando a biblioteca de asserção Chai (acessível via test.expect).

8. Melhores Práticas

O documento de referência destaca várias práticas recomendadas para o desenvolvimento robusto de aplicações CAP.

* Gerenciamento de Dependências:
  * Usar faixas de versão abertas (^) para receber os últimos patches e features.
  * Fixar dependências com package-lock.json antes de fazer o deploy em produção.
  * Minimizar o uso de pacotes de código aberto para reduzir a superfície de vulnerabilidades.
* Segurança da Aplicação:
  * CSP (Content Security Policy): Implementar usando middlewares como helmet.
  * CSRF (Cross-Site Request Forgery): A proteção é habilitada por padrão ao usar o App Router.
  * CORS (Cross-Origin Resource Sharing): Configurar no App Router ou via middleware customizado no CAP para ambientes de produção.
* Tratamento de Erros:
  * Adotar a filosofia "Let it crash" para erros de programação inesperados, garantindo que a aplicação reinicie em um estado limpo.
  * Não ocultar a origem dos erros; ao relançar exceções, preservar a informação original.
