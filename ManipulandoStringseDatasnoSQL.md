# Manipulando Strings e Datas no SQL

## LEN e DATALENGHT

- Retornam a quantidade de caracteres de uma palavra.   
Exemplo:
- Descubra a quantidade de caracteres da palavra 'SQL Hashtag'

      SELECT (LEN) ('SQL Hashtag')
- Irá aparecer a quantidade de caracteres (11)
  - O espaço também é considerado um caracter
  - Se houver espaço adicional depois da última letra, somente o comando 'DATALENGHT' irá reconhecer esse espaço como caracter.
 
## CONCAT

- Permite juntar mais de um texto em uma única palavra   
Exemplo:

      SELECT CONCAT ('Nome', ' ', 'Sobrenome')
- Irá retornar: ('Nome Sobrenome')

## LEFT e RIGHT

- LEFT: Extrai uma determinada quantidade de caracteres de um texto, da esquerda para a direita
- RIGHT: Extrai uma determinada quantidade de caracters de um texto, da direita para a esquerda   
Exemplo:

      SELECT LEFT ('Product126', 7)
- Sendo '7' a quantidade de caracteres
- Irá retornar: 'Product'

      SELECT RIGHT ('Alo123', 3)
  - Irá retornar: '123'
 
## REPLACE

- Substitui um determinado texto por outro texto
Exemplo 1:
- No texto 'Excel é melhor' substitua a palavra 'Excel' pela palavra 'SQL'

      SELECT REPLACE ('Excel é melhor', 'Excel', 'SQL')

Exemplo 2:
- Crie uma consulta a partir de DimCustomer onde você retorna o nome completo dos clientes, a coluna de gênero (abreviado) e uma coluna substituindo 'M' por 'Masculino' e 'F' por 'Feminino'

      SELECT * FROM DimCustomer
      SELECT
            FirstName AS 'Nome',
            LastName AS 'Sobrenome',
            Gender AS 'Gênero (Abrev)'
      REPLACE (REPLACE(Gender, 'M', 'Masculino'), 'F', 'Feminino' AS Gênero)

## TRANSLATE e STUFF

- TRANSLATE: Substitui cada caractere na ordem encontrada no texto

      SELECT TRANSLATE ('Argumento1', 'Argumento2', 'Argumento3')
  - Argumento 1: Texto
  - Argumento 2: Caracteres que deverão ser substituídos
  - Argumento 3: Caractreres novos (mesma sequência dos caracteres antigos)

- STUFF: Substitui qualquer texto com uma quantidade de caracteres limitados por um outro texto

      SELECT STUFF ('Argumento1', 'Argumento2', 'Argumento3', 'Argumento4')
  - Argumento 1: Texto
  - Argumento 2: Posição do primeiro caractere a ser substituído
  - Argumento 3: Quantidade de caracteres a serem substituídos
  - Argumento 4: Novo texto

## UPER e LOWER

- UPPER: Transforma um texto em maiúscula
- LOWER: Transforma um texto em minúscula

## FORMAT

- Formata um valor de acordo com uma formatação

      SELECT FORMAT ('Argumento1', 'Argumento2')
  - Argumento 1: Valor a ser formatado
  - Argumento 2: Tipo de formato
 
  - Tipos comuns de formatos
    - G: Geral (General)
    - N: Número (Number)
    - C: Moeda (Currency)

- É possível criar um terceiro 'argumento' para indicar o idioma da formatação.
Exemplo:

      SELECT FORMAT (CAST('20/05/2019' AS DATETIME) 'dd/MMMM/yy', 'en-US')
  - en-US: Inglês (EUA)
  - O comando irá retornar: 20/MAY/19

### Formatação personalizada

- Exemplo:

      SELECT FORMAT (123456, '## - ## - ##')
  - O comando irá retornar: '12 - 34 - 56'

## CHARINDEX e SUBSTRING

- CHARINDEX: Descobre a posição de um determinado caractere dentro um texto
- SUBSTRING: Extrai alguns caracteres de dentro de um texto

      SELECT CHARINDEX ('Argumento1', 'Argumento2')
  - Argumento 1: Caractere ou conjunto de caracteres desejado
  - Argumento 2: O texto onde será feita a consulta

          SELECT SUBSTRING ('Argumento1', 'Argumento2', 'Argumento3')
      - Argumento 1: O texto em que será extraído
      - Argumento 2: A posição inicial do texto que será extraído
      - Argumento 3: A quantidade de caracteres a partir do primeiro caractere do texto a ser extraído

- Exemplo:
  - Combine as funções CHARINDEX e SUBSTRING para extrair de forma automática qualquer sobrenome
 
        SELECT SUBSTRING ('Raquel Moreno', CHARINDEX (' ', 'Raquel Moreno') +1, 100)

## TRIM, LTRIM e RTRIM

TRIM: Retira espaços adicionais à esquerda e à direita do texto
LTRIM: Retira espaços adicionais à esquerda do texto
RTRIM: Retira espaços adicionais à direita do texto

- Utilizaremos os comandos no código ' ABC123 '

      DECLARE @varCodigo VARCHAR (50)
      SET @varCodigo = ' ABC123 '
      SELECT

        TRIM (@varCodigo) AS 'Trim'
  - Retorna 'ABC123' na coluna 'Trim'
 
            LTRIM (@varCodigo) AS 'Ltrim'
  - Retorna 'ABC123 ' na coluna 'Ltrim'
 
            RTRIM (@varCodigo) AS 'Rtrim'
  - Retorna ' ABC123' na coluna 'Rtrim'
 
 



  


  




