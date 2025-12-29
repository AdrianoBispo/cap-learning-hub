# Módulo 08 (Parte 3): Operações, DevOps e Qualidade - Deploy, Produção e Performance

![Infografico - Melhores Práticas de Desenvolvimento SAP CAP com Node.js](../Infograficos/08.03.02_Boas_Praticas_Nodejs.png)

Levar uma aplicação para o ambiente de produção é mais do que apenas um comando de `deploy`. Este capítulo final aborda as etapas críticas para empacotar, implantar e otimizar sua aplicação SAP CAP, garantindo que ela seja robusta, escalável e performática sob carga de trabalho real.

## Tópicos Abordados

1. **Do `cds watch` à Produção (`08.03.01_Do_cds_watch_a_Producao.pdf`)**: Este guia detalha o processo de `build` e `deploy` de uma aplicação CAP para o SAP BTP, Cloud Foundry. Aprenda a usar o `cds build` para criar os artefatos para o banco de dados (HANA) e para o serviço (Node.js), e como usar o `manifest.yml` para descrever e implantar sua aplicação na nuvem.

2. **Modelagem de Aspectos (`08.03.02_Modelagem_de_Aspectos.pdf`):** Introduz o conceito de `aspects`, uma técnica poderosa para reutilização de código e composição de modelos, permitindo adicionar conjuntos de campos e anotações a múltiplas entidades de forma consistente.

3. **Performance e Modelagem (`08.03.03_Performance_Modeling.pdf`)**: A performance de uma aplicação começa no modelo de dados. Este material explora como decisões de modelagem no CDS impactam o desempenho do banco de dados. Aprenda a usar `compositions` e `associations` de forma eficiente, a criar `views` para otimizar `queries` complexas e a analisar o SQL gerado pelo CAP para identificar gargalos.

4. **Boas Práticas em Node.js para SAP CAP (`08.03.04_Boas_Praticas_Nodejs.pdf`)**: Performance e estabilidade em produção dependem de um código bem escrito. Este artigo compila um conjunto de boas práticas essenciais para o desenvolvimento Node.js com CAP, incluindo o gerenciamento de concorrência, o uso correto de `async/await` em `handlers`, e a otimização do `event loop`.
