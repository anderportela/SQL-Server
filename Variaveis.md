## Tipos de Dados

- O tipo de dado é a maneira como o SQL consegue diferenciar cada valor dentro de um banco de dados.

### Inteiro:

- Exemplos: 1, 100, 568...

- Como o SQL entende um número inteiro: INT

### Decimal:

- Exemplos: 10.33, 90.91, 3.14

- Como o SQL entende um número decimal: FLOAT, DECIMAL (N, M).
    - N é o número de dígitos que o número pode ter, incluindo as casas decimais.
    - M é o número máximo de casas decimais.

### Texto/String:

- Exemplos: 'Carla', 'Motorola', '44', 'Pastel'

- Como o SQL entende um texto: VARCHAR (N)
    - N é o número de caracteres que o texto pode ter.

 ### Data:

- Exemplos: '01/01/2021', '23/03/2026'

- Como o SQL entende uma data: DATETIME

## Operações Básicas

### Operações com números

- Exemplos:

      SELECT 10+20  -- Retorna 30
      SELECT 20-5  -- Retorna 15
      SELECT 40*30  -- Retorna 1200
      SELECT 50/4  -- Retorna 12
- Se colocar um ponto decimal na conta, o SQL ´força' o resultado para decimal também:
    
      SELECT 50.0/4  -- Retorna 12.5

### Operações com textos

- Exemplos:

      SELECT 'Nome' + 'Sobrenome'  -- Retorna 'NomeSobrenome'
      SELECT 'Nome' + ' ' + 'Sobrenome'  -- Retorna 'Nome Sobrenome'

## Função SQL_VARIANT_PROPERTY

- Para descobrir o tipo de dado de um valor, utiliza-se a função SQL_VARIANT_PROPERTY

- Exemplo:

      SELECT SQL_VARIANT_PROPERTY ("Valor", 'BaseType')

## Função CAST

- Para declarar o tipo de dados de uma variável, utiliza-se a função CAST.
    - Alguns tipos mais comuns: INT (Inteiro), FLOAT (Decimal), VARCHAR (Texto), DATETIME (Data)

- Exemplo:

      SELECT CAST ('02/04/2026' AS DATETIME) -- Declara o valor '02/04/2026' como Data

- Sempre que for declarar um valor como 'VARCHAR', tem que definir o número máximo de caracteres.

- Exemplo:

      SELECT CAST ('24 Horas' AS VARCHAR(N)) -- N é o número máximo de caracteres

## Função FORMAT

- Estrutura:

      SELECT FORMAT ('valor', formato)

- Exemplos:

      SELECT FORMAT (1000, N)  -- Retorna 1,000.00
- Onde N é Número (Number)

      SELECT FORMAT (1000, G)  -- Retorna 1000
- Onde G é Geral (General)

### Formatações personalizadas

- Exemplo:

      SELECT FORMAT (123456789, '###-##-####')  -- Retorna 123-45-6789

### Formatações de datas

- Exemplos:

      SELECT FORMAT (CAST('07/04/2026' AS DATETIME), 'dd/MMM/yyyy')  -- Retorna 07/Abr/2026

      SELECT FORMAT (CAST('07/04/2026'AS DATETIME), 'dddd')  -- Retorna Terça-feira

- Por padrão, o retorno da função FORMAT é sempre um 'VARCHAR' (Texto)
 
## ROUND, FLOOR e CEILING - Funções de arredondamento

### ROUND (Arredondamento matemático)

    SELECT ROUND ('valor', número de casas decimais)

### ROUND (Diminuir casas decimais)

    SELECT ROUND ('valor', número de casas decimais, 1)
  - Onde está o '1', pode ser qualquer valor diferente de '0'

### FLOOR (Arredondamento para baixo)

- Exemplo:

      SELECT FLOOR (18.74) -- Retorna 18

### CEILING (Areedondamento para cima)

- Exemplo:

      SELECT CEILING (18.74) -- Retorna 19

## DECLARE e SET - Declarando variáveis

- Uma variável é um objeto que armazena o valor de um dado.

- Estrutura:

      DECLARE @var 'tipo'
      SET @var = 'valor'
      SELECT @var

- Exemplo:

      DECLARE @var INT
      SET @var = 50
      SELECT @var -- Retorna 50



