# Como realizar consultas de maneira simples no ambiente complexo de Big Data com Hive e Impala

Hive e Impala

- ​	Provem SQL para consulta nos dados do HDFS e HBase

- Hive

  - Software construido sobre o Apache Hadoop

  - Desenvolvido em 2007 pelo Facebook

  - Fornece acesso semelhante ao SQL(HQL)

  - HQL(Hive Query Language)

  - Gera jobs MapReduce ou Spark no cluster Hadoop

  - Fluxo de processamento

    - Parse HiveQL
    - Make optimizations
    - Plan execution
    - Submit to cluster
    - Monitor progress
    - Data Processing Engine (Map Reduce)

  - Database

    - Criar um database

      - ```
        CREATE DATABASE loudacre
        ou
        CREATE DATABASE IF NOT EXISTS loudacre
        ```

    - Eliminar um database

      - ```
        DROP DATABASE loudacre
        ou
        DROP DATABASE IF NOT EXISTS loudacre
        ```

  - Tabela

    ```
    CREATE TABLE jobs (
    	id INT,
    	title STRING,
    	salary INT,
    	posted TIMESTAMP
    )
    ROW FORMAT DELIMITED
    FIELDS TERMINATED BY ',';
    ```

    Existem dois tipos de tabela

    - Managed (Gerenciada)
      - Basicamente um arquivo criado pelo próprio no HDFS
      - Caso você drope a tabela, todo o dado posteriormente criado será eliminado no processo
    - EXTERNAL
      - Cria um metadado para acesso ao arquivo no HDFS
      - Nesse caso, se dropar a tabela, o dado permanecerá

  - Formatos de arquivos

    - Parquet
      - Formato colunar
      - Reduz o espaço de armazenamento
      - Aumenta a performance
      - Mais eficiente ao adicionar muitos registros de uma vez
      - A melhor escolha par acesso a dados colunares
    - Apache ORC
    - AVRO

  - Particionamento

    - Ajudar com performance

    - Uma partição é uma pasta e consegue ler como uma coluna

    - Particionamento pouco demais

      - Rediz a latencia no máximo pela metade

    - Particionar demais

      - Causa muito carga sobre namenode do cluster porque ele precisa manipular o grande número de diretórios 

    - Criar uma tabela particionada

      - ```
        CREATE TABLE tab_part
        (viewTime INT, userid BIGINT, page_url STRING, referrer_url STRING, ip STRING)
        COMMENT 'Essa tabela é particionada'
        PARTITIONED BY (dt STRING, country STRING)
        STORED AS TEXTFILE;
        ```

- Impala

  - Uma engine MPP (Massive Parallel Processing) open source para execução de queries SQL em ambiente Hadoop
  - Inspirado no projeto Google Dremel
  - Possui baixa latencia
  - Desenvolvida pela Cloudera em 2012 e agora é um top Project da Apache
  - Oferece melhora de performance de 5x a 50x
  - Ideal para queries interativas e analise de dados
  - Fluxo de processamento
    - Parse Impala SQL
    - Make optimizations
    - Plan execution
    - Execute query on the cluster

- Hive x Impala

  - Impala não salva resultados intermediários no disco durante consultas demoradas. Dependendo da versão, o Impala cancela uma consulta em execução se algum host no qual essa consulta está executando falhar

  - Se uma aplicação tiver necessidade de processamento em lote de dados o hive pode ser a melhor opção

  - Se houver necessidade de processamento em tempo real de consultas ad-hoc em um subconjunto de dados, o Impala será a melhor opção

  - Impala é mais rapido que o Apache Hive, mas isso não significa que ele seja a única solução SQL para todos os problemas de big data

  - O impara consome muita memória e não é executado de forma eficiente para operações de dados pesados, como joins, porque não é possível inserir tudo na memoria

  - |                           | Relational Database | Hive        | Impala      |
    | ------------------------- | ------------------- | ----------- | ----------- |
    | Query language            | SQL(full)           | SQL(subset) | SQL(subset) |
    | Update individual records | Yes                 | No          | No          |
    | Delete individual records | Yes                 | No          | No          |
    | Transactions              | Yes                 | No          | No          |
    | Index support             | Extensive           | Limited     | No          |

- Metastore

  - Banco de dados com tabelas que armazenam informações de schema o Hive e Impala vai utilizar

  - Caminho padrão

    - ```
      /user/hive/warehouse/<table_name>
      ```

  - Fluxo

    - Query>Acessa Metastore>Acessa HDFS

- Link vm

  - ```
    https://drive.google.com/file/d/1CsHc311jp4EuZ8be5KGaumniGAafa8sC/view?usp=sharing
    ```

- Arquivo suporte

  - ```
    https://gitlab.com/vmb1/hive
    ```

- Slides

  - ```
    https://drive.google.com/file/d/1duwf7g9lfAsIOJWRL26tx8RBfV8ySPon/view
    ```

    





