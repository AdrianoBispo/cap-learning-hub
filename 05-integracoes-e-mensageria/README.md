# 05. Integrações e Mensageria

Aplicações modernas não vivem isoladas. Este módulo aborda a comunicação síncrona e assíncrona com o mundo exterior.

## Conteúdo

### 1. Serviços Remotos (`cds.RemoteService`)
Para consumir APIs externas (ex: S/4HANA), o CAP utiliza `cds.connect.to`. Ele cria um proxy que permite consultar o serviço remoto usando a mesma sintaxe CQN usada para o banco de dados local (`srv.run(SELECT...)`), abstraindo a complexidade de HTTP e autenticação.

### 2. Mensageria Assíncrona (Event Mesh)
O `cds.MessagingService` permite arquiteturas desacopladas.
*   **Emissão:** Use `srv.emit('Evento', dados)` para publicar mensagens.
*   **Recepção:** Use `srv.on('Evento', handler)` para reagir.
*   O CAP suporta **CloudEvents** e integra-se transparentemente com brokers como SAP Event Mesh e Redis.
