# Módulo 6: Segurança e Compliance

Segurança em aplicações empresariais não é opcional. O SAP CAP adota uma filosofia "secure by default", integrando-se nativamente com os serviços de segurança da SAP BTP para proteger seus dados e serviços.

Este módulo aborda os dois pilares fundamentais da segurança: quem pode acessar a aplicação (autenticação), o que eles podem fazer (autorização), e como garantir a conformidade (compliance) através de logs de auditoria e privacidade de dados.

## Estrutura do Módulo

### 1. [Autenticação e Autorização](./01-autenticacao-e-autorizacao/README.md)

Controle o acesso à sua aplicação de forma declarativa e robusta.
- **Autenticação:** O CAP se integra nativamente com o serviço de Autenticação e Autorização da BTP (XSUAA). O runtime processa o token do usuário (JWT), disponibilizando sua identidade e atributos de forma segura no contexto da requisição (ex: `cds.context.user`).
- **Autorização:** Em vez de espalhar a lógica de permissão pelo código, você a define diretamente no seu modelo de dados com anotações. Use `@requires: 'Role'` para restringir o acesso a entidades ou serviços inteiros, e `@restrict` para definir permissões granulares de CRUD (Leitura, Escrita, Atualização, Deleção) com base em papéis (roles).

### 2. [Logs de Auditoria e Privacidade de Dados](./02-audit-log-e-privacidade/README.md)

Garanta a conformidade e a rastreabilidade exigidas em ambientes corporativos.
- **Privacidade de Dados:** Classifique dados sensíveis usando anotações como `@PersonalData.IsPotentiallyPersonal`. Isso é fundamental para atender a regulações como a LGPD/GDPR e se integrar a outros serviços de gerenciamento de dados na BTP.
- **Logs de Auditoria (Audit Logging):** Com o uso de plugins como `@cap-js/audit-logging`, o CAP pode registrar automaticamente eventos críticos de segurança — como o acesso a dados pessoais ou a alteração de registros importantes — no SAP Auditlog Service, garantindo a rastreabilidade completa das ações do usuário.

---

Ao final deste módulo, você saberá como proteger sua aplicação CAP usando um modelo de permissões declarativo, como integrar-se aos serviços de segurança da BTP e como implementar os requisitos de compliance essenciais para qualquer aplicação de nível empresarial.