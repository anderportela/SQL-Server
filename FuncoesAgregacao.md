# Funções de Agregação

## Função SUM

- Realiza a soma dos valores das colunas selecionadas
    
    Exemplo:
    
      SELECT
        SUM (‘COLUNA’)
      FROM
        ‘TABELA’
    
- Se quiser renomear a coluna gerada na função SUM, basta adicionar o comando AS após o nome da colunae renomear com aspas simples
- É possível utilizar mais de uma função SUM no memso código

## Função COUNT

- Realiza a contagem dos valores de uma coluna

Exemplo:

    SELECT
      COUNT (‘COLUNA’)
    FROM
      ‘TABELA’

*Obs: O comando COUNT ( * ) realiza a contagem da tabela inteira*

- As aplicações da função COUNT seguem regras parecidas com as da função SUM
- A função não contabilizam valores vazios (’Null’)
- Para contabilizar valores distintos, utilizamos COUNT DISTINCT

Exemplo:

    SELECT
      COUNT (DISTINCT ’COLUNA’)
    FROM
      ‘TABELA’

## Funções MIN e MAX

- Para retornar o maior valor de uma coluna, utilizamos a função MAX
- Para reternar o menor valor de uma coluna, utilizamos a função MIN

Exemplo:

    SELECT
      MAX (’COLUNA’)
    FROM
      ‘TABELA’

## Função AVG

- A função AVG retorna o valor médio de uma coluna

Exemplo:

    SELECT
      AVG (’COLUNA’)
    FROM
      TABELA
