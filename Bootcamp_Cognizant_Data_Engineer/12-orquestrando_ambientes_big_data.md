# Orquestrando ambientes de Big Data distribuídos com Zookeeper, Yarn e Sqoop

### Conhecendo o ambiente do Sqoop

- Link para vm
- https://drive.google.com/file/d/1CsHc311jp4EuZ8be5KGaumniGAafa8sC/view?usp=sharing

### Zookeeper e Sqoop

Zookeeper

- Serviço de coordenação distribuido
- Gerenciamento de um grande conjunto de nós
- Arquitetura simples e API
- ASsim como o Hadoop, vem simplificar o processo do desenvolvedor
- Fornece as rotas necessárias para as peças do cluster
- Identifica os nós por nomes (DNS like)
- Gerencia e coordena as configurações
- Funciona com esquema de eleição de líder (usa-se sempre pelo menos trÇes Zookeeper)
- Pode indisponibilizar o dado enquanto está sendo modificado
- Ajuda na recuperação automática de falhas (HBase, por exemplo)
- Leader
  - responsável pelo processamento de requests de escrita, eleito internamente
- Followers
  - recebem as requests de leitura

Sqoop

- ​	Originalmente desenvolvido pela Cloudera

- Movimenta dados entre banco de dados relacional e HDFS

- Pode-se importar todas as tabelas, apenas uma tabela ou parte de uma tabela para o HDFS

- Tambem permite exportar os dados do HDFS para um banco de dados

- Permite automatização do processo de ingestão

- Como funciona

  - Realiza a leitura linha por linha da tabela para escrever o arquivo no HDFS

  - O resultado do import é um conjunto de arquivos contendo a cópia dos dados da tabela importada

  - Under the hood, gera classes Java, permitindo que o usuário possa interagir com o dado importado

  - Pode importar dados e metadados da bancos de dados SQL direto para o Hive

  - Utiliza o mapreduce para realizar impor/export dos dados, provendo um processamento paralelo e tolerante a falha

  - Permite especificar o intervalo e quais colunas serão importadas

  - Prossibilita a especificação de delimitadores e formatos de arquivos

  - Realiza conexões com banco de dados em paralelo, exevutando comandos de Select(import) e Insert/Update(export)

  - Aceita conexão com diversos plug-ins: MySQL, PostgreeSQL, Oracle, Teradata, Netezza, Vertica, DB2 e SQL Server

  - O formato padrão do arquivo importado no HDFS é CSV

  - Comandos

    - Trazer o do banco de dados para dentro do Haddop

      - ```
        sqoop import
        ```

    - Script de conexão, passando o user e password do SQL

      - ```
        connect jdbc:mysql://mysql.example.com/sqoop\
        password sqoop\
        password sqoop
        ```

    - especifica destino no HDFS

      - ```
        table cities
        ```

    - especifica delimitador

      - ```
        fields-terminated-by "\t"
        ```

    - import delimitando resultados

      - ```
        where "state='CA'"
        ```

        

    ![image-20211109194830261](C:\Users\Micael\AppData\Roaming\Typora\typora-user-images\image-20211109194830261.png)

    - Lista de comandos
      - https://drive.google.com/file/d/101BSQDSdq6wJkBWn3S6ZoSqf7uE-c7ck/view?usp=sharing
    - Arquivos necessários
      - https://drive.google.com/drive/folders/1xaft6H3R3_UvA6-BFHuCvHuWczf6xwqG
    - Slides
      - https://drive.google.com/file/d/1ZN53soEHPYiRS1hCtEN3L3lYSnuCZH9-/view

    

