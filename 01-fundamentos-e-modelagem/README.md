# Módulo 1: Fundamentos e Modelagem com SAP CAP

![Infografico - Guia Rapido de Desenvolvimento SAP CAP (Node.js)](./Infograficos/01.01.01_Jornada_do_Construtor.png)

Bem-vindo ao ponto de partida da sua jornada com o **SAP Cloud Application Programming Model (CAP)**. Este módulo é dedicado à espinha dorsal de qualquer aplicação CAP: o **Core Data Services (CDS)**.

Aqui, você aprenderá a traduzir a intenção de negócio em modelos de dados declarativos e robustos, que servem como a única fonte da verdade para toda a sua aplicação, desde o banco de dados até a interface do usuário.

## Estrutura do Módulo

Este módulo está dividido nas seguintes seções, cada uma construindo sobre a anterior:

### 1. [Filosofia e Intenção](./01-filosofia-e-intencao/README.md)

Nesta seção, mergulhamos na mentalidade por trás do CAP. O foco é em modelar *o que* a aplicação deve fazer, não *como*.
- **Conceitos abordados:** Modelagem orientada a intenção, jornada do desenvolvedor e a construção de aplicações robustas.
- **Artefatos importantes:** Introdução a **Aspectos** como `cuid` e `managed` para enriquecer seus modelos de forma reutilizável.

### 2. [Linguagens Core: CDL, CSN e CXN](./02-linguagens-core-cdl-csn-cxn/README.md)

Exploramos as diferentes "faces" do CDS, cada uma com um propósito específico no ciclo de vida do desenvolvimento.
- **CDL (Conceptual Definition Language):** A linguagem humanamente legível para escrever seus modelos (`.cds`).
- **CSN (Core Schema Notation):** A representação canônica do seu modelo em JSON, usada pelo runtime do CAP.
- **CXN (CDS Expression Notation):** A notação interna para expressões, que garante consistência entre diferentes representações.

### 3. [Compilador e Reflexão](./03-compilador-e-reflexao/README.md)

Descubra a "mágica" que transforma seus modelos de domínio em artefatos concretos e como inspecioná-los em tempo de execução.
- **Compilador (`cds build`/`compile`):** O processo que transforma CDL em CSN e gera DDL para o banco de dados e metadados OData (EDMX).
- **API de Reflexão:** Como usar `cds.model` e `cds.linked_model` para navegar e interagir com a estrutura do seu modelo dinamicamente via código.

---

Ao final deste módulo, você terá uma base sólida sobre como pensar e construir modelos de dados eficientes com SAP CAP, preparando o terreno para os próximos módulos sobre serviços, persistência e interfaces de usuário.
