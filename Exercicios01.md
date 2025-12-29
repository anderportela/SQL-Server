EXERCÍCIOS:

1a) Existem 2.517 produtos cadastrados na base e, se não tiver, você deverá reportar ao seu
gestor para saber se existe alguma defasagem no controle dos produtos.

    select
    	*
    from
    	DimProduct

**Sim, existem 2517 produtos.**

1b) Até o mês passado, a empresa tinha um total de 19.500 clientes na base de controle.
Verifique se esse número aumentou ou reduziu.

    select
    	*
    from
    	DimCustomer

**O número de clientes diminuiu, atualmente a empresa tem 18869 clientes.**

2a) Selecione as colunas: CustomerKey, FirstName, EmailAddress, BirthDate da tabela
dimCustomer.

    select 
    	CustomerKey,
    	FirstName,
    	EmailAddress,
    	BirthDate
    from
    	DimCustomer

2b) Renomeie as colunas dessa tabela usando o alias (comando AS).

    select
    	CustomerKey as 'Chave',
    	FirstName as 'PrimeiroNome',
    	EmailAddress as 'Email',
    	BirthDate as 'Aniversário'
    from
    	DimCustomer

3a) A Contoso decidiu presentear os primeiros 100 clientes da história com um vale compras
de R$ 10.000. Utilize um comando em SQL para retornar uma tabela com os primeiros
100 primeiros clientes da tabela dimCustomer (selecione todas as colunas).

    select top(100)
    	*
    from
    	DimCustomer

3b) A Contoso decidiu presentear os primeiros 20% de clientes da história com um vale
compras de R$ 2.000. Utilize um comando em SQL para retornar 10% das linhas da sua
tabela dimCustomer (selecione todas as colunas).

    select top(20) percent
    	*
    from
    	DimCustomer

3c) Adapte o código do item a) para retornar apenas as 100 primeiras linhas, mas apenas as
colunas FirstName, EmailAddress, BirthDate.

    select top(100)
    	FirstName,
    	EmailAddress,
    	BirthDate
    from
    	DimCustomer

3d) Renomeie as colunas anteriores para nomes em português.

    select top(100)
    	FirstName as 'PrimeiroNome',
    	EmailAddress as 'Email',
    	BirthDate as 'Aniversário'
    from
    	DimCustomer

 4 - A empresa Contoso precisa fazer contato com os fornecedores de produtos para repor o
estoque. Você é da área de compras e precisa descobrir quem são esses fornecedores.
Utilize um comando em SQL para retornar apenas os nomes dos fornecedores na tabela
dimProduct e renomeie essa nova coluna da tabela.

    select
    	Manufacturer as 'Fornecedores'
    from
    	DimProduct

5 - O seu trabalho de investigação não para. Você precisa descobrir se existe algum produto
registrado na base de produtos que ainda não tenha sido vendido. Tente chegar nessa
informação.
Obs: caso tenha algum produto que ainda não tenha sido vendido, você não precisa descobrir
qual é, é suficiente saber se teve ou não algum produto que ainda não foi vendido.

    select distinct
    	ProductKey
    from
    	FactSales

**Com o código acima, decobrimos que foram vendidos 2516 produtos, mas no banco de dados temos 2517 produtos. Ou seja, 1 produto ainda não foi vendido.**
