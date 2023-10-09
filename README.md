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

<b>Exercício 11</b>
```
create database dbdis;
use dbdis;
create table tbCliente(
	Id int primary key auto_increment,
	NomeCli varchar(200) not null,
    NumEnd decimal(6,0) not null,
    CompEnd varchar(50) null,
    CepCli numeric(8) not null
);

create table tbClientePF(
	CPF decimal(11,0) unique primary key,
    RG decimal(9,0) not null,
    RG_dig char(1) not null,
    Nasc date not null,
    Id int not null
);

create table tbClientePJ(
	CNPJ decimal(9,0) unique primary key,
    IE decimal (11,0) unique,
    Id int not null
);

create table tbEndereco(
	Logradouro varchar(200) not null,
    CEP decimal(8,0) primary key,
    BairroId int not null,
    CidadeId int not null,
    UFId int not null
);

create table tbBairro(
	BairroId int primary key auto_increment,
    Bairro varchar(200) not null
);

create table tbCidade(
	CidadeId int primary key auto_increment,
    Cidade varchar(200) not null
);

create table tbEstado(
	UFId int primary key auto_increment,
    UF char(2) not null
);

create table tbFornecedor(
	Codigo int primary key auto_increment,
    CNPJ decimal(14,0) unique,
    Nome varchar(200) not null,
    Telefone decimal(11,0) null
);

create table tbProduto(
	CodigoBarras decimal(14,0) unique primary key,
    Nome varchar(200) not null,
    Valor decimal(8,2) not null,
    Qtd int null
);

create table tbCompra(
	NotaFiscal int primary key,
    DataCompra date not null,
    ValorTotal decimal(8,2) not null,
    QtdCompra int not null,
    Codigo int null
);

create table tbItemCompra(
	NotaFiscal int not null,
    CodigoBarras decimal(14,0) not null,
    ValorItem decimal(8,2) not null,
    Qtd int not null
);

create table tbVenda(
	NumeroVenda int primary key,
    DataVenda date not null,
    TotalVenda decimal(8,2) not null,
    Id_Cli int not null,
    NF int null
);

create table tbItemVenda(
	NumeroVenda int not null,
    CodigoBarras decimal(14,0) not null,
	ValorItem decimal(8,2) not null,
    Qtd int  not null
);

create table tbNota_Fiscal(
	NF int primary key,
    TotalNota decimal(8,2),
    DataEmissao date not null
);
#alter
ALTER TABLE tbCliente ADD FOREIGN KEY (CepCli) REFERENCES tbEndereco(CEP);

ALTER TABLE tbClientePF ADD FOREIGN KEY (Id) REFERENCES tbCliente(Id);

ALTER TABLE tbClientePJ ADD FOREIGN KEY (Id) REFERENCES tbCliente(Id);

ALTER TABLE tbEndereco ADD FOREIGN KEY (BairroId) REFERENCES tbBairro(BairroId);

ALTER TABLE tbEndereco ADD FOREIGN KEY (CidadeId) REFERENCES tbCidade(CidadeId);

ALTER TABLE tbEndereco ADD FOREIGN KEY (UFId) REFERENCES tbEstado(UFId);

ALTER TABLE tbCompra ADD FOREIGN KEY (Codigo) REFERENCES tbFornecedor(Codigo);

ALTER TABLE tbItemCompra ADD FOREIGN KEY (NotaFiscal) REFERENCES tbCompra(NotaFiscal);

ALTER TABLE tbItemCompra ADD FOREIGN KEY (CodigoBarras) REFERENCES tbProduto(CodigoBarras);

ALTER TABLE tbVenda ADD FOREIGN KEY (Id_Cli) REFERENCES tbCliente(Id);

ALTER TABLE tbVenda ADD FOREIGN KEY (NF) REFERENCES tbNota_Fiscal(NF);

ALTER TABLE tbItemVenda ADD FOREIGN KEY (NumeroVenda) REFERENCES tbVenda(NumeroVenda);

ALTER TABLE tbItemVenda ADD FOREIGN KEY (CodigoBarras) REFERENCES tbProduto(CodigoBarras);
   
show tables;
describe tbEndereco;

insert into tbFornecedor values
(default, '1245678937123', 'Revenda Chico Loco', '11934567897'),
(default, '1345678937123', 'José Faz Tudo S/A', '11934567898'),
(default, '1445678937123', 'Vatolodo Entregas', '11934567899'),
(default, '1545678937123', 'Astrogildo das Estrela', '11934567800'),
(default, '1645678937123', 'Amoroso Doce', '11934567801'),
(default, '1745678937123', 'Marcelo Dedal', '11934567802'),
(default, '1845678937123', 'Franciscano Cachaça', '11934567803'),
(default, '1945678937123', 'Joãozinho Chupeta','11934567804');

select * from tbFornecedor;

delimiter $$
create procedure spInsertCity (vCidade varchar(200))
begin
	if not exists(select Cidade from tbCidade where Cidade = vCidade) then
		insert into tbCidade(Cidade)
		values(vCidade);
	end if;
end $$

call spInsertCity ('Rio de Janeiro');
call spInsertCity ('São Carlos');
call spInsertCity ('Campinas');
call spInsertCity ('Franco da Rocha');
call spInsertCity ('Osasco');
call spInsertCity ('Pirituba');
call spInsertCity ('Lapa');
call spInsertCity ('Ponta Grossa');

select * from tbCidade;

delimiter $$
create procedure spInsertUf (vUF char(2))
begin
	if not exists (select UF from tbEstado where UF = vUF) then
		insert into tbEstado(UF)
		values(vUF);
	end if;
end $$

call spInsertUf ('SP');
call spInsertUf ('RJ');
call spInsertUf ('RS');

select * from tbEstado;

delimiter $$
create procedure spInsertBairro (vBairro varchar(200))
begin
	if not exists (select Bairro from tbBairro where Bairro = vBairro) then
		insert into tbBairro(Bairro)
		values(vBairro);
	end if;
end $$

call spInsertBairro ('Aclimação');
call spInsertBairro ('Capão Redondo');
call spInsertBairro ('Pirituba');
call spInsertBairro ('Liberdade');

select * from tbBairro;

#Exercicio 5
delimiter $$
create procedure spInsertProduto (vCB decimal(14,0), vNome varchar(200), vValor decimal(8,2), vQtd int)
begin
	if not exists (select CodigoBarras from tbProduto where CodigoBarras = vCB) then
		insert into tbProduto(CodigoBarras, Nome, Valor, Qtd)
		values(vCB,vNome, vValor, vQtd);
	end if;
end $$

call spInsertProduto ('12345678910111', 'Rei do Papel Mache', '54.61', 120 );
call spInsertProduto ('12345678910112', 'Bolinha de Sabão', '100.45', 120 );
call spInsertProduto ('12345678910113', 'Carro Bate', '44.00', 120 );
call spInsertProduto ('12345678910114', 'Bola Furada', '10.00', 120 );
call spInsertProduto ('12345678910115', 'Maçã Laranja', '99.44', 120 );
call spInsertProduto ('12345678910116', 'Boneco do Hitler', '124.00', 200 );
call spInsertProduto ('12345678910117', 'Farinha de Suruí', '50.00', 200 );
call spInsertProduto ('12345678910118', 'Zelador de Cemitério', '24.50', 100 );

select * from tbProduto;

#Exercicio 6
delimiter &&
create procedure spInsertEnderecooo (vLogradouro varchar (200), vBairro varchar (200), vCidade varchar (200), vUf char (2), vCEP decimal (11,0))
begin
     if not exists (select Bairro from tbBairro where Bairro = vBairro) then
		insert into tbBairro (Bairro)
		values (vBairro);
     end if;
     
     if not exists (select UF from tbEstado where UF = vUF) then
		insert into tbEstado (UF)
        values (vUF);
     end if;

     if not exists (select Cidade from tbCidade where Cidade = vCidade) then
		insert into tbCidade(Cidade)
        values (vCidade);
     end if;
     
	insert into tbendereco (Logradouro, BairroId, CidadeId, UFId, CEP) 
	values (vLogradouro, (select Bairroid from tbBairro where Bairro = vBairro), (select Cidadeid from tbCidade where Cidade = vCidade), (select UFid from tbEstado where UF = vUF), vCEP);

end &&

call spInsertEnderecooo ("Rua da Federal","Lapa","São Paulo","SP","12345050");
call spInsertEnderecooo ("Av Brasil","Lapa","Campinas","SP","12345051");
call spInsertEnderecooo ("Rua Liberdade","Consolação","São Paulo","SP","12345053");
call spInsertEnderecooo ("Av Paulista","Penha","Rio de Janeiro","RJ","12345054");
call spInsertEnderecooo ("Rua Ximbu","Penha","Rio de Janeiro","RJ","12345055");
call spInsertEnderecooo ("Rua Piu X1","Penha","Campinas","SP","12345056");
call spInsertEnderecooo ("Rua Chocolate","Aclimação","Barra Mansa","RS","12345057");
call spInsertEnderecooo ("Rua Pão na Chá","Barra Funda","Ponta Grossa","RS","12345058");

select * from tbEndereco;

#Exercicio 7
delimiter &&
create procedure spInsertClienteEx7(vNomeCli varchar(200), vNumEnd smallint, vCompEnd varchar(50), vCepCli decimal(8,0))
begin
	insert into tbCliente(NomeCli, NumEnd, CompEnd, CepCli)
				values(vNomeCli, vNumEnd, vCompEnd, vCepCli);
end &&

delimiter &&
create procedure spInsertClientePFEx7(vCpf decimal(11,0), vRg decimal(9,0), vRg_dig char(1), vNasc date, vId int)
begin
	insert into tbClientePF(CPF, RG, RG_Dig, Nasc, ID)
				values(vCpf, vRg, vRg_dig, vNasc, vId);
end &&

call spInsertClienteEx7('Pimpão', 325, null, 12345051);
call spInsertClientePFEx7(12345678911, 12345678, 0, '2000-10-12', 1);

call spInsertClienteEx7('Disney Chaplin', 89, 'Ap. 12', 12345053);
call spInsertClientePFEx7(12345678912, 12345679, 0, '2001-11-21', 2);

call spInsertClienteEx7('Marciano', 744, null, 12345054);
call spInsertClientePFEx7(12345678913, 12345680, 0, '2001-06-01', 3);

call spInsertEnderecooo ("Rua Veia","Jardim Santa Isabel","Cuiabá","MT","12345059");
call spInsertClienteEx7('Lança Perfume', 1284, null, 12345059);

call spInsertClienteEx7('Remédio Amargo', 2585, null, 12345058);
call spInsertClientePFEx7(12345678914, 12345681, 'X', '2004-04-05', 4);
call spInsertClientePFEx7(12345678915, 12345682, 0, '2002-07-15', 5);

select * from tbCliente;
select * from tbClientePF;
select * from tbEndereco;

#Exercicio 8
call spInsertEnderecooo('Rua dos Amores', 'Sei Lá', 'Recife', 'PE', 12345060);
delimiter $$
create procedure spInsertClientePJ(vNomeCli varchar(200), vNumEnd decimal(6,0), vCompEnd varchar(50), vCEP decimal(8,0), vCNPJ decimal(14,0) ,vIE decimal(11,0), vId int)
begin
    if not exists (select * from tbCliente where NomeCli= vNomeCli) then
		insert into tbCliente(NomeCli, NumEnd, CompEnd, CepCli)
		values(vNomeCli, vNumEnd, vCompEnd,(select CEP from tbEndereco where CEP = vCEP));
	end if;
	
    if not exists (select * from tbClientePJ where CNPJ = vCNPJ) then
        insert into tbClientePJ(CNPJ, IE, Id)
        values(vCNPJ, vIE, vId);
	end if;
end $$    

alter table tbClientePJ modify column CNPJ decimal(14,0);
call spInsertClientePJ('Paganada', 159, null, 12345051, 12345678912345, 98765432198, 1);
call spInsertClientePJ('Caloteando', 69, null, 12345053,12345678912346, 98765432199, 2);
call spInsertClientePJ('Semgrana', 189, null, 12345060, 12345678912347, 98765432100, 3);
call spInsertClientePJ('Cemreais', 5024, 'Sala 23', 12345060, 12345678912348, 98765432101, 4);
call spInsertClientePJ('Durango', 1254, null, 12345060, 12345678912349, 98765432102, 5);

select * from tbClientePJ;
select * from tbCliente;

#Exercicio 9
delimiter $$
create procedure spInsertCompra(vNotaFiscal int, vNome varchar (200), vDataCompra date, vCodigoBarras decimal (14,0), vValorItem decimal (8,2), vQtd int, vQtdCompra int, vValorTotal decimal(8,2)) 
begin
    if not exists (select * from tbFornecedor where Nome = vNome) then
        insert into tbFornecedor (Nome) values (vNome);
        set vNome = (select Nome from tbfornecedor where Nome= vNome);
	else
        select Nome into vNome from tbfornecedor where Nome = vNome;
    end if;

    if not exists (select * from tbCompra where NotaFiscal = vNotaFiscal) then
        insert into tbCompra (NotaFiscal, DataCompra, ValorTotal, QtdCompra) values (vNotaFiscal, vDataCompra, vValorTotal, vQtdCompra);
        set vNotaFiscal = (select NotaFiscal from tbCompra where NotaFiscal= vNotaFiscal);
	else
        select NotaFiscal into vNotaFiscal from tbCompra where NotaFiscal = vNotaFiscal;
    end if;
	select * from tbCompra;
    if not exists (select * from tbItemCompra where CodigoBarras = vCodigoBarras) then
        insert into tbItemCompra (NotaFiscal, CodigoBarras, ValorItem, Qtd) values (vNotaFiscal, vCodigoBarras, vValorItem, vQtd);
		set vCodigoBarras = (select CodigoBarras from tbItemCompra where CodigoBarras= vCodigoBarras);
	else 
		select CodigoBarras into vCodigoBarras from tbItemCompra where CodigoBarras = vCodigoBarras;
	end if;
end $$
select * from tbFornecedor;
call spInsertCompra(8459, 'Amoroso e Doce',STR_TO_DATE("01,05,2018","%d,%m,%Y"),12345678910111, 22.22, 200, 700, 21944.00);
call spInsertCompra(2482, 'Revenda Chico Loco',STR_TO_DATE("22,04,2020","%d,%m,%Y"),12345678910112, 40.50, 180, 180,  7290.00 );
call spInsertCompra(21563, 'Marcelo Dedal',STR_TO_DATE("12,07,2020","%d,%m,%Y"), 12345678910113,  3.00, 300, 300, 900.00);
call spInsertCompra(8459, 'Amoroso e Doce',STR_TO_DATE("04,12,2020","%d,%m,%Y"), 12345678910114,  35.00, 500, 700, 21944.00);
call spInsertCompra(156354 , 'Revenda Chico Loco',STR_TO_DATE("23,11,2021","%d,%m,%Y"), 12345678910115,  54.00, 350, 350, 18900.00);

select * from tbCompra


#Exercicio 10
delimiter &&
create procedure spVendaEx10(vNumeroVenda int, vDataVenda date, vTotalVenda decimal(8,2), vNomeCli varchar(200), vQtd int, vValorItem decimal(8,2), vCodigoBarras decimal (14,0))
begin
	if exists (select * from tbCliente where NomeCli = vNomeCli) then
	insert into tbVenda(NumeroVenda, DataVenda, TotalVenda) values (vNumeroVenda, vDataVenda, vTotalVenda);
end if;

 if exists (select * from tbItem_Venda where CodigoBarras = vCodigoBarras) then
  insert into tbItemVenda(Qtd, ValorItem, CodigoBarras) values (vQtd, vValorItem, vCodigoBarras);
  set vCodigoBarras = (select CodigoBarras from tbItem_Venda where CodigoBarras = vCodigoBarras);
end if;
end &&

call spVendaEx10("Pimpão", 1, '2000-01-01', 54.61, 1, 54.61, 12345678910111)
```
