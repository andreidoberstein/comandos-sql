# Principais comandos SQL

## Tipos de dados

Esses tipos de dados são usados para representar os valores mais simples que podem ser armazenados nas colunas de uma tabela do MySQL.

Alguns exemplos dos tipos de dados primitivos do MySQL:

### # Tipos numéricos inteiros, positivos ou negativos, sem casas decimais:
* SMALLINT - tamanho menor
* INT - tamanho comum
* BIGINT - tamanho maior

#### Exemplo:
```
CREATE TABLE items (
    id_item INT AUTO_INCREMENT PRIMARY KEY,
    codigo SMALLINT,
    lote BIGINT,
    PRIMARY KEY (id_item)
);

INSERT INTO users (codigo, lote) 
VALUES (23, 3847283123);
```

### # Tipos numéricos de ponto flutuante com casas decimais:
* FLOAT(8,2) - Nº 8 casas antes da vírgula, nº 2 casas depois da vírgula
* DOUBLE(10,2) - Nº 8 casas antes da vírgula, nº 2 casas depois da vírgula

#### Exemplo:
```
CREATE TABLE produtos (
  id_produto INT NOT NULL AUTO_INCREMENT,
  nome VARCHAR(50),
  valor_compra DOUBLE(10,4),
  valor_venda FLOAT(8,2),
  PRIMARY KEY (id_produto)
);

INSERT INTO produtos 
(nome, valor_compra, valor_venda) 
VALUES 
('Product A', 19.9905, 29.75),
('Product B', 12.4998, 18.75),
('Product C', 34.5687, 43.65);
```

### # Tipos de texto (CHAR, CHARACTER) armazena uma sequência fixa de caracteres.
* CHAR -  Utilizado para uma sequencia fixa
* VARCHAR - Armazena uma sequência variável de caracteres.

#### Exemplo
```
CREATE TABLE funcionario (
  id_funcionario INT NOT NULL AUTO_INCREMENT,
  nome VARCHAR(120),
  uf CHAR(2),
  PRIMARY KEY (id_funcionario)
);

INSERT INTO funcionario 
(nome, uf)
VALUES 
('Renato Gaúcho', 'SC'),
('Soares', 'SP');
```

### # Tipos de data e hora:
* DATE - Armazena datas (ano, mês e dia);
* TIME - Armazena horários do dia;
* DATETIME / TIMESTAMP - Armazena data e horário juntos
```
CREATE TABLE estudantes (
    id_estudante INT NOT NULL AUTO_INCREMENT,
    nome VARCHAR(80),
    aniversario DATE,
    horario_entrada TIME,
    created DATETIME,
    PRIMARY KEY (id_estudante)
);

INSERT INTO estudantes 
(nome, aniversario, horario_entrada, created)
VALUES
('Grohe', '2000-01-01', '08:30:00', '2023-01-01 21:08:50'),
('Kanemann', '1999-05-10', '18:20:22', '2023-01-01 02:00:00'),
('Geromel', '1998-11-20', '14:05:29', '2023-01-01 14:00:00');
```

### # Outros tipos de dados:
* BLOB - pode armazenar dados binários como imagens, multimedia e arquivos PDF;
* TEXT - Usado para armazenar grandes quantidades de texto
* ENUM - utilizado para armazenar um conjunto de valores constantes, fixos, que não podem ser modificados;

#### Exemplo
```
CREATE TABLE usuario (
  id_usuario INT AUTO_INCREMENT NOT NULL,
  imagem BLOB,
  conteudo TEXT,
  status_usuario ENUM('Ativo','Inativo'),
  PRIMARY KEY (id_usuario)
);
INSERT INTO usuario(imagem, conteudo, status_usuario)
VALUES
(0xFFD8FFE000104A46494600010101006000600000FFE10016457869660000, 'Mussum Ipsum, cacilds vidis litro abertis.', 'Ativo');
```

## Executando comandos básicos

### # Criar base de dados
```
CREATE DATABASE projeto_final;
```

### # Selecionar a base para executar os comandos
```
USE projeto_final;
```

### # Criar tabela de dados
```
CREATE TABLE users (
    id_user INT NOT NULL AUTO_INCREMENT,
    nome VARCHAR(255) NOT NULL,
    usuario VARCHAR(255) NOT NULL,
    senha VARCHAR(255) NOT NULL,
    sexo ENUM('M','F'),
    status ENUM('Ativo','Inativo') DEFAULT ('Ativo'),
    perfil ENUM('Admin','Usuario'),
    created DATETIME DEFAULT CURRENT_TIMESTAMP,
    PRIMARY KEY(id_user)
);
```

### # Visualizar todos os dados da tabela
```
SELECT * FROM users;
```

### # Deletar tabela
```
DROP TABLE users;
```

### # Inserir dados na tabela
```
INSERT INTO users(nome, usuario, senha, sexo, perfil)
VALUES('Alexandre', 'alex46', 'alex46', 'M', 'Admin'),
('Alexia', 'alexia10', 'alexia10', 'F', 'Admin'),
('Helio', 'helio46', 'helio46', 'M', 'Usuario');
```

### # Visualizar colunas com alias
```
SELECT u.nome FROM users u;
```

### # Visualizar colunas com condicional
```
SELECT A.nome FROM users A WHERE A.id_user = 2;
SELECT A.nome FROM users A WHERE A.nome = 'Helio';
SELECT * FROM users A WHERE A.nome LIKE '%xia%';
SELECT A.nome FROM users A WHERE A.sexo = 'M';
SELECT * FROM users A WHERE A.created = '2023-07-24 18:17:45';
SELECT * FROM users A WHERE A.created BETWEEN '2023-09-01' AND '2023-09-10';
```

### # Atualizar dados
```
UPDATE users SET nome = 'Alexandre Sergio', sexo = 'M' WHERE id_user = 1;
UPDATE users SET perfil = 'Usuario' WHERE id_user = 2;
```

### # Deletar dados
```
DELETE FROM users WHERE sexo = 'F' AND id_user = 2;
DELETE FROM users WHERE id_user != 3;
```

Referências
https://www.sqliz.com/mysql-ref/bigint-datatype/