# Módulo 3 (Parte 2): Dados e Persistência - Drivers e Serviços de Banco de Dados

![Infografico - Dados e Persistência de Banco de Dados](../Infograficos/03.02.02_DatabaseService_Masterclass.png)

Este diretório aborda a camada de persistência do SAP CAP, focando em como o framework се conecta a bancos de dados como SAP HANA e como o `DatabaseService` atua como a ponte entre seus modelos e o banco de dados físico.

## Conteúdo

Os documentos a seguir detalham a interação com a camada de banco de dados:

-   **Bancos de Dados Enterprise com CAP (`03.02.01_Banco_de_Dados_Enterprise.pdf`):** Explora a integração do CAP com bancos de dados robustos, especialmente SAP HANA. Discute a configuração de `cds.requires.db` para especificar o tipo de banco de dados e como o CAP utiliza drivers (`@sap/cds-hana`) para traduzir CQN em SQL nativo.

-   **DatabaseService Masterclass (`03.02.02_DatabaseService_Masterclass.pdf`):** Um mergulho profundo no `DatabaseService`, o serviço genérico que representa a conexão com o banco de dados. Veremos como ele herda de `cds.Service` e serve como a implementação padrão para as operações CRUD que não são sobrecarregadas na camada de aplicação.
