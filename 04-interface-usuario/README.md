# 04. Interface de Usuário (Fiori Elements)

O CAP simplifica drasticamente a criação de UIs empresariais ao adotar o desenvolvimento orientado a metadados.

## Conteúdo

### 1. Fiori Elements e Anotações
As anotações `@UI` no modelo CDS dirigem a renderização do frontend SAP Fiori Elements. Isso permite definir colunas, campos de busca, facetas e títulos diretamente no backend, mantendo a UI sincronizada com o modelo de dados.

### 2. Gestão de Rascunhos (Drafts)
A funcionalidade de **Draft** permite que usuários editem dados complexos em sessões longas sem bloquear o banco de dados ou perder trabalho não salvo. No CAP, isso é ativado com uma simples anotação `@odata.draft.enabled`, criando automaticamente uma entidade paralela de rascunho e gerenciando o ciclo de vida `EDIT` -> `SAVE` -> `ACTIVATE`.
