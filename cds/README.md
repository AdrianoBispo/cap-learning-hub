# Briefing sobre Core Data Services (SAP CDS)

O Core Data Services (CDS) é a espinha dorsal do SAP Cloud Application Programming Model (CAP), fornecendo uma estrutura declarativa para definir modelos de dados, serviços, consultas e expressões. Através da Conceptual Definition Language (CDL), uma linguagem legível por humanos, os desenvolvedores podem criar modelos de dados complexos e interfaces de serviço de forma concisa. Esses modelos são compilados para o formato canônico Core Schema Notation (CSN), uma especificação aberta baseada em JSON Schema, que serve como uma representação de modelo otimizada e de baixo impacto. Em tempo de execução, os modelos CDS são objetos JavaScript simples que aderem ao CSN, permitindo processamento e criação dinâmicos.

Os principais componentes do ecossistema CDS incluem:

* CDL (Conceptual Definition Language): Para a definição legível de modelos.
* CSN (Core Schema Notation): O formato canônico, similar a JSON, para representação dos modelos.
* CQL (CDS Query Language): Uma extensão do SQL padrão que suporta expressões de caminho, projeções aninhadas e uma sintaxe mais declarativa.
* CQN/CXN (Core Query/Expression Notation): Formatos de objeto JavaScript para representar consultas e expressões de forma programática.

O CDS promove a Modelagem Orientada a Aspectos, uma abordagem poderosa que permite estender definições existentes com novos campos, metadados e anotações sem modificar o código original. Isso facilita a separação de interesses (por exemplo, separar a lógica do domínio principal das anotações de UI) e a reutilização de funcionalidades comuns, como chaves primárias universais (cuid) e campos de auditoria (managed), fornecidos pelo pacote pré-construído @sap/cds/common. A definição de serviços, a exposição de entidades e o tratamento de associações são simplificados, com o framework gerenciando automaticamente tarefas complexas como o redirecionamento de associações em projeções. No geral, o CDS permite a criação de modelos de dados e serviços robustos, interoperáveis e de fácil manutenção, otimizados para o desenvolvimento de aplicações na nuvem.


--------------------------------------------------------------------------------


1. Introdução ao Core Data Services (CDS)

O Core Data Services (CDS) é o framework fundamental do SAP Cloud Application Programming Model (CAP). Ele oferece uma abordagem declarativa para capturar definições de serviço, modelos de dados, consultas e expressões de maneira unificada.

1.1. O Ecossistema CDS

O kit de ferramentas do CDS é projetado para analisar diversas linguagens de origem e compilá-las em vários formatos de destino, garantindo flexibilidade e interoperabilidade.

* Linguagens de Origem: Os modelos podem ser definidos em CDL (.cds), YAML ou JSON.
* Formato Canônico: Todas as fontes são analisadas e transformadas em um formato uniforme chamado Core Schema Notation (CSN). O CSN é uma especificação aberta, derivada do JSON Schema, que representa modelos CDS como objetos JavaScript simples. Esta natureza dinâmica permite que os modelos sejam processados e até mesmo criados em tempo de execução.
* Linguagens de Destino: A partir do CSN, o compilador pode gerar artefatos para diferentes destinos, como:
  * Serviços: OData, OpenAPI, AsyncAPI.
  * Persistência: SQL DDL, HANA DDL.
  * Outros: JSON, YAML.

1.2. Principais Notações e Linguagens

O CDS é composto por um conjunto de especificações que trabalham juntas:

Componente	Sigla	Descrição
Definition Language	CDL	A linguagem principal, legível por humanos, para modelar dados e serviços em arquivos .cds.
Schema Notation	CSN	O formato canônico para representar modelos CDS como objetos JavaScript, semelhante ao JSON Schema.
Query Language	CQL	Uma extensão do SELECT do SQL padrão para realizar consultas sobre modelos CDS.
Query Notation	CQN	A representação de consultas como objetos JavaScript simples, para uso programático.
Expression Notation	CXN	A representação de expressões como objetos JavaScript simples.

2. Conceptual Definition Language (CDL)

A CDL é a linguagem legível por humanos para definir modelos CDS em arquivos com a extensão .cds. Esses arquivos são compilados para a representação CSN para processamento em tempo de execução.

2.1. Fundamentos da Linguagem

Palavras-chave e Identificadores

* Palavras-chave: Usadas para iniciar declarações como entity, service, using. Elas não são sensíveis a maiúsculas/minúsculas, mas por convenção são usadas em minúsculas.
* Identificadores: Usados para nomear e referenciar definições. Eles são sensíveis a maiúsculas/minúsculas (Foo e foo são diferentes). Devem seguir o padrão ^[$A-Za-z_]\w*$, ou podem ser delimitados com ![...], embora esta prática deva ser evitada por questões de interoperabilidade.

Tipos de Dados Embutidos

O CDS fornece um conjunto de tipos de dados primitivos que são mapeados para os tipos correspondentes no banco de dados durante a implantação.

Tipo CDS	Observações	Mapeamento ANSI SQL (Exemplo)
UUID	CAP gera UUIDs compatíveis com RFC 4122.	NVARCHAR(36)
Boolean	Valores true, false, null, 0, 1.	BOOLEAN
Integer	Equivalente a Int32 por padrão.	INTEGER
Int16, Int32, Int64	Inteiros com sinal de 16, 32 e 64 bits.	SMALLINT, INTEGER, BIGINT
UInt8	Inteiro sem sinal de 8 bits (0-255).	TINYINT
Decimal(p,s)	Tipo decimal de ponto flutuante.	DECIMAL
Double	Ponto flutuante com mantissa binária.	DOUBLE
Date, Time	Apenas data (ex: 2022-12-31) ou hora (ex: 23:59:59).	DATE, TIME
DateTime, Timestamp	Data e hora. Timestamp tem precisão de microssegundos.	TIMESTAMP
String(len)	Comprimento padrão 255 (HANA: 5000).	NVARCHAR
Binary(len)	Comprimento padrão 255 (HANA: 5000).	VARBINARY
LargeBinary	Dados binários ilimitados (streaming).	BLOB
LargeString	Dados de texto ilimitados (streaming).	NCLOB
Map	Mapeado para NCLOB no HANA; tipo JSON.	NCLOB
Vector(dim)	Requer SAP HANA Cloud QRC 1/2024 ou posterior.	REAL_VECTOR

Literais

A CDL suporta literais semelhantes aos de JavaScript, Java e SQL, incluindo:

* Booleanos: true, false, null
* Números: 11, 2.4, 1e3
* Strings: 'Uma string',  Uma string \n com escapes , ```Uma string multilinha```
* Registros: { foo:'boo', bar:'car' }
* Arrays: [ 1, 'two', {three:4} ]
* Data/Hora: date'2016-11-24', time'16:11:32', timestamp'2016-11-24T12:34:56.789Z'

Importação de Modelos (using)

A diretiva using permite importar definições de outros modelos CDS, funcionando de forma semelhante ao require do Node.js ou import do ES6. A resolução de módulos segue as regras do Node.js (caminhos relativos com ./, absolutos com /, ou referências de módulo como @sap/cds/common resolvidas em node_modules).

Namespaces e Contextos

* namespace: Prefixa todas as definições subsequentes em um arquivo com um nome qualificado.
* context: Permite aninhar seções de namespace, criando uma estrutura hierárquica para as definições.

Comentários

A CDL suporta comentários de linha (//), de bloco (/* ... */) e de documentação (/** ... */). Comentários de documentação são armazenados na propriedade doc do CSN e podem ser traduzidos para a anotação @Core.Description em OData ou para a cláusula COMMENT em tabelas e colunas HANA.

2.2. Definições de Entidades e Tipos

Entidades e Tipos

* Entidades (entity): Representam tipos estruturados de dados persistentes, com elementos nomeados e tipados, e geralmente uma ou mais chaves primárias. São a base para operações CRUD.
* Tipos (type): Permitem declarar tipos customizados (simples, estruturados ou associações) para reutilização, como em elementos de entidades.

Tipos Estruturados e "Arrayed"

* Estruturados: Tipos podem ser definidos com múltiplos elementos internos, criando estruturas complexas. Podem ser definidos nominalmente (type Amount { ... }) ou inline dentro de uma entidade.
* "Arrayed" (many): O prefixo many ou array of indica que um elemento é uma coleção de um tipo. Em bancos de dados SQL, são mapeados para colunas LargeString e armazenados como um array JSON.

Elementos Virtuais e Calculados

* Virtuais (virtual): Elementos marcados como virtual não são persistidos no banco de dados, mas fazem parte dos metadados OData. Por padrão, são somente leitura (@Core.Computed: true), mas podem ser tornados graváveis com @Core.Computed: false. Seus valores devem ser preenchidos programaticamente em handlers after.
* Calculados: Elementos cujo valor é derivado de uma expressão.
  * "On-read": A expressão é avaliada no momento da leitura. É uma conveniência para evitar a repetição de expressões em consultas.
  * "On-write" (stored): A expressão é avaliada no momento da escrita, e o resultado é persistido como um campo regular. Isso pode melhorar o desempenho de filtros e ordenação ao custo de maior consumo de armazenamento.

2.3. Views e Projeções

Views e projeções permitem derivar novas entidades a partir de existentes, similarmente às views em SQL.

* as select from: Permite usar todo o poder da CQL, incluindo JOINs, UNIONs e cláusulas complexas, sendo traduzido para uma SQL view no banco de dados.
* as projection on: Uma variante mais restrita, indicando que a consulta não usa a totalidade dos recursos SQL (sem JOINs ou UNIONs manuais). É útil para expor entidades de serviços OData externos.

A assinatura da view (seus elementos e tipos) é inferida da projeção. As chaves primárias da entidade base são herdadas se todos os seus elementos-chave forem selecionados e não houver expressões de caminho com associações "to-many".

2.4. Associações e Composições

Associações capturam relacionamentos entre entidades.

* Não Gerenciadas (Unmanaged): Exigem uma cláusula on explícita que define a condição de junção usando chaves estrangeiras existentes.
* Gerenciadas (Managed): O CDS infere a condição de junção e adiciona automaticamente os elementos de chave estrangeira necessários com base nas chaves primárias da entidade alvo. É a forma preferencial para associações "to-one".
* "To-many": Usam uma cláusula on com o padrão <assoc>.<backlink> = $self, onde backlink é uma associação "to-one" na entidade alvo que aponta de volta para a origem.
* Composições (Composition): Um tipo especial de associação que denota uma relação de "contido em", formando estruturas de documento (pai-filho). O ciclo de vida do filho está ligado ao do pai. Podem ser gerenciadas, onde o CDS cria automaticamente a entidade de item de linha (Orders.Items) e o relacionamento.

2.5. Modelagem Orientada a Aspectos

Aspectos são um mecanismo poderoso para estender definições de forma flexível, baseado em uma abordagem de "mixin".

* extend: Adiciona campos, ações ou anotações a uma definição existente. Permite, por exemplo, aumentar o tamanho de um campo String.
* annotate: Um atalho para extend usado exclusivamente para adicionar ou sobrescrever anotações.
* Aspectos Nomeados (aspect): Permitem definir um conjunto de campos, ações e anotações reutilizáveis que podem ser aplicados a múltiplas entidades.
* Sintaxe de Inclusão (:): entity Foo : SomeAspect é um atalho sintático para extend Foo with SomeAspect, simulando uma herança múltipla.

2.6. Anotações

Anotações (@) adicionam metadados a qualquer definição no modelo CDS.

* Sintaxe: Prefixo @, podem ser colocadas antes, depois ou no final de uma definição.
* Alvos: Podem anotar serviços, entidades, elementos, enums, parâmetros, etc.
* Valores: Podem ser literais (true, 'foo'), referências a outros elementos (foo.bar), expressões ((foo.bar * 17)) ou arrays.
* Propagação: Anotações são herdadas de tipos base para tipos derivados. Uma conversão de tipo (cast) explícita em uma projeção interrompe a herança.
* Extensão de Arrays: A sintaxe de elipse (...) permite adicionar novos valores a um array de anotação existente (@anArray: [1, 2, ...]) em vez de sobrescrevê-lo.

2.7. Serviços

Serviços são definidos usando o bloco service e atuam como um context que agrupa um conjunto de entidades expostas como um endpoint de API.

* Exposição de Entidades: Entidades podem ser expostas diretamente ou através de projeções (as projection on). Anotações como @readonly podem restringir as operações permitidas.
* Redirecionamento de Associações: Quando entidades relacionadas são expostas em um serviço, suas associações são automaticamente redirecionadas para apontar para as projeções dentro do mesmo serviço, garantindo que a navegação funcione corretamente. Ambiguidades podem ser resolvidas com redirected to.
* Autoexposição (@cds.autoexpose): Entidades marcadas com esta anotação são automaticamente expostas como readonly em qualquer serviço que se associe a elas.
* Ações e Funções: Serviços e entidades podem definir ações (que modificam o estado) e funções (que retornam dados) customizadas, que podem ser vinculadas (bound) a uma entidade ou não vinculadas (unbound).
* Eventos: Serviços podem declarar eventos que emitem para canais de mensageria.

3. Formatos Canônicos (CSN, CQN, CXN)

Enquanto a CDL é a interface humana, os formatos canônicos são as representações de máquina usadas pelo framework.

3.1. Core Schema Notation (CSN)

CSN é a representação compacta de modelos CDS, otimizada para ser compartilhada e interpretada com o mínimo de dependências. Um modelo CSN é um objeto (JSON, YAML ou JavaScript) com as seguintes propriedades principais:

* definitions: Um dicionário de todas as definições nomeadas (entidades, tipos, serviços) com seus nomes totalmente qualificados como chaves.
* extensions: Um array de extensões ou anotações não aplicadas (extend ou annotate).
* requires: Um array de modelos importados.

Cada definição no CSN possui propriedades que descrevem sua natureza:

* kind: O tipo da definição (entity, service, type, etc.).
* elements: Um dicionário de elementos para tipos estruturados.
* type: O tipo base de uma definição.
* Anotações: Representadas como propriedades com prefixo @.
* query ou projection: Contém a representação CQN de uma view.
* target: Para associações, especifica a entidade alvo.

3.2. Query/Expression Notation (CQN/CXN)

* CQN (Core Query Notation): É a representação de consultas como objetos JavaScript. Uma consulta SELECT, por exemplo, é um objeto com uma propriedade SELECT que contém from, columns, where, etc. Isso permite a construção e manipulação programática de consultas.
* CXN (Core Expression Notation): É a representação de expressões individuais. Literais são representados com {val: ...}, referências com {ref: [...]} e expressões de operador com {xpr: [...]} (uma sequência de operandos e operadores em string).

4. CDS Query Language (CQL)

CQL é uma extensão do SQL padrão, projetada para funcionar nativamente com modelos CDS.

* Projeções Pós-fixadas: Permitem uma sintaxe mais fluida, onde a cláusula SELECT vem após o FROM, envolvida por chaves (SELECT from Authors { name, address.street }).
* Expansões e Inlines Aninhados: Projeções pós-fixadas podem ser aninhadas para expandir associações (author { name }) ou para embutir campos de uma estrutura ou associação (author.{ name, dateOfBirth }), simplificando a leitura de dados estruturados profundos.
* Seletor * Inteligente e Cláusula excluding: O seletor * em CQL substitui colunas inferidas por colunas definidas explicitamente com o mesmo nome. A cláusula excluding permite selecionar todos os campos, exceto alguns específicos (SELECT from Books { * } excluding { author }).
* Expressões de Caminho: Permitem navegar através de associações em qualquer cláusula SQL (SELECT title, author.name from Books). O CDS traduz essas expressões para os JOINs apropriados (SEMI JOIN em cláusulas from, LEFT OUTER JOIN em outras cláusulas).

5. Tipos e Aspectos Comuns (@sap/cds/common)

O CDS inclui um modelo pré-construído, @sap/cds/common, que fornece tipos e aspectos reutilizáveis para promover consistência e boas práticas.

5.1. Aspectos Reutilizáveis

* cuid: Adiciona uma chave primária canônica do tipo UUID chamada ID.
* managed: Adiciona quatro campos de auditoria (createdAt, createdBy, modifiedAt, modifiedBy) que são preenchidos automaticamente pelo runtime.
* temporal: Adiciona os campos validFrom e validTo para suportar dados com validade temporal.

5.2. Tipos e Listas de Códigos

@sap/cds/common define tipos reutilizáveis como Country, Currency e Language. Estes são definidos como associações a entidades de "lista de códigos" correspondentes (Countries, Currencies, Languages).

O aspecto CodeList é a base para essas entidades, fornecendo campos localizáveis (localized) para name e descr. A palavra-chave localized faz com que o CDS gere automaticamente uma entidade .texts associada (ex: Countries.texts) para armazenar as traduções, com uma view que combina os textos para a localidade do usuário.

6. Modelagem Orientada a Aspectos e a Natureza dos Modelos

6.1. Princípios de Modelagem

A abordagem de aspectos do CDS é semelhante à Programação Orientada a Aspectos (AOP), permitindo aumentar a modularidade pela separação de interesses transversais.

* Separação de Interesses: Em vez de poluir modelos de domínio com anotações de UI, estas podem ser fatoradas em arquivos separados usando annotate.
* Reutilização: Em vez de hierarquias de herança rígidas, aspectos reutilizáveis (cuid, managed) podem ser combinados de forma flexível.
* Customização: Definições de pacotes reutilizados podem ser adaptadas e estendidas com novos campos, associações ou aspectos, o que é fundamental para cenários de customização e verticalização de software.

6.2. A Natureza dos Modelos CDS

Um modelo é uma descrição de algo. No CDS, eles podem ter diferentes representações:

* Representações: A CDL é a sintaxe para representação legível por humanos, enquanto o CSN é a notação de objeto para representação por máquina.
* Reflexões: A compilação de um modelo CDS (CSN) para outros formatos como SQL DDL ou OData EDMX é uma "reflexão". É uma transformação que pode envolver perda de informação, pois cada formato de destino cobre apenas uma parte do modelo original (por exemplo, SQL DDL foca apenas na persistência).

Fundamentalmente, os modelos CDS são objetos JavaScript simples que aderem ao CSN. Eles podem ser criados a partir de fontes .cds, lidos de arquivos .json, ou construídos dinamicamente em tempo de execução, oferecendo um sistema de modelagem aberto e extensível.
