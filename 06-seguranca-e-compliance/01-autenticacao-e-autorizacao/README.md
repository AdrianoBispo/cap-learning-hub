# Módulo 06 (Parte 1): Segurança e Compliance - Autenticação e Autorização

![Infografico - Dominando a Autenticação no SAP CAP com Node.js ](../Infograficos/06.01.02_Authentication_Developers_Path.png)

A segurança é um pilar não negociável em aplicações corporativas. Este capítulo é dedicado a desmistificar a implementação de autenticação e autorização em SAP CAP, mostrando como o framework se integra perfeitamente com provedores de identidade e simplifica a definição de regras de acesso.

## Tópicos Abordados

1. **Segurança e Autenticação com SAP CAP (`06.01.01_Seguranca_e_Autenticacao.pdf`)**: Um guia essencial que introduz os conceitos de segurança no CAP. Aprenda a usar a anotação `@requires` para proteger serviços e entidades, e entenda como o objeto `cds.user` encapsula a identidade do usuário autenticado, permitindo a implementação de lógicas de autorização dinâmicas.

2. **O Caminho do Desenvolvedor para Autenticação (`06.01.02_Authentication_Developers_Path.pdf`)**: Este material detalha a jornada da autenticação no SAP CAP, desde o fluxo de `login` com `passport.js` até a validação de tokens JWT. O artigo explora como o CAP abstrai as complexidades, oferecendo uma API consistente (`req.user`) para acesso aos dados do usuário em diferentes contextos.
