*1. O gerente comercial pediu a você uma análise da Quantidade Vendida e Quantidade
Devolvida para o canal de venda mais importante da empresa: Store.*

*Utilize uma função SQL para fazer essas consultas no seu banco de dados. Obs: Faça essa
análise considerando a tabela FactSales.*

    SELECT 
    	SUM(SalesQuantity) AS 'Quantidade Vendida', -- Realiza a soma dos valores da coluna 'SalesQuantity'.
    	SUM(ReturnQuantity) AS 'Quantidade Devolvida' -- Realiza a soma dos valores da coluna 'ReturnQuantity'
    FROM
    	FactSales 

*2. Uma nova ação no setor de Marketing precisará avaliar a média salarial de todos os clientes
da empresa, mas apenas de ocupação Professional. Utilize um comando SQL para atingir esse
resultado.*

    SELECT
    	AVG(YearlyIncome) AS 'Média Anual de Salários' -- Realiza a média dos valores da coluna 'YearlyIncome'
    FROM
    	DimCustomer
    WHERE 
    	Occupation = 'Professional' -- Considera apenas os valores 'Professional' na coluna 'Occupation'

*3. Você precisará fazer uma análise da quantidade de funcionários das lojas registradas na
empresa. O seu gerente te pediu os seguintes números e informações*

    SELECT * FROM DimStore

*a) Quantos funcionários tem a loja com mais funcionários?*

    SELECT
    	MAX(EmployeeCount) -- Retorna o maior valor da coluna 'EmployeeCount'
    FROM
    	DimStore

*b) Qual é o nome dessa loja?*

    SELECT
    	TOP(1) StoreName AS 'Loja com mais funcionários' -- Retorna o valor da coluna da primeira linha listada e renomeia para 'Loja com mais funcionários'
    FROM
    	DimStore
    ORDER BY EmployeeCount DESC -- Retorna o valor da coluna 'EmployeeCount' na ordem decrescente

*c) Quantos funcionários tem a loja com menos funcionários?*

    SELECT
    	MIN(EmployeeCount) --Retorna o menor valor da coluna 'EmployeeCount'
    FROM
    	DimStore

*d) Qual é o nome dessa loja?*

    SELECT 
    	TOP(1) StoreName AS 'Loja com menos funcionários', --Retorna o valor da primeira linha listada da coluna 'StoreName' e renomeia para 'Loja com menos funcionários'
    FROM
    	DimStore
    WHERE
    	EmployeeCount IS NOT NULL -- Não considera valores 'NULL' 
    ORDER BY EmployeeCount --Ordena os valores da coluna em ordem crescente

*4. A área de RH está com uma nova ação para a empresa, e para isso precisa saber a quantidade
total de funcionários do sexo Masculino e do sexo Feminino.*

    SELECT * FROM DimEmployee

*a) Descubra essas duas informações utilizando o SQL.*

    SELECT 
    	COUNT(Gender) AS 'Homens' -- Realiza a contagem dos valores da coluna 'Gender' e renomeia para 'Homens'
    FROM
    	DimEmployee
    WHERE 
    	Gender = 'M' -- Retorna apenas as linhas com o valor 'M'

    SELECT 
    	COUNT(Gender) AS 'Mulheres' -- Realiza a contagem dos valores da coluna 'Gender' e renomeia para 'Mulheres'
    FROM
    	DimEmployee
    WHERE 
    	Gender = 'F'-- Retorna apenas as linhas com valor 'F'

*b) O funcionário e a funcionária mais antigos receberão uma homenagem. Descubra as
seguintes informações de cada um deles: Nome, E-mail, Data de Contratação.*

    SELECT 
    	TOP(1) FirstName AS 'Nome', -- Retorna o valor da primeira linha listada da coluna 'FirstName' e renomeia para 'Nome'
    	LastName AS 'Sobrenome', -- Renomeia a coluna 'LastName' para 'Sobrenome'
    	HireDate AS 'Admissão' -- Renomeia a coluna 'HireDate' para 'Admissão'
    FROM
    	DimEmployee
    WHERE
    	Gender = 'M' -- Retorna apenas os valores 'M' da coluna 'Gender'
    ORDER BY HireDate -- Lista em ordem crescente os valores da coluna 'HireDate'

    SELECT 
    	TOP(1) FirstName AS 'Nome', -- Retorna o valor da primeira linha listada da coluna 'FirstName' e renomeia para 'Nome'
    	LastName AS 'Sobrenome', -- Renomeia a coluna 'LastName' para 'Sobrenome'
    	HireDate AS 'Admissão' -- Renomeia a coluna 'HireDate' para 'Admissão'
    FROM
    	DimEmployee
    WHERE
    	Gender = 'F' -- Retorna apenas os valores 'F' da coluna 'Gender'
    ORDER BY HireDate -- Lista em ordem crescente os valores da coluna 'HireDate'

*5. Agora você precisa fazer uma análise dos produtos. Será necessário descobrir as seguintes
informações:*
    
    SELECT * FROM DimProduct

*a) Quantidade distinta de cores de produtos.*
*b) Quantidade distinta de marcas.*
*c) Quantidade distinta de classes de produtos.*

    SELECT
    	COUNT(DISTINCT ColorName) AS 'Quantidade de Cores', -- Realiza a contagem de valores distintos da coluna 'ColorName' e renomeia para 'Quantidade de Cores' 
    	COUNT(DISTINCT BrandName) AS 'Quantidade de Marcas', -- Realiza a contagem de valores distintos da coluna 'BrandName' e renomeia para 'Quantidade de Marcas'
    	COUNT(DISTINCT ClassName) AS 'Quantidade de Classes' -- Realiza a contagem de valores distintos da coluna 'ClassName' e renomeia para 'Quantidade de Classes'
    FROM
    	DimProduct
    WHERE 
    	ColorName IS NOT NULL AND BrandName IS NOT NULL AND ClassName IS NOT NULL -- Retorna apenas valores das colunas 'ColorName', 'BrandName' e 'ClassName' que não sejam 'Null'

