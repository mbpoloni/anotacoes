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
  df = pd.read_csv("caminho_arquivo", sep=";", parse_dates=["nome_coluna"], dayfirst=True)
  df
  ```

  atribui o objeto do caminho especificado a df, identifica que a separação dos dados é realizada por ";", converte a coluna "nome_coluna" para data colocando a o dia como inicio da data  e imprimi

- ```
  df.dtypes
  ```

  exibe o tipo de cada coluna do data frame

- ```
  df.coluna_data.dt.month
  ```

  exibe o mes da data
  
- valores vazios

  - Campo texto = retorna NaN
  - Campo data = retorna NaT

- pandera

  - biblioteca para validação

    ```
    schema = pa.DataFrameSchema(
    	columns = {
    	"nome_coluna": pa.Column(pa.DateTime, nullable=True)
    	}
    )
    ```

    cria um esquema para validação da coluna tipo Datetime

    ```
    schema.validate(df)
    ```

    faz a validação do esquema no dataframe df

    ```
    pa.Check.str_matches(r'^([0-1]?[0-9]|[2][0-3]):([0-5][0-9](:[0-5][0-9])?$'))
    ```

    faz a checagem de hora 

    ```
    pa.Check.str_length(2,2)
    ```

    faz a checagem da quantidade de dígitos

    ```
    pa.Column(pa.Int, required=False)
    ```

    habilita que o esquema valide mesmo não tendo a coluna presente

### Desenvolvimento do projeto ETL - Limpeza

```
df.loc[linha, coluna]
df.loc[1,'ocorrencia_cidade']
```

exibe o valor presente na célula da linha 1 e coluna ocorrencia_cidade

```
df.loc[1:3]
```

exibe os valores das linhas 1 até 3

```
df.loc[[10,40]]
```

exibe os valores das linhas 10 e 40

```
df.loc[:, 'nome_coluna']
```

exibe todas as linhas da coluna

```
df.nome_coluna.is_unique
```

verifica se os valores da coluna são unicos

```
df.set_index('nome_coluna', inplace=True)
```

define os valores da coluna como index

```
df.reset_index(drop=True, inplace=True)
```

reseta os valores de index

```
def.loc[0,nome_coluna] = ''
```

substitui o valor da celula na linha 0 da coluna especificada para ''

```
df.loc[:, nome_coluna] = ''
```

substitui todos os valores da coluna para ''

```
df['nome_coluna_nova'] = df.nome_coluna
```

copia uma nova coluna com os valores da coluna

```
df.loc[df.ocorrencia == 'SP', ['ocorrencia_classificacao']] = 'GRAVE'
```

altera o valor para grave na coluna 'ocorrencia_classificacao' one a ocorrencia for igual a SP

```
df.loc[df.ocorrencia_aerodromo == '****', ['ocorrencia_aerodromo']] = pd.NA
```

substitui os valores **** da coluna ocorrencia_aerodromo para NA

```
df.replace(['**','##!','####','****','*****','NULL'], pd.NA, inplace=True)
```

substitui por NA

```
df.isna() ou df.isnull()
```

exibe os valores que estão NA

```
df.isna().sum()
```

exibe a soma dos valores NA por coluna

```
df.fillna(0, inplace=True)
```

substitui os valores nulos por zero

```
df.fillna(value={'total_recomendacoes':10}, inplece=True)
```

substitui os valores NA da coluna total_recomendacoes por 10

```
df.drop(['nome_coluna'], axis=1, inplace=True)
```

elimina a coluna

```
df.dropna()
```

elimina as linhas que possuem valores NA

```
df.dropna(subset=['nome_coluna'])
```

elimina a linha que conter NA na coluna especifica

```
df.drop_duplicates(inplace=True)
```

elimina linhas duplicadas

missing values - valores não informados

​	Pode ser tratado pelo NA do pandas, ou NaN do Numpy

outlier - extrapolou o valor normal

