# Módulo 4: Interfaces de Usuário com Fiori Elements e Gestão de Rascunhos (Drafts)

![Infografico - Fiori Elements e Gestão de Rascunhos(Drafts)](./Infograficos/04.01.01_Fiori_Elements_Metadados.png)

Este módulo conecta o backend com o frontend, demonstrando um dos recursos mais poderosos do SAP CAP: a capacidade de gerar interfaces de usuário ricas e responsivas diretamente a partir dos seus modelos de dados.

Você aprenderá como usar o SAP Fiori Elements, um framework que interpreta metadados e anotações do seu serviço OData para renderizar UIs complexas (como List Reports e Object Pages) com pouquíssimo código, garantindo consistência e aderência ao design system da SAP.

## Estrutura do Módulo

### 1. [Fiori Elements e Anotações UI](./01-fiori-elements-annotations/README.md)

Transforme seus modelos de dados em interfaces de usuário funcionais usando o poder das anotações.
- **Desenvolvimento Orientado a Metadados:** Entenda como as anotações `@UI` (como `@UI.LineItem`, `@UI.FieldGroup`, `@UI.Chart`) adicionadas aos seus arquivos CDS descrevem a aparência e o comportamento da UI.
- **Da Intenção à Interface:** O serviço OData, enriquecido com metadados, instrui o Fiori Elements a renderizar tabelas, formulários, filtros e gráficos, mantendo a UI perfeitamente sincronizada com o backend.

### 2. [Gestão de Rascunhos (Drafts)](./02-gestao-de-rascunhos-drafts/README.md)

Melhore a experiência do usuário em cenários de edição de dados complexos com o suporte nativo a rascunhos.
- **Rascunho Transparente:** Com uma única anotação (`@odata.draft.enabled`), o CAP habilita a funcionalidade de "draft" (rascunho).
- **Ciclo de Vida:** O framework gerencia automaticamente o ciclo de vida completo: criação do rascunho, edição, salvamento (persistindo o rascunho) e ativação (movendo os dados para a entidade principal), garantindo que os dados não sejam perdidos e que não haja bloqueios desnecessários na tabela principal.

---

Ao final deste módulo, você será capaz de anotar seus modelos de serviço para gerar aplicações SAP Fiori Elements completas e de habilitar a funcionalidade de rascunho, proporcionando uma experiência de usuário robusta e padrão em suas aplicações de negócio.