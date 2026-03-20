
*1. a) Faça um resumo da quantidade vendida (Sales Quantity) de acordo com o nome do canal
de vendas (ChannelName). Você deve ordenar a tabela final de acordo com SalesQuantity,
em ordem decrescente.*

    SELECT TOP(50)  -- Seleciona as 50 primeiras linhas das colunas declaradas
    	ChannelName AS 'Canal de Vendas',  -- Renomeia a coluna 'ChannelName' para 'Canal de Vendas'
    	SUM(SalesQuantity) AS 'Qtde. Vendas'   -- Renomeia a soma dos valores da coluna 'SalesQuantity' para 'Qtde. Vendas'
    FROM
    	FactSales  -- Tabela principal
    INNER JOIN DimChannel  -- Relaciona os itens em comum entre as tabelas 'FactSales' e 'DimChannel'
    	ON FactSales.channelKey = DimChannel.ChannelKey  -- Relaciona as colunas mencionadas 
    GROUP BY ChannelName   -- Agrupa por itens da coluna 'ChannelName'
    ORDER BY SUM(SalesQuantity) DESC  -- Ordena a soma dos itens da coluna 'SalesQuantity' em ordem decrescente

*b) Faça um agrupamento mostrando a quantidade total vendida (Sales Quantity) e
quantidade total devolvida (Return Quantity) de acordo com o nome das lojas
(StoreName).*

    SELECT TOP(30)  -- Seleciona as 30 primeiras linhas das colunas declaradas
	  StoreName AS 'Loja',  -- Renomeia a coluna 'StoreName' para 'Loja'
	  SUM(SalesQuantity) AS 'Vendas',  -- Renomeia a soma dos itens da coluna 'SalesQuantity' para 'Vendas'
	  SUM(ReturnQuantity) AS 'Devoluções'  -- Renomeia a soma dos itens da coluna 'ReturnQuantity' para 'Devoluções'
    FROM
	    FactSales  -- Tabela principal
    INNER JOIN DimStore  -- Relaciona os itens em comum entre as tabelas 'FactSales' e 'DimStore'
    	ON FactSales.StoreKey = DimStore.StoreKey  -- Relaciona as colunas mencionadas
    GROUP BY StoreName  -- Agrupa por itens da coluna 'StoreName'

*c) Faça um resumo do valor total vendido (Sales Amount) para cada mês
(CalendarMonthLabel) e ano (CalendarYear).*

    SELECT TOP (30)  -- Relaciona as 30 primeiras linhas da colunas declaradas
  	  CalendarYear AS 'Ano',  -- Renomeia a coluna 'CalendarYear' para 'Ano'
  	  CalendarMonthLabel AS 'Mês',  -- Renomeia a coluna 'CalendarMonthLabel' para 'Mês'
  	  SUM(SalesAmount) AS 'Total Vendido'  -- Renomeia a soma dos itens da coluna 'SalesAmount' para 'Toatal Vendido'
    FROM
    	FactSales  -- Tabela principal
    INNER JOIN DimDate  -- Relaciona os itens em comum entre as tabelas 'FactSales' e 'DimDate'
    	ON FactSales.DateKey = DimDate.Datekey  -- Relaciona os itens das colunas mencionadas
    GROUP BY
    	CalendarYear,  -- Agrupa por itens da coluna 'CalendarYear'
    	CalendarMonthLabel,  -- Agrupa por itens da coluna 'CalendarMonthLabel'
    	CalendarMonth  -- Agrupa por itens da coluna 'CalendarMonth'
    ORDER BY 
    	CalendarMonth  -- Ordena os itens da coluna 'CalendarMonth' em ordem crescente

*2. Você precisa fazer uma análise de vendas por produtos. O objetivo final é descobrir o valor
total vendido (SalesQuantity) por produto.

a) Descubra qual é a cor de produto que mais é vendida (de acordo com SalesQuantity).*

    SELECT TOP(20)  -- Relaciona as 20 primeiras linhas das colunas declaradas 
    	ColorName AS 'Cor',  -- Renomeia a coluna 'ColorName' para 'Cor'
    	SUM(SalesQuantity) AS 'Quantidade Vendas'  -- Renomeia a soma dos itens da coluna 'SalesQuantity' para 'Quantidade Vendas'
    FROM
    	FactSales  -- Tabela principal
    INNER JOIN DimProduct  -- Relaciona os itens em comum das tabelas 'FactSales' e 'DimProduct'
    	ON FactSales.ProductKey = DimProduct.ProductKey  -- Relaciona os itens das colunas mencionadas
    GROUP BY 
    	ColorName  -- Agrupa po itens da coluna 'ColorName'
    ORDER BY 
    	SUM(SalesQuantity) DESC  -- Ordena a soma dos itens da coluna 'SalesQuantity' em ordem decrescente

  *b) Quantas cores tiveram uma quantidade vendida acima de 3.000.000.*

      SELECT TOP(20)  -- Relaciona as 20 primeiras linhas das colunas declaradas 
    	  ColorName AS 'Cor',  -- Renomeia a coluna 'ColorName' para 'Cor'
     	  SUM(SalesQuantity) AS 'Quantidade Vendas'  -- Renomeia a soma dos itens da coluna 'SalesQuantity' para 'Quantidade Vendas'
      FROM
    	  FactSales  -- Tabela principal
      INNER JOIN DimProduct  -- Relaciona os itens em comum das tabelas 'FactSales' e 'DimProduct'
    	  ON FactSales.ProductKey = DimProduct.ProductKey  -- Relaciona os itens das colunas mencionadas
      GROUP BY 
    	  ColorName  -- Agrupa po itens da coluna 'ColorName'
      HAVING	SUM(SalesQuantity) > 3000000  -- Filtra para retornar apenas os valores da soma dos itens da coluna 'SalesQuantity' acima de 3000000

*3. Crie um agrupamento de quantidade vendida (SalesQuantity) por categoria do produto
(ProductCategoryName). Obs: Você precisará fazer mais de 1 INNER JOIN, dado que a relação
entre FactSales e DimProductCategory não é direta.*

    SELECT 
    	ProductCategoryName AS 'Categoria', -- Renomeia a coluna 'ProductCategoryName' para 'Categoria'
    	SUM(SalesQuantity) AS 'Qtde. Vendida' -- Renomeia a soma dos itens da coluna 'SalesQuantity' para 'Qtde. Vendida'	
    FROM
    	FactSales -- Tabela principal
    INNER JOIN DimProduct -- Relaciona os itens em comum entre as tabelas 'FactSales' e 'DimProduct'
    	ON FactSales.ProductKey = DimProduct.ProductKey -- Relaciona os itens das tabelas listadas
    		INNER JOIN DimProductSubcategory -- Relaciona os itens em comum entre a tabela 'DimProduct' e 'DimProductSubcategory'
    			ON DimProduct.ProductSubcategoryKey = DimProductSubcategory.ProductSubcategoryKey -- Relaciona os itens das tabelas listadas
    				INNER JOIN DimProductCategory -- Relaciona os itens em comum entre as tabelas 'DimProductCategory' e 'DimProductSubcategory'
    					ON DimProductSubcategory.ProductCategoryKey = DimProductCategory.ProductCategoryKey -- Relaciona os itens da tabelas listadas
    GROUP BY ProductCategoryName -- Agrupa de acordo  com a tabela 'ProductCategoryName'

*4. a) Você deve fazer uma consulta à tabela FactOnlineSales e descobrir qual é o nome completo
do cliente que mais realizou compras online (de acordo com a coluna SalesQuantity).*

    SELECT
    	FactOnlineSales.CustomerKey AS 'ID', --Renomeia a coluna 'CustomerKey' da tabela 'FactOnlineSales' para 'ID'
    	FirstName AS 'Nome', -- Renomeia a coluna 'FirstName' para 'Nome'
    	LastName AS 'Sobrenome', -- Renomeia a coluna 'LastName' para 'Sobrenome'
    	SUM(SalesQuantity) AS 'Qtde. Vendida' -- Renomeia a soma dos valores da coluna 'SalesQuantity' para 'Qtde. Vendida'
    FROM
    	FactOnlineSales -- Tabela principal
    INNER JOIN DimCustomer -- Relaciona os itens em comum entre as tabelas 'FactOnlineSales' e 'DimCustomer'
    	ON FactOnlineSales.CustomerKey = DimCustomer.CustomerKey -- Relaciona os itens das tabelas mencionadas
    WHERE
    	CustomerType = 'Person' -- Filtra pelos dados em que a coluna 'CustomerType' é igual a 'Person'
    GROUP BY 
    	FactOnlineSales.CustomerKey, FirstName, LastName -- Agrupa de acordo com as tabelas mencionadas
    ORDER BY
    	SUM(SalesQuantity) DESC -- Ordena a soma dos valores da tabela 'SalesQuantity' em ordem decrescente
      
    -- Resposta: Robert Long, comprou 376 itens

*b) Feito isso, faça um agrupamento de produtos e descubra quais foram os top 10 produtos mais
comprados pelo cliente da letra a, considerando o nome do produto.*

    SELECT TOP(10) -- Seleciona os 10 primeiros itens
    	ProductName AS 'Produto', -- Renomeia a coluna 'ProductName' para 'Produto'
    	SUM(SalesQuantity) AS 'Qtde. Vendida' -- Renomeia a soma dos valores da coluna 'SalesQuantity' para 'Qtde. Vendida'
    FROM
    	FactOnlineSales -- Tabela principal
    INNER JOIN DimProduct -- Relaciona os itens em comum entre as tabelas 'FactOnlineSales' e 'DimProduct'
    	ON FactOnlineSales.ProductKey = DimProduct.ProductKey -- Relacioan os itens das tabelas mencionadas
    WHERE 
    	CustomerKey = 7665 -- Filtra pelos dados e que a coluna 'CustomerKey' seja '7665'
    GROUP BY
    	ProductName -- Agrupa de acordo com a coluna 'ProductName'
    ORDER BY
    	SUM(SalesQuantity) DESC -- Ordena a soma dos valores da tabela 'SalesQuantity' em ordem decrescente

*5. Faça um resumo mostrando o total de produtos comprados (Sales Quantity) de acordo com o
sexo dos clientes.*

      SELECT 
    	Gender AS 'Gênero', -- Renomeia a coluna 'Gender' para 'Gênero'
    	SUM(SalesQuantity) AS 'Qtde. Vendas' -- Renomeia a soma dos valores da coluna 'SalesQuantity' para 'Qtde. Vendas'
    FROM
    	FactOnlineSales -- Tabela principal
    INNER JOIN DimCustomer -- Relaciona os itens em comum entre as tabelas 'FactOnlineSales' e 'DimCustomer'
    	ON FactOnlineSales.CustomerKey = DimCustomer.CustomerKey -- Relaciona os itens em comum nas colunas mencionadas
    WHERE
    	Gender IS NOT NULL -- Filtra por valores que não sejam nulos
    GROUP BY
    	Gender -- Agrupa de acordo com os valores da coluna 'Gender'

  *6. Faça uma tabela resumo mostrando a taxa de câmbio média de acordo com cada
CurrencyDescription. A tabela final deve conter apenas taxas entre 10 e 100.*

    SELECT
    	CurrencyDescription AS 'Moeda', -- Renomeia a coluna 'CurrencyDescription' para 'Moeda'
    	AVG(AverageRate) AS 'Taxa média' -- Renomeia a méda dos valores da coluna 'AverageRate' para 'Taxa média'
    FROM
    	FactExchangeRate -- Tabela principal
    INNER JOIN DimCurrency -- Relaciona os itens em comum entre as tabelas 'FactExchangeRate' e 'DimCurrency'
    	ON FactExchangeRate.CurrencyKey = DimCurrency.CurrencyKey -- Relaciona os itens em comum nas tabelas mencionadas
    GROUP BY
    	CurrencyDescription -- Agrupa de acordo com os valores da coluna 'CurrencyDescription'
    HAVING 
    	AVG(AverageRate) BETWEEN 10 AND 100 -- Filtra para´os valores da média da coluna 'AverageRate' para enttre 10 e 100
    ORDER BY
    	AVG(AverageRate) -- Ordena de acordo com a média dos valores da coluna 'Average Rate'

  *7. Calcule a SOMA TOTAL de AMOUNT referente à tabela FactStrategyPlan destinado aos
cenários: Actual e Budget.*

    SELECT
    	ScenarioName AS 'Cenário', -- Renomeia a coluna 'ScenarioName' para 'Cenário'
    	SUM(Amount) AS 'Total' -- Renomeia a soma dos valores da coluna 'Amount' para 'Total'
    FROM
    	FactStrategyPlan -- Tabela principal
    INNER JOIN DimScenario -- Relaciona os itens em comum entre as tabelas 'FactStarategyPlan' e 'DimScenario'
    	ON FactStrategyPlan.ScenarioKey = DimScenario.ScenarioKey -- Relaciona os itens em comum das colunas mencionadas
    GROUP BY 
    	ScenarioName -- Agrupa pelos valores da coluna 'ScenarioName'
    HAVING
	    ScenarioName <> 'Forecast' -- Filtra por valores da coluna ScenarioName que sejam diferentes de 'Forecast'

*8. Faça uma tabela resumo mostrando o resultado do planejamento estratégico por ano.*

    SELECT
    	CalendarYear AS 'Ano', -- Renomeia a coluna 'CalendarYear' paa 'Ano'
    	SUM(Amount) AS 'Total' -- Renomeia a soma dos valores da coluna 'Amount' para 'Total'
    FROM
    	FactStrategyPlan -- Tabela principal
    INNER JOIN DimDate -- Relaciona os itens em comum entre as tabelas 'FactStrategyPlan' e	'DimDate'				
    	ON FactStrategyPlan.Datekey = DimDate.Datekey -- Relaciona os itens em comum das tabelas mencionadas
    GROUP BY
    	CalendarYear -- Agrupa de acordo com os valores da coluna 'CalendarYear'

  *9. Faça um agrupamento de quantidade de produtos por ProductSubcategoryName. Leve em
consideração em sua análise apenas a marca Contoso e a cor Silver.*

    SELECT
    	ProductSubcategoryName AS 'Subcategoria', -- Renomeia a coluna 'ProductSubcategoryName' para 'Subcategoria'
    	COUNT(*) AS 'Qtde. Produtos' -- Renomeia a quantidade dos itens da tabela 'DimProduct' para 'Qtde. Produtos'
    FROM
    	DimProduct -- Tabela principal
    INNER JOIN DimProductSubcategory -- Relaciona os itens em comum entre as tabelas 'DimProduct' e 'DimProductSubcategory'
    	ON DimProduct.ProductSubcategoryKey = DimProductSubcategory.ProductSubcategoryKey -- Relaciona os itens em comum das colunas mencionadas
    WHERE
    	BrandName = 'Contoso' AND ColorName = 'Silver' -- Filtra por itens que os valores da coluna 'BrandName' seja 'Contoso' e da coluna 'ColorName' seja 'Silver'
    GROUP BY
    	ProductSubcategoryName -- Agrupa de acordo com os valores da coluna 'ProductSubcategoryName'

*10. Faça um agrupamento duplo de quantidade de produtos por BrandName e
ProductSubcategoryName. A tabela final deverá ser ordenada de acordo com a coluna
BrandName *

    SELECT
    	BrandName AS 'Marca', -- Renomeia a coluna 'BrandName' para 'Marca'
    	ProductSubcategoryName AS 'Subcategoria', -- Renomeia a coluna 'ProductSubcategoryName' para 'Subcategoria'
    	COUNT(*) AS 'Qtde. Produtos' -- Renomeia a quantidade de itens da tabela 'DimProduct' para 'Qtde. Produtos' 
    FROM
    	DimProduct -- Tabela principal
    INNER JOIN DimProductSubcategory -- Relaciona os itens em comum entre as tabelas 'DimProduct' e 'DimProductSubcategory'
    	ON DimProduct.ProductSubcategoryKey = DimProductSubcategory.ProductSubcategoryKey -- Relaciona os itens em comum das colunas mencionadas
    GROUP BY
    	BrandName, ProductSubcategoryName -- Agrupa de acordo com os valores das colunas 'BrandName' e 'ProductSubcategoryName'
    ORDER BY
    	BrandName -- Ordena de acordo com os valores da coluna 'BrandName'

  
