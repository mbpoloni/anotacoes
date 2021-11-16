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
    
  - Aplicabilidade
  
    - ETL
    - Análise preditiva e aprendizado de máquina
    - Operações de acesso a dados (como consultas e visualizações SQL)
    - Mineração e processamento de texto
    - Processamento de eventos em tempo real
    - Aplicativos gráficos
    - Reconhecimento de padrões
  
  - Linguagens
  
    - Scala (nativa)
    - Python
    - Java
    - SQL
    - R
  
  - Exemplos RDD:
  
    - Python
  
      - ```
        rddArquivo = sc.textFile("hdfs///;//meucluster/data/arquivo.txt")
        ```
  
    - Scala
  
      - ```
        val rddArquivo = sc.textFile("hdfs://meucluster/data/arquivot.txt")
        ```
  
  - Uso interativo
  
    - Consegue trazer os arquivos e debugar códigos
  
  - Uso não iterativos
  
    - Uso do spark-submit
    - Consegue submeter programas desenvolvidos
  
  - Anatomia do Spark
  
    - Driver
      - Interface entre o Job e o cluster
      - Orquestra as tarefas que cada worker precisa realizar
      - Determina o ciclo de vida da aplicação Spark
      - Responsável por criar o SparkContext
      - 
    - Cluster Manager
      - Gerenciador do cluster
      - Yarn, Mesos
      - Gerenciador de recursos
    - Spark Master
      - Processo que solicita recursos no cluster e os disponibiliza para o driver Spark
      - Responsável por gerenciar esses containers(executors) durante o ciclo de vida do aplicativo  Spark
      - A UI do applications Mater para um aplicativo Spark é a UI do Spark. Isso está disponivel como um link da UI do Resource Manager
    - Executors
      - Quem de fato irá executar a tarefa
  
  - DAG
  
    - Local para verificar o comportamento do Job
    - 

