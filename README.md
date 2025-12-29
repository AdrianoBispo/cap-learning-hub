# Guia de Estudos SAP CAP com Nodejs

![Infografico - Guia Rapido de Desenvolvimento SAP CAP (Node.js)](./Infografico%20-%20Guia%20de%20Desenvolvimento%20SAP%20CAP%20com%20Nodejs.png)

> **Este repositório tem como objetivo guiar devs iniciantes e devs mais experientes que estão em busca de aprender sobre o universo SAP CAP utilizando o Node.js.**

## Estrutura do Repositório

Abaixo está o guia de navegação do nosso projeto:

| Diretório | Descrição |
| :--- | :--- |
| **[01. Fundamentos e Modelagem](./01-fundamentos-e-modelagem/)** | A base de tudo: Filosofia do CAP, CDL, CSN e o sistema de compiladores. |
| **[02. Runtime Node.js Core](./02-runtime-nodejs-core/)** | O coração da aplicação: Bootstrap do servidor, Event Handlers e TypeScript. |
| **[03. Dados e Persistência](./03-dados-e-persistencia/)** | Consultas CQL/CQN, drivers de banco de dados e gestão de dados temporais. |
| **[04. Interface de Usuário](./04-interface-usuario/)** | Criação de UIs com Fiori Elements, Anotações e gestão de Drafts. |
| **[05. Integrações e Mensageria](./05-integracoes-e-mensageria/)** | Conectando serviços remotos (S/4HANA) e arquitetura orientada a eventos. |
| **[06. Segurança e Compliance](./06-seguranca-e-compliance/)** | Autenticação (XSUAA), Autorização, Logs de Auditoria e Privacidade. |
| **[07. Arquitetura Avançada](./07-arquitetura-avancada/)** | Multitenancy (SaaS), Extensibilidade e Plugins. |
| **[08. Operações e Qualidade](./08-operacoes-devops-qualidade/)** | Testes automatizados, Observabilidade e CI/CD. |

## Organização e Nomenclatura dos Arquivos

Para garantir a organização, a rastreabilidade e a sequência lógica de leitura dos arquivos do projeto, foi então definida a seguinte **Regra de Nomenclatura Hierárquica**:

1. **DD (Diretório Principal)**: Dois dígitos representando a pasta raiz (ex: ``01`` para Fundamentos).
2. **SS (Subdiretório)**: Dois dígitos representando a subpasta (ex: ``01`` para Filosofia).
3. **FF (Fila/Ordem)**: Dois dígitos definindo a ordem de leitura recomendada dentro daquele tópico.
4. **Slug Descritivo**: O nome original ou simplificado do tópico, separado por underlines para legibilidade.

Exemplo: Se o arquivo `02.01.01_Server_Mastery.md` for movido acidentalmente para a pasta de banco de dados, o prefixo `02.01` indica imediatamente que ele pertence ao **`Módulo 02 (Runtime Node.js)`**, **`Submódulo 01 (Bootstrap)`**, e é o **`1º arquivo a ser lido`**.


## Links Úteis
  
  ### Documentação Oficial
  - [Capire - Documentação Oficial da SAP CAP](https://cap.cloud.sap/docs/)

  ### SAP Learning - Cursos Oficiais da SAP para você se aprofundar
  - [SAP Learning - Introduction to SAP Cloud Application Programming Model](https://learning.sap.com/courses/introduction-to-sap-cloud-application-programming-model)
  - [SAP Learning - Desenvolva extensões com CAP seguindo o Guia do desenvolvedor SAP BTP](https://learning.sap.com/courses/develop-extensions-with-cap-following-the-sap-btp-developer-s-guide)
  - [SAP Learning - Desenvolvendo um aplicativo SAP Fiori Elements baseado em um serviço CAP OData V4](https://learning.sap.com/courses/developing-an-sap-fiori-elements-app-based-on-a-cap-odata-v4-service)

  ### SAP Tutorials - Aprenda Praticando por meio dos tutoriais oficiais da SAP
  - [Tutorial SAP - Crie um aplicativo de negócios CAP utilizando o VS Code e Nodejs](https://developers.sap.com/mission.cp-starter-extensions-cap.html)
  - [Turorial SAP - Como Criar uma Aplicação SAP CAP Full Stack utilizando o BAS, Nodejs e Banco Hana](https://developers.sap.com/mission.hana-cloud-cap.html)
  - [Tutorial SAP - Desenvolva um aplicativo Node.js no SAP BTP Kyma Runtime](https://developers.sap.com/mission.cp-kyma-node-js.html)
  - [Tutorial SAP - Crie um aplicativo com Cloud Foundry Node.js Buildpack](https://developers.sap.com/tutorials/btp-cf-buildpacks-node-create.html)
  - [Tutorial SAP - Como desenvolver um App de Mensagens dentro do SAP BTP utilizando o Nodejs ou Java](https://developers.sap.com/mission.cp-enterprisemessaging-app-develop.html)

---

_Todo conteúdo presente nesse repositório foi gerado através do Notebook LM com base na documentação oficial da SAP Cloud Application Programming Model._
