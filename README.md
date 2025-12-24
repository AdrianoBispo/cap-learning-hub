# Guia de Estudos SAP CAP com Nodejs
Este repositório tem como objetivo guiar devs iniciantes e devs mais experientes que estão em busca de aprender sobre o universo SAP CAP utilizando o Node.js.

## Estrutura do Repositório

Abaixo está o guia de navegação do nosso projeto:

1.  **[Fundamentos e Modelagem](./01-fundamentos-e-modelagem/README.md)**: O coração do CAP. Tudo começa com CDS (Core Data Services), CDL e CSN.
2.  **[Runtime Node.js Core](./02-runtime-nodejs-core/README.md)**: Como o servidor `cds.server` funciona, o ciclo de vida de eventos e a injeção de lógica customizada via Handlers.
3.  **[Dados e Persistência](./03-dados-e-persistencia/README.md)**: O poder do CQL, CQN e a interação com bancos de dados (HANA, SQLite) através de `cds.db`.
4.  **[Interface de Usuário](./04-interface-usuario/README.md)**: Construção de UIs Fiori Elements dirigidas por anotações e gestão de Rascunhos (Drafts).
5.  **[Integrações e Mensageria](./05-integracoes-e-mensageria/README.md)**: Conectando-se a serviços remotos (S/4HANA) e arquitetura orientada a eventos.
6.  **[Segurança e Compliance](./06-seguranca-e-compliance/README.md)**: Autenticação, Autorização e Log de Auditoria automatizado.
7.  **[Arquitetura Avançada](./07-arquitetura-avancada/README.md)**: Multitenancy (SaaS) e Extensibilidade via Plugins.
8.  **[Operações, DevOps e Qualidade](./08-operacoes-devops-qualidade/README.md)**: Do `cds watch` à produção, testes automatizados e observabilidade.

## Organização e Nomenclatura dos Arquivos

Para garantir a organização, a rastreabilidade e a sequência lógica de leitura dos arquivos do projeto, foi então definida a seguinte **Regra de Nomenclatura Hierárquica**:

1. **DD (Diretório Principal)**: Dois dígitos representando a pasta raiz (ex: ``01`` para Fundamentos).
2. **SS (Subdiretório)**: Dois dígitos representando a subpasta (ex: ``01`` para Filosofia).
3. **FF (Fila/Ordem)**: Dois dígitos definindo a ordem de leitura recomendada dentro daquele tópico.
4. **Slug Descritivo**: O nome original ou simplificado do tópico, separado por underlines para legibilidade.

Exemplo: Se o arquivo `02.01.01_Server_Mastery.md` for movido acidentalmente para a pasta de banco de dados, o prefixo `02.01` indica imediatamente que ele pertence ao **`Módulo 02 (Runtime Node.js)`**, **`Submódulo 01 (Bootstrap)`**, e é o **`1º arquivo a ser lido`**.

## Links
- [Capire - Documentação Oficial da SAP CAP](https://cap.cloud.sap/docs/)
- [SAP Learning - Introduction to SAP Cloud Application Programming Model](https://learning.sap.com/courses/introduction-to-sap-cloud-application-programming-model)
- [SAP Learning - Desenvolva extensões com CAP seguindo o Guia do desenvolvedor SAP BTP](https://learning.sap.com/courses/develop-extensions-with-cap-following-the-sap-btp-developer-s-guide)
- [SAP Learning - Desenvolvendo um aplicativo SAP Fiori Elements baseado em um serviço CAP OData V4](https://learning.sap.com/courses/developing-an-sap-fiori-elements-app-based-on-a-cap-odata-v4-service)
- [Tutorial SAP - Crie um aplicativo de negócios CAP utilizando o VS Code e Nodejs](https://developers.sap.com/mission.cp-starter-extensions-cap.html)
- [Turorial SAP - Como Criar uma Aplicação SAP CAP Full Stack utilizando o BAS, Nodejs e Banco Hana](https://developers.sap.com/mission.hana-cloud-cap.html)
- [Tutorial SAP - Desenvolva um aplicativo Node.js no SAP BTP Kyma Runtime](https://developers.sap.com/mission.cp-kyma-node-js.html)
- [Tutorial SAP - Crie um aplicativo com Cloud Foundry Node.js Buildpack](https://developers.sap.com/tutorials/btp-cf-buildpacks-node-create.html)
- [Tutorial SAP - Como desenvolver um App de Mensagens dentro do SAP BTP utilizando o Nodejs ou Java](https://developers.sap.com/mission.cp-enterprisemessaging-app-develop.html)
