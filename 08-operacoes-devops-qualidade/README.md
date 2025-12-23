# 08. Operações, DevOps e Qualidade

O ciclo de vida "Day 2": garantir que a aplicação seja testável, observável e implantável.

## Conteúdo

### 1. Testes Automatizados
A biblioteca `@cap-js/cds-test` fornece um ambiente de teste robusto que sobe o servidor CAP em memória. Ela suporta testes de caixa branca (API programática) e caixa preta (HTTP/OData), integrando-se com Jest e Mocha.

### 2. Observabilidade e Logging
O módulo `cds.log` oferece logs estruturados (JSON para produção, legível para dev). Ele suporta correlação de requisições (traceability) e mascaramento de dados sensíveis, essencial para operação na nuvem.

### 3. Deploy e Performance
*   **Deploy:** Estratégias de build (`cds build`) para gerar artefatos otimizados para produção (CF ou Kubernetes/Kyma) e uso de `package-lock.json` para builds reproduzíveis.
*   **Performance:** Modelagem consciente para evitar *full table scans* (evitar UNIONs e campos calculados na leitura) e uso eficiente de conexões de banco de dados.
