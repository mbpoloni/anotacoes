# Explorando o poder do NoSQL com Cassandra e HBase

### Conceitos de NoSQL e requisitos básicos

- No SQL
  - Not Only SQL
  - Não SQL, Não Relacional
  - Termo genérico para representar os bancos de dados não relacionais
  - Surgiu da necessidade de gravação e leitura mais rápida e altas requisições simultâneas
- Relacional vs NoSQL

| Quando considerar NoSQL                                      | Quando considerar Relacional                                 |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| Carga de trabalho de alto volume que exigem grande escala    | Carga de trabalho é consistente e requer escala média para grande |
| Carga de trabalho não exigem garantias do ACID               | Garantias de ACID são necessárias                            |
| Os dados são dinâmicos e frequentemente alterados            | Dados são previsíveis e altamente estruturados               |
| OS dados podem ser expressos sem relações (joins)            | Os dados são expressos de maneira relacional                 |
| Alta velocidade de gravação e a segurança de gravação não é critica | A garantia de gravação é um requisito                        |
| Consulta de dados é simples e tende a ser simples            | Consulta e relatórios complexos                              |
| Dados exigem uma ampla distribuição geográfica               | Usuários são mais centralizados                              |

- Teorema de CAP
  - Ou Teorema de Brewer
  - Indica que o armazenamento de dados distribuidos só podem atender dois dos três atributos
    - Consistencia
    - Disponibilidade
    - Partição Tolerante a falhas
  - Por quê NoSQL no Big Data?
    - Pela melhor performance nas queries em grande volume de conjunto de dados (dataset)
    - Não é necessário analisar todo o conjunto de dados para fazer operações
  
- HBase
  - NoSQL distribuido e orientado a colunas (Column Familily ou Wide Column)

  - O armazenamento do Hbase é um esparso, distribuído, persistente, multidimensional e ordenado Map.

    - MAP: Tem chave e valor

  - Desvantagens
    - Não ter uma linguagem própria de SQL
    - Não suportar indices em colunas fora do 
    
  - Maior vantagem é a facilidade e integração com o ecossistemas Hadoop

  - Map

    - é indexado por uma linha chave (row key), coluna chave(column key), e uma coluna timestamp

    - Cada valo no Map é interpretado como um vetor de bytes (array of bytes)

    - O array of bytes nos permite gravar portanto qualquer informação se for necessário, inclusive documentos, arquivos, JSON, csv

    - Núcleo de dados do Hbase é um map

      ```
      {
      	"zzzzz": "Olá",
      	"xyz": "hello",
      	"aaaa": "world Hbase",
      	"1": "x",
      	"aaaa": "y"
      }
      ```

    - Multidimensional e ordenado

      - Criar listas dentro de listas

      ```
      {
      	--Row key--
      	"1": {
      		--columns family
      		"A": --valores "y",
              "B": --valores "w"
      	}
      }
      ```

  - Arquitetura Hbase

    ​	![image-20211021190038442](https://github.com/mbpoloni/anotacoes_aula/blob/master/img/image-20211021190038442.png)

    - Client
      - Responsavel por encontrar o Region Servers que estão atendendo as linhas em particular que estão sendo utilizadas, para isso é conslutado uma base de dados de matedados interna do Hbase, hbase:meta, que fica no Zookeeper
    - Zookeeper
      - Faz os nós conversarem entre si
      - É reponsavel por dar visibilidade a todos os nós de serviços do Hbase de que é o master atual, são servidores que atendem ao papel RegionServers, Region
    - HMaster
      - Responsavel por monitorar todas as instancias de RegionServer no cluster
      - É meio para todas as solicitações de mudanças de metadados
      - Recebe a requisião do cliente e verificar nos Region server qual contem a tabela
    - Region server
      - Quem faz a consulta no HDFS
        - Region - Representam os elementos básicos de disponibilidade e distribuição das tabelas e incluem o armazenamento de cada column family
    - HDFS
      - Responsável por fazer todas replicações
      - É o sistema de arquivos do ecossistema Hadoop
      - Cada arquivo está armazenado em múltiplos blocos e mantem tolerancias a falhas, os blocos são replicados pelo cluster Hadoop

- Cassandra

  - Banco de dados distribuido e orientado a colunas
  - Os dados armazenado são tipados e há conceitos mais complexos de modelagem como chave primário composta, partition key e cluster key
  - Possui linguagem CQL
  - Grande diferença para o Hbase
    - o Cassandra suporta tabela secundário de indices e permite filtros em colunas fora da primary key
  - Característica principal é armazenar em múltiplos nós sem nenhum ponto de falha
  - Conexão entre os nós é realizada de ponto a ponta, utilizando um protocolo chamado Gossip
  - Todos os nós sabem de todos nós
  - Componentens do cassandra
    - Node
      - Nó responsavel por armazenar os dados, é um componente básico da Arquitetura
    - Data Center
      - Representa uma coleção de nós
    - Cluster
      - Representa a coleção de vários Data Centers
    - Commit Log
      - Cada operação é escrita no log de commit. Esse logo é utilizado para recuperação em caso de incidentes graves
    - Mem-table
      - Depois que o dado é escrito no log de commit, o dado é escrito no Mem-table. O dado nessa localidade é temporário.
    - SStabte
      - Quando o Mem-table atingiu o limite, o dado é gravado no SStable

### Comandos gerais

- ```
  hbase shell
  ```

  - Chama o console do Hbase

- ```
  status
  ```

  - Trás o detalhamento dos servidores presentes

- ```
  version
  ```

  - Versão do Hbase

- ```
  table_help
  ```

  - Auxilia como utilizar comando que se referenciam a uma tabela

- Tabelas ou não podem estar no schema

- Não é possivel alterar um column family se a tabela estiver ativada

- Arquitetura voltada a eventos

  - Bancos noSQL com o objetivo de ser temporarios
  - Colunas com propriedades TTL

- Qualquer alteração de schema da tabela é necessário desabilita-la antes, para manter a consistencia nos dados

- ```
  create 'funcionario', 'pessoais', 'profissionais'
  ```

| funcionario | pessoais | profissionais |
| ----------- | -------- | ------------- |

- ```
  put 'funcionario', '1', 'pessoais:nome', 'Maria'
  ```

  ​	Insere um registro

- ```
  scan 'funcionario'
  ```

  ​	Retorna os valores da tabela

- ```
  enable 'funcionario'
  ```

  ​	Habilita a tabela

- ```
  disable 'funcionario'
  ```

  ​	Desabilita a tabela

- ```
  alter 'funcionario', NAME=>'hobby', VERSIONS => 5
  ```

  ​	Altera a tabela funcionario, incluido uma Column chamada hobby

- ```
  scan 'funcionario', {VERSIONS=>3}
  ```

  ​	Demonstra os registros de versão anterior

- ```
  count 'funcionario'
  ```

  ​	Retorna a quantidade de rowkeys

- ```
  create 'ttl_exemplo', {'NAME'=>'cf', 'TTL'=>20}
  ```

  ​	Criar uma tabela temporario com nome cf e tempo de 20 segundos

- ```
  cqlsh
  ```

  ​	Comando cassandra

- Cenários de utilização

  - ![image-20211025190628032](https://github.com/mbpoloni/anotacoes_aula/blob/master/img/image-20211025190628032.png)
  - ![image-20211025190640568](https://github.com/mbpoloni/anotacoes_aula/blob/master/img/image-20211025190640568.png)
  - ![image-20211025190824444](https://github.com/mbpoloni/anotacoes_aula/blob/master/img/image-20211025190824444.png)

