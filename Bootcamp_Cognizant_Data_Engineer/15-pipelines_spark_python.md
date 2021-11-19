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
      - A UI do applications Mater para um aplicativo Spark é a UI do Spark. Isso está disponível como um link da UI do Resource Manager
    - Executors
      - Quem de fato irá executar a tarefa

  - DAG

    - Local para verificar o comportamento do Job

  - Ambientes nuvem para Spark e Hadoop

    - AWS
      - EMR Elastic Map Reduce
        - 
      - AWS Gue DataBrew
        - Spark atraves de pipelines
        - Spark gráfico
        - As service

  - Databricks

    - https://community.cloud.databricks.com

  - Stream

    - Processamento de eventos em tempo real am sistemas big data
    - Capacidade de consumir, processar e obter insights de fontes de dados de streaming
    - Objetivos Spark Streaming
      - Latência baixa
      - Processamento de evento unico(e apenas uma vez)
      - Integração com Spark Core API

    - Porque
      - Necessidade de processamento de eventos como um componente-chave
      - Processamento de eventos integrado com sua estrutura de lote baseada em RDD
      - A abordagem Spark Streaming
        - Apresenta o conceito de discretized streams (ou DStreams)
        - São essencialmente lotes de dados armazeandos em vários RDDs, cada lote representando uma janela de tempo (normalmente em segundos)
        - Os RDDs resultantes podem ser processados usando a API Spark RDD principal e todas as transformações disponíveis

  - Máquina virtual

    - https://drive.google.com/file/d/1CsHc311jp4EuZ8be5KGaumniGAafa8sC/view?usp=sharing

  - Stream Context

    - Representa uma conexão a uma plataforma ou cluester Spark usando SparkContext
    - Usado para cirar os datasources de Dstreams controle a computação de streaming e as tranformações de DStream
    - Especifica o argumento bbatchDuration, que é um intervalo de tempo em segundos pelo qual os dados streaming serão divididos em lotes
    - Depois de instanciar um StreamingContext, você criaria uma conexão com um fluxo de dados e definiria uma série de tranformações a serem realizadas
    - o método start() ou ssc.start() é usado para acionar os dados de entrada depois que um StreamingContext é estabelecido
    - O Streaming Context pode ser interrompido programaticamente usando ssc.stop() ou ssc.awaitTermination()
    - Storage padrão MEMORY_AND_DISK_SER_2

  - Slides

    - https://drive.google.com/file/d/1a38ZM9QxjOCtWuLz6q-hdxhWS3eaeFvD/view

  - Cenário Lógico

    - Aquilo que está conversando com o usuário, mas tem que ser levado em consideração o que ele tiver disponivel

  - Cenário Físico

    - Analisar as necessidades e as ferramentas disponiveis

  - On Premises

    - Uma especie de Datalake, datacenter dentro do cliente
    - Data Source, Data Ingestion, File System, Storage, Data Visualization, Rest API
    - ![image-20211119102808385](https://github.com/mbpoloni/anotacoes_aula/blob/master/img/image-20211119102808385.png)

  - Cloud

    - Armazenamento e gerenciamento em nuvem

  - Camadas
  
    - Ingestão de dados divididos em camadas, prática de mercado
      - Raw Zone
        - Guardas as informações do jeito que elas vieram
      - Trusted Zone
        - Ingestão mais direcionada a regra de negocio
      - Refined Zone
        - Visões para relatorios
  
  - Armazenamento
  
    - Avro
  
      - Base em linhas
      - Serailização de suporte
      - Formato binario rapido
      - Suporta compressao de bloco divisivel
      - Evolução do esquema de suporte
      - Armazena o esquema no cabeçalho do arquivo
  
    - Parquet
  
      - Orientado por coluna
      - Altas taxas de compressao
      - Apenas colunas necessárias são buscadas
      - Pode ser lido e escrito usando Avro API
  
    - ORC
  
      - Orientado por coluna
      - Altas taxas de compressao
      - Suporte ao tipo Hive
      - Metadados armazenados usando buffers de protocolo
      - Compatível com HiveQL
      - Suporte e serialização
  
    - Spark SQL
  
      - Ler dataframe
  
        - ```
          df1 = spark.read.format("csv").option("header", "true").load(path)
          ```
  
      - Repartir e salvar df
  
        - ```
          df1.repartition(2).write.format("parquet").mode("overwrite").save(path)
          ```
  
      - Tabela temporaria
  
        - ```
          df1.createOrReplaceTempView(nome_tabela)
          ```
  
      - Consulta com SQL
  
        - ```
          spark.sql('SELECT...').show()
          ```
  
      - Slides
  
        - https://drive.google.com/file/d/1Hl7NaISZ8_u8es8q5cK2U6VZ_mzNbD35/view?usp=sharing
  
    

