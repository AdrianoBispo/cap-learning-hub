# Módulo 07 (Parte 2): Arquitetura Avançada - Plugins e Extensibilidade

![infografico - Criando Plugins CDS para Node.js](../Infograficos/07.02.02_Construindo_Extensoes_Modulares.png)

A capacidade de estender e adaptar uma aplicação sem modificar seu núcleo é um sinal de uma arquitetura madura e sustentável. O SAP CAP foi projetado com a extensibilidade em mente, permitindo que desenvolvedores e parceiros adicionem funcionalidades de forma modular e desacoplada, seja através de `plugins` reutilizáveis ou de extensões específicas para um projeto.

## Tópicos Abordados

1. **O Kit de Ferramentas de Extensibilidade do SAP CAP (`07.02.01_Extensibility_Toolkit.pdf`)**: Este material oferece uma visão geral do ecossistema de extensibilidade do CAP. Ele explora como usar `cds.env.features` para ativar ou desativar funcionalidades (`feature toggles`), como o `cds.requires` pode ser usado para compor aplicações a partir de módulos e como o `cds.extend()` permite modificar modelos e serviços existentes de forma não destrutiva.

2. **Construindo Extensões Modulares e Reutilizáveis (`07.02.02_Construindo_Extensoes_Modulares.pdf`)** Um guia prático para a criação de `plugins` e módulos de extensão. Aprenda a empacotar funcionalidades reutilizáveis, como `handlers` genéricos, `aspects` e lógicas de negócio, que podem ser facilmente adicionados a qualquer projeto CAP. O artigo aborda a publicação e o consumo de módulos via NPM, promovendo a componentização e o reuso.
