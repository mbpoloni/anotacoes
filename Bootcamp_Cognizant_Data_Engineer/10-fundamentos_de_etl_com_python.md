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

### Desenvolvimento do projeto ETL - Extração e validação

- ```
  import pandas as pd
  ```

  importa a biblioteca e atribui um alias

- ```
  df = pd.read_csv("caminho_arquivo", sep=";", parse_dates=["nome_coluna"])
  df
  ```

  atribui o objeto do caminho especificado a df, identifica que a separação dos dados é realizada por ";", converte a coluna "nome_coluna" para data  e imprimi

- ```
  df.dtypes
  ```

  exibe o tipo de cada coluna do data frame

- ```
  df.coluna_data.dt.month
  ```

  exibe o mes da data

