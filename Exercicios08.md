1. Quando estamos manipulando tabelas, é importante pensar em como os dados serão
apresentados em um relatório. Imagine os nomes dos produtos da tabela DimProduct. Os
textos são bem grandes e pode ser que mostrar os nomes completos dos produtos não seja a
opção mais interessante, pois provavelmente não vão caber em um gráfico e a visualização
ficará ruim.

a) Seu gestor te pede para listar todos os produtos para que seja criado um gráfico para ser
apresentado na reunião diária de equipe. Faça uma consulta à tabela DimProduct que
retorne (1) o nome do produto e (2) a quantidade de caracteres que cada produto tem,
e ordene essa tabela do produto com a maior quantidade de caracteres para a menor.

    SELECT
    	ProductName,  -- Seleciona a coluna 'ProductName'
    	LEN(ProductName) AS 'Letras'  -- Cria uma coluna com quantidade de letras das palavras da coluna 'ProductName' e renomeia para 'Letras'
    FROM
    	DimProduct  -- Tabela a ser utilizada
    ORDER BY
    	Letras  -- Ordene os valores de acordo com a coluna 'Letras'
    DESC  -- Ordem decrescente

b) Qual é a média de caracteres dos nomes dos produtos?

    SELECT
    	AVG (LEN (ProductName)) AS 'Médias'  -- Exibe a quantidade média de caracteres dos valores da coluna 'ProductName'
    FROM
    	DimProduct  -- Tabela a ser utilizada

c) Analise a estrutura dos nomes dos produtos e verifique se seria possível reduzir o tamanho
do nome dos produtos. (Dica: existem informações redundantes nos nomes dos produtos?
Seria possível substituí-las?)

    SELECT
    	ProductName,
    	REPLACE (REPLACE (ProductName, BrandName, ''), ColorName, '') AS 'Nome Abreviado'  -- Substitui os valores equivalentes às colunas 'BrandName' e 'ColorName' por espaço vazio
    FROM
    	DimProduct  -- Tabela a ser utilizada

  d) Qual é a média de caracteres nesse novo cenário?

      SELECT 
    	AVG (LEN (REPLACE (REPLACE (ProductName, BrandName, ''), ColorName, ''))) AS 'Média Abreviada'  -- Exibe a média de caracteres dos nomes abreviados dos produtos na coluna 'Média Abreviada'
    FROM
    	DimProduct  -- Tabela a ser utilizada

  2. A coluna StyleName da tabela DimProduct possui alguns códigos identificados por números
distintos, que vão de 0 até 9. Porém, o setor de controle decidiu alterar a identificação do StyleName, e em vez de usar
números, a ideia agora é passar a usar letras para substituir os números, conforme exemplo
abaixo:
0 -> A, 1 -> B, 2 -> C, 3 -> D, 4 -> E, 5 -> F, 6 -> G, 7 -> H, 8 -> I, 9 - J
É de sua responsabilidade alterar os números por letras na coluna StyleName da tabela
DimProduct. Utilize uma função que permita fazer essas substituições de forma prática e rápida.

    SELECT TOP(9)  -- Seleciona as nove primeiras linhas  
    	TRANSLATE (StyleName, '0123456789', 'ABCDEFGHIJ')  -- Converte os caracteres '0123456789' nos caracteres 'ABCDEFGHIJ'
    FROM
    	DimProduct  -- Tabela a ser utilizada

  3. O setor de TI está criando um sistema para acompanhamento individual de cada funcionário da
empresa Contoso. Cada funcionário receberá um login e senha. O login de cada funcionário será
o ID do e-mail. Já a senha será o FirtName + o dia do ano em que o funcionário nasceu, em MAIÚSCULA. 

O responsável pelo TI pediu a sua ajuda para retornar uma tabela contendo as seguintes colunas
da tabela DimEmployee: Nome completo (FirstName + LastName), E-mail, ID do e-mail e Senha.
Portanto, faça uma consulta à tabela DimProduct e retorne esse resultado.

    SELECT
    	FirstName + ' ' + LastName AS 'Nome Completo', -- Renomeia a junção das colunas 'FirstName' e 'LastName' como 'Nome Completo' 
    	EmailAddress AS 'Email',  -- Renomeia a coluna 'EmailAddress' como 'Email'
    	LOWER(LEFT (EmailAddress,CHARINDEX ('@', EmailAddress)-1)) AS 'Usuário',  -- Renomeia o texto em minúsculo antes do '@' de cada linha para 'Usuário'
    	UPPER(LEFT (EmailAddress,CHARINDEX ('@', EmailAddress)-1)) + DATENAME(DAYOFYEAR, BirthDate) AS 'Senha' -- Renomeia a junção do texto da linha anterior em maiúsculo com o dia do ano da coluna 'BithDate' como 'Senha'
    FROM
    	DimEmployee  -- Tabela a ser utilizada

  4. A tabela DimCustomer possui o primeiro registro de vendas no ano de 2001.
Como forma de reconhecer os clientes que compraram nesse ano, o setor de Marketing solicitou
a você que retornasse uma tabela com todos os clientes que fizeram a sua primeira compra neste
ano para que seja enviado uma encomenda com um presente para cada um.

Para fazer esse filtro, você pode utilizar a coluna DateFirstPurchase, que contém a informação da
data da primeira compra de cada cliente na tabela DimCustomer.
Você deverá retornar as colunas de FirstName, EmailAddress, AddressLine1 e DateFirstPurchase
da tabela DimCustomer, considerando apenas os clientes que fizeram a primeira compra no ano
de 2001.

    SELECT 
    	FirstName AS 'Nome',  -- Renomeia a coluna 'FirstName' como 'Nome'
    	EmailAddress AS 'Email',  -- Renomeia a coluna 'EmailAddress' como 'Email'
    	AddressLine1 AS 'Endereço',  -- Renomeia a coluna 'AddressLine1' como 'Endereço'
    	DateFirstPurchase AS 'Primeira Compra'  -- Renomeia a coluna 'DateFirstPurchase' como 'Primeira Compra'
    FROM
    	DimCustomer  -- Tabela a ser utilizada
    WHERE
    	DATENAME(YEAR, DateFirstPurchase) = '2001' -- Filtra para que exiba apenas os valores da coluna 'DateFirstPurchase'com o ano de 2001

5. A tabela DimEmployee possui uma informação de data de contratação (HireDate). A área de
RH, no entanto, precisa das informações dessas datas de forma separada em dia, mês e ano, pois
será feita uma automatização para criação de um relatório de RH, e facilitaria muito se essas
informações estivessem separadas em uma tabela.

Você deverá realizar uma consulta à tabela DimEmployee e retornar uma tabela contendo as
seguintes informações: FirstName, EmailAddress, HireDate, além das colunas de Dia, Mês e Ano
de contratação.

**Obs1: A coluna de Mês deve conter o nome do mês por extenso, e não o número do mês.
Obs2: Lembre-se de nomear cada uma dessas colunas em sua consulta para garantir que o
entendimento de cada informação ficará 100% claro.**

    SELECT
    	FirstName AS 'Nome',  -- Renomeia a coluna 'FirstName' para 'Nome'
    	EmailAddress AS 'E-mail',  -- Renomeia a coluna 'EmailAddress' para 'E-mail'
    	HireDate AS 'Data Contratação',  -- Renomeia a coluna 'HireDate' para 'Data Contratação'
    	DAY(HireDate) AS 'Dia da Contratação',  -- Renomeia o dia da coluna 'HireDate' para 'Dia da Contratação'
    	DATENAME(MONTH, HireDate) AS 'Mês da Contratação',  -- Renomeia o mês por extenso da coluna 'HireDate' para 'Mês da Contratação' 
    	YEAR(HireDate) AS 'Ano da Contratação'  -- Renomeia o ano da coluna 'HireDate' para 'Ano da Contratação'
    FROM
    	DimEmployee  -- Tabela a ser utilizada

6. Descubra qual é a loja que possui o maior tempo de atividade (em dias). Você deverá fazer essa
consulta na tabela DimStore, e considerar a coluna OpenDate como referência para esse cálculo.

        SELECT
        	StoreName AS 'Loja',  -- Renomeia a coluna 'StoreName' para 'Loja'			
        	OpenDate AS 'Abertura',  -- Renomeia a coluna'OpenDate' para 'Abertura'
        	DATEDIFF(DAY, OpenDate, GETDATE()) AS 'Dias em Funcionamento'  -- Renomeou a diferença de dias da inauguração até o momento
        FROM
        	DimStore  -- Tabela a ser utilizada
        WHERE
        	CloseDate IS NULL  -- Filtra para exibir resultaos apenas para as lihas em branco da coluna 'CloseDate'
        ORDER BY DATEDIFF(DAY, OpenDate, GETDATE()) DESC  -- Oredena em ordem decrescente a diferença de dias da inauguração até o momento.


