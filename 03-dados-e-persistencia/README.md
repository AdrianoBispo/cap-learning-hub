# Módulo 03: Dados e Persistência

![Infográfico sobre Persistência de Dados](../Infograficos/03.02.01_Banco_de_Dados_Enterprise.png)

A persistência de dados é um pilar de qualquer aplicação enterprise. Este módulo cobre como o SAP CAP abstrai o acesso ao banco de dados através de **CQL** e **CQN**, como ele se integra a bancos de dados como SAP HANA, e como lida com cenários avançados como dados temporais e localização (i18n).

## Tópicos

| Tópico | Descrição |
| :--- | :--- |
| [**Consultas com CQL e CQN**](./01-queries-cql-cqn/README.md) | Explora a CDS Query Language (CQL) e sua representação em objeto (CQN) para interagir com a camada de persistência. |
| [**Drivers e Serviços de DB**](./02-drivers-e-servicos-db/README.md) | Foca na camada de serviço de persistência (`DatabaseService`) e como o CAP interage com o banco de dados (ex: SAP HANA). |
| [**Dados Temporais**](./03-dados-temporais/README.md) | Explica o suporte nativo do CAP para dados temporais, permitindo consultas em um ponto específico no tempo ("time travel queries"). |
| [**Dados Localizados e i18n**](./04-dados-localizados-cdsi18n/README.md) | Detalha como o CAP simplifica o desenvolvimento de aplicações multilíngues, gerenciando traduções de textos e dados. |
| [**Infográficos do Módulo**](./Infograficos/README.md) | Coleção de todos os infográficos e diagramas visuais relacionados a este módulo. |

---

Entender a camada de persistência do CAP é fundamental para criar serviços de dados eficientes, escaláveis e prontos para o ambiente corporativo.
