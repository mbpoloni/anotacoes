# 11-Monitoramento de clusters Hadoop de alto nível com HDFS e YARN

### Teoria e prática com HDFS

- Big Data

  - Processo de análise e interpretação de um grande volume de dados armazenados remotamente
  - Pode integrar qualquer dado coletado sobre um assunto ou uma empresa
  - Onde há um registro feito, a tecnologia o alcança
  - Ordem de Petabytes

- ![image-20211108110707343](https://github.com/mbpoloni/anotacoes_aula/blob/master/img/image-20211108110707343.png)

- Escalabilidade vertical

  - Aumentar a potencia computacional de uma máquina

- Escalabilidade horizontal

  - Intercalando máquinas menores, processamento distribuído

- Escalar elasticamente

  - Manter uma capacidade computacional menor, e quando precisar aumentar o poder computacional

- Cluster

  - Grupo de computadores que trabalham juntos, provê armazenamento, processamento e gerenciamento de recursos

  - Formando por Nós

    - Computador individual no cluster
    - Gerencia a distribuição de trabalho para os nós workers

  - Daemon

    - Programa(serviço) rodando em um nó
    - Cada um tem sua função no cluster

  - Hadoop

    - Projeto open source escrito em java
    - Escalável, confiável, processamento distribuido
    - S.O de big data
    - Pode utilizar hardware comum(commodity cluster computing)
    - Framework para computação distribuida, com filesystem distribuido (HDFS)
    - Infraestrutura confiável capaz de lidar com falhas(hardware, software, rede)
    - Core do Hadoop
      - Processing
        - Spark
        - MapReduce
      - Resource Management
        - Yarn
      - Storage
        - HDFS

  - HDFS

    - Hadoop distribuited file system

    - Baseado no Google FS

    - Escalável e tolerante a falhas

    - Arquivos texto, sequence file, Parquet, AVRO, ORC

    - Tamanho mínimo de um bloco é 128MB

    - Fator de replicação (default: 3)

      - Replica o arquivo 3 vezes entre as maquina

    - NameNode

      - Gerencia o namespace
      - Armazena as informações de localização das partes do arquivo

    - DataNode

      - Armazena os blocos de arquivos

    - Secondary NameNode

      - Oferece tarefas de ponto de verificação e manutenção do Namenode

    - Armazenamento distribuido:

      - O arquivo é dividido em partes e distribuído aos nodes

    - Copiar arquivo HDFS para local

      ```
      hdfs dfs -get /tmp/file_teste.txt
      ```

    - Ingestão manual

      ```
      hdfs dfs -put file_teste.txt /user/everis-bigdata/
      ```

  - Principais comandos

    - Subir os serviços

      ```
      sudo service hadoop-hdfs-namenode start
      sudo service haddop-hdfs-secondarynamenode start
      sudo service hadoop-hdfs-datanode start
      sudo service haddop-mapreduce-historyserver start
      sudo service haddop-yarn-resourcemanager start
      sudo service haddopyarn-nodemanager start
      ```

    - pegar os primeiros 10 registro do arquivo no hdfs

      ```
      hdfs hdfs -cat /tmp/file_teste.txt |head -10
      ```

    - criar um arquivo

      ```
      hdfs dfs -touchz /tmp/delete/empty_file
      ```

    - mostra as informações do hdfs

      ```
      sudo -u hdfs hdfs fsck /tmp/ -files -blocks
      ```

    - Endereço VM

      ```
      https://drive.google.com/file/d/1CsHc311jp4EuZ8be5KGaumniGAafa8sC/view?usp=sharing
      ```

  - YARN
  
    - Yet Another Resource Negotiatior
  
    - Gerenciamento de recusos
  
    - Gerenciamento e monitoramento de jobs
  
    - Recursos dos nós são alocados somente quando requisitado(via container)
  
    - Componentes
  
      - Application
        - um job subetido ao Hadoop
      - Application Master
        - gerencia a execução e o escalonamento das tarefas (1 por aplicação)
      - Container
        - unidade de alocação de recursos (ex: c1=1 Gb RAM, 2CPU)
      - Resource Manager
        - gerenciador global de recursos
      - Node Manager
        - gerencia o ciclo de vida e monitora os recursos do Container
  
    - Olhar log
  
      - ```
        sudo -u hdfs yarn logs -applicationId
        application_1611089476809_0001 | more
        ```
  
    - Gravar log em um arquivo local
  
      - ```
        sudo -u hdfs yarn logs -applicationId application_1611089476809_0001 > wordcount.log
        ```
  
- Caminho apresentação

  - ```
    https://drive.google.com/file/d/1mSzcFASKCTir5ecdRNA7hHb7DoVfOMM0/view
    ```

    

