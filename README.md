# MySql_Exercicios
Exercícios iniciais desenvolvidos em aula da matéria BD II (Banco de Dados dois)
================================================================================

<b>Exercício 1:</b>
```
create table tbUsuario(
idUsuario int PRIMARY KEY,
NomeUsuario varchar(45) null,
DataNascimento datetime null
);

create table tbEstado(
Id int PRIMARY KEY,
Uf char(2) null
);

create table tbCliente(
CodigoCli smallint PRIMARY KEY,
Nome varchar(50) null,
Endereco varchar(60) null
);

create table tbProduto(
Barras float(13, 0) PRIMARY KEY,
Valor float(9, 4) null,
Descricao text null
);

show tables;
describe tbUsuario;
describe tbEstado;
describe tbCliente;
describe tbProduto;

show databases;

alter table tbCliente modify column Nome varchar(58) null;
alter table tbProduto add column Qtd int null;

drop table tbEstado;
alter table tbUsuario drop column DataNascimento;
```
<br>

<b>Exercício 2:</b>
```
create table tbProduto(
idProp int PRIMARY KEY,
NomeProd varchar(50) not null,
Qtd int null,
DataValidade date not null,
Preco decimal(6, 2) not null
);

create table tbCliente(
Codigo int PRIMARY KEY,
NomeCli varchar(50) not null,
DataNascimento date null
);

describe tbProduto;
describe tbCliente;
```

<br>

<b>Exercício 3:</b>
```
create database db_comercio;
use db_comercio;

create table tbCliente(
Id int PRIMARY KEY,
NomeCli varchar(200) not null,
NumEnd decimal(6, 0) not null,
CompEnd varchar(50) null
);

create table tbClientePF(
CPF decimal (11, 0) PRIMARY KEY,
RG int null,
Rgdig char(1) null,
Nascimento date not null
);

describe tbCliente;
describe tbClientePF;
```

<br>

<b>Exercício 4:</b>
```
Não upado.
```

<br>

<b>Exercício 5:</b>
```
create database db_selma_carline;
use db_selma_carline;

create table tbVenda(
NF int PRIMARY KEY AUTO_INCREMENT,
DataValidade date not null
);

describe tbVenda;

alter table tbVenda add column Preco decimal(6, 2) not null;
alter table tbVenda add column Qtd tinyint null;

alter table tbVenda drop column DataValidade;
alter table tbVenda add column DataVenda date null;


create table produto(
CodigoB float(13, 0) PRIMARY KEY,
NomeProd varchar(50) not null
);

alter table tbVenda add column CodigoB float(13, 0) not null;
alter table tbVenda add foreign key (CodigoB) references produto(CodigoB);

describe produto;
```

<br>

<b>Exercício 6:</b>
```
create database db_desenvolvimento;
use db_desenvolvimento;

create table tbProduto(
IdProp int PRIMARY KEY,
NomeProd varchar(50) not null,
Qtd int null,
DataValidade date not null,
Preco decimal(7,2) not null
);

describe tbProduto;

alter table tbProduto add column Peso decimal(4,2) null;
alter table tbProduto add column Cor varchar(50) null;
alter table tbProduto add column Marca varchar(50) not null;

alter table tbProduto drop column Cor;

alter table tbProduto modify column Peso decimal(4,2) not null;

/*Não é possível apagar a coluna "Cor"
pois ela já foi apagada anteriormente.*/

create database dbLojaGrande;

alter table tbProduto add column Cor varchar(50) null;

create database dblojica;
use dblojica;

create table tbCliente(
NomeCli varchar(50) not null,
CodigoCli int PRIMARY KEY,
DataCadastro date not null
);

describe tbCliente;

use dbLojaGrande;

create table tbFuncionario(
NomeFunc varchar(50) not null,
CodigoFunc int PRIMARY KEY,
DataCadastro datetime not null
);

describe tbFuncionario;

drop database dbLojaGrande;

use dblojica;
alter table tbCliente add column cpf decimal(11,0) not null unique;
```

<b>Exercício 7:</b>
```
create database dbescola;
use dbescola;

create table tbCliente(
IdCli int PRIMARY KEY,
NomeCli varchar(50) not null,
NumEnd smallint null,
DataCadastro datetime DEFAULT(curdate())
);

alter table tbCliente modify column DataCadastro datetime DEFAULT(current_timestamp());
alter table tbCliente add column CPF decimal(11,0) not null unique;
alter table tbCliente add column Cep decimal (5,0) null;

create database dbempresa;

create table tbEndereco(
Cep decimal(5,0) PRIMARY KEY,
Logradouro varchar(250) not null,
IdUf tinyint null
);

alter table tbCliente add foreign key Fk_Cep_TbCliente(Cep) references tbEndereco(Cep);

describe tbCliente;

/*1 - Referenciar a chave estrangeira para a chave primaira
2 - Manter o código limpo
3 - Usar a constraint "DEFAULT" corretamente*/

show databases;

use dbempresa;
drop database dbempresa;
```

<br>

<b>Exercício 8:</b>
```
use dbescola;

create table tbEst(
IdUf tinyint PRIMARY KEY,
NomeUfs char(2) not null,
NomeEstado char(40) not null
);

alter table tbEndereco add foreign key Fk_IdUf_TbEndereco(IdUf) references tbEst(IdUf);
alter table tbEst drop column NomeEstado;

rename table tbEst to tbEstado;

alter table tbEstado RENAME COLUMN NomeUfs TO NomeUf;

alter table tbEndereco add column IdCid mediumint null;

create table tbCidade(
IdCid mediumint PRIMARY KEY,
NomeCidade varchar(50) not null
);

alter table tbCidade modify column NomeCidade varchar(250) not null;

alter table tbEndereco add foreign key Fk_IdCid_TbEndereco(IdCid) references tbCidade(IdCid);
```

<br>

<b>Exercício 9:</b>
```

/*Exercício 9*/
create database db_banco;
use db_banco;

create table tbCliente(
CPF bigint PRIMARY KEY,
Nome varchar(50) not null,
Sexo char(1) not null,
Endereco varchar(50) not null
);

create table tbConta(
NumeroConta int PRIMARY KEY,
Saldo decimal(7, 2) null,
TipoConta smallint not null,
NumAgencia int not null /*fk*/ 
);

create table tbHistorico(
CPF bigint null,
foreign key (CPF) references tbCliente(CPF),
NumeroConta int null,
foreign key (NumeroConta) references tbConta(NumeroConta),
DataInicio date null
);

create table tbTelefone_Cliente(
Telefone int PRIMARY KEY,
CPF bigint null,
foreign key (CPF) references tbCliente(CPF)
);

create table tbAgencia(
NumeroAgencia int PRIMARY KEY,
CodBanco int null, /*fk*/
Endereco varchar(50) not null
);

alter table tbConta add foreign key (NumAgencia) references tbAgencia(NumeroAgencia);

create table tbBanco(
Codigo int PRIMARY KEY,
Nome varchar(50) not null
);

alter table tbAgencia add foreign key (CodBanco) references tbBanco(Codigo);

show tables;
```
