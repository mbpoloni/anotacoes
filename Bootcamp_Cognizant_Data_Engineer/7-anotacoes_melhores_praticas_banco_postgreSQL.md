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
- 





