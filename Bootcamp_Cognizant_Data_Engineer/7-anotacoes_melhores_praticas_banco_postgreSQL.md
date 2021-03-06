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

- Primary Key

  - Conjunto de um ou mais campos que nunca se repetem em uma tabela
  - Os valores garantem a integridade do dado unico
  - O atributo de chave primaria deve sempre eixistir
  - Os atributos identificadores devem ser o conjunto mínimo que pode identificar cada instancia de uma entidade
  - Não devem ser usadas chaves externas
  - Não deve conter informação volátil, não pode se alterar

- Foreingn Key

  - Campo ou conjunto de campos que são referências de chaves primárias de outras tabelas

- Cuidado para não ter muitas repetições

- Tipos de dados

  - Numéricos

    ![image-20210929111704437](C:\Users\micaelpo\AppData\Roaming\Typora\typora-user-images\image-20210929111704437.png)

  - Caracteres

    ![image-20210929111801742](C:\Users\micaelpo\AppData\Roaming\Typora\typora-user-images\image-20210929111801742.png)

  - Data

    ![image-20210929111913397](C:\Users\micaelpo\AppData\Roaming\Typora\typora-user-images\image-20210929111913397.png)

  - Booleanos

    - True, or False

- DML

  - Data manipulation language
  - INSERT, UPDATE, DELETE, SELECT
    - INSERT
      - INSERT INTO [nome tabela] ([campos da tabela,]) VALUES([valores de acordo com a ordem dos campos])
      - INSERT INTO [nome tabela] ([campos da tabela,]) SELECT([valores de acordo com a ordem dos campos])
      - Exemplo:
        - INTER INTO agencia (banco_numero, numero, nome) VALUES (341,1,'Centro da cidade') ON CONFLICT (banco_numero, numero) DO NOTHING;
    - UPDATE
      - UPDATE [nome da tabela] SET [campo1] = [novo valor do campo1], [campo2] = [novo valor do campo,]... [WHERE + condições] *Sempre utilizar updates com condições*
      - UPDATE (tabela) SET campo1 = novo_valor WHERE (condição);
    - DELETE
      - DELETE FROM [nome da tabela] [WHERE + condições] *Sempre utilizar deletes com condições*
      - DELETE FROM tabela SET campo1 = novo_valor WHERE (condição);
    - SELECT
      - SELECT [campos da tabela] FROM[nome da tabela] [WHERE + condições] *Sempre tentar evitar o SELECT* *
      - Exemplo: 
        - SELECT nome FROM cliente WHERE email LIKE '%gmail.com'
        - LIKE - respeita o case sensitive
        - ILIKE - não respeita o case sensitive
      - Condição WHERE / AND / OR

- DDL

  - Data definition language

  - CREATE, ALTER, DROP

    - CREATE TABLE [IF NOT EXISTS] [nome tabela] (

      [nome do campo] [tipo] [regras] [opções],

      [nome do campo] [tipo] [regras] [opções]

      );

    - Exemplo:

      - CREATE TABLE IF NOT EXISTS agencia(
    
        banco_numero INTEGER NOT NULL,
    
        numero INTEGER NOT NULL,
    
        nome VARCHAR(80) NOT NULL,
    
        ativo BOOLEAN NOT NULL DEFAULT TRUE,
    
        data_criacao TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
    
        PRIMARY KEY (banco_numero, numero)
    
        FOREIGN KEY (banco_numero) REFERENCES banco (numero);
    
    - Boas práticas:
    
      - ativo BOOLEAN NOT NULL DEFAULT TRUE,
      - data_criacao TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP
    
  - ALTER TABLE [nome tabela] [opções]

  - DROP TABLE [nome da table]


### Fundamentos da Structured Query Language (SQL)

- CRUD: Create, Read, Update, Delete
- IDEMPOTÊNCIA
  - Propriedades que algumas ações/operações possuem possibilitandos-as de serem executadas diversas vezes sem alterar o resultado após a aplicação inicial
- Melhores práticas em DDL
  - Criar colunas que são atributos básicos do objeto
  - Cuidado com regras (constraints)
  - Cuidado com excesso de Fks
  - Cuidado com o tamanho indevido de colunas
- TRUNCATE
  - Esvazia a tabela
  - RESTART IDENTITY
    - Reinicia a contagem do id
  - CASCADE
    - Apaga os foreign keys

- Funções agregadas
  - SELECT * FROM information_schema.columns WHERE table_name = 'banco';
    - Seleciona as informações de columa
    
  - SELECT column_name, data_type FROM information_schema_columns WHERE table_name = 'banco';

  - www.postgresql.org/docs/11/functions-aggregate.html

  - AVG
    - SELECT AVG(valor) FROM cliente_transacoes;
    
  - COUNT
    - SELECT COUNT(numero) from clientes;
    - SELECT COUNT(numero), email FROM cliente WHERE email ILIKE '%gmail.com' GROUP BY email
    - SELECT COUNT(id) , tipo_transacao_id FROM cliente_transacoes GROUP BY tipo_transacao_id HAVING COUNT (id) > 150
    
  - MAX
    - SELECT MAX(valor) FROM cliente_transacoes
    - SELECT MAX(valor), tipo_transacao_id FROM cliente_transacoes GROUP BY tipo_transacao_id
    
  - MIN
    - SELECT MIN(numero)  FROM cliente_transacoes
    - SELECT MIN(valor), tipo_transacao_id FROM cliente_transacoes GROUP BY tipo_transacao_id
    
  - SUM
    - SELECT SUM (valor) FROM cliente_transacoes
    - SELECT SUM(valor), tipo_transacao_id FROM cliente_transacoes GROUP BY tipo_transacao_id ORDER BY tipo_transacao_id ASC
    - SELECT SUM(valor), tipo_transacao_id FROM cliente_transacoes GROUP BY tipo_transacao_id ORDER BY tipo_transacao_id DESC
    
  - JOIN

    - Relação entre as tabelas

    - JOIN OU INNER JOIN

      - Exibe os registros relacionados entre as tabelas

      - Exemplo:

        ```
        SELECT tabela1.campos, tabela2.campos
        FROM tabela1
        JOIN tabela2
        ON tabela2.campo = tabela1.com
        ```

        ```
        SELECT count(distinct banco.numero)
        FROM banco
        JOIN agencia ON agencia.banco_numero = banco.numero
        ```

        

      - Tentar utilizar campos que são primary keys e foreign keys para otimizar os recursos do banco

    - LEFT JOIN OU LEFT OUTER JOIN

      - Exibe os registros da tabela da esquerda(primeira tabela mencionada) e os campos que houver relacionamento da direita, se não houve trás o registro nulo.

      - Exemplo:

        ```
        SELECT tabela1.campos, tabela2.campos
        FROM tabela1
        LEFT JOIN tabela2
        ON tabela2.campo = tabela1.campo
        ```

      - 

    - RIGHT JOIN OU RIGHT OUTER JOIN

      - Exibe os registros da tabela da direita(segunda tabela mencionada) e os campos que houver relacionamento da esquerda, se não houve trás o registro nulo.

      - Exemplo:

        ```
        SELECT tabela1.campos, tabela2.campos
        FROM tabela1
        RIGHT JOIN tabela2
        ON tabela2.campo = tabela1.campo
        ```

        

    - FULL JOIN OU FULL OUTER JOIN

      - Trás todas possibilidades de relacionamentos possíveis

      - Exemplo:

        ```
        SELECT tabela1.campos, tabela2.campos
        FROM tabela1
        FULL JOIN tabela2
        ON tabela2.campo = tabela1.campo
        ```

    - CROSS JOIN

      - Todos os dados de uma tabela serão cruzados com todos os dados da tabela rederenciada no CROSS JOIN criando uma matriz

      - Exemplo:

        ```
        SELECT tabela1.campos, tabela2.campos
        FROM tabela1
        CROSS JOIN tabela2
        ```

      - Desperdício de recurso

    - ALIAS

      - Utilizar alias para não precisar digitar o nome da tabela

        ```
        SELECT tbla.valor, tblb.valor
        FROM teste_a tbla
        CROSS JOIN teste_b tblb;
        ```

  - Common Table Expressions CTE

    - Forma aixiliar de organizar statements, ou seja, blocos de códigos, para consultas muito grandes, gerando tabelas temporárias e criando relacionamento entre elas.

    - Dentro dos statements podem ter SELECTS, INSTERS, UPDATES OU DELETES

    - Usando quando envolve uma lógica mais complexa

    - Cria tabelas temporárias

      ```
      WITH [NOME1 AS (SELECT (campos,)FROM tabela_A [WHERE]),[nome2]AS (SELECT (campos,) FROM tabela_B [WHERE]) SELECT [nome1], (campos1), [NOME2], (campos) FROM [nome1] JOIN[nome2]]
      ```

  - Views

    - São camadas para as tabelas

    - São alias para uma ou mais queries

    - Aceitam comandos de SELECT, INSERT, UPDATE, E DELETE

      - INSERT, UPDATE, DELETE = É aceito somente em views de uma tabela

    - ```
      CREATE VIEW name AS query
      ```

    - Parâmetros

      - OR REPLACE - Substitui caso haja uma view
      - TEMP | TEMPORARY - Cria uma view somente na instancia, se fechar a sessão as informações serão perdidadas. Se houver uma outra pessoa programando no mesmo banco ela não terá acesso a view
      - RECURSIVE - Select dentro da view, que chama a view até esgotar uma determinada opção

    - Idempotencia

      ```
      CRETE OR REPLACE VIEW vw_banco AS (
      	SELECT numero, nome, ativo
      	FROM banco
      	);
      SELECT numero, nome, ativo
      FROM vw_bancos;
      ```

    - Não define datatype pois assume o tipo de dado da consulta

    - CREATE, UPDATE OU DELETE so funcionam para views com apenas uma tabela

      ```
      INSERT INTO vw_bancos(numero, nome, ativo)VALUES(100,'Banco CEM', TRUE)
      UPDATE vw_bancos SET nome = 'Banco 100' WHERE numero = 100
      DELETE FROM vw_bancos WHERE numero = 100
      ```

      - Insere os dados na tabela, a view serve como uma janela

    - TEMPORARY

      - VIEW presente apenas na sessão do usuário. Se você desconectar e conectar novamente, a VIEW não estará disponível

    - RECURSIVE

      - O comando dela chama ela mesmo, numa espécie de loop

        ```
        CREATE OR REPLACE RECURSIVE VIEW nome_da_view (campos_da_view) AS (
        	SELECT base
        	UNION ALL
        	SELECT campos
        	FROM tabela_base
        	JOIN(nome_da_view))
        ```

      - UNION 

        - Unifica

      - UNION ALL

        - Nao unifica

    - WITH OPTIONS

      ```
      CREATE OR REPLACE VIEW vw_bancos AS (
      	SELECT numero, nome, ativo
      	FROM banco
      	WHERE ativo IS TRUE
      	)WITH LOCAL CHECK OPTION
      	
      INSERT INTO vw_banco (numero, nome, ativo) VALUES (100,'Banco 100', FALSE)
      
      --Retorna erro pois requer que ativo = true
      ```

      - Valida conforme as regras que houver WITH LOCAL CHECK OPTION

      ```
      WITH CASCADE CHACK OPTION
      ```

      - Valida as regras da view e das views que a view relaciona

  - TRANSAÇÃO

    - Conceito fundamental de todos os sistemas de bancos de dados

    - Conceito de multiplas etapas/códigos reunidos em apenas 1 transação, onde o resultado precisa ser tudo ou nada.

      ```
      BEGIN;
      	UPDATE conta SET valor = valor -100
      	WHERE nome = 'Alice';
      	
      	UPDATE conta SET valor = valor + 100
      	WHERE nome = 'Bob'
      COMMIT;
      ```

      - Se ocorrer algum erro entre o BEGIN  e o COMMIT ocorre um rollback e qualquer aleração é desfeita

    - SAVEPOINT 

      - Manter as alterações realizadas até o momento 

      ```
      BEGIN;
      UPDATE banco SET ativo = TRUE WHERE numero = 0;
      SELECT numero, nome, ativo FROM banco WHERE numero = 0;
      ROOLBACK
      ```

  - FUNÇÕES

    - Conjunto de códigos que são executados dentro de uma transação com a finalidade de facilitar a programação e obter o reaproveitamento/reutilização de códigos
  
      - query language functions (funções escritas em SQL)
      - procedural language functions (funções escritas em PL/pgSQL ou PL/py)
      - internal functions
      - C-language functions
  
      ```
      CREATE OR REPLACE FUNCTION name 
      ```
  
    - RETURNS
  
      - INTEGER
      - CHAR/VARCHAR
      - BOOLEAN
      - ROW
      - TABLE
      - JSON
  
    - LANGUAGE
  
      - SQL
      - PLPGSQL
      - PLJAVA
      - PLPY
  
    - SECURITY
  
      - INVOKER - permitir que a função seja executada com as permissões do usuário que a chamar
      - DEFINER - as permissões de usuário que criou a função passa para o usuário que chamou a função
  
    - COMPORTAMENTO
  
      - IMMUTABLE - Não pode alterar o banco de dados, Evitar selects
      - STABLE - Não pode alterar o banco de dados. Pode conter selects
      - VOLATILE - Comportamento padrão, aceita todos os cenários
  
    - SEGURANÇA E BOAS PRÁTICAS
  
      - CALLED ON NULL INPUT
        - Se qualquer um dos parâmetros for num, a função será executada
      - RETURNS NULL ON NULL INPUT
        - Se qualquer um dos parâmetros for null, a função retornará null
  
    - RECURSO
  
      - COST
        - Custo/row em unidades de CPU
      - ROWS
        - Número estimados de linhas que será analisada pelo planner
  
    - SQL
  
      - Não é possível utilizar transações
  
      ```
      CREATE OR REPLACE FUNCTION fc_somar (num1 INTEGER, num2 INTEGER)
      RETURNS INTEGER
      LANGUAGE SQL
      AS $$
      	SELECT num1 + num2;
      $$;
      ```
  
    - PLPGSQL
  
      - Pode utilizar transações
  
  

