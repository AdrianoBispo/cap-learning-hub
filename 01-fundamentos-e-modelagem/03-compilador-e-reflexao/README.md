# Módulo 1 (Parte 3): Fundamentos e Modelagem - Compilador CDS

![Infografico - Guia Rapido sobre o Compilador CDS do SAP CAP com Node.js](../Infograficos/01.03.02_Compiler_Deep_Dive.png)

Este diretório explora duas das capacidades mais poderosas do SAP CAP: o compilador CDS e a API de reflexão. Juntos, eles permitem a transformação de modelos declarativos (CDL) em representações consumíveis (CSN) e a interação dinâmica com esses modelos em tempo de execução.

## Tópicos Abordados

Os documentos a seguir abordam o processo de compilação, a introspecção de modelos e técnicas de modelagem avançada:

1. **Introdução ao Compilador CDS (`01.03.01_Introducao_ao_Compilador_CDS.pdf`):** Apresenta o papel fundamental do compilador `cds.compile`, que transforma os arquivos `.cds` (CDL) em um formato JSON canônico (CSN), o qual é utilizado pelos serviços e runtimes.

2. **Dominando o Compilador de Modelos CAP (`01.03.02_Dominando_Compilador_de_Modelos_CAP.pdf`):** Um mergulho profundo nas funcionalidades do compilador, incluindo a "tradução" para diferentes alvos (como SQL DDL e OData metadata), extensibilidade e o uso de "backends".

3. **Dominando a Reflexão de Modelos (`01.03.03_Dominando_Reflexao_de_Modelos.pdf`):** Demonstra como usar a API de reflexão (`cds.reflect`) para inspecionar a estrutura de um modelo (entidades, propriedades, anotações) em tempo de execução, permitindo a criação de lógicas genéricas e dinâmicas.

