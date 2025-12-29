# Introdução ao SQL
- Para criar uma janela em branco no SSMS, clique com o botão direito do mouse no banco de dados e na opção ‘*Nova Consulta*’. Ou o atalho *CTRL+N*
- Para selecionar todas as colunas de uma determinada tabela, digite:
    
    
        SELECT
        
           *
        
        FROM
        
            ‘Nome da Tabela’
    
- Para selecionar colunas específicas de uma tabela, digite:
    
    
        SELECT
        
            ‘Nome da(s) Coluna(s)’
        
        FROM
        
            ‘Nome da Tabela'
    

- Para executar apenas uma linha de códigos, tem que selecionar a linha antes de dar o comando de ‘*Executar*’, caso contrário, todas as linhas de código serão executadas.
- Para adicionar comentários na consulta, insira ‘- -’ no início de cada linha de comentário. Também pode-se utilizar ‘/*’ no começo do comentário e ‘*/’ no final do comentário.
- Para selecionar as primeiras linhas de uma tabela, utiliza-se o comando **SELECT TOP( )**.
    - Exemplo: Para retornar as 300 primeiras linhas  de uma tabela:
        
            SELECT TOP(300)
            
                * 
            
            FROM
            
                ‘Nome da Tabela’
        
- Também pode-se utilizar para retornar uma porcentagem das linhas da tabela.
    - Exemplo: Retornar as primeiras 15% das linhas da tabela:
    
            SELECT TOP(15) PERCENT
            
                *
            
            FROM
            
                ‘Nome da Tabela’
        

- Para retornar apenas valores distintos de uma coluna, utiliza-se o comando **DISTINCT**

        SELECT DISTINCT
  
            ‘Nome da Coluna’
        
        FROM
        
            ‘Nome da Tabela’

- Para renomear colunas, utiliza-se o comando **AS**.
    - Exemplo: Renomear a coluna ‘ProductName’ da tabela ‘dimProduct’ para ‘Produto’:
        
            SELECT
            
                ProductName AS ‘Produto’
            
            FROM
            
                dimProduct
