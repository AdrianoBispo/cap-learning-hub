# Módulo 2 (Parte 3): Runtime Node.js Core - Ferramentas, SDK e Utilitários

![Infografico - Ferramentas e Utilitários](../Infograficos/02.03.02_cds_utils_Toolbox.png)

Este diretório explora as ferramentas e APIs que o SDK do SAP CAP para Node.js oferece para facilitar o desenvolvimento. Abordaremos desde a interação programática com serviços até a gestão de transações de banco de dados.

## Conteúdo

Os documentos a seguir fornecem um guia prático sobre as principais ferramentas do SDK:

-   **Node.js SDK Deep Dive (`02.03.01_Nodejs_SDK_Deep_Dive.pdf`):** Um mergulho profundo nas APIs centrais, como `cds.connect`, `cds.run` e a API de Querying (CQL/CQN). Aprenda a consumir outros serviços (internos ou externos) de forma programática.

-   **`cds.utils`: A Caixa de Ferramentas (`02.03.02_cds_utils_Toolbox.pdf`):** Apresenta o `cds.utils`, um conjunto de funções utilitárias fornecidas pelo framework para tarefas comuns, como geração de UUIDs (`cds.utils.uuid()`), tratamento de erros e manipulação de mensagens.

-   **Transações: Autopilot e Manual (`02.03.03_Transacoes_Autopilot_Manual.pdf`):** Explica como o CAP gerencia transações de banco de dados. Detalha o modo "autopilot" (padrão) e como assumir o controle manual com `cds.tx`, garantindo a atomicidade de operações complexas.
