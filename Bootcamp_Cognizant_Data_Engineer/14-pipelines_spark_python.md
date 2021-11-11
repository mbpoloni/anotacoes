# Criando pipelines de dados eficientes com Spark e Python

- Spark
  - Projeto de processamento de dados distribuído de código aberto que foi iniciado em 2009
  - Escrito em Scala, que é construído em cima da Java Virtual Machine e Java runtime
  - Capaz de ser executado no Windows e também no Linux
  - Mais de 500 organizações utilizam Spark
  - Spark como uma abstração
    - Permite que os desenvolvedores criem rotinas de processamento de dados complexas e de vário estágios, fornecendo uma API de alto nível e uma estrutura tolerante a falhas que permite ao programadores se concentrar na lógica em vez de questões ambientais ou de infraestrutura
  - Spark é rápido, eficiente e escalonável
    - Implementa uma estrutura distribuída e tolerante a falhas a memória chamada Resilient Distributed Dataset(RDD)
    - Maximiza o uso da memória em várias máquinas, melhorando o desempenho geral em ordens de magnitude. A reutilização dessas estruturas na memória pelo Spark o tona adequado para operações iterativas de aprendizado de máquina, bem como para consultas interativas