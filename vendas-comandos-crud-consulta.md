# Comandos SQL para CRUD - Referência

## Resumo
C -> Create (insere dados)
R -> Read (ler dados)
U -> Update (atualizar dados)
D -> Delete (excluir dados)

<!-- ___________________________________________________________ -->
## Resumo (SELECT)
### Ler dados da tabela produtos
```sql
SELECT * FROM produtos;
SELECT nome, preco FROM produtos;
SELECT nome FROM produtos WHERE preco < 5000;
SELECT nome, descricao FROM produtos WHERE fabricante_id = 3; #Apple
```
### Operadores lógicos: E OU NÂO

```sql
SELECT * FROM produtos WHERE preco >=5000 AND preco < 8000;

-- Consulta nome, preco de produtos da Apple ou Microsoft
SELECT nome, preco FROM produtos WHERE fabricante_id = 3 OR fabricante_id = 8;
-- Outra maneira usando função IN(Lista)
SELECT nome, preco FROM produtos WHERE fabricante_id IN(3, 8);


-- Monte uma consulta que traga nome, preco, e quantidade
-- de todos os produtos exceto os do fabricante apple
SELECT nome, preco, quantidade FROM produtos WHERE NOT fabricante_id = 3 ; # versão 1 usando NOT

SELECT nome, preco, quantidade FROM produtos WHERE fabricante_id != 3 ; # versão 2 usando operador != (diferente)
```
<!-- ___________________________________________________________ -->
### Filtros
```sql
-- Filtro que ordena pelo nome (AZ) Crescente
SELECT nome, preco  FROM produtos ORDER BY nome;

-- Filtro que ordena pelo nome (ZA) Decrescente
SELECT nome, preco  FROM produtos ORDER BY nome DESC;

-- Like + operador coringa % (significa qualquer texto)
SELECT nome, descricao  FROM produtos WHERE descricao LIKE '%processador%';
```

<!-- ___________________________________________________________ -->
### Operações e funções de agregação
```sql
-- Traz o resultado da soma de todos os preços
SELECT SUM(preco) from produtos;

-- Traz o resultado da soma de todos os preços com ALIAS (Apelido)
SELECT SUM(preco) AS TOTAL from produtos;

-- Traz o resultado da soma da quantidade
SELECT SUM(quantidade) AS "Quantidade em estoque" from produtos;

-- Traz o resultado da soma da quantidade da Apple
SELECT SUM(quantidade) AS "Quantidade em estoque" from produtos WHERE fabricante_id = 3;

-- Average Média dos preços
SELECT AVG(preco) AS "Média dos preços" from produtos;

-- Average Média dos preços (Com 2 casas de precisão)
SELECT ROUND(AVG(preco), 2) AS "Média dos preços" from produtos;

-- Contagem de produtos
SELECT COUNT(id) AS "Quantidade de produtos" from produtos;

-- Contagem de fabricantes evitando a duplicidade em campos que não são chave-primária (Distinct)
SELECT COUNT(DISTINCT fabricante_id) AS "Quantidade de fabricantes" from produtos;

-- Traz o Total (preco unitário * quantidade total)
SELECT nome, preco, quantidade, (preco * quantidade) AS "Total"  from produtos;

```
<!-- ___________________________________________________________ -->
### Agrupamentos
```sql
-- Retorna os preços de cada fabricante (Agrupados)
SELECT fabricante_id, SUM(preco) AS TOTAL from produtos GROUP BY fabricante_id;

```

<!-- ___________________________________________________________ -->
### UPDATE (sempre com Where) OBS: Comando perigoso

### Atualizar dados de uma tabela
```sql
UPDATE fabricantes SET nome = 'Microsoft Brasil' WHERE id = 8;

-- Mudar o preço do Ultrabook da positivo para 5200
UPDATE produtos SET preco = 5200 WHERE id = 7;

-- Mudar a quantidade dos produtos da Asus e da Apple para 15
UPDATE produtos SET quantidade = 15 WHERE fabricante_id = 1 OR fabricante_id = 3;

```
<!-- ___________________________________________________________ -->
### Excluir dados de uma tabela
```sql
-- Exclui o fabricante LG
DELETE FROM fabricantes WHERE id = 4; --LG

-- Deleta os produtos que tem o preco <= 2000 e preco > 500
DELETE FROM produtos WHERE preco <= 2000 AND preco > 500;

```
<!-- ___________________________________________________________ -->
### Consulta em duas ou mais tabelas (Junção)
```sql
-- Consultar campos de diferentes tabelas (Produtos x Fabricantes)
SELECT produtos.nome, fabricantes.nome FROM produtos INNER JOIN fabricantes ON produtos.fabricante_id = fabricantes.id;

-- (Produtos x Fabricantes) melhorada exibindo (TÍTULO)
SELECT produtos.nome AS Produto, fabricantes.nome AS Fabricante FROM produtos INNER JOIN fabricantes ON produtos.fabricante_id = fabricantes.id;

-- (Produtos x Fabricantes) melhorada exibindo (TÍTULO) e classificada por (PRODUTOS) A-Z e depois por (FABRICANTES) A-Z
SELECT produtos.nome AS Produto, fabricantes.nome AS Fabricante FROM produtos INNER JOIN fabricantes ON produtos.fabricante_id = fabricantes.id ORDER BY produtos.nome, fabricantes.nome;

-- Fabricante, soma dos preços e quantidade de produtos
SELECT fabricantes.nome AS Fabricante, SUM(produtos.preco) AS Total, COUNT(produtos.fabricante_id) AS "QTD de produtos" FROM produtos INNER JOIN fabricantes ON produtos.fabricante_id = fabricantes.id GROUP BY Fabricante ORDER BY Total;

-- Trazer a quantidade de produtos de cada fabricante (Somente dos fabricantes que tem produtos cadastrados) usando "INNER JOIN"
SELECT fabricantes.nome AS Fabricante, COUNT(produtos.id) AS "QTD de produtos" FROM produtos INNER JOIN fabricantes ON produtos.fabricante_id = fabricantes.id GROUP BY Fabricante;

-- Trazer a quantidade de produtos de cada fabricante (Mesmo dos fabricantes que não tem produtos) usando "RIGHT JOIN"
SELECT fabricantes.nome AS Fabricante, COUNT(produtos.id) AS "QTD de produtos" FROM produtos RIGHT JOIN fabricantes ON produtos.fabricante_id = fabricantes.id GROUP BY Fabricante;

```