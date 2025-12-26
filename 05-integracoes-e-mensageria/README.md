# Módulo 5: Integrações e Mensageria

![Infografico - ](./Infograficos/05.01.01_Dominando_a_Conexão_de_Serviços_com_CAP.png)

Nenhuma aplicação vive em uma ilha. Este módulo explora como as aplicações SAP CAP se comunicam com o mundo exterior, seja consumindo outros serviços em tempo real ou participando de arquiteturas de eventos assíncronas.

Você aprenderá os padrões para construir aplicações que se integram de forma robusta e escalável com outros sistemas, como um S/4HANA, ou com outros microserviços.

## Estrutura do Módulo

### 1. [Serviços Remotos e Integração Síncrona](./01-servicos-remotos/README.md)

Aprenda a consumir APIs externas (OData ou REST) de forma transparente e eficiente.
- **Conexão e Consumo:** Usando `cds.connect.to('MyExternalAPI')`, o CAP cria um objeto de serviço proxy para o sistema remoto.
- **Abstração de Protocolo:** Uma vez conectado, você pode usar a mesma API fluente (`cds.ql`) para interagir com o serviço externo como se fosse uma fonte de dados local. O CAP gerencia a chamada HTTP, a autenticação (via Destinations) e a tradução dos dados, simplificando drasticamente o código de integração.

### 2. [Mensageria e Comunicação Assíncrona](./02-mensageria-assincrona/README.md)

Construa sistemas desacoplados e resilientes utilizando o paradigma de eventos.
- **`MessagingService`:** O CAP fornece uma abstração para brokers de mensagens (como SAP Event Mesh, RabbitMQ, Redis).
- **Publicar e Assinar:** Use a API simples `srv.emit('MeuEvento', payload)` para publicar uma mensagem e `srv.on('MeuEvento', handler)` para se inscrever e reagir a ela.
- **Microserviços Orientados a Eventos:** Este padrão é a base para criar microserviços que reagem a mudanças de estado em outros sistemas sem acoplamento direto, permitindo maior escalabilidade e resiliência. O CAP também pode propagar eventos de alteração de dados (CRUD) automaticamente.

---

Ao concluir este módulo, você será capaz de projetar e implementar soluções que não apenas expõem dados, mas também se conectam a um ecossistema mais amplo de serviços e eventos, uma habilidade essencial para o desenvolvimento de aplicações empresariais modernas.