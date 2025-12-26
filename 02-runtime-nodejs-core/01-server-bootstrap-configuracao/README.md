# Módulo 2 (Parte 1): Runtime Node.js Core - Server Bootstrap e Configuração

![Infografico - Guia Completo do objeto CDS do SAP CAP Nodejs](../Infograficos/02.01.03_Objeto_cds_Guia_Completo.png)

Este diretório foca no coração do runtime do SAP CAP para Node.js. Abordaremos como um servidor CAP é iniciado, como as configurações são gerenciadas e qual o papel do objeto global `cds`.

## Conteúdo

Os documentos a seguir detalham o processo de inicialização e configuração de um serviço CAP em Node.js:

-   **Node.js Server Mastery (`02.01.01_Nodejs_Server_Mastery.pdf`):** Um guia completo sobre o `cds.server`, que é responsável por iniciar o servidor Express.js, carregar os modelos CDS e expor os serviços definidos.

-   **Desvendando `cds.env` (`02.01.02_Desvendando_cds_env.pdf`):** Explora o `cds.env`, o objeto central para configuração de aplicações CAP. Veremos como ele consolida configurações de `package.json`, variáveis de ambiente e perfis (`development`, `production`).

-   **O Objeto `cds`: Guia Completo (`02.01.03_Objeto_cds_Guia_Completo.pdf`):** Apresenta o objeto `cds`, que serve como o principal ponto de entrada para as APIs do CAP. Ele fornece acesso a serviços, ao modelo (`cds.model`), a utilitários e ao ciclo de vida da aplicação.
