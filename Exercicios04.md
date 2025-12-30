    SELECT * FROM FactSales

*Os exercícios abaixo estão divididos de acordo com uma determinada tabela do Banco de Dados FACTSALES*  
*1. a) Faça um resumo da quantidade vendida (SalesQuantity) de acordo com o canal de vendas
(channelKey)*

    SELECT
    	channelKey AS 'Canal de Vendas', -- Seleciona a coluna 'channelKey' e renomeia para 'Canal de Vendas'
    	COUNT (SalesQuantity) AS 'Quantidade de Vendas' -- Realiza a contagem dos valores da coluna 'SalesQuantity' e renomeia para 'Quantidade de Vendas'
    FROM
    	FactSales
    GROUP BY 
    	channelKey --Agrupa os dados de acordo com a coluna 'channelKey'

*b) Faça um agrupamento mostrando a quantidade total vendida (SalesQuantity) e quantidade
total devolvida (Return Quantity) de acordo com o ID das lojas (StoreKey).*

    SELECT
    	StoreKey AS 'ID da Loja', -- Seleciona a coluna 'StoreKey' e renomeia para 'ID da loja'
    	SUM(SalesQuantity) AS 'Quantidade Vendida', -- Soma os valores da coluna 'SalesQuantity'
    	SUM(ReturnQuantity) AS 'Quantidade Devolvida' -- Soma os valores da coluna 'ReturnQuatity'
    FROM
    	FactSales --Dados utilizados da tabela 'FactSales'
    GROUP BY
    	StoreKey -- Agrupa os dados de acordo com os dados da coluna 'StoreKey'

*c) Faça um resumo do valor total vendido (SalesAmount) para cada canal de venda, mas apenas
para o ano de 2007.*

    SELECT
    	channelKey AS 'Canal de Venda', -- Seleciona a coluna 'channelKey' e renomeia como 'Canal de Venda'
    	SUM (SalesAmount) AS 'Total Vendido' --Soma os valores da coluna 'SalesAmount' e renomeia como 'Total Vendido'
    FROM
    	FactSales --Dados utilizados da tabela 'FactSales'
    WHERE
    	DateKey BETWEEN '20070101' AND '20071231' -- Filtra dados da coluna 'DateKey' entre '20070101' e '20071231'
    GROUP BY 
    	channelKey -- Agrupa os dados de acordo com a coluna 'channelKey'

*2. Você precisa fazer uma análise de vendas por produtos. O objetivo final é descobrir o valor
total vendido (SalesAmount) por produto (ProductKey)*

*a) A tabela final deverá estar ordenada de acordo com a quantidade vendida e, além disso,
mostrar apenas os produtos que tiveram um resultado final de vendas maior do que
$5.000.000.*

    SELECT
    	ProductKey AS 'Produto', -- Seleciona a coluna 'ProductKey' e renomeia para 'Produto'
    	SUM (SalesAmount) AS 'Total de Vendas' -- Soma os valores da coluna 'SalesAmount' e renomeia para 'Total de Vendas'
    FROM
    	FactSales -- Utiliza os dados da tabela 'FactSales'
    GROUP BY
    	ProductKey -- Agrupa os dados de acordo com a coluna 'ProductKey'
    HAVING
    	SUM(SalesAmount) >= 5000000 -- Seleciona os valores da soma da coluna 'SalesAmount' que sejam maior ou igual a 5000000
    ORDER BY 
    	SUM(SalesAmount) DESC -- Ordena os valores da soma da coluna 'SalesAmount' em ordem decrescente

*b) Faça uma adaptação no exercício anterior e mostre os Top 10 produtos com mais vendas.
Desconsidere o filtro de $5.000.000 aplicado.*

    SELECT TOP(10) -- Seleciona os 10 primeiros valores
    	ProductKey AS 'Produto', -- Seleciona a coluna 'ProductKey' e renomeia para 'Produto'
    	SUM(SalesAmount) AS 'Total de Vendas' -- Soma os valores da coluna 'SalesAmount' e renomeia para 'Total de Vendas'
    FROM
    	FactSales -- Utiliza os dados da tabela 'FactSales'
    GROUP BY
    	ProductKey -- Agrupa os dados de acordo com a coluna 'ProductKey'
    ORDER BY 
    	SUM(SalesAmount) DESC -- Ordena os valores da soma da coluna 'SalesAmount' em ordem decrescente

*3. a) Você deve fazer uma consulta à tabela FactOnlineSales e descobrir qual é o ID
(CustomerKey) do cliente que mais realizou compras online (de acordo com a coluna
SalesQuantity).*

    SELECT TOP(1) -- Seleciona apenas o primeiro valor
    	CustomerKey AS 'ID do cliente', -- Seleciona os dados da coluna 'CustomerKey' e renomeia como 'ID do cliente'
    	SUM(SalesQuantity)AS 'Quantidade de Compras' -- Seleciona a soma dos valores da coluna 'SalesQuantity' e renomeia como 'Quantidade de Compras'
    FROM
    	FactOnlineSales -- Utiliza dados da tabela 'FactOnlineSales'
    GROUP BY
    	CustomerKey -- Agrupa os dados de acordo com a coluna 'CustomerKey'
    ORDER BY
    	SUM(SalesQuantity) DESC -- Ordena a soma dos valores da coluna 'SalesQuantity' em ordem decrescente

*b) Feito isso, faça um agrupamento de total vendido (SalesQuantity) por ID do produto
e descubra quais foram os top 3 produtos mais comprados pelo cliente da letra a) - ID do cliente = 19037.*

    SELECT TOP(3) -- Seleciona apenas os três primeiros valores
    	ProductKey AS 'ID do Produto', -- Seleciona os dados da coluna 'ProductKey' e renomeia para 'ID do Produto'
    	SUM(SalesQuantity) AS 'Total Vendido' -- Seleciona a soma dos valores da coluna 'SalesQuantity' e renomeia para 'Total Vendido'
    FROM
    	FactOnlineSales -- Utiliza dados da tabela 'FactOnlineSales'
    WHERE
    	CustomerKey = '19037' -- Filtra para utilizar somente os dados do cliente '19037'
    GROUP BY
    	ProductKey -- Agrupa de acordo com os valores da coluna 'Product Key'
    ORDER BY
    	SUM(SalesQuantity) DESC -- Ordena os dados da soma dos valores da coluna 'SalesQuantity' em ordem decrescente

*4. a) Faça um agrupamento e descubra a quantidade total de produtos por marca.*

    SELECT
    	BrandName AS 'Marca', -- Selieciona os dados da coluna BrandName' e renomeia para 'Marca'
    	COUNT(BrandName) AS 'Quantidade' -- Realiza a contagem da quantidade de dados da coluna 'BrandName'
    FROM
    	DimProduct -- Utiliza os dados da tabela 'DimProduct'
    GROUP BY
    	BrandName -- Agrupa os dados de acordo com a coluna 'BrandName'

*b) Determine a média do preço unitário (UnitPrice) para cada ClassName.*

    SELECT 
    	ClassName AS 'Classe do Produto', -- Seleciona os dados da coluna 'ClassName'  renomeia para 'Classe do Produto'
    	AVG(UnitPrice) AS 'Média de Preços'  -- Faz uma média com s valores da coluna 'UnitPrice' e renomeia para 'Médai de Preços'
    FROM
    	DimProduct -- Utiliza dados da tabela DimProduct'
    GROUP BY 
    	ClassName -- Agrupa de acordo com a coluna 'Classname'
	
*c) Faça um agrupamento de cores e descubra o peso total que cada cor de produto possui.*

    SELECT 
    	ColorName AS 'Cor', -- Seleciona os dados da coluna 'ColorName' e renomeia para 'Cor'
    	COUNT(Weight) AS 'Peso' -- Faz uma contagem dos valores da coluna 'Weight' e renomeia para 'Peso'
    FROM
    	DimProduct -- Utiliza dos dados tabela 'DimProduct'
    GROUP BY
    	ColorName -- Agrupa de acordo com os valores da coluna 'ColorName'

*5. Você deverá descobrir o peso total para cada tipo de produto (StockTypeName).
A tabela final deve considerar apenas a marca ‘Contoso’ e ter os seus valores classificados em
ordem decrescente.*

    SELECT 
    	StockTypeName AS 'Tipo de Produto', -- Seleciona os dados da coluna 'StockTypeName' e renomeia para Tipo de Produto'
    	SUM(Weight) AS 'Peso' --Faz a soma dos valores da coluna 'Weight' e renomeia para 'Peso'
    FROM
    	DimProduct -- Utiliza dados da tabela 'DimProduct'
    WHERE
    	BrandName = 'Contoso' -- Filtra apenas os produtos da marca 'Contoso'
    GROUP BY
    	StockTypeName -- Ordena os dados de acordo com a coluna 'StockTypeName'
    ORDER BY 
    	SUM(Weight) DESC -- Ordena os dados das soma dos pesos em ordem decrescente

*6. Você seria capaz de confirmar se todas as marcas dos produtos possuem à disposição todas as
16 opções de cores?*

    SELECT
    	BrandName AS 'Marca', -- Seleciona os dados da coluna 'BrandName' e renomeia para 'Marca'
    	COUNT(DISTINCT ColorName) AS 'Quantidade de Cores' -- Realiza a contagem de valores distintos da coluna 'ColorName' e renomeia para 'Quantidade de Cores'
    FROM
    	DimProduct -- Utiliza os dados da tabela 'DimProduct'
    GROUP BY 
    	BrandName -- Agrupa de acordo com os dados da coluna 'BrandName'

*7. Faça um agrupamento para saber o total de clientes de acordo com o Sexo e também a média
salarial de acordo com o Sexo. Corrija qualquer resultado “inesperado” com os seus
conhecimentos em SQL.*

    SELECT *  from DimCustomer
    
    SELECT
    	Gender AS 'Gênero', -- Seleciona os dados da coluna 'Gender' e renomeia para 'Gênero'
    	COUNT(CustomerKey) AS 'Qtde. Clientes', -- Realiza a contagem dos dados da coluna 'CustomerKey' e renomeia para 'Qtde. Clientes'
    	AVG(YearlyIncome) AS 'Média Salarial' -- Realiza a média dos valores da coluna 'YearlyIncome' e renomeia para 'Média Salarial'
    FROM
    	DimCustomer -- Utiliza os dados da tabela 'DimCustomer'
    WHERE
    	Gender IS NOT NULL -- Filtra os dados da coluna 'Gender' e seleciona os valores diferentes de 'Null'
    GROUP BY 
    	Gender -- Agrupa de acordo com os dados da coluna 'Gender'

*8. Faça um agrupamento para descobrir a quantidade total de clientes e a média salarial de
acordo com o seu nível escolar. Utilize a coluna Education da tabela DimCustomer para fazer
esse agrupamento.*
	
    SELECT 
    	Education AS 'Nível Escolar', -- Seleciona os dados da coluna 'Education' e renomeia para 'Nível Escolar'
    	COUNT (Education) AS 'Qtde. Total', -- Realiza a contagem dos dados da coluna 'Education' e renomeia para 'Qtde. Total'
    	AVG (YearlyIncome) AS 'Média Salrial' -- Faz a méida dos dados da coluna 'YearlyIncome' e renomeia para 'Média Salarial'
    FROM 
    	DimCustomer
    WHERE
    	Education IS NOT NULL -- Filtra os dados da coluna 'Education' e seleciona valores diferentes de NULL
    GROUP BY 
    	Education -- Agrupa de acordo com os dados da coluna 'Education'

*9. Faça uma tabela resumo mostrando a quantidade total de funcionários de acordo com o
Departamento (DepartmentName). Importante: Você deverá considerar apenas os
funcionários ativos.*

    SELECT * FROM DimEmployee
    
    SELECT
    	DepartmentName AS 'Departamento', -- Seleciona os dados da coluna 'DepartmentName' e renomeia para 'Departamento'
    	COUNT(DepartmentName) AS 'Qtde. Funcionários)' -- Realiza a contagem dos dados da coluna 'DepartmentName' e renomeia para 'Funcionários'
    FROM 
    	DimEmployee
    WHERE
    	Status IS NOT NULL -- Filtra os dados que não estão com valores nulos (Null)
    GROUP BY
    	DepartmentName -- Agrupa de acordo com a coluna 'DepartmentName'

*10. Faça uma tabela resumo mostrando o total de VacationHours para cada cargo (Title). Você
deve considerar apenas as mulheres, dos departamentos de Production, Marketing,
Engineering e Finance, para os funcionários contratados entre os anos de 1999 e 2000*

    SELECT
    	Title AS 'Cargo', -- Seleciona os dados da coluna 'Title' e renomeia para 'Cargo'
    	SUM(VacationHours) AS 'Horas' -- Soma os valores da coluna 'VacationHours' e renomeia para 'Horas'
    FROM
    	DimEmployee
    WHERE 
    	Gender = 'F' AND DepartmentName IN ('Production', 'Marketing', 'Engineering', 'Finance') AND HireDate BETWEEN '1999-01-01' AND '2000-12-31'
    	--Filtra o gênero para 'F (Feminino), os setores para 'Produção', 'Marketing', 'Engenharia' e 'Finanças' e filtra os contratos iniciados entre 01-01-1999 e 31-12-2000 
    GROUP BY
    	Title -- Agrupa de acordo com a coluna 'Title'
