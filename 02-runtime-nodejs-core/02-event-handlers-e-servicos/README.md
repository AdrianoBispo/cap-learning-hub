# Módulo 02 (Parte 2): Event Handlers e Serviços

![Infográfico sobre a Anatomia de um Serviço](../Infograficos/02.02.01_Anatomia_de_um_Servico.png)

O coração da lógica de negócios em CAP reside nos serviços e seus event handlers. Este módulo detalha como registrar handlers para eventos (CRUD), a dualidade dos serviços (sua definição vs. implementação), o fluxo de requisições e o uso da classe `ApplicationService`.

## Conteúdo

| Documento | Infográfico | Descrição |
| :--- | :--- | :--- |
| [A Anatomia de um Serviço CAP](./02.02.01_Anatomia_de_um_Servico.pdf) | [Visualizar](../Infograficos/02.02.01_Anatomia_de_um_Servico.png) | Descreve a estrutura de um serviço CAP, incluindo a definição (`.cds`) e a implementação (`.js`), e como elas se conectam. |
| [Dominando a Dualidade dos Serviços](./02.02.02_Services_Dominando_a_Dualidade.pdf) | [Visualizar](../Infograficos/02.02.02_Services_Dominando_a_Dualidade.png) | Explora a separação entre a definição da API do serviço e sua implementação, um conceito-chave para criar serviços flexíveis. |
| [Fluxo de Requisições: Síncrono e Assíncrono](./02.02.03_Fluxo_Requisicoes_Sync_Async.pdf) | [Visualizar](../Infograficos/02.02.03_Fluxo_Requisicoes_Sync_Async.png) | Ilustra o ciclo de vida de uma requisição, desde o cliente até a resposta, passando pelas fases `before`, `on` e `after` dos event handlers. |
| [Mestria do `ApplicationService`](./02.02.04_ApplicationService_Mastery.pdf) | [Visualizar](../Infograficos/02.02.04_ApplicationService_Mastery.png) | Um guia para a classe `ApplicationService`, a base para a criação de toda a lógica de negócios customizada em suas aplicações. |