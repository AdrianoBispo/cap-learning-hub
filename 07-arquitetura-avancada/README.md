# Módulo 7: Arquitetura Avançada

Este módulo explora tópicos que elevam sua aplicação CAP de um projeto padrão para uma solução de software escalável, customizável e pronta para o mercado, como um produto **Software-as-a-Service (SaaS)**.

Aqui, você aprenderá a construir aplicações que podem servir múltiplos clientes (tenants) com segurança e a criar uma arquitetura modular e extensível.

## Estrutura do Módulo

### 1. [Multitenancy e Aplicações SaaS](./01-multitenancy-saas/README.md)

Transforme sua aplicação em um produto SaaS com o suporte nativo a multitenancy do CAP.
- **Isolamento de Dados:** Entenda como o CAP, em conjunto com a SAP BTP e o SAP HANA Cloud, provisiona automaticamente um container de banco de dados (HDI container) separado para cada cliente (tenant) que assina a aplicação. Isso garante que os dados de um cliente sejam completamente isolados dos outros.
- **Provisionamento de Tenants:** O processo é orquestrado pelo serviço *SaaS Provisioning* (saas-registry) na BTP, que, ao receber uma nova assinatura, notifica o *sidecar* de serviços multitenancy (MTX) da sua aplicação para preparar o ambiente do novo tenant, incluindo a implantação do esquema de banco de dados.

### 2. [Plugins e Extensibilidade](./02-plugins-e-extensibilidade/README.md)

Construa aplicações modulares e permita customizações sem alterar o código-fonte principal.
- **Extensibilidade do Modelo:** O CAP permite estender modelos de dados de forma não invasiva. Use a palavra-chave `extend` para adicionar novos campos a uma entidade existente ou `mixin` para agrupar campos reutilizáveis. Isso é crucial para adaptações específicas de clientes ou para dividir o modelo em múltiplos domínios.
- **Plugins (`cds-plugin`):** Descubra o ecossistema de plugins do CAP. Ao adicionar um pacote npm que segue a convenção `cds-plugin.js`, você pode injetar funcionalidades adicionais (como logs de auditoria, exportação para Excel, etc.) de forma transparente e reutilizável em seus projetos, sem a necessidade de configuração manual.

---

Dominar estes conceitos de arquitetura avançada é o que permite a construção de soluções empresariais verdadeiramente robustas, que podem crescer em escala para atender múltiplos clientes e se adaptar a novos requisitos de negócio com o mínimo de atrito.