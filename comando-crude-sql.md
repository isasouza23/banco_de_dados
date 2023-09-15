# Comandos SQL - Para CRUD (Referência)

## Resumo
C -> Create (Insere dados)
R -> Read (Ler dados)
U -> Update (Atualizar dados)
D -> Delete (Deletar dados)

## Insert
## Fabricantes

```sql
    INSERT INTO fabricantes (nome) VALUES('Asus');
    INSERT INTO fabricantes (nome) VALUES('Dell');
    INSERT INTO fabricantes (nome)
    VALUES('Apple'), ('LG'), ('Samsung'), ('Brastemp');
    INSERT INTO fabricantes (nome)
    VALUES('Positivo'), ('Microsoft');
   
```
<!-- _________________________ -->

## Insert
## Produtos

```sql
    INSERT INTO produtos (nome, descricao, preco, quantidade, fabricante_id)
    VALUES('Ultrabook', 'Ultrabook Asus Intel Core i9', 6500.99,7,1 );

    INSERT INTO produtos (nome, descricao, preco, quantidade, fabricante_id)
    VALUES('Geladeira', 'Fost-Free com acesso a internet',8500.99,10,6);

    INSERT INTO produtos (nome, descricao, preco, quantidade, fabricante_id)
    VALUES('Tablet Android', 'Tablet 10 polegadas com 256Gb de armazenamento',4999,3,5);

    INSERT INTO produtos (nome, descricao, preco, quantidade, fabricante_id)
    VALUES('Iphone 15 Pro Max', 'Processador Bionic 15 com 512Gb de armazenamento',9999.97,3,3);

    INSERT INTO produtos (nome, descricao, preco, quantidade, fabricante_id)
    VALUES('Ipad mini', 'Tablet com tela de retina 4k com 512Gb de armazenamento',5000,8,3);

    INSERT INTO produtos (nome, descricao, preco, quantidade, fabricante_id)
    VALUES('Xbox', 'Console de última geração...',2500,6,8);

    INSERT INTO produtos (nome, descricao, preco, quantidade, fabricante_id)
    VALUES('Ultrabook', 'AMD Ryzen 5 16Gb RAM...',4500.97,12,7);
```