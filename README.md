# Exerc-cio-TRIGGER
create database pedido;
use pedido;

CREATE TABLE Pedidos(

IDPedido INT AUTO_INCREMENT PRIMARY KEY,

DataPedido DATETIME,

NomeClient VARCHAR (100)

);


INSERT INTO Pedidos (DataPedido, NomeCLiente) values

(NOW(),'CLiente 1'),

(NOW(),'CLiente 1'),

(NOW(),'CLiente 1');


DELIMITER $

CREATE TRIGGER RegistroDataCriacaoPedido

BEFORE INSERT ON Pedidos

FOR EACH ROW

BEGIN 

 SET NEW.DataPedido = NOW();
 
END;

$

DELIMITER ;v


este codigo cria uma tabela e um trigger, trigger este que estancia a data "DataPedido" a data atual da inserção.

-----------------------------------------------------------------------------------------------------------------------------------------

create database FILMES;

use FILMES;



create table Filmes(

id		int		primary key		auto_increment,

titulo varchar(60),

minutos int

);


delimiter $


create trigger chk_minutos before insert on Filmes

for each row

begin

 if new.minutos < 0 then
 
   set new.minutos = null;
   
 end if;
 
end$gin


  

delimiter ;


insert into Filmes (titulo, minutos) values ("Piratas do Caribe 1, 120");

insert into Filmes (titulo, minutos) values ("Piratas do Caribe 2, 135");

insert into Filmes (titulo, minutos) values ("Piratas do Caribe 3, 0");

insert into Filmes (titulo, minutos) values ("Piratas do Caribe 4, -80");

insert into Filmes (titulo, minutos) values ("Piratas do Caribe 5, 180");



delimiter $

create trigger chk_minutos before insert on Filmes

 for each row

 begin 
 
  if new.minutos < 0 then
  
  
  -- Lançar um Erro
  
  signal SQLSTATE '45000'			-- exceção não tratada
  
  set MESSAGE_TEXT = "valor inválido para minutos",
  
  MYSQL_ERRNO = 2022;
  
  end if;
  
  end; $
  
  
  delimiter ;
  

create table log_deletions (

id			int		primary key auto_increment,

titulo		varchar(60),

quando		datetime,

quem		varchar(40)

);


delimiter $

create trigger log_deletions after delete on Filmes

for each row

begin

 insert into Log deletions values (null, old.titulo, sysdate(), user);
 
delimiter :





