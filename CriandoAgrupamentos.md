# Criando Agrupamentos

## GROUP BY (Parte 1)
- Utiliza-se GROUP BY para agrupar dados em relação às colunas.  
  Exemplo:
  
      SELECT
      'COLUNA'
       COUNT( * )
      FROM
      'TABELA'
      GROUP BY 'COLUNA QUE SERÁ EXIBIDA'
  
- Irá aparecer os valores da coluna e da contagem dos valores da tabela
  
- Do total de funcionários, agrupar em relação ao tipo de loja  
  Exemplo:

      SELECT
        SUM (EmployeeCount), -- Somar quantidade de funcionários
        StoreType -- Tipos de loja
      FROM
        DimStore -- Tabela
      GROUP BY StoreType -- Irá agrupar a quantidade de funcionários por tipo de loja

- É possível também utilizar o GROUP BY em conjunto com o ORDER BY  
  Exemplo:

      SELECT
        SUM (EmployeeCount),
        StoreType
      FROM
        DimStore
      GROUP BY StoreType
      ORDER BY EmployeeCount -- Irá ordenar o número de funcionários em ordem crescente

- Também é possível combinar o GROUP BY com o WHERE
- É importante que se utilize o comando WHERE antes do comando GROUP BY
  Exemplo:

      SELECT
        ColorName -- Coluna com os nomes das cores
        COUNT ( * ) -- Contabiliza os valores da tabela
      FROM
        DimProduct -- Tabela
      WHERE BrandNAme = 'Contoso' -- Filtra apenas da marca 'Contoso'
      GROUP BY ColorName -- Agrupa por nome da cor

- O filtro HAVING é feito após o agrupamento (GROUP BY)  
  Exemplo:

      SELECT
        BrandName -- Coluna com os nomes das marcas
        COUNT (BrandName) -- Cotabiliza os valores da coluna 'BrandName'
      FROM
        DimProduct -- Tabela
      GROUP BY BrandName -- Agrupa por nome de marcas
      HAVING COUNT(BrandName) > = 200 -- Exibe apenas as marcas que têm 200 ou mais itens

- O comando WHERE filtra a tabela original, antes do agrupamento
- O comando HAVING fitra a tabela após o agrupamento
    
