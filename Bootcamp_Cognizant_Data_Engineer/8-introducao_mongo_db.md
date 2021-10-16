# Introdução ao MongoDB e banco de dados NoSQL

### Conhecendo os tipos de banco de dados NoSQL

- NoSQL

  - Not Only SQL

- Diferenças BD Relacional e NoSQL

  | Item           | BD Relacional                                                | No SQL                                                       |
  | -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
  | Escalabilidade | Aumento da capacidade para um unico recurso<br />Processador, memória e disco rígido<br />Escalabilidade em forma vertical | Replicas de dados apenas para leitura<br />Escalabilidade em forma horizontal<br />Particionando os dados (sharding) entre os nós é o mais conhecido |
  | Schemas        | Rígida e montada                                             | Ausença completa ou quase completa de schema<br />Schema-free/schemaless |
  | Performance    | Ligado diretamente a performance do disco rígido             | Depende do tamanho do cluster                                |
  | Transações     | Atomicidade - não é executado pela metade<br />Consistencia - quando a transação for concluída o banco vai estar conforme os esquemas pré definidos<br />Isolamento - uma trasação nunca irá interferir em outra transação<br />Durabilidade - quando a transação for concluida não será perdido | Basically Available<br />Soft-State<br />Eventually Consistent |

  - Características e vantegens de NoSQL

    - Flexibilidade
    - Escalabilidade
    - Alta performance

  - Tipos de banco de dados NoSQL

    - Document Store

      - São livres de esquemas podendo utilizar JSON, XML entre outros

      - Dados e documentos autocontidos e auto descritivos, permite redundância e inconsistência

      - Mais utilizados

        - Mongo DB

      - Mongo DB

        - Schema free

        - Alta performance

        - Código aberto

        - Utiliza json para armazenamento de dados

        - Tem suporte a indices

        - Auto-sharding - escala de forma horizontal

        - Map-reduce - ferramenta de consulta e agregação

        - GridFS - armazenamento de arquivos

        - Os dados não podem depender de outros dados

        - Estruturação

          - Document -> Tupla/Registro
          - Collection -> Tabela
          - Embedding/linking -> Join

        - Quando usar

          | Usar                   | Não usar                                       |
          | ---------------------- | ---------------------------------------------- |
          | Grande volume de dados | Necessidade de relacionamentos/joins           |
          | Dados não estruturados | Propriedades ACID e transações são importantes |
          
        - Client Mongo

          - robomongo.org

        - Mongo DBCloud

          - mongodb.com
          - Liberar o IP para acesso ao cluster
          - Criar usuário para acesso

        - Mongo DB Compass

          - Client de acesso ao cluster

        - Schema Design

          - Relações

            - Embedding

              - Documentos autocontidos - todos os dados estão dentro dele

                | Prós                                      | Contras                        |
                | ----------------------------------------- | ------------------------------ |
                | Consulta informações em uma unica query   | Limite de 16 MB por documentos |
                | Atualiza o registro em uma única operação |                                |

                

            - Referência

              - Documentos com dependência de outros documentos ou collections

                | Prós                                                         | Contras                                       |
                | ------------------------------------------------------------ | --------------------------------------------- |
                | Documentos pequenos                                          | Duas ou mais queries ou utilização do $lookup |
                | Não duplica informação                                       |                                               |
                | Usado quando os dados não são acessados em todas as consultas |                                               |

            - Recomendação de relacionamentos

              - One-to-one

                - prefira atributos chave-valor no documento

                  ```
                  {
                  	"_id": IbjectID("jsdhksdjahfsdkajgkfg"),
                  	"name": "Patrick,
                  	"steet": "Av das aguas",
                  	"numver": 102
                  }
                  ```

              - One-to-few ou one-to-many

                - preferivel embedding

                  ```
                  {
                  	"_id": ObjectId("sdlfhslkdjfsadkfjl"),
                  	"name": "Patrick",
                  	"adresses": [
                      	{"street": "Av das aguas", "number": 102},
                      	{"street": "Ruas vivas", "number": 100}
                  		]
                  }
                  ```

              - One-to-many ou Many-to-many

                - preferivel referencia

                  ```
                  {
                  	"_id": ObjetcId("dskajfhdskjfhs"),
                  	"name": "Patrick",
                  	"adresses": [
                  		ObjectId("123"), ObjectId("1234")
                  		]		
                  }
                  
                  /** Address*/
                  {
                  	"_id": ObjectId("123"),
                  	"street": "Av das aguas",
                  	"number": 102
                  }
                  ```

        - Boas práticas

          - Evitar documentos muito grandes
          - Usar campos objetivos e curtos
          - Analisar as queries utilizando explain()
          - Atualizar apenas campos alterados
          - Evite negações em queries
          - Listas/Arrays dentro dos documentos não podem crescer sem limite

        - JSON vs BSON

          - BSON
            - Serialização codificada em binário de documentos semelhantes a JSON
            - Contem extensões que permitem a representação de tipos de dados que não fazem parte da especificação JSON. Por exemplo, BSON tem um tipo de Date, ObjectID

        - Prática

          - listar os databases

            ```
            show databases
            ```

          - criar database - não possui comando especifico

            ```
            use nome_do_database
            ```

          - criar collections

            - pode ser criada da forma explicita e implicita

    - Key-Value Store

      - Armazena um conjunto de dados, simples ou complexos, identificados por um identificador exclusivo

      - Não existe definição de schema

      - Constituído por duas partes

        - Chave
        - Valor

      - Usos

        - Cache, sessão de usuário, carrinho de compra

      - Mais utilizados

        - Redis
        - DynamoDB

      - Redis

        - Características

          - Alto desempenho
          - Estrutura de dados na memória
          - Versatilidade de uso
          - Replicação e persistencia

        - Sandbox

          - try.redis.io

        - Atribuir valor a chave

          ```
          SET user1:name 'Bob Esponja'
          ```

        - Consultar valor da chave

          ```
          GET user1:name
          ```

        - Atribuir JSON a chave

          ```
          SET user '{"name": "Patrick", "age": 31}'
          ```

        - Definir tempo de expiração dos dados (ex - segundos, px-milisegundos)

          ```
          SET user2:name "Lula Molusco" EX 10
          ```

        - Verificar se a chave existe

          ```
          EXISTS user1:name
          ```

        - Inserir uma lista a uma chave

          ```
          LPUSH user1: hobbies "Caçar agua viva"
          ```

        - Consultar valor de uma lista com base no index

          ```
          LINDEX user1:hobbies 0
          ```

        - Consultar todos os valores da lista

          ```
          LRANGE user1:hobbies 0 1
          ```

        - Consultar o tipo de valor de uma chave

          ```
          TYPE user1:name
          ```

        - Consultar o tempo de expiração da chave

          ```
          TTL user1:name - retorna em segundos
          PTTL user1:name - retorna em milisegundos
          ```

        - Remover o tempo de expiração

          ```
          PERSIST user2:name
          ```

        - Remoção da chave

          ```
          DEL user2:name
          ```

          

    - Wide-Column Store

      - Menor diferença para o banco de dados relacionais

      - Armazenam os dados em colunas

      - Estrutura

        - Key Space (Equiparado a database nos bancos de dados convencionais)
          - Column family (Equiparado a tabelas nos banco de dados convencionais)
            - Row key é a chave que representa uma linha de coluna (Equiparado a primary key)
              - Column representa um valor contendo Name, Value, Timestamp

      - Banco mais usado Cassandra

      - Consulta por chaves primarias

      - Cassandra: 

        - Sandbox: www.katacoda.com

        - Não possui transações

        - CQL - Cassandra query language

        - Criar um key space:

          ```
          CREATE KEYSPACE nome WITH replication = {'class': 'SimpleStrategy', 'replication_factor': 1};
          ```

        - Usar o key space

          ```
          use name;
          ```

        - Criar column family

          ```
          CREATE COLUMNFAMILY clients (name TEXT PRIMARY KEYM age int);
          ```

        - Selecionar dados

          ```
          SELECT * FROM clients
          ```

        - Inserir dados

          ```
          INSERT INTO clients (name, age) VALUES ('Bob Esponja', 38);
          ```

        - Inserir dados com JSON

          ```
          INSERT INTO clients JSON '{"name": "Patrick"}';
          ```

        - Selecionar timestamp

          ```
          SELECT age, WRITETIME(age) FROM lista;
          ```

        - Sintaxes de consulta

          ```
          ##Retornar valores filtrados
          SELECT * FROM clients WHERE name='Bob esponja';
          
          ##Retorna JSON
          SELECT JSON * from clients;
          ```

        - Update

          ```
          UPDATE clients SET age=33 WHERE name='Patrick';
          ```

        - Alterar column family

          ```
          ALTER COLUMNFAMILY clients ADD hobby text;
          ```

        - Deletar registro

          ```
          DELETE FROM clients WHERE name = 'Bob esponja';
          ```

          

    - Graph Store

      - Estruturas matematicas

      - Comumente usados em detecção de fraudes

      - Compostas em:

        - Nós
          - São os dados
          - Poder ter propriedades ou não ter
          - Pode ter label ou não
        - Vertices
          - Relacionamentos

      - Neo4j mais utilizado

      - Aplica as propriedades ACID

      - Linguagem sifer

      - Sandbox - sandbox.neo4j.com

      - Criar label, nó e setar propriedades

        - ```
          CREATE (:Client {name : "Bob Esponja", age: 28, hobbies: ['Caça agua-viva, Comer hamburegueres']})
          ```

      - Consultar

        - ```
          MATCH (bob_esponja) RETURN bob_esponja;
          ```

    - DOCKER

      - Docker compose - contem as instruções para a criação dos containers

        ```
        version: '3.8'
        
        services: 
        		db:
        			image:mongo
        			container_name: db
        			restart: always
        			environment:
        				-MONGO_INITDB_ROOT_USERNAME=dio
        				-MONGO_INITDB_ROOT_PASSWORD=dio
                    ports:
                    	-"27017:27017"
                   	volumes:
                   		-/User/...:/data/db -(local dos dados no container)
                   		
        ```

      - subir

        ```
        docker-compose up -d
        ```

      - verificar se o container subiu

        ```
        docker container ps
        ```

        

    

    

    