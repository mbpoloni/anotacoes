# Arquitetura de sistemas avançado

### 1-Conceitos de integração de sistemas e mensageria

- O que é uma arquitetura de mensageria
  - Centralizador de comunicação entre os outros serviços da aplicação

| Prós                                                         | Contras                 |
| ------------------------------------------------------------ | ----------------------- |
| Desacoplamento                                               | Single point of failure |
| Facil plug & play                                            | Difícil monitoramento   |
| Comunicação assíncrona                                       |                         |
| Simples escalabilidade                                       |                         |
| Broadcasting                                                 |                         |
| Permite Event source (permite reconstruir o banco de dados através os eventos) |                         |

- Comunicação assíncrona entre serviços
  - Utilizar o Message broker para a comunicação e consumo das mensagem dos serviços em paralelo
- Gerenciamento de erros
  - Dead letter queue (Filas de re-tentativas)
  - Monitoramento entre serviços
  - Rastreamento de fluxo
- Rastreamento de fluxo
  - Coletar, indexar e armazenar os logs do serviço em um único lugar (Exemplo: ELK Stack Elastic)
  - Utilizar track ID nas operações como Meta data

### 2-Arquitetura de dados não estruturados e business intelligence

- BI

  - Conjunto que irá fornecer ferramentas para a tomada de decisões

  - Composto basicamente por:

    - Ferramentas
    - Infraestrutura
    - Profissionais (corpo técnico)
    - Dados

  - Data

    - Os dados podem vir de diversos locais
      - Dados da operação (SGDB)
      - Dados gerenciais
      - Pesquisa de campo
      - Indicadores de marcado

  - BI - Solution

    - Infraestrutura
    - Gerenciamento dos dados
    - Analytics
    - Compartilhamento
    - Ferramentas gerais

  - Data warehouse

    - Estilo de modelagem de dados de forma eficiente

    - Conceitos

      | OLTP (Online Transaction Processing)                         | OLAP (Online Analytical Processing)               |
      | ------------------------------------------------------------ | ------------------------------------------------- |
      | Transações ponto a ponto do sistema (ex: Adicionar, atualizar) | Consolidação dos dados (ex: Agrupamento por tipo) |
      | Baseados em transação                                        | Baseado em analytics                              |
      | Atende uma grande gama de usuário                            | Atende uma gama reduzida de usuários              |

      ![image-20210909173241573](https://github.com/mbpoloni/anotacoes_aula/blob/master/img/image-20210909173241573.png)

- Big data

  - Grande volume de dados, estruturados ou não estruturados
  - Formatos diversos de dados
  - Não é uma ferramenta isolada

- Dados estruturados

  - Dados armazenados em forma de tabelas em um banco de dados

-  Dados semi-estruturados

  - Estruturas pequenas de dados semi estruturados
    - XML
    - RDF
    - OWL
    - JSON

  - noSQL
    - Se comportam como banco de dados estruturados (relacionais), mas proporciona mais flexibilidade para inserir dados sem um regra muito específica
    - Mais populares
      - mongo
      - cassandra
      - redis
      - riak
      - apache hbase
      - couchdb
    - variam como eles armazenam os dados
      - key-value
      - wide colunm store
      - document store
      - graph store
  - Controlar as regras no sistema, pois o banco é mais flexível

- Dados não estruturados

  - Grande coleção de vários tipos de informações
  - Ferramentas que podem gerir informação
  - Mais populares
    - hadoop
    - google big query
    - apache spark
    - datatorrent
    - presto
  - Necessário um ecossistema

- Data Lake

  - É um big data mais corporativo, mais tratado
  - ![image-20210909175735033](https://github.com/mbpoloni/anotacoes_aula/blob/master/img/image-20210909175735033.png)
  - Consiste em uma seleção e limpeza dos dados vindos de uma base estruturada e não estruturada

- Tutorial mongoDB

  - https://www.quackit.com/mongodb/tutorial/

### 3-Fundamentos de arquitetura de aplicações em nuvem

- Cloud computing
  - Provedor ou serviço que faz o gerenciamento de hardware/software
  - Boa opção para não ter o serviço em uma infraestrutura interna
  - IAAS (Infrastructure as a service)
    - Locação de infraestrutura para disponibilizar serviços
  - PAAS (Platform as a service)
    - Ter não somente a infraestrutura, mas tambem possui um meio de automatizar o como é possivel gerencias as máquinas
    - Customização mais facil das máquinas conforme os serviços
  - BAAS (Backend as a service)
    - Firebase
    - Foco em ter o front funcionando
  - ![image-20210909182640614](https://github.com/mbpoloni/anotacoes_aula/blob/master/img/image-20210909182640614.png)
- Disponibilidade
  - IAAS
    - Não se preocupar com hardware e internet
  - PAAS
    - Não se preocupar com um possível aumento de demanda de serviços
  - BAAS
    - Não há backend service
  - Kubernets (K8S)
    - Ter multiplos nodos
    - Mínimo de instancias: 3
    - Mínimo de nodos: 3
    - Distribui os serviços nos nodos e instancias conforme a demanada
    - Load balancer
      - Distribuir de maneira organica entre as instancias
- Serverless
  - Sem servidor, sem serviço rodando
  - Não ter que cuidar de um servidor nem em cloud computing
  - Quem garante o recebimento do request é o proprio provedor
  - API gateway
    - Gerencia as rotas de cada serviço
  - Desvantagem: custo maior, número maior de lambdas, tempo de execução das lambdas

### Desenvolvimento e operação de software integrado

- DevOps
  - Integrar o times de Development, Quality Assurance e IT operation
  - Conjuntos de práticas que integram e automatizam os processos entre as equipames para a produção rápida e confiável de software
  - Criar uma equipe com cultura de colaboração
  - Mudança de mentalidade, uma cultura, um movimento, uma filosofia
  - Framework CALMS
    - Culture
      - Ferramentas e automações são inúteis se não forem compartilhadas
    - Automation
      - Eliminar qualquer trabalho manual e repetitivo
    - Lean
      - Ser objetivos e enxutos
    - Measurement
      - Mensurar e obter métricas é o ponto de partida para novas melhorias
    - Sharing
      - Compartilhar informações para descentralizar o conhecimento
      - Torna o time autossistentável
  - Três caminhos
    - Flow 
      - Visa eliminar desperdícios e gargalos no processo
      - É trilhado entre a demanda e a entrega
      - Aplicação de metodologias ágeis
    - Feedback
      - Visam resolver problemas o quanto antes
      - Monitoramento é a chave
    - Learning
      - Gerar o conhecimento através da experimentação
      - Hipóteses são melhores do que uma certeza imediata
      - Eliminar a cultura da culpa
- Entregando software (ciclo infinito)
  - Etapas
    - plan
      - draw.io
      - teams
      - balsamiq
    - code
      - visual studio
      - sublime
      - git
    - build
      - docker
      - container
      - npm
    - teste
      - unit.net
      - loader.io
      - selenium
    - release
      - disponibilizar para o cliente
    - deploy
      - azure pipelines
      - circleci
      - app veyor
      - jenkins
    - operate
      - kubernets
      - aws
      - terraform
    - monitor
      - coletar e entender
      - datadog
      - prometheus
      - pushover

- Continuous Integration x Continuous Delivery x Continuous Deployment
  - Continuous Integration
    - Pode conter diversas etapas
      - Construção
      - Teste unitário
      - Analise de qualidade do código
      - Empacotamento de release
    - Tem como limite a geração do artefato
  - Continuous Deployment
    - Após o pipeline de Continuous Integration o Continuous Deployment é realizado de maneira automatica
  - Continuous Delivery
    - Semelhante ao Continuous Deployment
    - Necessita de um aprovador no meio do caminho
  - Principais ferramentas
    - Jenkins
    - Travis CI
  - Pipelines
    - Possui as etapas
- Code quality analysis 
  - Principais ferramentas
    - Sonarqube
    - codeclimate
    - codacy
  - Server para resolver problemas
    - Identificar complexidade ciclomatica
      - Quantos caminhos independentes o código pode seguir
    - Identificar código duplicado
    - Vulnerabilidade/code smell
    - Padronização e estilo
    - Histórico de débito técnico

