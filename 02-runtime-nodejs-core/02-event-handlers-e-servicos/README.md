# Módulo 2 (Parte 2): Runtime Node.js Core - Event Handlers e Serviços

![Infografico - ](../Infograficos/02.02.02_Services_Dominando_a_Dualidade.png)

Este diretório mergulha na implementação de lógica de negócios customizada em SAP CAP através de *event handlers*. Vamos entender a estrutura dos serviços, como registrar *handlers* para eventos do ciclo de vida (CRUD) e a dualidade entre serviços de aplicação e serviços conectados.

## Tópicos Abordados

Os documentos a seguir são essenciais para dominar a implementação de serviços no runtime Node.js:

1. **Anatomia de um Serviço (`02.02.01_Anatomia_de_um_Servico.pdf`):** Descreve a estrutura de um arquivo de implementação de serviço (`.js`), mostrando como registrar *handlers* com `srv.before`, `srv.on` e `srv.after` para interceptar e modificar o comportamento padrão.

2. **Services: Dominando a Dualidade (`02.02.02_Services_Dominando_a_Dualidade.pdf`):** Explica a diferença entre `ApplicationService` (onde sua lógica de negócios reside) e `cds.Service` (a interface genérica para interagir com qualquer serviço, seja ele local ou remoto).

3. **Fluxo de Requisições: Síncrono e Assíncrono (`02.02.03_Fluxo_Requisicoes_Sync_Async.pdf`):** Detalha o fluxo de uma requisição através das fases de um evento (`before`, `on`, `after`), explicando o papel do `Promise chain` e como manipular o objeto de requisição (`req`) e os dados (`req.data`).

4. **ApplicationService Mastery (`02.02.04_ApplicationService_Mastery.pdf`):** Um guia avançado sobre a classe `ApplicationService`, da qual seus serviços herdam. Aborda o método `init()` e outras técnicas para estruturar sua lógica de negócios de forma modular e reutilizável.
