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
  - Desvantagens
    - Não ter uma linguagem própria de SQL
    - Não suportar indices em colunas fora do 
