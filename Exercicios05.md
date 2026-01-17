
*1. Utilize o INNER JOIN para trazer os nomes das subcategorias dos produtos, da tabela
DimProductSubcategory para a tabela DimProduct.*

    SELECT
    	DimProduct.ProductName AS 'Produto', -- Renomeia a coluna 'ProductName' da tabela 'DimProduct' para 'Produto'
    	DimProduct.ProductSubcategoryKey AS 'ID', -- Renomeia a coluna 'ProductSubcategoryKey' da tabela 'DimProduct' para 'ID'
    	DimProductSubcategory.ProductSubcategoryName AS 'Subcategoria' -- Renomeia a coluna 'ProductSubcategoryName' da tabela 'DimProductSubcategory' para 'Subcategoria'
    FROM
    	DimProduct -- Tabela principal
    INNER JOIN DimProductSubcategory -- Relaciona os itens em comum entre a tabela principal e tabela 'DimProductSubcategory'
    	ON DimProduct.ProductSubcategoryKey = DimProductSubcategory.ProductSubcategoryKey -- Relaciona as linhas das colunas mencionadas


*2. Identifique uma coluna em comum entre as tabelas DimProductSubcategory e
DimProductCategory. Utilize essa coluna para complementar informações na tabela
DimProductSubcategory a partir da DimProductCategory. Utilize o LEFT JOIN.*

    SELECT 
    	ProductSubcategoryKey AS 'ID', -- Renomeia a coluna 'ProductSubcategoryKey' para 'ID'
    	ProductSubcategoryName AS 'Subcategoria', -- Renomeia a coluna 'ProductSubcategory' para 'Subcategoria'
    	ProductCategoryName AS 'Categoria' -- Renomeia a coluna 'ProductCategoryName' como 'Categoria'
    FROM
    	DimProductSubcategory -- Tabela principal
    LEFT JOIN DimProductCategory -- Relaciona todos os itens da tabela 'DimProductSubcategory' e os itens em comum entre as duas tabelas
    	ON DimProductSubcategory.ProductCategoryKey = DimProductCategory.ProductCategoryKey -- Relaciona as linhas das colunas mencionadas    


*3. Para cada loja da tabela DimStore, descubra qual o Continente e o Nome do País associados
(de acordo com DimGeography). Seu SELECT final deve conter apenas as seguintes colunas:
StoreKey, StoreName, EmployeeCount, ContinentName e RegionCountryName. Utilize o LEFT
JOIN neste exercício.*

    SELECT
    	StoreKey AS 'ID Loja', -- Renomeia a coluna 'StoreKey' como 'ID Loja'
    	StoreName AS 'Loja', -- Renomeia a coluna 'StoreName' como 'Loja'
    	EmployeeCount AS 'Funcionários', -- Renomeia a coluna 'EmployeeCount' como 'Funcionários'
    	ContinentName AS 'Continente', -- Renomeia a coluna 'ContinentName' como 'Continente'
    	RegionCountryName AS 'País' -- Renomeia a coluna 'RegionCountryName' como 'País'
    FROM
    	DimStore -- Tabela principal
    LEFT JOIN DimGeography -- Relaciona todos os itens da tabela 'DimStore' e os itens em comum entre as duas tabelas
    	ON DimStore.GeographyKey = DimGeography.GeographyKey -- Relaciona os itens das colunas mencionadas


*4. Complementa a tabela DimProduct com a informação de ProductCategoryDescription. Utilize
o LEFT JOIN e retorne em seu SELECT apenas as 5 colunas que considerar mais relevantes.*

    SELECT
    	ProductName AS 'Produto', -- Renomeia a coluna 'ProductName' para 'Produto'
    	ProductDescription AS 'Descrição', -- Renomeia a coluna 'ProductDescription' para 'Descrição'
    	Manufacturer AS 'Fabricante', -- Renomeia a coluna 'Manufacturer' para 'Fabricante'
    	BrandName AS 'Marca', -- Renomeia a coluna 'BrandName' para 'Marca'
    	ProductCategoryDescription AS 'Categoria' -- Renomeia a coluna 'ProductCategoryDescription' para 'Categoria'
    FROM
    	DimProduct -- Tabela principal
    LEFT JOIN DimProductSubcategory -- Relaciona todos os itens da tabela principal e os itens em comum com a tabela 'DimProductCategory'
    	ON DimProduct.ProductSubcategoryKey = DimProductSubcategory.ProductSubcategoryKey -- Relaciona os itens das colunas mencionadas
    LEFT JOIN DimProductCategory -- Relaciona todos os itens da tabela principal e os itens em comum com a tabela 'DimProductCategory'
    	ON DimProductSubcategory.ProductCategoryKey  = DimProductCategory.ProductCategoryKey -- Relaciona os itens das colunas mencionadas


*5. A tabela FactStrategyPlan resume o planejamento estratégico da empresa. Cada linha
representa um montante destinado a uma determinada AccountKey.*

*a) Faça um SELECT das 100 primeiras linhas de FactStrategyPlan para reconhecer a tabela.*

    SELECT TOP(100) -- Seleciona as 100 primeiras linhas da tabela
    	*
    FROM
    	FactStrategyPlan
    
    select top(30) * from DimAccount

*b) Faça um INNER JOIN para criar uma tabela contendo o AccountName para cada
AccountKey da tabela FactStrategyPlan. O seu SELECT final deve conter as colunas:
• StrategyPlanKey
• DateKey
• AccountName
• Amount*

    SELECT
    	StrategyPlanKey,
    	DateKey,
    	AccountName,
    	Amount
    FROM
    	FactStrategyPlan -- Tabela principal
    INNER JOIN DimAccount -- Seleciona os itens em comum entre as duas tabelas
    	ON FactStrategyPlan.AccountKey = DimAccount.AccountKey -- Relaciona os itens das colunas mencionadas


*6. Vamos continuar analisando a tabela FactStrategyPlan. Além da coluna AccountKey que
identifica o tipo de conta, há também uma outra coluna chamada ScenarioKey. Essa coluna
possui a numeração que identifica o tipo de cenário: Real, Orçado e Previsão.*

*Faça um INNER JOIN para criar uma tabela contendo o ScenarioName para cada ScenarioKey
da tabela FactStrategyPlan. O seu SELECT final deve conter as colunas:
• StrategyPlanKey
• DateKey
• ScenarioName
• Amount *

    SELECT 
    	StrategyPlanKey,
    	DateKey,
    	ScenarioName,
    	Amount
    FROM
    	FactStrategyPlan -- Tabela principal
    INNER JOIN DimScenario -- Relaciona os itens em comum entre as duas tabelas
    	ON FactStrategyPlan.ScenarioKey = DimScenario.ScenarioKey -- Relaciona todos os itens das colunas mencionadas

*7. Algumas subcategorias não possuem nenhum exemplar de produto. Identifique que
subcategorias são essas.*

    SELECT
    	ProductSubcategoryName AS 'Subcategoria', -- Renomeia a coluna 'ProductSubcategoryName' para 'Subcategoria'
    	ProductName AS 'Produto' -- Renomeia a coluna 'ProductName' para 'Produto'
    FROM
    	DimProduct -- Tabela principal
    RIGHT JOIN DimProductSubcategory -- Relaciona os itens que aparecem somente na tabela 'DimProductSubcategory'
    	ON DimProduct.ProductSubcategoryKey = DimProductSubcategory.ProductSubcategoryKey -- Relaciona todos os itens das colunas mencionadas
    WHERE
    	DimProduct.ProductName IS NULL -- Filtra para aparecer somente os itens da coluna 'ProductName' da tabela 'DimProduct' que estiverem vazios

*8. A tabela abaixo mostra a combinação entre Marca e Canal de Venda, para as marcas Contoso,
Fabrikam e Litware. Crie um código SQL para chegar no mesmo resultado.*

  *NÃO É POSSÍVEL CARREGAR A IMAGEM DO ENUNCIADO DO EXERCÍCIO!!!*

    SELECT
    	DISTINCT BrandName AS 'Marca', -- Exibe apenas valores distintos da coluna 'BrandName' e renomeia a coluna para 'Marca'
    	ChannelName AS 'Canal de Venda' -- Renomeia a coluna 'ChannelName' para 'Canal de Venda'
    FROM
    	DimProduct CROSS JOIN DimChannel -- Combina as colunas das tabelas 'DimProduct' e 'DimChannel'
    WHERE BrandName IN ('Contoso', 'Fabrikam', 'Litware') -- Filtra para exibir somente as marcas mencionadas

*9. Neste exercício, você deverá relacionar as tabelas FactOnlineSales com DimPromotion.
Identifique a coluna que as duas tabelas têm em comum e utilize-a para criar esse
relacionamento.*

*Retorne uma tabela contendo as seguintes colunas:
• OnlineSalesKey
• DateKey
• PromotionName
• SalesAmount*

*A sua consulta deve considerar apenas as linhas de vendas referentes a produtos com
desconto (PromotionName <> ‘No Discount’). Além disso, você deverá ordenar essa tabela de
acordo com a coluna DateKey, em ordem crescente.*

    SELECT TOP(100)  -- Seleciona as 100 primeiras linhas das colunas mencionadas abaixo
    	OnlineSalesKey,
    	DateKey,
    	PromotionName,
    	SalesAmount
    FROM
    	FactOnlineSales -- Tabela principal
    INNER JOIN DimPromotion  -- Relaciona os itens em comum entre as duas tabelas
    	ON FactOnlineSales.PromotionKey = DimPromotion.PromotionKey -- Relaciona todos os itens das colunas mencionadas
    WHERE
    	 PromotionName <> 'No Discount' -- Filtra as linhas da coluna PromotionName' que sejam diferentes de 'No Discount'
    ORDER BY
    	DateKey ASC  -- Ordena as linhas da coluna 'DateKey' em ordem crescente

*10. A tabela abaixo é resultado de um Join entre a tabela FactSales e as tabelas: DimChannel,
DimStore e DimProduct.*
*Recrie esta consulta e classifique em ordem decrescente de acordo com SalesAmount.*

*NÃO É POSSÍVEL CARREGAR A IMAGEM DO ENUNCIADO DO EXERCÍCIO!!!*

    SELECT TOP(50)  -- Relaciona as 50 primeiras linhas das colunas mencionadas abaixo
    	SalesKey,
    	ChannelName,
    	StoreName,
    	ProductName,
    	SalesAmount 
    FROM
    	FactSales -- Tabela principal
    INNER JOIN DimChannel -- Relaciona os itens em comum entre a tabela princiapl e a tabela 'DimChannel'
    	ON FactSales.channelKey = DimChannel.ChannelKey  -- Relaciona todos os itens das colunas mencionadas
    INNER JOIN DimStore  -- Relaciona os itens em comum entre a tabela princiapl e a tabela 'DimStore'
    	ON FactSales.StoreKey = DimStore.StoreKey  -- Relaciona todos os itens das colunas mencionadas
    INNER JOIN DimProduct  -- Relaciona os ites em comum entre a tabela principal e a tabela 'DimProduct'
    	ON FactSales.ProductKey = DimProduct.ProductKey  -- Relaciona todos os itens das colunas mencionadas
    ORDER BY
    	SalesAmount DESC  -- Ordena os itens da coluna 'SalesAmount' em ordem decrescente
