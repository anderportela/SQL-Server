*1. Declare 4 variáveis inteiras. Atribua os seguintes valores a elas:*

*valor 1 = 10   
valor 2 = 5   
valor 3 = 34   
valor 4 = 7*   

*a) Crie uma nova variável para armazenar o resultado da soma entre valor1 e valor2. Chame
essa variável de soma.*

    DECLARE @valor1 INT = 10, @valor2 INT = 5 -- Declara as variáveis 'valor1' e 'valor2' como INT (inteiro)
    DECLARE @soma INT = @valor1 + @valor2 -- Declara a variávael 'soma' como INT (inteiro)
    SELECT @soma -- Exibe o valor da variável 'soma'

*b) Crie uma nova variável para armazenar o resultado da subtração entre valor3 e valor 4.
Chame essa variável de subtracao*

    DECLARE @valor3 INT = 34, @valor4 INT = 7 -- Declara as variáveis 'valor3' e 'valor4' como INT (inteiro)
    DECLARE @subtracao INT = @valor3 - @valor4 -- Declara a variável 'subtracao' como INT (inteiro)
    SELECT @subtracao -- Exibe o valor da variável 'subtracao'

*c) Crie uma nova variável para armazenar o resultado da multiplicação entre o valor 1 e o
valor4. Chame essa variável de multiplicacao.*

    DECLARE @valor1 INT = 10, @valor4 INT = 7 -- Declara as variáveis 'valor1' e 'valor4' como INT (inteiro)
    DECLARE @multiplicacao INT = @valor1 * @valor4 -- Declara a variável 'multiplicacao' como INT (inteiro)
    SELECT @multiplicacao -- Exibe o valor da variável 'multiplicacao'

*d) Crie uma nova variável para armazenar o resultado da divisão do valor3 pelo valor4. Chame
essa variável de divisao. Obs: O resultado deverá estar em decimal, e não em inteiro*

    DECLARE @valor3 FLOAT = 34, @valor4 FLOAT = 7 -- Declara as variáveis 'valor3' e 'valor4' como FLOAT (decimal)
    DECLARE @divisao FLOAT = @valor3 / @valor4 -- Declara a variável 'divisao' como FLOAT (decimal)
    SELECT @divisao -- Exibe o valor da variável 'divisao'

*e) Arredonde o resultado da letra d) para 2 casas decimais.*

    DECLARE @valor3 FLOAT = 34, @valor4 FLOAT = 7 -- Declara as variáveis 'valor3' e 'valor4' como FLOAT (decimal)
    DECLARE @divisao FLOAT = @valor3 / @valor4 -- Declara a variável 'divisao' como FLOAT (decimal)
    SELECT ROUND (@divisao, 2) -- Exibe o valor da variável 'divisao' arredondado em 2 casas decimais

*2. Para cada declaração das variáveis abaixo, atenção em relação ao tipo de dado que deverá ser
especificado.
a) Declare uma variável chamada ‘produto’ e atribua o valor de ‘Celular’.
b) Declare uma variável chamada ‘quantidade’ e atribua o valor de 12.
c) Declare uma variável chamada ‘preco’ e atribua o valor 9.99.
d) Declare uma variável chamada ‘faturamento’ e atribua o resultado da multiplicação entre
‘quantidade’ e ‘preco’.
e) Visualize o resultado dessas 4 variáveis em uma única consulta, por meio do SELECT.*

    DECLARE @produto VARCHAR(20) = 'Celular', -- Declara a variável 'produto' como VARCHAR (texto)
            @quantidade INT = 12, -- Declara a variável 'quantidade' como INT (inteiro)
            @preco FLOAT = 9.99 -- Declara a variável 'preco' como FLOAT (decimal)
    DECLARE @faturamento FLOAT = (@quantidade * @preco) -- Declara a variável 'faturamento' como FLOAT (decimal)'
    SELECT @produto, @quantidade, @preco, @faturamento -- Exibe os valores das variáveis 'produto', 'quantidade', 'preco' e 'faturamento'


*3. Você é responsável por gerenciar um banco de dados onde são recebidos dados externos de
usuários. Em resumo, esses dados são:*
*- Nome do usuário*
*- Data de nascimento*
*- Quantidade de pets que aquele usuário possui*
*Você precisará criar um código em SQL capaz de juntar as informações fornecidas por este
usuário. Para simular estes dados, crie 3 variáveis, chamadas: nome, data_nascimento e
num_pets. Você deverá armazenar os valores ‘André’, ‘10/02/1998’ e 2, respectivamente.*

    DECLARE @nome VARCHAR(50) = 'André',  -- Declara a variável 'nome' como VARCHAR (texto)
            @data_nascimento DATETIME = '10/02/1998',  -- Declara a variável 'data_nascimento' como DATETIME (data)
            @num_pets INT = 2  -- Declara a variável 'num_pets' como INT (inteiro)
    SELECT 'Meu nome é ' + @nome + ', nasci em ' + FORMAT(CAST(@data_nascimento as datetime), 'dd/MM/yyyy') + ' e tenho ' + FORMAT(CAST(@num_pets AS INT), '#') + ' pets.'  -- Exibe e soma os valores das variáveis mencionadas 


*4. Você acabou de ser promovido e o seu papel será realizar um controle de qualidade sobre as
lojas da empresa.*

*A primeira informação que é passada a você é que o ano de 2008 foi bem complicado para a
empresa, pois foi quando duas das principais lojas fecharam. O seu primeiro desafio é descobrir
o nome dessas lojas que fecharam no ano de 2008, para que você possa entender o motivo e
mapear planos de ação para evitar que outras lojas importantes tomem o mesmo caminho.*

*O seu resultado deverá estar estruturado em uma frase, com a seguinte estrutura:
‘As lojas fechadas no ano de 2008 foram: ’ + nome_das_lojas*


    SET NOCOUNT ON  -- Desativa a contagem de linhas na tela de 'Print'
    DECLARE @lojas_off AS VARCHAR(100)  -- Declara a variável 'lojas_off' como VARCHAR (texto)
    SET @lojas_off = '' -- Configura a variável 'lojas_off' como espaço em branco
    
    SELECT 
        @lojas_off = @lojas_off + StoreName + ', ' -- Exibe os valores adicionados na variável 'lojas_off' separados por vírgula
    FROM
        DimStore -- Tacela principal
    WHERE FORMAT(CloseDate, 'yyyy') = 2008 -- Filtra os valores da coluna 'CloseDate' que contenham o ano de 2008
    PRINT 'As lojas fechadas em 2008 foram: ' + @lojas_off  -- Exibe a soma do texto e do valor da variável 'lojas_off'


*5. Você precisa criar uma consulta para mostrar a lista de produtos da tabela DimProduct para
uma subcategoria específica: ‘Lamps’.
Utilize o conceito de variáveis para chegar neste resultado.*

    DECLARE @idsubcategoria AS INT,  -- Declara a variável 'idsubcategoria' como INT (inteiro)
            @nomesubcateoria AS VARCHAR(50)  -- declara a variável 'nomesubcategoria' como VARCHAR (texto)
    
    SET @nomesubcateoria = 'Lamps'  -- Configura a variável 'nomesubcategoria' para 'Lamps'
    SET @idsubcategoria = (SELECT ProductSubcategoryKey FROM DimProductSubcategory WHERE ProductSubcategoryName = @nomesubcateoria)
    -- Configura a variável 'idsubcategoria' para valores da linha 'ProductSubcategoryName' que condizam com o valor da variável 'idsubcategoria'
    SELECT 
        *
    FROM
        DimProduct  -- Seleciona toda a tabela 'DimProduct'
    WHERE
        ProductSubcategoryKey = @idsubcategoria  -- Filtra os valores da linha 'ProductSubcategoryKey' para o valor da variável 'idsubcategoria' 
