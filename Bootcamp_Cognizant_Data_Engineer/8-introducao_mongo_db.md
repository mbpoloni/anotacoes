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

    - Key-Value Store

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

          

      

      

    