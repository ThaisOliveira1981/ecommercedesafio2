# ecommercedesafio2
CRIEI UM BANCO DE DADOS ECOMMERCE .
---------segue script de criação:-------------
create database ecommerce;
use ecommerce;
create table clients(
idclient int auto_increment primary key,
Fname varchar(10),
Minit char(3),
Lname varchar(20),
cpf char(11) not null,
Adress varchar(30),
constraint unique_cpf_client unique (cpf)
);
desc clients;
create table product(
idProduct int auto_increment primary key,
Pname varchar(10) not null,
classification_kids bool default false,
category enum('eletrônico','vetimenta','brinquedos','Alimentos','Móveis') not null,
avaliação float default 0,
size varchar(10)
);
create table pagamento(
idPagamento int auto_increment primary key
);
create table cartao(
idCartao int auto_increment primary key,
NomeTitular varchar(45),
NumeroCartao char(16),
DataValidae char(5)
);
create table pagamentocomcartao(
idPagamento int,
idCartao int,
valor varchar(30),
primary key (idPagamento,idCartao),
constraint fk_pagamento foreign key (idPagamento) references pagamento(idPagamento),
constraint fk_cartao foreign key (idCartao) references cartao(idCartao)
);
create table boleto(
idBoleto int auto_increment primary key,
valor varchar(45),
datavencimento date
);
create table pagamentocomboleto(
idPagamento int,
idBoleto int,
valor varchar(30),
primary key (idPagamento,idBoleto),
constraint fk_pagamentoboleto foreign key (idPagamento) references pagamento(idPagamento),
constraint fk_boleto foreign key (idBoleto) references boleto(idBoleto)
);
create table orders(
idOrder int auto_increment primary key,
idOrderClient int,
orderStatus enum('Cancelado','Confirmado','Em processamento') default 'Em processamento',
orderDescription varchar(255),
sendValue float default 10,
idPagamento int,
constraint fk_ordes_client foreign key (idOrderClient) references clients(idClient),
constraint fk_orders_pagamento foreign key (idPagamento) references pagamento(idPagamento)
);
create table estoque(
idEstoque int auto_increment primary key,
Endereço varchar(45) not null
);
create table productStorage(
idProduct int,
idEstoque int,
quantidade int default 0,
primary key (idProduct,idEstoque),
constraint fk_product foreign key (idProduct) references product(idProduct),
constraint fk_estoque foreign key (idEstoque) references estoque(idEstoque)
);
create table fornecedor(
idFornecedor int auto_increment primary key,
SocialName varchar(255) not null,
cnpj char(14) not null,
contact char(11) not null,
constraint unique_supplier unique (cnpj)
);
create table seller(
idSeller int auto_increment primary key,
SocialName varchar(255) not null,
cnpj char(14),
cpf char(9),
contact char(11) not null,
NomeFantasia varchar(255),
Endereço varchar(255),
constraint unique_cnpj_supplier unique (cnpj),
constraint unique_cpf_supplier unique (cpf)
);
create table productSeller(
idProduct int,
idSeller int,
quantidade int default 1,
primary key (idProduct,idSeller),
constraint fk_product_seller foreign key (idSeller) references seller(idSeller),
constraint fk_product_product foreign key (idProduct) references Product(idProduct)
);
create table produtoporFornecedor(
idProduct int,
idFornecedor int,
quantidade int default 1,
primary key (idProduct,idFornecedor),
constraint fk_product_Fornecedor foreign key (idFornecedor) references Fornecedor(idFornecedor),
constraint fk_product_product_Fornecedor foreign key (idProduct) references Product(idProduct)
);
create table ProdutoPedido(
IdOrder int,
IdProduct int,
quantidade int default 1,
PStatus enum('disponível','sem estoque') default 'disponível',
primary key (IdOrder,IdProduct),
constraint fk_pedido foreign key (IdOrder) references orders(IdOrder),
constraint fk_produto foreign key (IdProduct) references Product(idProduct)
);
show tables;
alter table clients auto_increment=1;
alter table Product auto_increment=1;
alter table Pagamento auto_increment=1;
alter table Cartao auto_increment=1;
alter table Boleto auto_increment=1;
alter table Orders auto_increment=1;
alter table Estoque auto_increment=1;
alter table Fornecedor auto_increment=1;
alter table Seller auto_increment=1;

create table Entrega(
idEntrega int auto_increment primary key,
idOrder int,
EndereçodeEntrega varchar(255),
StatusEntrega enum('entregue', 'cancelada', 'devolvido', 'pendente'),
CodRastreio varchar(45)
);

create table Entrega(
idEntrega int auto_increment,
idOrder int,
EndereçodeEntrega varchar(255),
StatusEntrega enum('entregue', 'cancelada', 'devolvido', 'pendente'),
CodRastreio varchar(45),
Primary Key(idEntrega,idOrder),
constraint fk_order foreign key(idOrder) references orders(idOrder)
);
alter table Entrega auto_increment=1;

