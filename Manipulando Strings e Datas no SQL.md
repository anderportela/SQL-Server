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
