# Ordenando e filtrando dados

- Para ordenar dados em ordem crescente, utiliza-se o comando ORDER BY.
    
    Exemplo:
    
      SELECT TOP (100)
        *
      ORDER BY
        ‘NOME DA COLUNA’
    
- Para ordenar dados em ordem decrescente, utiliza-se o comando DESC após o comando ORDER BY
    
    Exemplo:
      
      SELECT TOP (100)
        *
      ORDER BY
        ‘NOME DA COLUNA’
      DESC
    

- Também é possível ordenar com mais de uma coluna.
    
    Exemplo:
    
      SELECT
        ‘COLUNA 1’
        ‘COLUNA 2’
      FROM
        ‘TABELA’
      ORDER BY
        ‘COLUNA 1’ DESC,
        ‘COLUNA 2’
    
- Combinando o comando ORDER BY com o comando TOP(’N’) conseguimos encontrar o maior valor de uma coluna.
    
    Exemplo:
      
      SELECT TOP(1)
        ‘COLUNA’
      FROM
        ‘TABELA’
      ORDER BY
        ‘COLUNA’
      DESC
    
- Podemos filtrar colunas com valores numéricos com o comando WHERE
    
    Exemplo: Quantos produtos têm o preço acima de R$ 2000 ?
    
      SELECT
        ‘PRODUTO’
        ‘PREÇO’
      FROM
        ‘TABELA’
      WHERE
        ‘PREÇO’ > = 2000
    

- Também podemos filtrar por texto como o comando WHERE
    
    Exemplo:
    
      SELECT
        *
      FROM
        ‘TABELA’
      WHERE
        ‘COLUNA’ = ‘TEXTO’
    

- Também é possível filtrar por datas com o comando WHERE
    
    Exemplo:
    
      SELECT
        *
      FROM
        ‘TABELA’
      WHERE
        ‘COLUNA’ > = ‘YYYY - MM - DD’
    
    *YYYY - 4 dígitos para o ano*
    *MM - 2 dígitos para o mês*
    *DD - 2 dígitos para o dia*
    
- O comando WHERE pode ser combinado com os operadores AND, OR e NOT
    - AND: Mostra as linhas da tabela se todas as condições forem atendidas
    - OR: Mostra as linhas da tabela se pelo menos uma das condições for atendida
    - NOT: Mostra o oposto do que for considerado no filtro
    
    Exemplo: Selecione todas as linhas da tabela DimProduct onde a cor do produto pode ser igual a Preto ou Vermelho, mas a marca deve ser ‘Fabrikam’
    
      SELECT
        *
      FROM
        DimProduct
      WHERE
        (ColorName = ‘Black’ OR ColorName = ‘Red’ ) AND BrandName = ‘Fabrikam’
    
    *Obs: Colocar entre parentêsis os critérios que serão utilizados primeiramente*
    
- O comando IN após o comando WHERE  é muito útil para qundo há múltiplas opções
    
    Exemplo:
    
      WHERE
        ‘COLUNA’
      IN (’Opção 1’, ‘Opção 2’, ‘Opção 3’)
    
    *Obs: Se fosse utilizar somente o OR para cada opção, teríamos que colocar o nome da coluna antes do nome da opção.*
    
- Para filtrar apenas um trecho de texto, utilizamos o comando LIKE após o nome da coluna e também utilizamos o símbolo % antes e depois do trecho a ser pesquisado.
    
    Exemplo:
    
      WHERE
        ‘COLUNA’
      LIKE ‘% TRECHO %’
    
- Para filtrar dados entre valores, poderemos utilizar o comando BETWEEN e AND
    
    Exemplo:
    
      WHERE
        ‘COLUNA’
      BETWEEN ‘VALOR 1’ AND ‘VALOR 2’
    
- Também é possível fazer o inverso com o comando NOT antes do BETWEEN

- Para encontrar valores vazios, basta utilizar o comando IS NULL
    
    Exemplo:
    
      WHERE
        ‘COLUNA’
      IS NULL
    
- Também podemos fazer o inverso com o comando IS NOT NULL
