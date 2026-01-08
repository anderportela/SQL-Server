# JOINs no SQL

## Porque precisamos do JOIN?  
- Com o JOIN, podemos relacionar tabelas diferentes por meio de uma coluna em comum.

## Chave Primária vs Chave Estrangeira  
- Uma **chave primária** é uma coluna que identifica as informações distintas de uma tabela. Geralmente é uma coluna de ID.
- Uma **chave estrangeira** é uma coluna que permite relacionar as linhas de uma segunda tabela com a chave primária de uma primeira tabela.

## Tabela Fato vs Tabela Dimensão  
- Uma **tabela dimensão** é uma tabela que contpem características de um determinado elemento: lojas, produtos, funcionários, clientes, etc...
  - Nessa tabela, nenhum dos elementos principais irá se repetir. É onde vamos encontrar nossas **chaves primárias**.  
- Uma **tabela fato** é uma tabela que vai registrar os fatos ou acontecimentos de uma empresa/negócio em determinados períodos de tempo (venda, devoluções, aberturas de chamados, receitas, despesas, etc..)
  - Geralmente é uma tabela com milhares de informações e composta essencialmente por colunas de ID usadas para buscar as informações complementares de uma tabela dimensão, conhecidas como **chaves estrangeiras**.
- Geralmente, tabelas com começo *Dim* são **tabelas dimensão** e tabelas com começo *Fact* são **tabelas fato**.
- Não necessariamente uma relação acontece entre uma **tabela fato** e uma **tabela dimensão**.
- Duas tabela dimensão também podem se relacionar.
- O que não ocorre é uma relação entre duas tabelas fato.

## Tipos de JOIN
- LEFT (OUTER) JOIN
  - Todos os itens da Tabela A + Interseção com a Tabela B.

- RIGHT (OUTER) JOIN
  - Todos os itens da Tabela B + Interseção com a Tabela A.
 
- INNER JOIN
  - Apenas a interseção entre as Tabelas A e B.

- FULL (OUTER) JOIN
  - Todas as linhas da Tabela A + Todas as linhas da Tabela B + Interseção entre as duas tabelas.
 
- LEFT (ANTI) JOIN
  - Apenas as linhas da Tabela A exclusivamente.
 
- RIGHT (ANTI) JOIN
  - Apenas as linhas da Tabela B exclusivamente.
 
- FULL (ANTI) JOIN  
  - As linhas que estão somente na Tabela A + As linhas que estão somente na Tabela B.
 
- Exemplo de código com o comando INNER JOIN:

      SELECT
        Tabela_A.coluna1,
        Tabela_A.coluna2,
        Tabela_A.coluna3,
        Tabela_B.coluna4
      FROM
        Tabela_A -- Tabela principal
      INNER JOIN Tabela_B
        ON Tabela_A.chave_estrangeira = Tabela_B.chave_primária  

- Exemplo de código com o comando LEFT (ANTI) JOIN:

      SELECT
        Tabela_A.coluna1,
        Tabela_A.coluna2,
        Tabela_A.coluna3,
        Tabela_B.coluna4
      FROM
        Tabela_A
      LEFT JOIN Tabela_B
        ON Tabela_A.chave_estrangeira = Tabela_B.chave_primária
      WHERE
        Tabela_B.coluna4 IS NULL  

## CROSS JOIN  
- É utilizado para combinar colunas de tabelas diferentes.

Exemplo:

    SELECT
      coluna da Tabela A,
      coluna da Tabela B
    FROM
      Tabela A CROSS JOIN Tabela B  

## Múltiplos JOINs  
- Quando é necessário relacionar itens da Tabela A com a Tabela C, mas a Tabela C só tem correspondência com a Tabela B, podemos utilizar múltiplos JOINs.

Exemplo:  

    SELECT
      coluna da Tabela A,
      coluna da Tabela B,
      coluna da Tabela C
    FROM
      Tabela A
    INNER JOIN Tabela B
      ON Tabela_A.chave_estrangeira = Tabela_B.chave_primária
    INNER JOIN Tabela C
      ON Tabela_B.chave_estrangeira = Tabela_C.chave_primária  

## UNION e UNION ALL  
- O comando **UNION** permite juntar tabelas que contém a **mesma estrutura de linhas**.

Exemplo:  

    SELECT
      *
    FROM
      Tabela_A
    UNION
    SELECT
      *
    FROM
      Tabela_B  

 - O comando **UNION** exclui as linhas duplicadas.
 - O comando **UNION ALL** exibe todas as linhas, inclusive as duplicadas.   


  

  
