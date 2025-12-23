# 06. Segurança e Compliance

Segurança no CAP é "Secure by Design". Este módulo cobre como proteger sua aplicação e garantir conformidade.

## Conteúdo

### 1. Autenticação e Autorização
*   **Autenticação:** Integração automática com XSUAA/IAS via passport strategies. O usuário autenticado é acessível em `req.user`.
*   **Autorização:** Definida declarativamente no modelo CDS com `@restrict` e `@requires`. Isso garante que as regras de acesso estejam junto aos dados, não espalhadas no código.

### 2. Audit Log e Privacidade
*   **Audit Log:** O plugin `@cap-js/audit-logging` automatiza o registro de leituras de dados sensíveis e modificações de dados pessoais.
*   **Privacidade:** Anotações como `@PersonalData` classificam quais dados são sensíveis, integrando-se com serviços de retenção e proteção de dados da BTP.
