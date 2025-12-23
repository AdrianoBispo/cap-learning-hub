# 01. Fundamentos e Modelagem (CDS)

Este módulo explora a "Espinha Dorsal" da aplicação CAP: o **Core Data Services (CDS)**. O modelo de domínio é a fonte única da verdade, capturando a intenção do negócio de forma declarativa.

## Conteúdo

### 1. Filosofia e Intenção
O foco é descrever *o que* a aplicação faz, e não *como*. Utilizamos **Aspectos** reutilizáveis como `cuid` (para chaves universais) e `managed` (para auditoria automática) para manter os modelos limpos e focados no negócio.

### 2. Linguagens Core: CDL, CSN e CXN
*   **CDL (Conceptual Definition Language):** A linguagem legível por humanos usada nos arquivos `.cds`. É focada em ser concisa e expressiva.
*   **CSN (Core Schema Notation):** O formato JSON compilado que as máquinas e o runtime consomem. É a representação canônica e otimizada do modelo.
*   **CXN (CDS Expression Notation):** A representação interna de expressões lógicas e aritméticas dentro do modelo.

### 3. Compilador e Reflexão
O compilador transforma CDL em CSN e gera artefatos como SQL DDL e OData EDMX. Em tempo de execução, utilizamos a API de reflexão (`cds.linked`) para inspecionar e navegar pelo modelo de forma dinâmica, garantindo tipos seguros e validações.