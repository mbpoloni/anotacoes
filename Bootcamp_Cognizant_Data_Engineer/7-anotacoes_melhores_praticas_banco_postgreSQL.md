# Conceitos e melhores práticas com banco de dados PostgreSQL

### Introdução ao banco de dados PostgreSQL

- Fundamentos de banco de dados
  - Dados
    - São valores brutos, registros soltos que são recolhidos e armazenados sem sofrer nenhuma alteração
  - Informações
    - Estruturação de dados, organização de dados. 
    - Conjuntos de dados relacionados entre si que geram valor.
    - Material do conhecimento
- Modelo relacional
  - Modelar
    - Criar um modelo.
  - Modelo
    - Determinar o comportamento de um programa
  - Modelo de dados
    - Ferramentas que mostram como os dados estão organizados e se relacionam entre si.
  - Modelo relacional
    - Representativo, que se baseia no principio que todos os dados serão gravados em tabelas com linhas e colunas
    - Linhas ou tuplas onde estão os valores
    - Colunas são os atributos
    - ![image-20210916113148188](https://github.com/mbpoloni/anotacoes_aula/blob/master/img/image-20210916113148188.png)
    - Tabelas
      - Conjuntos de dados dispostos em colunas e linhas referentes a um objetivo comum.
      - O que pode ser definido como tabelas
        - Coisas tangíveis (Elementos físicos, carro, produto, animal)
        - Funções (Perfis de usuário, status)
        - Eventos ou ocorrências (Produtos de um pedido, histórico de dados)
    - Colunas importantes
      - Chave primária PK
        - Conjunto de um ou mais campos que nunca se repetem
      - Chave Estrangeira FK
        - Valor de referência a uma PK de outra tabela, para criar um relacionamento
      - ![image-20210916113818102](https://github.com/mbpoloni/anotacoes_aula/blob/master/img/image-20210916113818102.png)
      - Sistema de gerenciamento de banco de dados SGBD
        - Conjunto de softwares responsáveis pelo gerenciamento de um banco de dados.
        - MySQL
        - SQL Server
        - mongoDB
        - ProstgreSQL
- Introdução ao PosrgreSQL
  - Sistema de gerenciamento de banco de dados SGBD relacional
  - Arquitetura
    - Multiprocessos vários processos são iniciados
    - ![image-20210916114402729](https://github.com/mbpoloni/anotacoes_aula/blob/master/img/image-20210916114402729.png)
    - Modelo cliente/servidor
      - Cliente - interface gráfica
      - Servidor - fazer os processos de armazenamento
    - Características
      - Open source
      - Point in time recovery
      - Linguagem procedural com suporte a varias linguagens
      - Views, functions, procedures, triggers
      - Permite complexas
      - Suporte a dados geográficos
      - Controle de concorrência
- pg_lsclusters
  - lista os clusters (somente Ubuntu)
- pg-createcluster -d /home/postgres/aula 11 aula --start
  - cria e inicializa um cluster versão 11 de nome aula no endereço  /home/postgres/aula
- psql
  - valida se é possível se conectar com o banco de dados
- pgAdmin
  - Ferramenta gráfica para interagir com o banco de dados

### Objetos e tipos de dados do ProstgreSQL

- postgresql.conf

  - Onde estão definidas e armazenas todas as configurações

  - dentro de PGDATA

  - a view pg_settings

    - guarda todas as configurações atuais
    - reflete o que está no postgresql.conf
    - o que está em funcionamento

  - ```
    SELECT name, setting
    FROM pg_settings;
    ```

  - ```
    SHOW [parâmetro]
    ```

  - No ubuntu está em local diferente

  - ```
    LISTEN_ADRESS
    ```

    - Endereços TCP/IP das interfaces que o servidor PostgreSQL vai escutar/liberar conexões.
    - Cuidado com *

  - ```
    PORT
    ```

    - A porta TCP que o servidor vai ouvir. O padrão é 5432

  - ```
    MAX_CONNECTIONS
    ```

    - Número máximo de conexões simultâneas no servidor PostgreSQL

  - ```
    SUPERUSER_RESERVED_CONNECTIONS
    ```

    - Número de conexões (slots) reservadas para conexções ao banco de dados de super usuários

  - ```
    AUTHENTICATION_TIMEOUT
    ```

    - Tempo máximo em segundos para o cliente conseguir uma conexão com o servidor

  - ```
    PASSWORD_ENCRYPTION
    ```

    - Algoritmo de criptografia das senhas dos novos usuários criados no banco de dados

  - ```
    SSL
    ```

    - Habilita a conexão criptografada por SSL (Somente se o PostgreSQL foi compilado com suporte SSL)

  - ```
    SHARED_BUFFERS
    ```

    - Tamanho da memória compartilhada do servidor PostrgreSQL para cache/buffer de tabelas, índices e demais relações
    - 25% do tamanho da memória

  - ```
    WORK_MEM
    ```

    - Tamanho da memória para operações de agrupamento e ordenação (ORDER BY, DISTINCT, MERGE JOINS)

  - ```
    MAINTENANCE_WORK_MEM
    ```

    - Tamanho da memória para operações como VACUUM, INDEX, ALTER TABLE
    - Operações de administração do banco de dados

- pg_hba.conf

  - Responsável pelo controle de autenticação dos usuários

  - ![image-20210916191349946](https://github.com/mbpoloni/anotacoes_aula/blob/master/img/image-20210916191349946.png)

  - Métodos de autenticação

    - ![image-20210916191437708](https://github.com/mbpoloni/anotacoes_aula/blob/master/img/image-20210916191437708.png)

  - ```
    host 	all	all 0.0.0.0/0 md5
    ```

    - Não fazer isso em produção, habilita qualquer acesso com senha

- pg_ident.conf

  - Responsável por mapear os usuário do sistema operacional com os usuários do banco de dados.
  - A opção ident deve ser utilizado
    - ![image-20210916192010518](https://github.com/mbpoloni/anotacoes_aula/blob/master/img/image-20210916192010518.png)

- Comandos administrativos

  - Comandos administrativos UBUNTU
    - ![image-20210916192112078](https://github.com/mbpoloni/anotacoes_aula/blob/master/img/image-20210916192112078.png)
  - Comandos administrativos CentOS
    - ![image-20210916192342379](https://github.com/mbpoloni/anotacoes_aula/blob/master/img/image-20210916192342379.png)
  - Comandos administrativos Windows
    - Interface gráfica
  - Comandos administrativos através de binários
    - ![image-20210916192515387](https://github.com/mbpoloni/anotacoes_aula/blob/master/img/image-20210916192515387.png)
    - pg_dump não é backup
  - Arquitetura de banco
    - Cluster
      - Coleção de banco de dados que compartilham as mesmas configurações
      - Pode ter um ou mais banco de dados
  - Banco de dados
    - Conjunto de schemas com seus objetos/relações (tabelas, funções, views)
  - Schemas
    - Conjunto de objetos/relações (tabelas, funções, views)
  - ![image-20210916193012738](https://github.com/mbpoloni/anotacoes_aula/blob/master/img/image-20210916193012738.png)
  
- PGAdmin

  - Interface gráfica para interagir com o banco de dados
  - Se houver problemas de conexão com o banco de dados
    - Liberar acesso ao cluster em postreesql.conf
    - Liberar acesso ao cluster para o usuário do banco de dados em pg_hba.conf
    - Criar/editar usuários
  - listen_addresses = 'localhost'
    - endereços que podem se conectar ao banco de dados
  - nomecluster versao_postrgree local start
    - exemplo: pg_cluster 11 aula start
  - psql -h 127.0.0.1 -p 5432 -U postgres aula
    - utilizar o binário psql no host (-h) 127.0.0.1 na porta (-p) 5432 com o usuário (-U) postgres no banco aula
  - todo comando sql termina com ;
  - ALTER USER postgres PASSWORD '123';
    - altera senha do usuário postgres para 123
  - \q
    - sai do banco sql
  - peer
    - se o usuário do banco for igual ao usuário do sistema operacional libera acesso
  - md5
    - solicita autenticação de usuario
  - nomecluster versao_postrgree local reload
    - restarta o banco com um tempo de downtime baixo
  - schemas
    - grupos de objetos
  - database sessions
    - conexões com o banco de dados
  - transactions per seconds
    - transações que estão acontecendo no banco de dados
  - tuples in / tuples out
    - tuples in: comandos instert, delete que está sendo recebido
    - tuples out: retorno de informações do banco
  - CREATE DATABASE auladb;
    - cria um banco de dados com o nome auladb
  - Roles | Users | Grupos de usuários
    - são contas, perfis de atuação em um banco de dados, que possuem permissões em comum ou específicas
    - nas versões anteriores do PostgreSQL 8.1, usuários e roles tinham comportamentos diferentes, atualmente, roles e users são alias
    - CREATE ROLE name [[WITH] option[...]]
      - cria uma role/usuario
      - Opções
        - ![image-20210922184414677](https://github.com/mbpoloni/anotacoes_aula/blob/master/img/image-20210922184414677.png)
      - IN ROLE
        - a nova rola passa a pertencer a role informada
      - ROLE
        - a role informada passa a pertencer a nova role
      - CREATE ROLE daniel LOGIN CONNECTION LIMIT 1 PASSWORD '123' IN ROLE professores
  - GRANT
    - conecede acesso após a criaçã da role
    - GRANT [role a ser concedida] TO [role a assumir as permissões]
    - privilégios de acesso aos objetos do banco de dados
      - ![image-20210922191201019](https://github.com/mbpoloni/anotacoes_aula/blob/master/img/image-20210922191201019.png)
    - ![image-20210922191322880](https://github.com/mbpoloni/anotacoes_aula/blob/master/img/image-20210922191322880.png)
  - REVOKE
    - remove as permissõs de uma role
    - REVOKE [role que será revogada] FROM [role que terá suas permissões revogadas]
    - REVOKE professores FROM daniel
      - dessaocia a role daniel de professores
    - ![image-20210922191715682](https://github.com/mbpoloni/anotacoes_aula/blob/master/img/image-20210922191715682.png)
  - ALTER
    - altera a role
    - ALTER ROLE role_specification [WITH] OPTION [...]
  - DROP
    - elimina a role
    - DROP ROLE role_specification
  
- Database

  - É o banco de dados
  - CREATE DATABASE name
  - ALTER DATABE name
    - ALTER DATABASE name RENAME TO new_name
  - DROP DATABASE name

- Schemas

  - É um grupo de objetos, como tabelas, types, views, funções, entre outros
  - CREATE SCHEMA schema_name
    - CREATE SCHEMA IF NOT EXISTS schema_name
  - ALTER SCHEMA name
  - DROP SCHEMA name
    - DROP SCHEMA IF EXISTS name

- Objetos

  - São as tabelas, views, funções, types, sequence

- 08:34



