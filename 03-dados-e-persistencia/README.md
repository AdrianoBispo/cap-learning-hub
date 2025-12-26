# Módulo 3: Dados e Persistência

![Infografico - Guia Rapido de Banco de Dados SAP CAP com Node.js](./Infograficos/03.02.01_Banco_de_Dados_Enterprise.png)

Com os modelos definidos e os serviços em execução, é hora de interagir com os dados. Este módulo mergulha fundo na camada de persistência do SAP CAP, mostrando como consultar e manipular dados de forma eficiente e segura.

Você aprenderá a usar as linguagens de consulta do CAP, entenderá como ele se conecta a diferentes bancos de dados e descobrirá recursos avançados para lidar com dados localizados e temporais.

## Estrutura do Módulo

### 1. [Queries com CQL e CQN](./01-queries-cql-cqn/README.md)

Abstraia a complexidade do SQL com as poderosas linguagens de consulta do CAP.
- **CQL (CDS Query Language):** Uma evolução do SQL, projetada para trabalhar com entidades e associações do CDS. Aprenda a usar *path expressions* e projeções aninhadas.
- **CQN (Core Query Notation):** A representação em objeto JavaScript de uma query.
- **`cds.ql`:** A API fluente e programática para construir queries CQN de forma segura, evitando SQL injection e garantindo a portabilidade entre bancos de dados.

### 2. [Drivers e Serviços de Banco de Dados](./02-drivers-e-servicos-db/README.md)

Descubra como o CAP se comunica com o banco de dados de forma agnóstica.
- **`DatabaseService` (`cds.db`):** O serviço genérico que representa a conexão com o banco de dados primário.
- **Drivers de Banco de Dados:** Entenda como o CAP utiliza drivers para suportar **SQLite** em desenvolvimento e **SAP HANA** em produção, sem alterar seu código de serviço.

### 3. [Localização e Dados Temporais](./03-localizacao-e-dados-temporais/README.md)

Explore recursos avançados de modelagem para cenários de negócio complexos.
- **Localização (`localized`):** Simplifique a internacionalização (i18n) de seus dados. O CAP gera automaticamente as tabelas de texto e views necessárias para servir o conteúdo no idioma do usuário.
- **Dados Temporais (`:temporal`):** Habilite o gerenciamento de validade de registros (`validFrom`, `validTo`) e realize consultas de "viagem no tempo" para auditar o estado dos dados em qualquer momento.

---

Ao final deste módulo, você estará apto a construir uma lógica de negócios rica que consulta e persiste dados de maneira robusta, aproveitando ao máximo as abstrações que o SAP CAP oferece para trabalhar com SAP HANA e outros bancos de dados.