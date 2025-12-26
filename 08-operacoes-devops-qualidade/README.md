# Módulo 8: Operações, DevOps e Qualidade

O ciclo de vida de uma aplicação não termina no desenvolvimento. Este módulo final aborda as práticas de "Day 2": como garantir a qualidade, a observabilidade e o desempenho da sua aplicação em um ambiente produtivo.

Aqui, você aprenderá a construir testes automatizados, a gerar logs estruturados e a empacotar e implantar sua aplicação na nuvem, seguindo as melhores práticas de DevOps e performance.

## Estrutura do Módulo

### 1. [Testes Automatizados](./01-testes-automatizados/README.md)

Garanta a qualidade e a estabilidade do seu código com uma suíte de testes robusta.
- **Framework de Teste:** Explore o pacote `@sap/cds-test`, que se integra a runners como o **Jest** para facilitar os testes de serviços CAP.
- **Tipos de Teste:** Aprenda a escrever tanto testes de API "in-process" (caixa-branca), que invocam seus `handlers` diretamente, quanto testes de integração "black-box" via requisições HTTP/OData, simulando o comportamento de um cliente real.

### 2. [Observabilidade e Logging](./02-observabilidade-logging/README.md)

Entenda o que está acontecendo dentro da sua aplicação em tempo de execução.
- **Logging Estruturado:** Domine a API `cds.log()`, que gera logs legíveis para humanos durante o desenvolvimento e logs estruturados em JSON para produção. Estes logs são essenciais para análise, monitoramento e integração com plataformas como o Kibana ou Splunk.
- **Rastreabilidade:** Veja como o CAP inclui automaticamente um `correlation-id` em todas as mensagens de log de uma mesma requisição, permitindo rastrear uma transação completa através de múltiplos serviços e componentes.

### 3. [Deploy, Produção e Performance](./03-deploy-producao-performance/README.md)

Leve sua aplicação do ambiente de desenvolvimento (`cds watch`) para a produção.
- **Build para Produção:** O comando `cds build` compila seus modelos, transpila o código (se usar TypeScript) e prepara um pacote otimizado para implantação em ambientes de nuvem como o SAP BTP (Cloud Foundry) ou Kyma (Kubernetes).
- **Boas Práticas e Performance:** Receba dicas sobre modelagem de dados performática e práticas de desenvolvimento Node.js que garantem que sua aplicação seja escalável e eficiente sob carga.

---

**Parabéns!** Ao concluir este módulo, você terá percorrido toda a jornada de desenvolvimento com o SAP CAP: da concepção do modelo de dados à sua implementação, segurança, integração e, finalmente, operação em um ambiente produtivo. Você está pronto para construir aplicações empresariais robustas e de ponta a ponta.