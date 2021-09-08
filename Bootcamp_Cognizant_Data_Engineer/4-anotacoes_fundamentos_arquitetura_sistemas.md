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

    ### Conceitos de arquitetura em aplicações para internet

  - Tipos de arquitetura

    - Monolito

      - Uma aplicação distribuída em mais instancias

      - Comunicação de funcionalidade através de chamada de código no sistema

      - ![image-20210908164911545](C:\Users\Micael\AppData\Roaming\Typora\typora-user-images\image-20210908164911545.png)

      - Proxy faz o gerenciamento e a distribuição da demanda entre as instancias

        | Prós                       | Contas                                   |
        | -------------------------- | ---------------------------------------- |
        | Baixa complexidade         | Stack única                              |
        | Monitoramento simplificado | Compartilhamento de recurso              |
        |                            | Acoplamento (comunicação entre serviços) |
        |                            | Mais complexo a escalabilidade           |

        

    - Microserviços 1

      - ![image-20210908165124168](C:\Users\Micael\AppData\Roaming\Typora\typora-user-images\image-20210908165124168.png)

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

      - ![image-20210908170029100](C:\Users\Micael\AppData\Roaming\Typora\typora-user-images\image-20210908170029100.png)
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

      - ![image-20210908170558585](C:\Users\Micael\AppData\Roaming\Typora\typora-user-images\image-20210908170558585.png)

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

