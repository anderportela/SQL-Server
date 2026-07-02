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


