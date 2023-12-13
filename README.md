  # Consultas PARTE 2 MySQL 🐬

https://github.com/luishenriquebk/mysql_consultas_parte2/assets/102004702/41ff5693-5233-451f-8720-1d222d415136

Este repositório contém atividades realizadas no MySQL para praticar conceitos de consultas entre os registros de uma banco de dados no MySQL.
#### Link do projeto: https://drive.google.com/drive/folders/1M5NkgGeplUOB1f3DA6ErcZmmABnMZ0bd?usp=drive_link


## Atividades Realizadas:

Antes de iniciar as atividades devemos criar o DATABASE ao qual vamos usar nesse projeto introdutório:

```sql
CREATE DATABASE IF NOT EXISTS manipulacao_de_dados; 
USE manipulacao_de_dados; -- USANDO NOVA DATABASE;
```

Agora vamos criar nossas tabelas?

```sql
CREATE TABLE EMPREGADO(
	ID_EMPREGADO INT AUTO_INCREMENT PRIMARY KEY,
    NOME VARCHAR(100) NOT NULL,
    CARGO VARCHAR (45) NOT NULL,
    SALARIO DECIMAL(6, 2) NOT NULL,
    DATA_ADMISSAO DATE,
    CIDADE VARCHAR(45),
    TELEFONE VARCHAR(15)
);  
```
Vamos inserir alguns registros em nossas tabelas?

```
INSERT INTO EMPREGADO (NOME, CARGO, SALARIO, DATA_ADMISSAO, CIDADE, TELEFONE)
VALUES 
('João Silva', 'Analista', 5000.00, '2022-01-15', 'São Paulo', '123-4567'),
('Maria Souza', 'Gerente', 7000.00, '2021-11-20', 'Rio de Janeiro', '987-6543'),
('Pedro Almeida', 'Desenvolvedor', 4000.00, '2022-03-05', 'Belo Horizonte', '111-2222'),
('Ana Oliveira', 'Analista', 5500.00, '2022-02-28', 'Brasília', '333-4444'),
('Luiz Santos', 'Gerente', 7200.00, '2021-09-10', 'Porto Alegre', '555-6666'),
('Mariana Costa', 'Desenvolvedor', 4200.00, '2022-04-18', 'Curitiba', '777-8888'),
('Rafael Lima', 'Analista', 5100.00, '2022-01-02', 'Salvador', '999-0000'),
('Julia Fernandes', 'Gerente', 7500.00, '2021-12-25', 'Fortaleza', '112-1133'),
('Carlos Pereira', 'Desenvolvedor', 4300.00, '2022-05-07', 'Manaus', '114-1155'),
('Fernanda Castro', 'Analista', 5200.00, '2022-03-15', 'Recife', '116-1177');
```
Exibindo os valores das duas TABELAS criadas exibidos:

```
SELECT * FROM CLIENTE;
SELECT * FROM VENDA;

| id_cliente | nome_cliente    | email_cliente         | idade_cliente | genero | cidade_cliente     | id_venda | -- CLIENTE
|------------|-----------------|-----------------------|---------------|--------|--------------------|----------|
| 1          | Lucas Castro    | lccastro@gmail.com    | 25            | M      | Vila Velha         | 1        |
| 2          | Arthur Pacheco  | pacheco@gmail.com     | 24            | M      | Vila Velha         | 2        |
| 3          | Alexia          | alexia@gmail.com      | 23            | F      | Montes Claros      | 3        |
| 4          | Henrique        | henrique@gmail.com    | 25            | M      | Montes Claros      | 4        |
| 5          | Joao            | joao@gmail.com        | 25            | M      | Vitorai            | 5        |

| id_venda | valor_total | forma_pagamento | data_compra | -- VENDA
|----------|-------------|-----------------|-------------|
| 1        | 50.00       | Debito          | 2023-12-07  |
| 2        | 30.00       | PIX             | 2023-12-10  |
| 3        | 45.00       | Debito          | 2023-12-11  |
| 4        | 50.00       | Debito          | 2023-12-12  |
| 5        | 75.00       | Credito         | 2023-12-14  |
```

### 1. UTILIZANDO WHERE PARA FILTRAR COM BASE EM DIFERENTES CONDIÇÕES:

Para realizar a consulta com diferentes condições foi utilizado o seguinte comando e condições:

```sql
SELECT * FROM VENDA
WHERE forma_pagamento = 'Debito' AND valor >= 35;

| id_venda | valor_total | forma_pagamento | data_compra |
|----------|-------------|-----------------|-------------|
| 3        | 45.00       | Debito          | 2023-12-11  |
| 4        | 50.00       | Debito          | 2023-12-12  |

```

### 2. SELECIONANDO DADOS DE MÚLTIPLAS TABELAS USANDO INNER JOIN:

Para selecionar esses registros utilizando foi usado o seguint comando:

```sql
SELECT * FROM CLIENTE
INNER JOIN VENDA ON CLIENTE.id_venda = VENDA.id_venda;

| id_cliente | nome_cliente    | email_cliente         | idade_cliente | genero | cidade_cliente     | id_venda || id_venda | valor_total | forma_pagamento | data_compra | 
|------------|-----------------|-----------------------|---------------|--------|--------------------|----------||----------|-------------|-----------------|-------------|
| 4          | Arthur Pacheco  | pacheco@gmail.com     | 24            | M      | Vila Velha         | 2        || 2        | 30.00       | PIX             | 2023-12-10  |
| 5          | Alexia          | alexia@gmail.com      | 23            | F      | Montes Claros      | 3        || 3        | 45.00       | Debito          | 2023-12-11  |
| 6          | Henrique        | henrique@gmail.com    | 25            | M      | Montes Claros      | 4        || 4        | 50.00       | Debito          | 2023-12-12  |
| 7          | Joao            | joao@gmail.com        | 25            | M      | Vitorai            | 5        || 5        | 75.00       | Credito         | 2023-12-14  |

```

### 3. UTILIZANDO LEFT JOIN PARA RETORNAR TODOS OS REGISTROS DE UMA TABELA, E OS CORRESPONDENTES DA TABELA RELACIONADA:

Para realizar essa conusulta foram realizados os seguintes comandos:


```sql
SELECT * FROM CLIENTE
LEFT JOIN VENDA ON CLIENTE.id_cliente = VENDA.id_cliente;

| id_cliente | nome_cliente    | email_cliente         | idade_cliente | genero | cidade_cliente     | id_venda || id_venda | valor_total | forma_pagamento | data_compra | 
|------------|-----------------|-----------------------|---------------|--------|--------------------|----------||----------|-------------|-----------------|-------------|
| 4          | Arthur Pacheco  | pacheco@gmail.com     | 24            | M      | Vila Velha         | 2        || 2        | 30.00       | PIX             | 2023-12-10  |
| 5          | Alexia          | alexia@gmail.com      | 23            | F      | Montes Claros      | 3        || 3        | 45.00       | Debito          | 2023-12-11  |
| 6          | Henrique        | henrique@gmail.com    | 25            | M      | Montes Claros      | 4        || 4        | 50.00       | Debito          | 2023-12-12  |
| 7          | Joao            | joao@gmail.com        | 25            | M      | Vitorai            | 5        || 5        | 75.00       | Credito         | 2023-12-14  |
```

### 4. UTILIZANDO FUNÇÕES DE AGREGAÇÃO:

Para realizar esse tipo de consulta foi executado o seguinte comando:

```sql
SELECT COUNT(*) AS TOTAL_CLIENTES FROM CLIENTE;
SELECT SUM(VALOR) AS TOTAL_RECEITA FROM VENDA;
SELECT ROUND(AVG(IDADE), 2) AS IDADE_MEDIA FROM CLIENTE;
SELECT MIN(VALOR) AS VALOR_MININO FROM VENDA;
SELECT MAX(VALOR) AS VALOR_MAXIMO FROM VENDA;

| TOTAL_CLIENTES | TOTAL_RECEITA  | IDADE_MEDIA | VALOR_MININO | VALOR_MAXIMO |
|----------------|--------------- |-------------|--------------|--------------|
| 4              | 250.00         | 24.25       | 30.00        | 75.00        |
```
