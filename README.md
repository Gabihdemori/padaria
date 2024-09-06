drop database if exists padaria;
create database padaria character set utf8 collate utf8_general_ci;
use padaria;

create table clientes (
    id_cliente int not null auto_increment primary key,
    nome varchar(100) not null,
    telefone varchar(11) not null,
    email varchar(100),
    nascimento date,
    idade varchar(100)
);

create table produtos (
    codigo_produto int not null primary key,
    nome_produto varchar(100) not null,
    preco_produto float not null,
    quant_estoque int not null
);

create table pedidos (
    id_pedido int not null auto_increment primary key,
    codigo_pedido int not null,
    val_final float,
    data_pedido date not null,
    id_cliente int not null,
    foreign key (id_cliente) references clientes(id_cliente)
);

-- tabela pedido_produtos (relacionamento muitos-para-muitos entre pedidos e produtos)
create table pedido_produtos (
    id_pedido int not null,
    codigo_produto int not null,
    quantidade int not null,
    primary key (id_pedido, codigo_produto),
    foreign key (id_pedido) references pedidos(id_pedido),
    foreign key (codigo_produto) references produtos(codigo_produto)
);

show tables;


insert into clientes (id_cliente, nome, telefone, email, nascimento, idade) values
(1, 'alberto aguira ávila', '1913914552', 'alberto@gmail.com', '1980-05-15', '44 anos');

insert into produtos (codigo_produto, nome_produto, preco_produto, quant_estoque) values
(101, 'pão francês', 0.50, 100),
(102, 'croissant', 1.20, 50),
(103, 'baguete', 1.00, 30);

insert into pedidos (id_pedido, codigo_pedido, val_final, data_pedido, id_cliente) values
(1, 1001, 5.00, '2024-09-01', 1),
(2, 1002, 3.40, '2024-09-02', 1);


insert into pedido_produtos (id_pedido, codigo_produto, quantidade) values
(1, 101, 6),  -- 6 pães franceses
(1, 102, 2),  -- 2 croissants
(2, 103, 3);  -- 3 baguetes


update produtos set quant_estoque = 94 where codigo_produto = 101;  -- estoque do pão francês
update produtos set quant_estoque = 48 where codigo_produto = 102;  -- estoque do croissant
update produtos set quant_estoque = 27 where codigo_produto = 103;  -- estoque da baguete

update pedidos set val_final = 5.40 where id_pedido = 1;  -- valor final do pedido 1

show tables;






drop database if exists Oficina;
create database Oficina character set utf8 collate utf8_general_ci;
use Oficina;

create table funcionarios (
    id_funcionario int not null auto_increment primary key,
    nome_funcionario varchar(100) not null,
    especialidade_funcionario varchar(100) not null
);

create table veiculos (
    placa_veiculo varchar(10) not null primary key,
    tipo_veiculo varchar(50),
    modelo_veiculo varchar(100)
);

create table servicos (
    num_servico int not null auto_increment primary key,
    desc_servicos varchar(255),
    preco_servico decimal(10, 2) not null,
    id_funcionario int not null,
    placa_veiculo varchar(10) not null,
    foreign key (id_funcionario) references funcionarios (id_funcionario),
    foreign key (placa_veiculo) references veiculos (placa_veiculo)
);

show tables;

insert into funcionarios (nome_funcionario, especialidade_funcionario) values
('rafael pedigree', 'mecânico'),
('mariana ferraz', 'eletricista'),
('carlos santiego', 'pintor');

insert into veiculos (placa_veiculo, tipo_veiculo, modelo_veiculo) values
('lsn4i42', 'carro', 'fusca'),
('lsn4i59', 'moto', 'titan'),
('lsn4i69', 'caminhão', 'volvo');

insert into servicos (desc_servicos, preco_servico, id_funcionario, placa_veiculo) values
('troca de óleo', 50.00, 1, 'lsn4i42'),
('reparo de elétrica', 120.00, 2, 'lsn4i59'),
('pintura de carro', 300.00, 3, 'lsn4i69');



