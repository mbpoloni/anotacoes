# Fundamentos de ETL com python

### Fundamentos de ETL

- ETL
  - Extract
    - Os dados são extraídos de diferentes fontes de dados
  - Transform
    - Propagados para a área de preparação de dados, onde são transformados e limpos
  - Load
    - Carregados no data warehouse
- Repositorio
  - https://github.com/ftiosso/dio-curso-etl
- Porque é necessário?
  - Devido a diversidade tipos de fonte de dados (API, JSON, Excel, Banco de dados relacional, etc)
  - Carregar de forma integra para a análise
- Extração
  - Pode ser extraido em lotes (Batch), exigindo grande processamento
    - Agendado para horarios em que há menor requisição
  - Real time
    - Dados gerados em tempo real
- Visão geral

![image-20211025193729806](C:\Users\Micael\AppData\Roaming\Typora\typora-user-images\image-20211025193729806.png)

- Ferramentas e pacotes para python
  - Apache airflow
  - Luigi
  - bonobo
  - bubbles
  - petl
  - pandas

### Preparação do projeto ETL

- Origem dos dados
  - Modelo de dados
    - Contem informações como os dados estao relacionados
- 

