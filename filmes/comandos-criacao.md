# Comandos SQL - Referência
<!-- ________________________________ -->

## Modelagem física

### Criar banco de dados

```sql

CREATE DATABASE filmes CHARACTER SET utf8mb4;




<!-- _________________________ -->

### Criar a tabela de genêros

```sql
CREATE TABLE generos(
    id INT NOT  NULL PRIMARY KEY AUTO_INCREMENT,
    genero VARCHAR(45) NOT NULL
)

<!-- __________________________ -->

### Criar a tabela de filmes

```sql
CREATE TABLE filmes(
    id INT NOT  NULL PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(45) NOT NULL
    lancamento YEAR(4) NOT NULL
    genero_id INT NOT NULL
)



<!-- _________________________ -->

### Adicionar linha tabela de filmes

```sql
ALTER TABLE filmes ADD genero_id INT NOT NULL
AFTER lancamento;  


<!-- __________________________ -->

### Criação da chave estrangeira (relacionamento entre tabelas)

```sql
ALTER TABLE filmes
    # CONSTRAINT é uma restrição definida no relacionamento
    ADD CONSTRAINT fk_filmes_generos

    # A chave estrangeira deve fazer referência a chave primária 
    FOREIGN KEY(genero_id) REFERENCES generos(id)

# Inserir genêros

```sql
INSERT INTO generos (genero)
    VALUES('Ação'), ('Terror'), ('Romance'), ('Ficção Científica');


## Inserir filmes

```sql
    INSERT INTO filmes (titulo, lancamento, genero_id)
    VALUES('Velozes e furiosos 3', 2006,1);
    INSERT INTO filmes (titulo, lancamento, genero_id)
    VALUES('Fale comigo', 2022,2);
    INSERT INTO filmes (titulo, lancamento, genero_id)
    VALUES('La La Land', 2017,3);
    INSERT INTO filmes (titulo, lancamento, genero_id)
    VALUES('Interestelar', 2014,4);