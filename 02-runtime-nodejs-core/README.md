# 02. Runtime Node.js Core

Este módulo detalha como o CAP ganha vida no ambiente Node.js. O runtime é responsável por servir os modelos, gerenciar transações e orquestrar o fluxo de eventos.

## Conteúdo

### 1. Bootstrap e Servidor (`server.js`)
O comando `cds serve` inicia o processo, mas o verdadeiro poder reside na customização do `server.js`. O bootstrap emite eventos como `bootstrap`, `served` e `listening`, permitindo a injeção de middlewares Express ou configurações customizadas.

### 2. Event Handlers e Serviços
Tudo no CAP é um serviço (`cds.Service`). A lógica de negócios é implementada interceptando eventos nas fases:
*   **`@Before`**: Validações e pré-processamento.
*   **`@On`**: Implementação core (ex: leitura/escrita no DB).
*   **`@After`**: Enriquecimento de resultados.

### 3. Ferramentas Essenciais (SDK e Utils)
*   **`cds.context`**: O armazenamento local assíncrono que carrega o usuário, tenant e locale através da pilha de execução.
*   **`cds.utils`**: Uma caixa de ferramentas para manipulação de arquivos, UUIDs e caminhos de forma segura e agnóstica ao sistema operacional.
