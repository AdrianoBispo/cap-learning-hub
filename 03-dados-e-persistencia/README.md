# 03. Dados e Persistência

O CAP abstrai a complexidade do SQL através de APIs fluentes e agnósticas de banco de dados. Este módulo cobre como interagir com seus dados de forma programática.

## Conteúdo

### 1. Queries (CQL e CQN)
*   **CQL (CDS Query Language):** Uma linguagem de consulta poderosa que evolui o SQL. Permite projeções aninhadas, *path expressions* para navegar associações e *infix filters*.
*   **CQN (Core Query Notation):** A representação em objetos JavaScript das queries. O `cds.ql` fornece uma API fluente (ex: `SELECT.from('Books')`) para construir CQN de forma segura contra SQL Injection.

### 2. Drivers e Serviços de DB
O serviço primário de banco de dados é acessível via `cds.db`. O CAP suporta nativamente **SQLite** para desenvolvimento local (in-memory ou arquivo) e **SAP HANA Cloud** para produção, gerenciando automaticamente pools de conexão e transações.

### 3. Localização e Dados Temporais
*   **Localização:** O modificador `localized` gera automaticamente tabelas de textos e views que resolvem o idioma do usuário em tempo de leitura.
*   **Dados Temporais:** O aspecto `:temporal` habilita consultas de "viagem no tempo" e gerenciamento de validade de registros (`validFrom`, `validTo`).
