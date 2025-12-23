# 07. Arquitetura Avançada

Tópicos para cenários complexos, como aplicações SaaS e modularização de código.

## Conteúdo

### 1. Multitenancy (SaaS)
O CAP fornece suporte nativo para aplicações SaaS multitenant. A arquitetura utiliza um **Sidecar MTX** para gerenciar a assinatura de tenants, isolamento de dados (via containers HDI separados) e atualizações de esquema em tempo de execução sem downtime.

### 2. Plugins e Extensibilidade
O ecossistema CAP é altamente modular.
*   **Plugins:** Pacotes NPM que se autoconfiguram (`cds-plugin.js`) para adicionar funcionalidades ao servidor.
*   **Extensões:** O conceito de `extend` e `mixin` permite que tenants ou módulos adicionem campos e entidades ao modelo base sem modificar o código original.
