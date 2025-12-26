# Módulo 2: Runtime do Node.js e Serviços

![Infografico - O Ciclo de Vida de um Servidor SAP CAP utilizando Node.js](./Infograficos/02.01.01_Nodejs_Server_Mastery.png)

Este módulo é o coração da execução da sua aplicação CAP no ambiente Node.js. Aqui, transformamos os modelos de dados estáticos do Módulo 1 em serviços vivos e interativos.

Você aprenderá como o runtime do CAP inicializa o servidor, processa requisições, gerencia a lógica de negócios através de eventos e interage com o banco de dados, com um guia especial para configuração com TypeScript.

## Estrutura do Módulo

### 1. [Bootstrap e Configuração do Servidor](./01-server-bootstrap-configuracao/README.md)

Nesta seção, desvendamos o processo de inicialização do servidor CAP.
- **Conceitos abordados:** O ciclo de vida do bootstrap (`cds.on('bootstrap')`), customização do servidor Express via `server.js`, e a configuração centralizada através do objeto `cds.env`.

### 2. [Event Handlers e Arquitetura de Serviços](./02-event-handlers-e-servicos/README.md)

Explore a arquitetura orientada a eventos que define o CAP. A lógica de negócio é implementada interceptando requisições em diferentes fases do ciclo de vida.
- **Padrão de implementação:** Uso dos handlers `@Before`, `@On` e `@After` para validação, execução e enriquecimento de dados.
- **Conceitos-chave:** A dualidade dos serviços (definição vs. implementação), o fluxo de requisições e a classe `ApplicationService` como base para sua lógica.

### 3. [Ferramentas Essenciais do SDK](./03-ferramentas-sdk-utils/README.md)

Domine as ferramentas que o SDK do Node.js oferece para construir uma lógica de negócios robusta e eficiente.
- **APIs fundamentais:** Execução de queries com `cds.run`, `cds.ql`, gerenciamento de transações com `cds.tx` e o acesso ao contexto da requisição com `cds.context`.
- **Utilitários:** Funções auxiliares como `cds.utils` para tarefas comuns.

### 4. [Setup com TypeScript](./04-typescript-setup/README.md)

Leve seu desenvolvimento CAP para o próximo nível com a segurança de tipos do TypeScript.
- **Guia de configuração:** Passos para inicializar e configurar um projeto CAP para compilar e executar código TypeScript.
- **Vantagens:** Geração de tipos a partir dos seus modelos CDS, autocomplete aprimorado e maior robustez no código da sua aplicação.

---

Ao concluir este módulo, você será capaz de implementar lógicas de negócio complexas, customizar o comportamento do servidor e estruturar seu projeto com as melhores práticas de desenvolvimento em Node.js e TypeScript no ecossistema SAP CAP.