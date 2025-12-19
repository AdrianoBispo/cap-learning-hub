# Briefing de Capacidades do SAP Cloud Application Programming Model (CAP)

Este documento sintetiza as principais capacidades e conceitos do SAP Cloud Application Programming Model (CAP), um framework que visa acelerar o desenvolvimento de aplicações de nível empresarial. A filosofia central do CAP é a modelagem declarativa através do Core Data Services (CDS), que permite capturar a intenção de negócio ("o quê") em vez de detalhes de implementação ("como"). Essa abordagem, combinada com runtimes genéricos para Node.js e Java, automatiza tarefas repetitivas e permite que os desenvolvedores se concentrem na lógica de negócio específica.

As principais capacidades abrangem todo o ciclo de vida da aplicação:

* Modelagem de Domínio: O CDS fornece uma linguagem concisa para modelagem de entidades, associações, tipos e aspectos. Ele suporta nativamente conceitos avançados como dados localizados para internacionalização, dados temporais para consultas de séries temporais ("time-travel") e dados gerenciados para preenchimento automático de campos de ciclo de vida (como createdAt e createdBy).
* Provisão de Serviços: O CAP adota um paradigma centrado em serviços, onde todas as funcionalidades são expostas através de APIs. Os runtimes fornecem implementações genéricas para operações CRUD, consultas complexas via OData (incluindo $filter, $expand, $search, $apply), paginação, controle de concorrência com ETags e bloqueio pessimista. A lógica de negócio personalizada é adicionada através de manipuladores de eventos.
* Consumo de Serviços: O framework facilita a integração com serviços externos (CAP ou OData de terceiros) através da importação de suas definições de API. Isso permite o desenvolvimento local com serviços mockados, a criação de projeções para adaptar as APIs externas e a combinação de dados de múltiplas fontes (mashups).
* Multitenancy e Extensibilidade (MTX): O CAP oferece suporte robusto para aplicações SaaS (Software as a Service) através de serviços dedicados para provisionamento de inquilinos (SaasProvisioningService) e extensibilidade (ExtensibilityService), permitindo que clientes SaaS estendam o modelo de dados e a lógica da aplicação de forma segura e isolada.
* APIs e Interfaces de Usuário: O modelo CDS é a fonte única para a geração automática de APIs OData V4 e V2. Além disso, o CAP possui integração profunda com o SAP Fiori elements, permitindo a criação de UIs ricas e responsivas através de anotações no modelo de serviço. O suporte a rascunho (draft) é uma funcionalidade integrada que melhora a experiência do usuário em aplicações de entrada de dados.
* Implantação e Operações: O CAP foi projetado para ambientes de nuvem, com ferramentas para implantação em runtimes como SAP BTP (Kyma e Cloud Foundry). A integração com SAP HANA Cloud é otimizada, utilizando a SAP HANA Deployment Infrastructure (HDI) para evolução de esquema sem perda de dados e aproveitando recursos nativos do banco de dados, como busca semântica com vector embeddings.
* Funcionalidades Transversais: O framework inclui soluções prontas para uso, como um plugin de auditoria (@cap-js/audit-logging) para registrar eventos de acesso e modificação de dados pessoais e sensíveis, em conformidade com as regulamentações de privacidade de dados.

Em suma, o SAP Cloud Application Programming Model (CAP) oferece um conjunto abrangente e coeso de ferramentas e padrões para a construção de aplicações cloud-native, promovendo a reutilização, a eficiência e a conformidade com as melhores práticas de desenvolvimento.


--------------------------------------------------------------------------------


1. Fundamentos de Modelagem com CDS (Core Data Services)

O CDS é o pilar do CAP, focando em modelos conceituais que descrevem a estrutura e a semântica do domínio de negócio.

1.1. Filosofia Central: Captura de Intenção

A principal diretriz do CDS é capturar a intenção de negócio ("o quê") em vez de detalhes de implementação imperativos ("como"). Isso mantém os modelos de domínio concisos e compreensíveis, permitindo que os runtimes do CAP forneçam implementações genéricas e otimizadas. Aspectos pré-definidos como cuid (para chaves primárias UUID canônicas) e managed (para campos de auditoria como createdAt, createdBy) são exemplos dessa filosofia.

1.2. Modelagem de Domínio e Boas Práticas

O CDS utiliza conceitos de Modelagem Entidade-Relacionamento (ERM) e os enriquece com recursos de Modelagem Orientada a Aspectos.

* Aspectos: Permitem a separação de responsabilidades, decompondo modelos em arquivos separados que podem ser combinados usando diretivas como extend ou annotate. Isso é útil para aplicar anotações de UI, autorização ou outras preocupações transversais sem poluir o modelo de domínio principal.
* Nomenclatura: Recomenda-se capitalizar nomes de tipos e entidades (ex: Books) e usar letras minúsculas para nomes de elementos (ex: title). Nomes devem ser concisos, evitando a repetição do contexto (use Authors.name em vez de Authors.authorName).
* Chaves Primárias: A prática recomendada é usar chaves primárias técnicas, simples e imutáveis. O tipo UUID é preferido por sua unicidade universal, o que facilita a integração entre sistemas. O CAP fornece preenchimento automático para chaves UUID.
* Associações e Composições:
  * Associações Gerenciadas: Para associações to-one, o CAP pode gerenciar automaticamente as chaves estrangeiras, simplificando o modelo.
  * Associações To-Many: Requerem uma condição on explícita para definir a relação de backlink.
  * Composições: Modelam relacionamentos de contenção (parte-de-todo), onde o ciclo de vida da entidade filha está estritamente ligado à entidade pai. Elas são a base para operações de escrita profunda (deep inserts/updates).

1.3. Gestão de Dados Localizados (Modificador localized)

Para suportar dados multilíngues, o CDS utiliza o modificador localized.

* Declaração: Marcar um elemento de entidade com localized (ex: title: localized String;) instrui o compilador a prepará-lo para tradução.
* Mecanismo Interno: Nos bastidores, o CAP cria uma entidade .texts separada para cada entidade com campos localizados. Essa entidade contém a chave primária da entidade original, um campo locale e os campos traduzíveis. Associações texts (composição to-many) e localized (associação to-one) são adicionadas à entidade original. A associação localized filtra automaticamente os textos com base na variável de sessão $user.locale.
* Leitura e Escrita:
  * Para Usuários Finais: As consultas (SELECT from Books) são transparentemente roteadas para uma view SQL gerada (localized.Books) que usa coalesce para buscar o texto no idioma do usuário ou, como fallback, o texto padrão da tabela principal.
  * Para Interfaces de Tradução: A leitura e escrita de todas as traduções são feitas através da associação texts, que é independente do $user.locale.

1.4. Gestão de Dados Temporais (Anotações @cds.valid.from/to)

O CAP oferece suporte nativo para entidades com validade controlada por aplicação, permitindo consultas "as-of-now" e "time-travel".

* Declaração: A anotação @cds.valid.from/to em elementos de data/timestamp (ex: validFrom, validTo) ativa os mecanismos de dados temporais. É comum usar um aspecto reutilizável, como o temporal de @sap/cds/common.
* Estrutura de Dados: A abordagem comum é separar uma entidade "cabeçalho" atemporal (com a chave lógica) de uma entidade de "detalhes" temporal que contém os dados que mudam ao longo do tempo e os campos de validade.
* Consultas:
  * As-of-now: Requisições READ sem parâmetros temporais retornam automaticamente os dados válidos no momento da consulta.
  * Time-travel: Parâmetros de consulta OData como sap-valid-at, sap-valid-from e sap-valid-to podem ser usados para consultar o estado dos dados em diferentes pontos ou períodos no tempo.
  * Dados Temporais Transitivos: Ao expandir através de múltiplas entidades temporais, podem ocorrer resultados redundantes. Isso pode ser resolvido adicionando associações alternativas com condições que alinham os períodos de validade das entidades relacionadas.

1.5. Dados Gerenciados e Variáveis Pseudo

O CAP pode preencher automaticamente campos de auditoria e ciclo de vida.

* Anotações: @cds.on.insert e @cds.on.update instruem os manipuladores genéricos a preencherem um campo na criação e/ou atualização. O aspecto managed de @sap/cds/common agrupa um conjunto padrão desses campos (createdAt, createdBy, modifiedAt, modifiedBy).
* Variáveis Pseudo: São usadas nessas anotações para fornecer os valores:
  * $now: A hora atual do servidor (em UTC).
  * $user: O ID do usuário autenticado.
  * $user.<attr>: Um atributo específico do usuário.
  * $uuid: Um UUID v4 gerado.

2. Camada de Serviço: Provisão e Consumo

O CAP é construído em torno de um paradigma centrado em serviços, onde todas as interações ocorrem como resposta a eventos.

2.1. Definição e Exposição de Serviços

* Serviços como APIs: Uma definição de serviço no CDS (service BookshopService { ... }) declara as entidades e operações que ele expõe, efetivamente definindo sua API pública.
* Serviços como Fachadas: É uma boa prática definir serviços como projeções (projection on my.Books) sobre um modelo de domínio subjacente. Isso desacopla a API pública da estrutura de persistência, permitindo expor visões customizadas para diferentes casos de uso.
* Autoexposição: Entidades anotadas com @cds.autoexpose (geralmente listas de códigos) são automaticamente incluídas nos serviços que as referenciam, facilitando a implementação de listas de valores (value helps) em UIs.

2.2. Provedores Genéricos e Funcionalidades Padrão

Os runtimes CAP fornecem manipuladores genéricos que cobrem a maioria das necessidades de serviço sem a necessidade de codificação.

Funcionalidade	Descrição
Operações CRUD	Suporte completo para GET, POST, PUT, PATCH, DELETE em entidades expostas.
Leituras e Escritas Profundas	Operações de CREATE e UPDATE podem incluir dados para entidades filhas em uma composição (deep insert/update). GET com $expand realiza leituras profundas.
Pesquisa	A anotação @cds.search define quais campos são pesquisáveis. O runtime traduz o parâmetro de consulta OData $search em uma busca eficiente no banco de dados. Em SAP HANA Cloud, suporta busca fuzzy (tolerante a erros).
Paginação	Resultados de leitura são automaticamente paginados (padrão de 1000 registros). A anotação @cds.query.limit permite customizar os limites de paginação em nível global, de serviço ou de entidade.
Controle de Concorrência	Otimista: Ativado com a anotação @odata.etag. O runtime usa ETags para detectar modificações concorrentes e evitar "lost updates".<br>Pessimista: Suportado em bancos de dados como HANA através de bloqueios exclusivos (SELECT ... FOR UPDATE), para cenários onde dados são lidos com a intenção de serem atualizados na mesma transação.

2.3. Lógica Customizada e Validação de Entradas

Quando a lógica genérica não é suficiente, manipuladores de eventos customizados podem ser implementados.

* Validação: Anotações no modelo CDS impõem regras de validação que são verificadas automaticamente pelo runtime:
  * @readonly: Protege campos contra escrita.
  * @mandatory: Garante que um campo não seja nulo.
  * @assert.format: Valida strings contra uma expressão regular.
  * @assert.range: Valida tipos ordinais (números, datas) contra um intervalo [min, max].
  * @assert.target: Verifica se a entidade alvo de uma associação to-one existe no banco de dados.
* Manipuladores de Eventos: Em Node.js (arquivos .js homônimos) ou Java (classes EventHandler), desenvolvedores podem registrar lógica nos hooks on, before e after de eventos CRUD (ex: CREATE, READ) para implementar validações complexas, enriquecer dados ou disparar ações subsequentes.

2.4. Consumo de Serviços Externos

O CAP simplifica a integração com serviços remotos.

1. Importação da API: A especificação da API remota (preferencialmente em formato EDMX para OData) é importada para o projeto, gerando um arquivo CDS que descreve as entidades e operações do serviço.
2. Configuração: O serviço é declarado na seção cds.requires do package.json (Node.js), especificando seu kind (ex: odata-v2) e o caminho para o modelo CDS importado.
3. Mocking Local: Ao executar cds watch, o CAP automaticamente cria um mock server para serviços externos configurados, permitindo o desenvolvimento local desacoplado e rápido. Dados de mock podem ser fornecidos em arquivos .csv.
4. Consumo Programático: A API cds.connect.to('<service-name>') obtém um objeto de serviço para interagir com o serviço remoto (ou seu mock). Consultas podem ser executadas usando CDS Query Language (CQL).
5. Projeções e Mashups: É possível criar projeções locais sobre entidades de serviços remotos para renomear campos ou expor um subconjunto de dados. Manipuladores de eventos são usados para delegar as requisições da projeção local para o serviço remoto, com o CAP tratando do mapeamento de dados.
6. Conectividade e Destinos: Em ambientes de produção, a conexão com sistemas remotos é gerenciada através de Destinos do SAP BTP. A configuração no cds.requires aponta para um destino que contém a URL, credenciais e outros metadados de conexão.

3. Multitenancy, Extensibilidade e Ciclo de Vida (MTX)

O CAP fornece um conjunto de serviços, comumente chamados de MTX, para habilitar aplicações SaaS multitenant. Esses serviços geralmente rodam em um contêiner separado (sidecar).

3.1. Arquitetura e Serviços MTX

* Habilitação: A funcionalidade é ativada através de atalhos de configuração como "multitenancy": true ou "extensibility": true na seção cds.requires.
* Serviços Principais:
  * SaasProvisioningService: Gerencia o ciclo de vida dos inquilinos (tenants).
  * ExtensibilityService: Permite que os inquilinos estendam o modelo de dados da aplicação com campos e entidades customizados.
  * ModelProviderService: Fornece o modelo CDS da aplicação para os outros serviços MTX.

3.2. Configuração e Ciclo de Vida de Inquilinos

O SaasProvisioningService expõe endpoints REST para gerenciar inquilinos, que são tipicamente chamados pela plataforma (ex: SAP BTP SaaS Provisioning).

* subscribe: Cria os recursos necessários para um novo inquilino, como um container HDI dedicado no SAP HANA ou um banco de dados SQLite.
* upgrade: Atualiza o esquema do banco de dados de um inquilino para a versão mais recente da aplicação. No SAP HANA, isso é feito através de evolução de esquema sem perda de dados. No SQLite, geralmente envolve recriar o banco de dados.
* unsubscribe: Remove os recursos do inquilino.

Essas operações podem ser executadas de forma síncrona ou assíncrona (usando o header Prefer: respond-async).

3.3. Restrições de Extensibilidade

O provedor da aplicação pode controlar o que pode ser estendido pelos inquilinos através da configuração extension-allowlist no cds.xt.ExtensibilityService.

* Regras: As regras podem ser aplicadas a namespaces, serviços ou entidades específicas.
* Limites: É possível definir restrições como:
  * Número máximo de novos campos (new-fields).
  * Lista de campos existentes que podem ser estendidos (fields).
  * Número máximo de novas entidades em um serviço (new-entities).
  * Lista de anotações permitidas (annotations).
  * Bloqueio de namespaces inteiros (namespace-blocklist).

4. APIs, Interfaces de Usuário e Eventos

O CAP gera automaticamente interfaces a partir dos modelos CDS.

4.1. Exposição de APIs OData

O CAP tem suporte de primeira classe para OData V4 e V2.

Característica OData	Suporte no CAP
Opções de Consulta	Cobertura abrangente para $select, $expand, $filter, $orderby, $top, $skip, $count, $search.
Agregação de Dados	O $apply é suportado para agregações, permitindo transformações como groupby, aggregate (com métodos sum, min, max, etc.) e filter.
Anotações	Anotações OData para UI (ex: @UI.LineItem), semântica e capacidades podem ser definidas diretamente nos modelos CDS. O framework mapeia a sintaxe do CDS para o formato EDMX XML. Suporta qualificadores (ex: @Common.ValueList#Legal).
Singletons	Entidades podem ser marcadas como @odata.singleton para representar um recurso único.
Tipos Abertos	OData V4 suporta Open Types, permitindo que clientes adicionem propriedades dinâmicas.

4.2. Suporte a Interfaces SAP Fiori

O CAP está profundamente integrado com o SAP Fiori elements.

* Adição de Apps Fiori: As aplicações Fiori são adicionadas ao diretório app/ do projeto CAP. Ferramentas como o SAP Fiori tools (no VS Code ou Business Application Studio) simplificam esse processo.
* Anotações de UI: A aparência e o comportamento das UIs Fiori são controlados por anotações nos modelos de serviço CDS. Os vocabulários mais comuns são @UI, @Common, @Communication. O editor de código fornece code completion e diagnósticos para essas anotações.
* Suporte a Rascunho (Draft):
  * Habilitação: A anotação @odata.draft.enabled em uma entidade de serviço ativa o suporte a rascunho.
  * Funcionamento: As alterações dos usuários são salvas em uma cópia de rascunho no servidor, permitindo que sessões de edição sejam interrompidas e retomadas. A coreografia de rascunho (EDIT, PATCH, ACTIVATE) é gerenciada pelo runtime.
  * Validação: Validações (baseadas em anotações ou customizadas) podem ser executadas durante a edição do rascunho, fornecendo feedback imediato ao usuário.
* Visões Hierárquicas: O CAP suporta a renderização de dados hierárquicos em Tree Tables do Fiori através da anotação @Aggregation.RecursiveHierarchy.

4.3. Publicação de Eventos via AsyncAPI

O CAP pode gerar especificações AsyncAPI a partir de eventos definidos nos modelos CDS.

* Geração: O comando cds compile srv --to asyncapi converte as definições de eventos de um serviço em um documento AsyncAPI.
* Customização: Presets no .cdsrc.json e anotações @AsyncAPI.* no modelo CDS podem ser usados para enriquecer o documento gerado com metadados como title, version, description e extensões específicas do fornecedor (prefixadas com x-).

5. Implantação e Operações

O CAP é projetado para ser implantado em plataformas de nuvem modernas.

5.1. Implantação em Ambientes Cloud Native (SAP BTP, Kyma Runtime)

* Conteinerização: As aplicações CAP são empacotadas como imagens de contêiner (geralmente Docker).
* Orquestração Kubernetes: A implantação no Kyma é gerenciada usando Kubernetes. O CAP fornece ferramentas para gerar a configuração necessária.
* Helm Charts: O comando cds add kyma adiciona um Helm chart ao projeto. O arquivo chart/values.yaml é usado para configurar a implantação, incluindo:
  * Repositório da imagem do contêiner (image.repository).
  * Domínio do cluster (domain).
  * Segredos para acesso a registros privados (imagePullSecret).
  * Configurações de recursos do contêiner (resources), variáveis de ambiente (env) e probes de saúde (health).
  * Bindings para serviços do BTP (bindings).

5.2. Integração e Evolução de Esquema com SAP HANA Cloud

* HDI (HANA Deployment Infrastructure): A implantação no SAP HANA é feita através do HDI. O comando cds build --for hana compila os modelos CDS em artefatos HDI (.hdbtable, .hdbview, etc.).
* Implantação:
  * cds deploy --to hana: Um comando para implantações ad-hoc a partir do ambiente de desenvolvimento local, útil para setups híbridos. Ele compila, cria um container HDI e implanta os artefatos.
  * cf deploy / cf push: Para implantações produtivas, o processo é geralmente gerenciado através de um MTA (Multi-Target Application), que inclui um módulo deployer dedicado para o banco de dados.
* Evolução de Esquema:
  * Para evitar a recriação de tabelas com grandes volumes de dados, entidades podem ser anotadas com @cds.persistence.journal.
  * Isso faz com que o cds build gere artefatos .hdbmigrationtable em vez de .hdbtable.
  * Em compilações subsequentes, o CAP compara o modelo atual com o estado anterior e gera scripts de migração (ex: ALTER TABLE) que são aplicados pelo HDI sem perda de dados para alterações compatíveis. Alterações incompatíveis (ex: reduzir o tamanho de um campo) são geradas como comentários e requerem intervenção manual.

5.3. Funcionalidades Nativas do SAP HANA

O CAP permite o uso de funcionalidades específicas do SAP HANA.

* Vector Embeddings: O tipo cds.Vector(dimensions) permite armazenar e consultar vetores de embeddings diretamente no banco de dados. Funções como cosineSimilarity podem ser usadas em consultas CQL para realizar buscas semânticas, potencializando casos de uso de IA generativa e recomendação.
* Funções Geoespaciais: O CDS suporta a sintaxe para funções espaciais do HANA (ex: ST_GeomFromText).
* Outras Funções: Funções SQL nativas do HANA (ex: current_timestamp, sysuuid()) podem ser usadas em projeções e views.

5.4. Auditoria de Dados (Plugin @cap-js/audit-logging)

O plugin @cap-js/audit-logging oferece suporte pronto para uso para auditoria de dados, especialmente em relação à privacidade.

* Configuração: Adicione o plugin ao projeto (npm add @cap-js/audit-logging) e anote entidades e elementos com @PersonalData.Entity, @PersonalData.Field e @PersonalData.IsPotentiallySensitive.
* Log Automático: O plugin intercepta automaticamente:
  * Operações de escrita que envolvem dados anotados como pessoais.
  * Operações de leitura que envolvem dados anotados como sensíveis.
* Log Customizado: É possível se conectar ao serviço audit-log e enviar eventos de log programaticamente. O serviço define quatro tipos de eventos principais: SensitiveDataRead, PersonalDataModified, SecurityEvent, e ConfigurationModified.
* Integração: Os logs gerados podem ser enviados para o SAP Audit Log Service no SAP BTP para visualização e armazenamento centralizado.

6. Reutilização e Composição de Módulos

O CAP promove a reutilização de conteúdo (modelos, código, dados, UIs) através de pacotes npm (para Node.js) ou Maven (para Java).

6.1. Importação de Conteúdo de Reutilização

Pacotes de reutilização são instalados como dependências padrão do projeto. Uma vez instalados, seu conteúdo pode ser referenciado usando diretivas using from.

* Exemplo: using { CatalogService } from '@capire/bookshop/srv/cat-service'; importa a definição do CatalogService do pacote @capire/bookshop.
* Pontos de Entrada: Pacotes de reutilização podem fornecer um index.cds para facilitar a importação de todo o seu conteúdo com uma única diretiva using from 'package-name';.

6.2. Estratégias de Integração: Embutir vs. Integrar

* Embutir (Embedding): Por padrão, quando o conteúdo é importado, ele se torna parte integrante do projeto consumidor. O serviço, sua implementação e seus dados iniciais são servidos a partir do processo da aplicação principal.
* Integrar (Integrating): Alternativamente, uma aplicação pode consumir um serviço de reutilização como um microserviço remoto. Nesse caso, apenas a definição da API do serviço é importada, e a aplicação é configurada para se conectar a ele em tempo de execução (veja a seção 2.4 sobre Consumo de Serviços).

6.3. Delegação de Chamadas e Testes Locais

Em cenários de mashup onde um serviço local precisa expor dados de um serviço remoto, a delegação de chamadas é usada.

* Implementação: Um manipulador de eventos no serviço local (CatalogService) se conecta ao serviço remoto (ReviewsService) e encaminha a requisição, retornando a resposta do serviço remoto ao cliente original.
* Testes Locais: O CAP simplifica o teste desses cenários. Ao executar cds watch, todos os serviços requeridos são mockados e executados no mesmo processo, permitindo testes de ponta a ponta em um ambiente local de baixa complexidade. Para testar a integração remota real, mas ainda localmente, cada serviço pode ser iniciado em um processo separado, e o cds watch gerencia a descoberta e o binding automático entre eles através do arquivo ~/.cds-services.json.
