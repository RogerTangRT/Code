# Projeto DBA Challenge 20240802
## Candidato:  Roger Tang

## Uma descrição sobre o projeto em frase
Esse projeto modela vendas dos produtos de uma loja 

## Deve conter uma lista com linguagem, framework e/ou tecnologias usadas
Linguagem SQL

## Como instalar e usar o projeto (instruções)
Basta executar as consultas em um visualizador de banco de dados contendo as tabelas populadas  do projeto 
As respostas estão no arquivo Solução.md

## Adicione o link do repositório com a sua solução no teste
https://github.com/RogerTangRT/Code


# Consultas
## 1) Listar todos Clientes que não tenham realizado uma compra;

SELECT *
FROM Customers
WHERE NOT EXISTS (
    SELECT 1
    FROM Orders
    WHERE Customers.customer_id = Orders.customer_id
)


## 2) Listar os Produtos que não tenham sido comprados

SELECT * 
FROM products
WHERE NOT EXISTS (
    SELECT 1
    FROM order_items
    WHERE products.product_id = order_items.product_id
)

## 3) Listar os Produtos sem Estoque;

SELECT *
FROM products
WHERE NOT EXISTS (
    SELECT 1
    FROM stocks
    WHERE products.product_id = stocks.product_id
)

## 4) Agrupar a quantidade de vendas que uma determinada Marca por Loja. 

SELECT COUNT(*) AS quantidade_de_vendas
FROM orders
INNER JOIN stores ON (orders.store_id = stores.store_id)
INNER JOIN order_items ON (orders.order_id = order_items.order_id)
INNER JOIN products ON (order_items.product_id = products.product_id)
INNER JOIN brand ON (products.brand_id = brand.brand_id)
WHERE brand.brand_name = 'Marca 1'
GROUP BY stores.store_id

## 5) Listar os Funcionarios que não estejam relacionados a um Pedido.

SELECT *
FROM staff
WHERE NOT EXISTS (
    SELECT 1
    FROM orders
    WHERE staff.staff_id = orders.staff_id
)
