# Módulo 3 (Parte 1): Dados e Persistência - Queries com CQL e CQN

![Infografico - CQL a Evolução do SQL](../Infograficos/03.01.01_CQL_Evolucao_SQL.png)

Este diretório foca na linguagem de consulta do SAP CAP, o **CDS Query Language (CQL)**, e sua representação em objeto, o **CDS Query Notation (CQN)**. Entender CQL e CQN é fundamental para realizar operações de banco de dados de forma segura, eficiente e agnóstica de fornecedor.

## Tópicos Abordados

Os documentos a seguir exploram a sintaxe e a aplicação das queries em CAP:

1. **CQL: A Evolução do SQL (`03.01.01_CQL_Evolucao_SQL.pdf`):** Apresenta o CQL como uma extensão do SQL padrão, enriquecido com conhecimento do modelo de dados. Aprenda a sintaxe para `SELECT`, `INSERT`, `UPDATE`, `DELETE`, projeções, `path expressions` e como ele simplifica joins e associações.

2. **CQN: Desconstrução Arquitetural (`03.01.02_CQN_Desconstrucao_Arquitetural.pdf`):** Descreve o CQN, a representação em objeto JavaScript das queries CQL. É com objetos CQN que interagimos no runtime Node.js para construir e executar consultas dinamicamente.

3. **Dominando Queries no Node.js (`03.01.03_Dominando_Queries_Nodejs.pdf`):** Um guia prático que mostra como usar a API `cds.run` e `srv.run` com CQN para executar queries. Cobre exemplos de `SELECT` com `where`, `limit`, `orderBy`, e operações de escrita como `INSERT`, `UPDATE` e `DELETE`.
