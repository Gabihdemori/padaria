-- Remover o banco de dados se ele já existir
DROP DATABASE IF EXISTS Padaria;
CREATE DATABASE Padaria CHARACTER SET utf8 COLLATE utf8_general_ci;
USE Padaria;

-- Tabela Clientes
CREATE TABLE Clientes (
    id_cliente INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    nome varchar(100) NOT NULL,
    telefone VARCHAR(11) NOT NULL,
    email VARCHAR(100),
    nascimento DATE,
    idade VARCHAR(100)
);

-- Tabela Produtos
CREATE TABLE Produtos (
    codigo_produto INT NOT NULL PRIMARY KEY,
    nome_produto VARCHAR(100) NOT NULL,
    preco_produto FLOAT NOT NULL,
    quant_estoque INT NOT NULL
);

-- Tabela Pedidos
CREATE TABLE Pedidos (
    id_pedido INT NOT NULL AUTO_INCREMENT PRIMARY KEY,
    codigo_pedido INT NOT NULL,
    val_final FLOAT NOT NULL,
    data_pedido DATE NOT NULL,
    id_cliente INT NOT NULL,
    FOREIGN KEY (id_cliente) REFERENCES Clientes(id_cliente)
);

-- Tabela Pedido_Produtos (relacionamento muitos-para-muitos entre Pedidos e Produtos)
CREATE TABLE Pedido_Produtos (
    id_pedido INT NOT NULL,
    codigo_produto INT NOT NULL,
    quantidade INT NOT NULL,
    PRIMARY KEY (id_pedido, codigo_produto),
    FOREIGN KEY (id_pedido) REFERENCES Pedidos(id_pedido),
    FOREIGN KEY (codigo_produto) REFERENCES Produtos(codigo_produto)
);

-- Exibir as tabelas criadas
SHOW TABLES;****
