# Módulo 1 (Parte 2): Fundamentos e Modelagem - Linguagens Core (CDL, CSN, CXN)

![Infografico - O Ecossistema SAP CDS](../Infograficos/01.02.01_SAP_CDS_Projeto_e_Realidade.png)

Este diretório aprofunda o conhecimento nas linguagens que formam o coração do SAP Cloud Application Programming Model (CAP). Entenderemos como o Core Data Services (CDS) se materializa através de diferentes representações, cada uma com um propósito específico no ciclo de vida do desenvolvimento.

## Tópicos Abordados

Os documentos a seguir detalham as linguagens essenciais do CDS:

1. **SAP CDS: Do Projeto à Realidade (`01.02.01_SAP_CDS_Projeto_e_Realidade.pdf`):** Conecta a fase de design do modelo com sua implementação prática, mostrando como o CDS traduz a intenção de negócio em artefatos de software concretos.

2. **CDL: Modelagem Inteligente (`01.02.02_CDL_Modelagem_Inteligente.pdf`):** Foco na **CDS Definition Language (CDL)**, a linguagem declarativa usada por desenvolvedores para criar modelos de dados, serviços e anotações de UI de forma legível e concisa.

3. **CSN: A Anatomia dos Modelos (`01.02.03_CSN_Anatomia_dos_Modelos.pdf`):** Explora a **CDS Schema Notation (CSN)**, a representação JSON canônica de um modelo CDS. O CSN é o que o compilador CDS gera e o que os runtimes (Node.js/Java) consomem.

4. **CXN: O Blueprint do CDS (`01.02.04_CXN_The_CDS_Blueprint.pdf`):** Apresenta uma visão sobre os modelos Core Expression Notation (CXN), um formato intermediário utilizado pelo compilador CDS para processar e avaliar expressões complexas, garantindo consistência e otimização antes da geração do CSN final.
