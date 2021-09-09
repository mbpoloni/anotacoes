# Fundamentos de arquitetura de sistemas

### 1-Vantagens e desenvolvimento de web services

- WEB services: soluções par aplicações se comunicarem independente da linguagem
- Foi inicialmente criado para troca de mensagens, utilizando linguagem XML sobre o protocolo HTTP sendo identificado por URI
- Web services são API´s que se comunicam por meio de redes sobre o protocolo HTTP
- Vantagens
  - Linguagem comum
  - Integração
  - Reutilização de implementação
  - Segurança
  - Custos
- Principais tecnologias
  - SOAP
  - REST
  - XML
  - JSON
- SOAP
  - Simple object access protocol
  - protocolo baseado em XML para acessar serviços web
  - é uma definição de como serviços web se comunicam
  - desenvolvido para facilitar integrações entre aplicações
  - meio de transporte genérico, pode ser usado por outros protocolos além do HTTP

- XML

  - Extensible Markup Language
  - linguagem de marcação, criada na decada de 90 pela W3C
  - não tem limitação de criação de tags
  - linguagem comum para integrações entre aplicações

- SOAP Message

  - possui estrutura única que deve sempre ser seguida
    - SOAP Envelope (primeiro elemento do documento, é usado para encapsular toda a mensagem SOAP )
      - SOAP Header (elemento onde possui informações de atributos e metadados da requisição)
      - SOAP Body (elemento que contem os detalhes da mensagem)

- WSDL

  - Web services description language
  - funciona como um contrato do serviço
  - a descrição é feita em um documento XML, onde é descrito o serviço, especificações de acesso, operações e métodos

- XSD

  - XML schema definition
  - usado para definir a estrutura de dados que será validada no XML
  - funciona como uma documentação de como deve ser montado o SOAP Message que será enviado através de Web Service

- REST

  - Representational State Transfer

  - estilo de arquitetura de software que define a implementação de um serviço web

  - pode trabalhar com XML, JSON ou outros

  - Vantagens

    - integrações entre aplicações
    - utiliza método HTTP
    - arquitetura de fácil compreensão
    - Requisição -> Servidor -> Resposta (Texto, JSON, XML, ...)
    - Quando uma aplicação web disponibiliza um conjunto de rotinas e padrões através de serviços web podemos chamar esse conjunto de API

  - API

    - Application programming interface
    - conjunto de rotinas documentados e disponibilizados por uma aploicação par que outras aplicações possam consumir suas funcionalidades

  - Métodos HTTP:

    - GET: solicita a representação de um recurso naquele momento
    - POST: solicita a criação de um recurso
    - DELETE: solicita a exclusão de um recurso
    - PUT: solicita a atualização de um recurso

  - JSON

    - JavaScript Object Notation
    - formatação leve para troca de mensagens entre sistemas
    - usa-se uma estrutura de chave e valor e também listas ordenadas
    - um dos formatos mais populares para troca de mensagens entre sistemas

  - Código de estado

    - 1XX: Informativo
    - 2XX: Sucesso
    - 3XX: Redirecionamento
    - 4XX: Erro do cliente
    - 5XX: Erro do servidor

### 2-Conceitos de arquitetura em aplicações para internet

- Tipos de arquitetura

  - Monolito

    - Uma aplicação distribuída em mais instancias

    - Comunicação de funcionalidade através de chamada de código no sistema

    - ![image-20210908164911545](C:\workspace\anotacoes_aulas\img\image-20210908164911545.png)

    - Proxy faz o gerenciamento e a distribuição da demanda entre as instancias

      | Prós                       | Contas                                   |
      | -------------------------- | ---------------------------------------- |
      | Baixa complexidade         | Stack única                              |
      | Monitoramento simplificado | Compartilhamento de recurso              |
      |                            | Acoplamento (comunicação entre serviços) |
      |                            | Mais complexo a escalabilidade           |

      

  - Microserviços 1

    - ![image-20210908165124168](C:\workspace\anotacoes_aulas\img\image-20210908165124168.png)

    - Um serviço para cada operação da aplicação

    - Proxy faz o gerenciamento conforme o tipo de serviço solicitado pelo cliente

    - Serviço 3 é um serviço interno

    - Pode tornar uma arquitetura caótica conforme o aumento de comunicação entre serviços

      | Prós                   | Contras                                  |
      | ---------------------- | ---------------------------------------- |
      | Stack dinâmica         | Acoplamento (comunicação entre serviços) |
      | Simples escalabilidade | Monitoramento mais complexo              |
      |                        | Provisionamento mais complexo            |

      

  - Microserviços 2

    - ![image-20210908170029100](C:\workspace\anotacoes_aulas\img\image-20210908170029100.png)
    - Contém um Message Broker, cria um independência entre serviços e um buffer caso algum serviço não esteja disponível
    - Vantagens
      - Fácil atualização de serviços, sem a parada do sistema
      - Com o message broker, proporciona um buffer, e assim que o serviço voltar a funcionar ele processa os trabalhos antigos
    - Desvantagens
      - A plataforma inteira fica refém do Message broker

    | Prós                   | Contras                       |
    | ---------------------- | ----------------------------- |
    | Stack dinâmica         | Monitoramento mais complexo   |
    | Simples escalabilidade | Provisionamento mais complexo |
    | Desacoplamento         |                               |

    - Mais complexo no gerenciamento de erros
      - Solução
        - Dead letter queue
        - Filas de re-tentativas
    - 

  - Microserviços 3

    - ![image-20210908170558585](C:\workspace\anotacoes_aulas\img\image-20210908170558585.png)

    - Pipeline

      - Proporciona etapas para se chegar aos serviços (Meio de campo)

      | Prós                   | Contras                                               |
      | ---------------------- | ----------------------------------------------------- |
      | Stack dinâmica         | Provisionamento mais complexo                         |
      | Simples escalabilidade | Plataforma inteira depende do gerenciador de pipeline |
      | Desacoplamento         |                                                       |
      | Menor complexidade     |                                                       |

    - Mais complexo no gerenciamento de erros, necessário de controle de estados

      - Solução
        - Dead letter queue
        - Filas de re-tentativas
        - Sistema de roll back

### 3-A arquitetura de aplicações móveis e internet das coisas

- Internet

  - Início com arpanet em 1969
  - Objetivo conectar computadores de centros de pesquisa
  - Rede de pessoas conectadas

- Internet das coisas

  - Coisas que não são pessoas, se conectam na internet
  - Embutir sensores para coletar dados, usar dados para tomar decisões
  - Conceitos básicos de IOT
    - Things
      - Sensores para coletar dados
    - Cloud
      - Onde é armazenado e processados os dados
    - Intelligence
      - Usar os dados gerados de forma inteligente

- Computação ubiqua

  - tecnologia recua para um plano de fundo
  - terceira onda da computação
  - As tecnologias mais importantes são aquelas que desaparecem. Elas se integram à vida do dia a dia, ao nosso cotidiano, até serem indistinguiveis dele.

- Desafios

  - Privacidade e segurança
  - Quantidade exponencial de dispositivos conectadas na rede
  - Ser capaz de processar e armazenar uma enorme quantidade de informações
  - Gerar valor a partir dos dados coletados

- Arquitetura de IOT

  - Things	

    - Dispositivo para coleta de dados
    - O que considerar na escolha
      - Baixo consumo de energia
      - Rede de dados limitado
      - Resiliência
      - Segurança
      - Customização
      - Baixo custo

  - Protocolo de comunicação

    - Protocolo de comunicação único (MQQT)

      - Base na pilha TCP/IP

      - Protocolo de mensagem assíncrona M2M (envia e não aguarda resposta)

      - Criado pela IBM para conectar sensores de pipelines de petróleo a satélites

      - Padrão OASIS suportado pela linguagens de programação mais populares

      - Modelo Publis/Subscribe

        - As things entregam as informações para o Broker que entrega a mensagem para os clientes que estão escritos.

        - ![image-20210909101707582](C:\workspace\anotacoes_aulas\img\image-20210909101707582.png)

        - Publish

          - Publica um tópico no borker MQTT
          - pub mqtt://broker.io/a6g3I9/gps/position

          | mqqt      | broket.io | a6g3I9          | gps    | position         |
          | --------- | --------- | --------------- | ------ | ---------------- |
          | PROTOCOLO | BROKET    | USER IDENTIFIER | SENSOR | INFORMATION TYPE |

        - Subscribe

          - Consome as informações do broker
          - sub mqtt://broker/user/gps/position
          - sub mqtt://broker/+/gps/position: subscribe em todos usuários
          - sub mqtt://broker/+/gps/+: subscribe todas informações de GPS
          - sub mqtt://broker/+/#: subscribe todos usuário de todos os sensores

        - QoS

          - Quality of service
            - QoS 0
              - Nível de menor esforço
              - Não tem garantia nenhuma de que a mensagem foi entregue
              - Mensagem não é retransmitida
            - QoS 1
              - Mensagem primeiro é armazenada no client
              - Garantia que a mensagem foi entregue no mínimo uma vez ao recebedor
              - Mensagem pode ser retransmitida se não houver confirmação de entrega
              - Mecanismo mais comum
            - QoS 2
              - Broker informa o client que a mensagem foi gravada
              - Garantia que a mensagem foi entregue no mínimo uma vez ao recebedor
              - Mensagem pode ser retransmitida se não houver confirmação de entrega

        - Cloud

          - Maior número de devices conectados e transmitindo dados na infraestrutura
          - TB´s ou PB´s de informações
          - ![image-20210909104314190](C:\workspace\anotacoes_aulas\img\image-20210909104314190.png)
            - Worker: subscribe no tópico do broker
            - Data store: armazena as informações
            - Cache: As informações mais relevantes para o final
            - Analitics: Dashboard que consome as informações da área de cache

        - Client - Broker - Worker - Data Store

        - Estrutura POC

          | Thing       | Broker           | Worker  | Data Store |
          | ----------- | ---------------- | ------- | ---------- |
          | App Android | Eclipse Mosquito | Node.js | MySQL      |

        - Estrutura MVP

          | Thing         | Broker | Worker         | Data Store  |
          | ------------- | ------ | -------------- | ----------- |
          | GPS Embarcado | HiveMQ | Akka Scala JVM | Banco noSQL |

        - Estrutura completa nuvem (Cloud Native)

          | Thing         | Broker       | Worker                | Data Store |
          | ------------- | ------------ | --------------------- | ---------- |
          | GPS Embarcado | AWS IoT Core | AWS Kinesis Firehouse | AWS S3     |

  - IOT na Prática

    - ![image-20210909111356155](C:\workspace\anotacoes_aulas\img\image-20210909111356155.png)
    - ![image-20210909111412093](C:\workspace\anotacoes_aulas\img\image-20210909111412093.png)
    - ![image-20210909111857723](C:\workspace\anotacoes_aulas\img\image-20210909111857723.png)
    - Modelo cliente servidor
      - Cliente->Request->Servidor
      - Servidor->Resposta->Cliente

