# Guia de Estudos SAP CAP com Node.js

![Infografico - Guia Rapido de Desenvolvimento SAP CAP (Node.js)](./Infografico%20-%20Guia%20de%20Desenvolvimento%20SAP%20CAP%20com%20Nodejs.png)

> **Este repositório é um guia completo para desenvolvedores que desejam aprender e dominar o SAP Cloud Application Programming Model (CAP) com Node.js. Seja você um iniciante buscando uma introdução clara ou um desenvolvedor experiente procurando aprofundar seus conhecimentos, este guia oferece um caminho estruturado e prático.**

## Estrutura do Repositório

O conteúdo está organizado em módulos progressivos, do básico ao avançado. Cada módulo foca em um aspecto específico do desenvolvimento com SAP CAP.

| Módulo | Descrição Detalhada |
| :--- | :--- |
| **[01. Fundamentos e Modelagem](./01-fundamentos-e-modelagem/)** | Comece aqui. Entenda a filosofia por trás do CAP, a importância da modelagem com intenção e domine as linguagens essenciais: CDL, CSN e CXN. |
| **[02. Runtime Node.js Core](./02-runtime-nodejs-core/)** | O coração da sua aplicação. Aprenda sobre o bootstrap do servidor, o ciclo de vida dos serviços, o tratamento de eventos e como configurar seu ambiente com TypeScript. |
| **[03. Dados e Persistência](./03-dados-e-persistencia/)** | Explore como o CAP interage com bancos de dados. Domine as linguagens de consulta CQL e CQN, entenda os drivers de serviço e aprenda a lidar com dados temporais e localizados. |
| **[04. Interface de Usuário](./04-interface-usuario/)** | Da intenção à interface. Descubra como criar UIs ricas e intuitivas com Fiori Elements, utilizando anotações para definir o comportamento e a aparência da sua aplicação. |
| **[05. Integrações e Mensageria](./05-integracoes-e-mensageria/)** | Conecte seu aplicativo ao mundo. Aprenda a consumir serviços remotos (como S/4HANA) e a construir uma arquitetura robusta e escalável com mensageria assíncrona. |
| **[06. Segurança e Compliance](./06-seguranca-e-compliance/)** | Proteja sua aplicação. Implemente autenticação e autorização com XSUAA, gerencie logs de auditoria e garanta a privacidade dos dados de acordo com as melhores práticas. |
| **[07. Arquitetura Avançada](./07-arquitetura-avancada/)** | Leve suas habilidades para o próximo nível. Explore tópicos como desenvolvimento de aplicações multitenant (SaaS), extensibilidade e a criação de plugins modulares. |
| **[08. Operações e Qualidade](./08-operacoes-devops-qualidade/)** | Garanta a qualidade e a robustez da sua aplicação em produção. Aprenda a escrever testes automatizados, implementar logging e observabilidade, e siga as boas práticas de CI/CD. |

## Organização e Nomenclatura dos Arquivos

Para garantir a organização, a rastreabilidade e a sequência lógica de leitura dos arquivos do projeto, foi então definida a seguinte **Regra de Nomenclatura Hierárquica**: **`DD.SS.FF_Slug_Descritivo`**

1. **DD (Diretório Principal)**: Dois dígitos representando a pasta raiz.
2. **SS (Subdiretório)**: Dois dígitos representando a subpasta.
3. **FF (Fila/Ordem)**: Dois dígitos definindo a ordem de leitura recomendada dentro daquele tópico.
4. **Slug Descritivo**: O nome original ou simplificado do tópico, separado por underlines para legibilidade.

## Como Contribuir

Contribuições são bem-vindas! Se você encontrar erros, tiver sugestões de melhoria ou quiser adicionar novo conteúdo, siga estes passos:

1.  **Fork** este repositório.
2.  Crie uma nova **branch** para sua feature (`git checkout -b feature/nova-feature`).
3.  Faça suas alterações e **commit** (`git commit -m 'feat: Adiciona nova feature'`).
4.  Envie para a sua branch (`git push origin feature/nova-feature`).
5.  Abra um **Pull Request**.

## Links Úteis
  
  ### Documentação Oficial
  - [Capire - Documentação Oficial da SAP CAP](https://cap.cloud.sap/docs/)

  ### Cursos Oficiais da SAP
  - [SAP Learning - Introduction to SAP Cloud Application Programming Model](https://learning.sap.com/courses/introduction-to-sap-cloud-application-programming-model)
  - [SAP Learning - Desenvolva extensões com CAP seguindo o Guia do desenvolvedor SAP BTP](https://learning.sap.com/courses/develop-extensions-with-cap-following-the-sap-btp-developer-s-guide)
  - [SAP Learning - Desenvolvendo um aplicativo SAP Fiori Elements baseado em um serviço CAP OData V4](https://learning.sap.com/courses/developing-an-sap-fiori-elements-app-based-on-a-cap-odata-v4-service)

  ### Tutoriais Oficiais da SAP
  - [Tutorial SAP - Crie um aplicativo de negócios CAP utilizando o VS Code e Nodejs](https://developers.sap.com/mission.cp-starter-extensions-cap.html)
  - [Turorial SAP - Como Criar uma Aplicação SAP CAP Full Stack utilizando o BAS, Nodejs e Banco Hana](https://developers.sap.com/mission.hana-cloud-cap.html)
  - [Tutorial SAP - Desenvolva um aplicativo Node.js no SAP BTP Kyma Runtime](https://developers.sap.com/mission.cp-kyma-node-js.html)
  - [Tutorial SAP - Crie um aplicativo com Cloud Foundry Node.js Buildpack](https://developers.sap.com/tutorials/btp-cf-buildpacks-node-create.html)
  - [Tutorial SAP - Como desenvolver um App de Mensagens dentro do SAP BTP utilizando o Nodejs ou Java](https://developers.sap.com/mission.cp-enterprisemessaging-app-develop.html)

## Licença

Este projeto é distribuído sob a licença MIT. Veja o arquivo `LICENSE` para mais detalhes.

---

_Todo o conteúdo deste repositório foi gerado com o auxílio de um Notebook LM, tendo como base a documentação oficial do SAP Cloud Application Programming Model._