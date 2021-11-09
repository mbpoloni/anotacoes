# Introdução a Engenharia de Dados na AWS

### Conheça os serviços da AWS

- Conceitos de big data
  - A falha em tratar corretamente dos desafios de big data causam:
    - Escalada de custos
    - Redução de produtividade e competitividade
  - Uma estratégia sólida de big data pode ajudar as organizações a:
    - Reduzir custos
    - Ganhar eficiência
  - Na maioria dos casos, o processamento de big data envolve um fluxo de dados comum, da coleta de dados brutos ao consumo de informações práticas
    - Coletar dados brutos
    - Armazenar de forma segura e escalável
    - Processar e analisar transformando os dados
    - Consumir e visualizar de forma amigável e agregando valor
- Divisão de Big data na AWS
  - Collection
  - Storage
  - Processing
  - Analysis
  - Visualization
- AWS Snow Family
  - Dispositivos portáteis altamente seguros para coletar e processar dados e migração para dentro e para fora da AWS
    - Migração
      - Snowcone
      - Snowball edge
      - Snowmobile
    - Edge computing
      - Locais em que não tem constante acesso para transferência de dados
      - Snowcone
      - Snowball edge
  - Aplicações
    - Conectividade limitada
    - Banda limitada
    - Alto custo da rede
    - Banda compartilhada reduz taxa de transferência
    - Conexão instável
- AWS Kinesis
  - Alternatica gerenciada ao Apache Kafka
  - Ótimo para logs de aplicativos, métricas, IoT, clickstreames, big data "em tempo real" e frameworks de processamento de streaming
  - Dados replicados automaticamente de forma síncrona para 3 AZ
  - 3 Módulos
    - Kinesis Streams
      - Ingestão de streaming de baixa latencia em escala (vídeo e data streams)
      - Os fluxos são divididos em fragmentos (shards)
      - A capacidade total de um stream é a soma da capacidade dos shards
      - Taxa de ingestão = 1MB ou 1000 mensagens/segundo
      - Taxa de leitura = 2MB/s
      - Retenção de dados é de 24 horas por padrão, pode ir até 7 dias
      - Capacidade de reprocessar/reproduzir dados
      - Vários aplicativos podem consumir o mesmo fluxo
      - Partition Key : agrupar dados por shard em um stream
      - Sequence Number: número único por partition key dentro de um shard
    - Kinesis Analytics
      - Análises em tempo real em streams usando SQL
    - Kinesis Firehose
      - Fluxos de carga em S3, Redshift, ElasticSearch e splunk
  - Kinesis producers
    - aplicativo que insere registros de dados de usuário em um stream de dados do Kinesis - Ingestão
  - Kinesis Consumers
    - aplicação para ler e processar registros de dados de streamings de dados do Kinesis
  - Kinesis Agent
    - monitora continuamente um conjunto de arquivos e envia novos dados ao stream, baseado em Java
  - Kinesis Analistics
    - Maneira fácil de tranformar e analisar dados de straming em tempo real com o Apache Flink (estrutura e um mecanismo de código aberto para o processamento de streams de dados)
    - Streaming ETL
    - Geração continua de métricas
    - Análise responsiva
  - Kinesis Firehose
    - Serviço totalmente gerenciado, sem administração
    - Quase em tempo real (latencia de 60 segundos)
    - Carregar dados no Redshift / Amazon S2 / ElasticSearch / Splunk
    - Escala automática
    - Suporta diversos formatos de dados
  - Elastic MapReduce
    - Serviço totalmente gerenciado
    - Estrutura gerenciada do Hadoop em instancias EC2 (máquinas virtuais da AWS)
    - Inclui spark, HBase, Presto, Flink, Colmeia, e mais
    - Notebook EMR
      - Cluster EMR
        - Master node
          - Gerencia o cluster
          - Rastreia o status das tarefas, monitora o cluster
          - Única instância EC2
          - Também conhecido como "nó lider"
        - Core node
          - Hospeda dados HDFS e executa tarefas
        - Task Node
          - Executa tarefas, não hospeda dados
          - Opcional
          - Sem risco de perda de dados ao remover
          - Bom uso de instâncias pontuais
    - Vários pontos de integração com AWS
    - HDFS

- AWS Glue
  - Serviço de integração de dados sem servidor
  - AWS DataBrew
    - ferramenta visual para enriquecer, limpar e normalizar os dados sem escrever código
  - AWS Flue Elastic Views
    - permite utilizar SQL para combinar e replicar os dados em diferentes armazenamento de dados
  - Glue Crawler verifica dados em S3 e cria esquemas
    - Pode ser executado periodicamente
    - Preenche o catalogo de dados do glue
    - Armazena apenas a definição da tabela
    - Os dados originais permaecem no S3
  - Dados não estruturados são tratados como estruturados
    - Redshift Spectrum
    - Athena
    - EMR
    - Quicksight
- AWS Redshift
  - Serviço de armazenamento de dados gerenciado em escala de petabytes
  - desempenho 10 x melhor do que outro DW
  - projetado para OLAP (Online analytical processing), não OLTP(Online transaction processing)
  - economico
  - interfaces SQL, ODBC, JDBC
  - escala sob demanda
  - replicação e backups integrados
  - monitoramento via CloudWatch / CloudTrail
  - Usos
    - acelerar as cargas de trabalho de análise
    - data warehouse e data lake unificados
    - modernização do data warehouse
    - analisar dados de vendas globais
    - armazenar dados históricos do mercado de ações
    - analisar impressoes de anuncios e cliques
    - dados de jogos agregados
    - analisar tendencias sociais

### Mão á obra

- Criando delivery stream

  - Boa prática bucket não usar camelcase

- Serviço de instancias EC2

  - Conexão via Putty
  - login padrão 
    - ec2-user

- JSON contendo os flows com as instruções

- Github

  - https://github.com/cassianobrexbit/dio-live-aws-bigdata-2

- Slides

  - https://drive.google.com/file/d/1JlfVVU1ee5f1COL9Fb2TH5_WWxzix0SU/view

  







