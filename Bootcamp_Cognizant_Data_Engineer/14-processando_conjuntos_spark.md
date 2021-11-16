# Processando grandes conjuntos de dados de forma paralela e distribuída com Spark

- Spark
  - Framework analítico distribuído, capaz de realizar diversas operações de maneira extremamente rápida
  
  - Framework in-memory, RAM é fundamental para o bom funcionamento
  
  - Computação distribuída
  
  - Permite usar diversas linguagens
    - Scala
    - Java
    - Python
    - R
    - SQL
  
  - 100x mais rápido que o mapreduce tradicional
  
  - Arquitetura
    - Drive Program (Máquina que esta gerindo os recursos do SPARK)
      - Spark Context (Gerenciar o acesso aos arquivos, quebra em tasks)
      
        - É o primeiro passo de um programa Spark
      
        - É o ponto de entrada do programa, ele é responsável por fazer a comunicação entre o programa e o ambiente
      
        - Quando o contexto é criado todos os objetos Spark criados ficam associados a este contexto
      
        - Várias propriedades do spark são configuradas diretamente no Spark Context
      
        - Criando Spark context em Scala
      
          - ```
            import org.apache.spark.SparkContext
            import org.apache.spark.SparkConf
            
            val conf = new SparkConf().setAppName("meu aplicativo spark")
            val sc = new SparkContext(conf)
            ```
      
            
    - Cluster Manager (Gerenciador de recurso (YARN))
    - Worker Node (Máquinas disponíveis para trabalhar)
      - Executor (Agrupador de tasks, pode conversar com outro executor)
        - Task
      - Cache
  
  - Bibliotecas
    - Apache Spark Core
      - Spark SQL
        - Voltada para processamento de dados estruturados
      - Spark Streaming
        - Voltado para dados vindos do Kafta, microbytes
      - MLlib
        - Módulo para trabalhar com Machine Learning
      - GraphX
        - Voltada para trabalhar com gráficos
  
  - RDD
    - Resilient Distributed Dataset
      - Principal abstração do Spark
      - Coleção de elementos particionados entre os diversos nós de um cluster
      - Resiliente a falhas
      - Naturalmente distribuídos, podendo existir em diversos nós de um cluster
      - Imutáveis
  
  - Cluster mode
    - O Spark distribuirá a carga entre diversas máquinas, nesse modo depende de gerenciadores de recursos
      - Yarn
      - Mesos
      - EC2
      - Kubernetes
  
  - VM
    - https://drive.google.com/file/d/1CsHc311jp4EuZ8be5KGaumniGAafa8sC/view?usp=sharing
  
  - Ler arquivo SQL com spark
  
    - ```
      val insurance = spark.read.format("csv").option("sep", ",").option("header", "true").load("file:///homr/everis/avengers.csv")
      insurance.show()
      ```
  
  - Pyspark
  
    - Shell interativo em python
  
    - ```
      insurance = spark.read.format("csv").option("sep", ",").option("header", "true").load("file:///homr/everis/avengers.csv")
      insurance.show()
      ```
  
  - Spark SQL
  
    - Módulo SQL do Spark, sendo ele uma abstração acia do core do Spark
  
    - Trabaha exclusivamente com objetos conhecidos como Dataframes e datasets. Estes são exevutados acima do Spark Core (RDDs). Em outras palavras, Dataframes e Datasets nada mais são que abstrações de tabelas dentro do Spark
  
    - Manipulação de dados quase que exclusivamente com SQL ANSI 2003
  
    - Permite trabalhar com diversas fontes de dados de maneira unificada, podendo cruzar diversas informações de maneira extremamente simples
  
    - Não trabalha com todos JDBC, necessário trabalhar com módulos
  
    - Operações que geram outro dataframe
  
      - ```
        df.printSchema()
        df.show(50, false)
        df.select("field1", "field2").show()
        df.select($"field1", $"field2"+1).show()
        df.filter($"age">21).show()
        df.groupBy("age").count().show()
        df.withColumn("new_column_name", col("old_column_name")).show()
        df.withColumn("new_column_name", col("old_column_name").cast("long")).show()
        df.avg("age").show()
        df.sum("sales").show()
        df.max("age").show()
        ```
  
    - Criar tempviews
  
      - ```
        df.createTempView(people)
        df.createOrReplaceTempView("people")
        df.createGlobalTempView("people")
        df.createOrReplaceGlobalTempView("people")
        ```
  
        
  
  - Spark Session
  
    - Ponto central do módulo de dataframes
  
    - Internamente tem um Spark Context associado
  
    - Várias aplicações podem ser aplicadas ao Spark Session
  
    - União do SQL Context e do Hive Context
  
    - Criar Spark Session
  
      - ```
        import org.apache.spark.sql.SparkSession
        
        val spark = SparkSession
        	.builder()
        	.appName("Spark SQL")
        	.config("configuracao", "valor da configuracao")
        	.getOrCreate()
        ```
  
    - 

